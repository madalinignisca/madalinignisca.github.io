---
layout: post
title:  "How do I setup Wireguard on a Debian or CentOS server and connect from Windows client?"
date:   2024-11-13 19:30:00
categories: [howto]
tags: [wireguard,windows,debian,ubuntu]
---

Below is a tailored guide for setting up **WireGuard** with a **Debian/Ubuntu** server and a **Windows** client. This step-by-step guide will help you establish a secure WireGuard VPN connection to access servers within your private network.

---

### **Prerequisites**

1. **Server (Debian/Ubuntu):**
   - A machine running Debian or Ubuntu.
   - Root or sudo access.

2. **Client (Windows):**
   - A Windows PC.
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

#### **On the Windows Client:**

1. **Download WireGuard for Windows:**
   - Visit the [WireGuard Downloads Page](https://www.wireguard.com/install/) and download the **Windows installer**.

2. **Install the Application:**
   - Run the downloaded `.exe` file and follow the installation prompts to install WireGuard on your Windows PC.

---

### **2. Generate Key Pairs**

WireGuard requires a public and private key pair for both server and client.

#### **On the Debian/Ubuntu Server:**

1. **Navigate to WireGuard Directory:**

   It's good practice to store WireGuard configurations in `/etc/wireguard/`.

   ```bash
   cd /etc/wireguard
   ```

2. **Generate Server Keys:**

   ```bash
   umask 077
   wg genkey | tee server_private.key | wg pubkey > server_public.key
   ```

   - **Explanation:**
     - `umask 077` ensures that the generated keys have appropriate permissions.
     - `wg genkey` generates a private key.
     - `wg pubkey` derives the corresponding public key.

3. **View the Keys (Optional):**

   ```bash
   cat server_private.key
   cat server_public.key
   ```

   *Keep your private keys secure and never share them.*

#### **On the Windows Client:**

1. **Open WireGuard Application:**
   - Launch the WireGuard app from the Start menu.

2. **Generate Client Keys:**
   - Click on **"Add Tunnel"** > **"Add Empty Tunnel..."**.
   - The application will automatically generate a private and public key pair for the client.
   - **Example Configuration:**

     ![WireGuard Add Tunnel](https://www.wireguard.com/assets/screenshots/add-tunnel.png)

3. **Note Down the Keys:**
   - After the tunnel is created, you can view the generated keys in the configuration window.
   - **Alternatively**, you can generate keys manually using PowerShell:

     ```powershell
     cd "C:\Program Files\WireGuard"
     .\wg.exe genkey | tee client_private.key | .\wg.exe pubkey > client_public.key
     ```

     *Ensure you run PowerShell with administrative privileges.*

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
   # Windows Client Configuration
   PublicKey = <CLIENT_PUBLIC_KEY>
   AllowedIPs = 10.0.0.2/32
   ```

   **Replace:**
   - `<SERVER_PRIVATE_KEY>` with the content of `server_private.key`.
   - `<CLIENT_PUBLIC_KEY>` with the client's public key generated earlier.
   - `eth0` with the server’s primary network interface if different (e.g., `ens3`, `enp0s25`).

3. **Enable IP Forwarding Permanently:**

   ```bash
   echo "net.ipv4.ip_forward=1" | sudo tee -a /etc/sysctl.conf
   sudo sysctl -p
   ```

4. **Adjust Firewall Rules:**

   - **Allow WireGuard Port (51820/UDP):**

     If you're using UFW (Uncomplicated Firewall):

     ```bash
     sudo ufw allow 51820/udp
     ```

   - **Apply iptables Rules:**
     - The `PostUp` and `PostDown` directives in the WireGuard configuration handle NAT and forwarding.

     *If not using UFW, ensure that iptables are properly set up to allow WireGuard traffic.*

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

### **4. Configure the Windows Client**

1. **Launch WireGuard Application:**
   - Open the WireGuard app from the Start menu.

2. **Create a New Tunnel:**
   - Click on **"Add Tunnel"** > **"Add Empty Tunnel..."** or **"Add from File..."** if you have a configuration file.

   ![WireGuard Add Tunnel](https://www.wireguard.com/assets/screenshots/windows-add-tunnel.png)

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
   # If you only need to access the private network, use:
   # AllowedIPs = 10.0.0.0/24, 192.168.1.0/24
   PersistentKeepalive = 25  # Helps maintain the connection
   ```

   **Replace:**
   - `<CLIENT_PRIVATE_KEY>` with the client's private key.
   - `<SERVER_PUBLIC_KEY>` with the server's public key (`server_public.key`).
   - `<SERVER_PUBLIC_IP>` with your server’s public IP address or domain name.

   **Example Configuration:**

   ```ini
   [Interface]
   Address = 10.0.0.2/24
   PrivateKey = jK8lk3H1bYH2bU8lM2+UfXQjkzm2JwrL9gE9kK3lZ0M=
   DNS = 1.1.1.1
   
   [Peer]
   PublicKey = sA7Zk3K1kbYH2bU8lM2+UfXQjkzm2JwrL9gE9kK3lZ0M=
   Endpoint = 203.0.113.1:51820
   AllowedIPs = 0.0.0.0/0, ::/0
   PersistentKeepalive = 25
   ```

4. **Save and Activate the Tunnel:**
   - Click **"Save"**.
   - Toggle the switch next to the tunnel to **"On"** to activate the VPN connection.

   ![WireGuard Activate Tunnel](https://www.wireguard.com/assets/screenshots/windows-toggle-tunnel.png)

---

### **5. Exchange Configuration Details Between Server and Client**

Ensure that both server and client have each other's public keys and necessary configuration details.

#### **On the Server (`wg0.conf`):**

- **Peer Section:**
  - **PublicKey:** Client's public key.
  - **AllowedIPs:** `10.0.0.2/32` (the client's VPN IP).

#### **On the Windows Client (WireGuard App):**

- **Peer Section:**
  - **PublicKey:** Server's public key.
  - **AllowedIPs:** `0.0.0.0/0, ::/0` (all traffic) or specify particular subnets like `10.0.0.0/24, 192.168.1.0/24` if you only need access to the private network.
  - **Endpoint:** Server’s public IP and WireGuard port (`51820`).

**Optional:** If you plan to add more clients in the future, ensure each client has a unique `[Peer]` section in the server's `wg0.conf` with their respective public keys and unique `AllowedIPs`.

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

#### **On the Windows Client:**

1. **Check Connection Status:**
   - In the WireGuard app, the tunnel status should indicate an active connection.

2. **Ping the Server's VPN IP:**

   - Open **Command Prompt** or **PowerShell** and execute:

     ```powershell
     ping 10.0.0.1
     ```

     You should receive responses, confirming connectivity.

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

   From the Windows client, you can SSH into a private server (e.g., `192.168.1.10`):

   ```powershell
   ssh user@192.168.1.10
   ```

   **Ensure that:**
   - `192.168.1.10` can route traffic back to `10.0.0.0/24` via the WireGuard server.
   - Necessary ports (e.g., SSH port 22) are open on `192.168.1.10`.

---

### **8. Optional: Manage Multiple Windows Clients**

To add more Windows clients, repeat the key generation and configuration steps for each client:

1. **Generate Unique Key Pairs for Each Client:**
   - Each client should have its own private and public key pair.

2. **Assign a Unique VPN IP Address:**
   - For example, `10.0.0.3/24`, `10.0.0.4/24`, etc.

3. **Add a `[Peer]` Section in the Server's `wg0.conf` for Each Client:**

   ```ini
   [Peer]
   PublicKey = <CLIENT_2_PUBLIC_KEY>
   AllowedIPs = 10.0.0.3/32
   ```

4. **Configure Each Windows Client with Its Unique Configuration:**
   - Follow the same steps as in **Section 4** to set up each client.

5. **Restart WireGuard on the Server to Apply Changes:**

   ```bash
   sudo systemctl restart [email protected]
   ```

6. **Activate the Tunnel on Each Windows Client:**
   - Open the WireGuard app and toggle the respective tunnel to **"On"**.

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
  - Regularly check active WireGuard connections using `sudo wg` on the server and the WireGuard app on Windows.

---

### **10. Troubleshooting Tips**

- **No Connection Established:**
  - **Verify Server's UDP Port:**
    - Ensure that the server's UDP port `51820` is open and accessible from the client’s network.
    - Use tools like `nmap` or online port checkers to verify.

  - **Check Public and Private Keys:**
    - Ensure that the server and client configurations have the correct public and private keys.

  - **Endpoint Accuracy:**
    - Confirm that the `Endpoint` in the client configuration points to the correct server IP and port.

- **Handshake Issues:**
  - **Firewall Restrictions:**
    - Ensure that firewalls on both server and client are not blocking WireGuard traffic.

  - **Network Connectivity:**
    - Confirm that both server and client have internet access.

- **Routing Problems:**
  - **IP Forwarding:**
    - Ensure that IP forwarding is enabled on the server.

  - **Correct `AllowedIPs`:**
    - Verify that `AllowedIPs` in both server and client configurations are correctly set.

- **Windows Specific Issues:**
  - **WireGuard App Permissions:**
    - Ensure that the WireGuard app has the necessary permissions to create VPN interfaces.
    - Run the WireGuard app as an administrator if necessary.

  - **Antivirus/Firewall:**
    - Some antivirus or firewall software on Windows might interfere with WireGuard. Temporarily disable them to test the connection.

- **Logging and Diagnostics:**
  - **Server Logs:**
    - Check WireGuard logs on the server for any errors:

      ```bash
      sudo journalctl -u [email protected]
      ```

  - **Client Logs:**
    - In the WireGuard app on Windows, view the tunnel logs for any connection issues.

---

### **Resources**

- **Official WireGuard Documentation:** [https://www.wireguard.com/#documentation](https://www.wireguard.com/#documentation)
- **WireGuard Quick Start Guide:** [https://www.wireguard.com/quickstart/](https://www.wireguard.com/quickstart/)
- **WireGuard for Windows:** [https://www.wireguard.com/install/](https://www.wireguard.com/install/)
- **WireGuard GitHub Repository:** [https://github.com/WireGuard/WireGuard](https://github.com/WireGuard/WireGuard)

---

By following this guide, you should be able to set up a secure WireGuard VPN connection between your Debian/Ubuntu server and Windows client, enabling access to servers within your private network. Adjust configurations as needed based on your specific network architecture and security requirements.
