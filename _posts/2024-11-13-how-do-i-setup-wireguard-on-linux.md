---
layout: post
title:  "How do I setup Wireguard on a Debian or CentOS?"
date:   2024-11-13 19:00:00
categories: [howto]
tags: [wireguard,debian,ubuntu,centos,fedora,almalinux,rockylinux]
---

Setting up WireGuard to connect to servers within a private network involves configuring both the WireGuard **server** and **client**. Below is a comprehensive, step-by-step guide to help you establish a secure WireGuard VPN connection to access your private network servers.

### **Prerequisites**

1. **Servers and Clients**: At least one server (acting as the WireGuard server) and one or more clients.
2. **Operating Systems**: Instructions here are primarily for Linux (e.g., Ubuntu). Adjust commands as needed for other OSes.
3. **Root/Superuser Access**: You’ll need administrative privileges on both server and client machines.
4. **WireGuard Installed**: Ensure WireGuard is installed on both server and clients.

### **1. Install WireGuard**

**On the Server and Clients:**

For **Ubuntu/Debian-based systems**:

```bash
sudo apt update
sudo apt install wireguard
```

For **CentOS/RHEL**:

```bash
sudo yum install epel-release
sudo yum install wireguard-tools
```

For **Fedora**:

```bash
sudo dnf install wireguard-tools
```

For **Windows or macOS**: Download and install the appropriate WireGuard application from the [official website](https://www.wireguard.com/install/).

### **2. Generate Key Pairs**

WireGuard uses public and private keys for authentication.

**On the Server:**

```bash
wg genkey | tee server_private.key | wg pubkey > server_public.key
```

**On the Client:**

```bash
wg genkey | tee client_private.key | wg pubkey > client_public.key
```

*Keep your private keys secure and never share them.*

### **3. Configure the WireGuard Server**

**a. Assign an Internal IP Address**

Decide on a private subnet for the VPN, e.g., `10.0.0.0/24`. Assign an IP to the server, e.g., `10.0.0.1/24`.

**b. Create the WireGuard Configuration File**

Create `/etc/wireguard/wg0.conf` with the following content:

```ini
[Interface]
Address = 10.0.0.1/24
ListenPort = 51820
PrivateKey = <SERVER_PRIVATE_KEY>
# SaveConfig = true  # Optional: allows dynamic configuration changes

# Optional: Define allowed IPs for server's access to the private network
# Replace "192.168.1.0/24" with your actual private network range
PostUp = iptables -A FORWARD -i %i -j ACCEPT; iptables -A FORWARD -o %i -j ACCEPT; iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
PostDown = iptables -D FORWARD -i %i -j ACCEPT; iptables -D FORWARD -o %i -j ACCEPT; iptables -t nat -D POSTROUTING -o eth0 -j MASQUERADE

[Peer]
# Client Configuration
PublicKey = <CLIENT_PUBLIC_KEY>
AllowedIPs = 10.0.0.2/32
```

**Replace:**
- `<SERVER_PRIVATE_KEY>` with the content of `server_private.key`.
- `<CLIENT_PUBLIC_KEY>` with the content of `client_public.key`.
- `eth0` with the appropriate network interface connected to the internet.

**c. Enable IP Forwarding**

Allow the server to forward packets:

```bash
echo "net.ipv4.ip_forward=1" | sudo tee -a /etc/sysctl.conf
echo "net.ipv6.conf.all.forwarding=1" | sudo tee -a /etc/sysctl.conf
sudo sysctl -p
```

**d. Adjust Firewall Rules**

Ensure that UDP traffic on WireGuard’s port is allowed and configure NAT if accessing the internet:

```bash
sudo ufw allow 51820/udp
# If using iptables as in the config above, ensure they are applied
```

**e. Start and Enable WireGuard**

```bash
sudo wg-quick up wg0
sudo systemctl enable wg-quick@wg0
```

### **4. Configure the WireGuard Client**

**a. Assign an Internal IP Address**

Assign an IP within the VPN subnet to the client, e.g., `10.0.0.2/24`.

**b. Create the WireGuard Configuration File**

Create `/etc/wireguard/wg0.conf` on the client with the following content:

```ini
[Interface]
Address = 10.0.0.2/24
PrivateKey = <CLIENT_PRIVATE_KEY>
DNS = 1.1.1.1  # Optional: specify DNS server

[Peer]
PublicKey = <SERVER_PUBLIC_KEY>
Endpoint = <SERVER_PUBLIC_IP>:51820
AllowedIPs = 0.0.0.0/0, ::/0  # Routes all traffic through VPN
# If you only need to access the private network, use:
# AllowedIPs = 10.0.0.0/24, <PRIVATE_NETWORK_CIDR>
PersistentKeepalive = 25  # Optional: helps with NAT traversal
```

**Replace:**
- `<CLIENT_PRIVATE_KEY>` with the content of `client_private.key`.
- `<SERVER_PUBLIC_KEY>` with the content of `server_public.key`.
- `<SERVER_PUBLIC_IP>` with your server’s public IP address.
- `<PRIVATE_NETWORK_CIDR>` with your actual private network range, e.g., `192.168.1.0/24`.

**c. Adjust Firewall on Client (If Necessary)**

Ensure that the client’s firewall allows outbound UDP traffic on WireGuard’s port.

**d. Start and Enable WireGuard on Client**

```bash
sudo wg-quick up wg0
sudo systemctl enable wg-quick@wg0
```

### **5. Verify the Connection**

**On the Server:**

Run:

```bash
sudo wg
```

You should see the client connected with its latest handshake time.

**On the Client:**

Ping the server’s WireGuard IP:

```bash
ping 10.0.0.1
```

Access private network servers using their private IPs.

### **6. Routing and Accessing Private Network Servers**

If the WireGuard server is part of a larger private network, ensure that:

- **Routing is Configured:** The WireGuard server should have routes to the private network, and other devices on the private network should route return traffic through the WireGuard server.
  
- **Firewall Rules Allow Traffic:** Ensure firewalls on the server and private network servers allow traffic from the WireGuard subnet (`10.0.0.0/24`).

**Example: Access a private server `192.168.1.10` from the client:**

1. Ensure the WireGuard server can reach `192.168.1.10`.
2. On the WireGuard server, add a route to the private network if not already present.
3. On `192.168.1.10`, ensure it can route traffic back to `10.0.0.0/24` via the WireGuard server.
4. From the client, you should be able to SSH or access services on `192.168.1.10`:

   ```bash
   ssh user@192.168.1.10
   ```

### **7. Optional: Automate Key Exchange for Multiple Clients**

For environments with multiple clients:

1. **Assign Unique IPs:** Allocate a unique WireGuard IP to each client.
2. **Add Peer Sections:** Add a `[Peer]` section for each client in the server’s `wg0.conf`.
3. **Distribute Configurations:** Provide each client with its respective configuration file.

### **8. Security Best Practices**

- **Use Strong Keys:** Ensure keys are generated securely and kept confidential.
- **Restrict Allowed IPs:** Limit `AllowedIPs` in peer configurations to the necessary IP ranges.
- **Regularly Update Software:** Keep WireGuard and your system packages up to date to mitigate vulnerabilities.
- **Monitor Connections:** Periodically check active WireGuard connections using `sudo wg`.

### **Troubleshooting Tips**

- **No Connection:** Verify that the server’s port (e.g., 51820) is open and accessible from the client’s network.
- **Handshake Issues:** Ensure correct public keys are used and that the server’s public key is accurately specified in the client config and vice versa.
- **Routing Problems:** Confirm that IP forwarding is enabled on the server and that proper routes are set on both server and client.
- **Firewall Blocks:** Double-check firewall rules on both server and client sides.

### **Resources**

- [Official WireGuard Documentation](https://www.wireguard.com/#documentation)
- [WireGuard Quick Start Guide](https://www.wireguard.com/quickstart/)
- [WireGuard Configuration Examples](https://www.wireguard.com/#example-configuration)

By following this guide, you should be able to establish a secure WireGuard VPN connection to access servers within your private network seamlessly. Adjust configurations as needed based on your specific network architecture and security requirements.
