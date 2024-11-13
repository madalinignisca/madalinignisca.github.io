---
layout: post
title:  "How do I setup Wireguard on a Debian or CentOS server and connect from MacOS client?"
date:   2024-11-13 20:00:00
categories: [howto]
tags: [wireguard,macos,debian,ubuntu]
---

Below is a tailored guide for setting up **WireGuard** with a **Debian/Ubuntu** server and a **macOS** client. This step-by-step guide will help you establish a secure WireGuard VPN connection to access servers within your private network.

---

### **Prerequisites**

1. **Server (Debian/Ubuntu):**
   - A machine running Debian or Ubuntu.
   - Root or sudo access.

2. **Client (macOS):**
   - A macOS device.
   - Administrative privileges for installation.

3. **WireGuard Installed:**
   - WireGuard installed on both server and client.

---

### **1. Install WireGuard**

#### **On the Debian/Ubuntu Server:**

1. **Update Package List:**

   ```bash
   sudo apt update
   ```

2. **Install WireGuard:**

   ```bash
   sudo apt install wireguard
   ```

#### **On the macOS Client:**

1. **Download WireGuard for macOS:**
   - Visit the [WireGuard Downloads Page](https://www.wireguard.com/install/) and download the macOS application.

2. **Install the Application:**
   - Open the downloaded `.dmg` file and drag the WireGuard app to your Applications folder.

---

### **2. Generate Key Pairs**

WireGuard requires a public and private key pair for both server and client.

#### **On the Debian/Ubuntu Server:**

1. **Navigate to WireGuard Directory:**

   ```bash
   cd /etc/wireguard
   ```

2. **Generate Server Keys:**

   ```bash
   umask 077
   wg genkey | tee server_private.key | wg pubkey > server_public.key
   ```

#### **On the macOS Client:**

1. **Open WireGuard Application:**
   - Launch the WireGuard app from Applications.

2. **Generate Client Keys:**
   - Click on **"Add Tunnel"** > **"Create from scratch"**.
   - The app will automatically generate a private and public key pair for the client.

   *Alternatively, you can generate keys via Terminal if preferred:*

   ```bash
   umask 077
   wg genkey | tee client_private.key | wg pubkey > client_public.key
   ```

---

### **3. Configure the WireGuard Server**

1. **Assign an Internal IP Address:**
   - Choose a private subnet for the VPN, e.g., `10.0.0.0/24`.
   - Assign `10.0.0.1/24` to the server.

2. **Create WireGuard Configuration File:**

   Create or edit `/etc/wireguard/wg0.conf` with the following content:

   ```ini
   [Interface]
   Address = 10.0.0.1/24
   ListenPort = 51820
   PrivateKey = <SERVER_PRIVATE_KEY>
   
   # Enable IP Forwarding and NAT
   PostUp = sysctl -w net.ipv4.ip_forward=1
           iptables -A FORWARD -i wg0 -j ACCEPT
           iptables -A FORWARD -o wg0 -j ACCEPT
           iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
   PostDown = sysctl -w net.ipv4.ip_forward=0
             iptables -D FORWARD -i wg0 -j ACCEPT
             iptables -D FORWARD -o wg0 -j ACCEPT
             iptables -t nat -D POSTROUTING -o eth0 -j MASQUERADE
   
   [Peer]
   # macOS Client Configuration
   PublicKey = <CLIENT_PUBLIC_KEY>
   AllowedIPs = 10.0.0.2/32
   ```

   **Replace:**
   - `<SERVER_PRIVATE_KEY>` with the content of `server_private.key`.
   - `<CLIENT_PUBLIC_KEY>` with the client's public key generated earlier.
   - `eth0` with the server’s primary network interface if different.

3. **Enable IP Forwarding Permanently:**

   ```bash
   echo "net.ipv4.ip_forward=1" | sudo tee -a /etc/sysctl.conf
   sudo sysctl -p
   ```

4. **Adjust Firewall Rules:**

   - **Allow WireGuard Port (51820/UDP):**

     ```bash
     sudo ufw allow 51820/udp
     ```

   - **Apply iptables Rules:**
     - The `PostUp` and `PostDown` directives in the WireGuard configuration handle NAT and forwarding.

5. **Start and Enable WireGuard:**

   ```bash
   sudo systemctl start [email protected]
   sudo systemctl enable [email protected]
   ```

6. **Verify WireGuard Status:**

   ```bash
   sudo wg
   ```

   You should see the server interface `wg0` active.

---

### **4. Configure the macOS Client**

1. **Launch WireGuard Application:**
   - Open the WireGuard app from Applications.

2. **Create a New Tunnel:**
   - Click on **"Add Tunnel"** > **"Add Empty Tunnel..."** or **"Import from File or Archive"** if you have a configuration file.

3. **Configure the Tunnel:**
   
   If creating manually, fill in the details as follows:

   ```ini
   [Interface]
   Address = 10.0.0.2/24
   PrivateKey = <CLIENT_PRIVATE_KEY>
   DNS = 1.1.1.1  # Optional: specify a DNS server
   
   [Peer]
   PublicKey = <SERVER_PUBLIC_KEY>
   Endpoint = <SERVER_PUBLIC_IP>:51820
   AllowedIPs = 0.0.0.0/0, ::/0  # Routes all traffic through VPN
   PersistentKeepalive = 25  # Helps maintain the connection
   ```

   **Replace:**
   - `<CLIENT_PRIVATE_KEY>` with the client's private key.
   - `<SERVER_PUBLIC_KEY>` with the server's public key (`server_public.key`).
   - `<SERVER_PUBLIC_IP>` with your server’s public IP address or domain name.

4. **Save and Activate the Tunnel:**
   - Click **"Save"**.
   - Toggle the switch next to the tunnel to **"On"** to activate the VPN connection.

---

### **5. Exchange Configuration Details Between Server and Client**

Ensure that both server and client have each other's public keys and necessary configuration details.

#### **On the Server (`wg0.conf`):**
- **Peer Section:**
  - **PublicKey:** Client's public key.
  - **AllowedIPs:** `10.0.0.2/32` (the client's VPN IP).

#### **On the Client (WireGuard App):**
- **Peer Section:**
  - **PublicKey:** Server's public key.
  - **AllowedIPs:** `0.0.0.0/0, ::/0` (all traffic) or specify particular subnets like `10.0.0.0/24, 192.168.1.0/24` if you only need access to the private network.
  - **Endpoint:** Server’s public IP and WireGuard port (`51820`).

---

### **6. Verify the Connection**

#### **On the Debian/Ubuntu Server:**

1. **Check WireGuard Interface:**

   ```bash
   sudo wg
   ```

   You should see the client listed with the latest handshake timestamp.

2. **Ping the Client from Server:**

   ```bash
   ping 10.0.0.2
   ```

   You should receive responses.

#### **On the macOS Client:**

1. **Check Connection Status:**
   - In the WireGuard app, the tunnel status should indicate an active connection.

2. **Ping the Server's VPN IP:**

   ```bash
   ping 10.0.0.1
   ```

   Open **Terminal** and execute the above command to ensure connectivity.

3. **Access Private Network Resources:**
   - You can now SSH, browse, or access services on servers within your private network using their internal IP addresses.

---

### **7. Routing and Accessing Private Network Servers**

If your WireGuard server is part of a larger private network, perform the following to ensure seamless access:

1. **Ensure Proper Routing on the Server:**
   - The server should have routes to the private network.
   - Other devices in the private network should route traffic destined for the WireGuard subnet (`10.0.0.0/24`) through the WireGuard server.

2. **Firewall Adjustments:**
   - Verify that firewalls on both the WireGuard server and the private network servers allow traffic from the WireGuard subnet.

3. **Example Access:**
   
   From the macOS client, you can SSH into a private server (e.g., `192.168.1.10`):

   ```bash
   ssh user@192.168.1.10
   ```

   Ensure that `192.168.1.10` can route traffic back to `10.0.0.0/24` via the WireGuard server.

---

### **8. Optional: Manage Multiple macOS Clients**

To add more macOS clients, repeat the key generation and configuration steps for each client:

1. **Generate Unique Key Pairs for Each Client.**
2. **Assign a Unique VPN IP Address (e.g., `10.0.0.3/24`, `10.0.0.4/24`, etc.).**
3. **Add a `[Peer]` Section in the Server's `wg0.conf` for Each Client.**
4. **Configure Each macOS Client with Its Unique Configuration.**
5. **Restart WireGuard on the Server to Apply Changes:**

   ```bash
   sudo systemctl restart [email protected]
   ```

---

### **9. Security Best Practices**

- **Protect Private Keys:**
  - Ensure that private keys on both server and client are kept secure and are not exposed.

- **Use Strong Keys:**
  - Always generate keys using WireGuard’s secure methods.

- **Limit `AllowedIPs`:**
  - Restrict `AllowedIPs` to the necessary IP ranges to minimize exposure.

- **Regular Updates:**
  - Keep WireGuard and your operating systems updated to protect against vulnerabilities.

- **Monitor Connections:**
  - Regularly check active WireGuard connections using `sudo wg` on the server.

---

### **10. Troubleshooting Tips**

- **No Connection Established:**
  - Verify that the server's UDP port `51820` is open and accessible from the client’s network.
  - Ensure that both server and client have correctly configured public and private keys.

- **Handshake Issues:**
  - Double-check that the public keys are accurately placed in the respective configurations.
  - Ensure that `Endpoint` in the client configuration points to the correct server IP and port.

- **Routing Problems:**
  - Confirm that IP forwarding is enabled on the server.
  - Verify that firewall rules are correctly set to allow forwarding and NAT.

- **macOS Specific Issues:**
  - Ensure that the WireGuard app on macOS has the necessary permissions (e.g., network permissions).
  - Restart the WireGuard app or the macOS device if connectivity issues persist.

---

### **Resources**

- **Official WireGuard Documentation:** [https://www.wireguard.com/#documentation](https://www.wireguard.com/#documentation)
- **WireGuard Quick Start Guide:** [https://www.wireguard.com/quickstart/](https://www.wireguard.com/quickstart/)
- **WireGuard macOS App:** [https://www.wireguard.com/install/](https://www.wireguard.com/install/)

---

By following this guide, you should be able to set up a secure WireGuard VPN connection between your Debian/Ubuntu server and macOS client, enabling access to servers within your private network. Adjust configurations as needed based on your specific network architecture and security requirements.
