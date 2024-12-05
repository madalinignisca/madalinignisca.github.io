---
layout: post
title:  "Renaming Network Interface in Debian by MAC Address"
date:   2024-12-05 23:00:00
categories: [howto]
tags: [network,debian,ubuntu]
---

In Debian Linux, you can rename a network interface by using the `udev` rules to match it by its MAC address and assign a custom name. Here's how you can do it:

1. **Identify the MAC Address**: First, you'll need to know the MAC address of the interface you want to rename. You can find it using the following command:

   ```bash
   ip link show
   ```

   Look for the line that starts with your current interface name (e.g., `eth0`, `ens33`, etc.) and note its MAC address (it looks something like `00:1A:2B:3C:4D:5E`).

2. **Create a Udev Rule**: You'll need to create a new `udev` rule file. Open a terminal and create a new file in the `/etc/udev/rules.d/` directory. You can use any text editor, for example:

   ```bash
   sudo nano /etc/udev/rules.d/10-network.rules
   ```

   In this file, you will add a rule to rename the interface based on its MAC address. Use the following format:

   ```plaintext
   SUBSYSTEM=="net", ACTION=="add", ATTR{address}=="00:1A:2B:3C:4D:5E", NAME="customname"
   ```

   Replace `00:1A:2B:3C:4D:5E` with your actual MAC address, and `customname` with your desired interface name.

3. **Reload Udev Rules**: After saving the file, reload the `udev` rules with the following command:

   ```bash
   sudo udevadm control --reload-rules
   ```

4. **Reboot or Trigger Udev**: You can either reboot your system or trigger the `udev` rules for the interfaces. You can trigger all `udev` rules with:

   ```bash
   sudo udevadm trigger
   ```

5. **Verify the Change**: After rebooting or triggering the rules, you can check whether the interface has been renamed using:

   ```bash
   ip link show
   ```

This should display your network interfaces with the new name you assigned.

### Example Udev Rule

Here’s an example of what the rule might look like:

```plaintext
SUBSYSTEM=="net", ACTION=="add", ATTR{address}=="00:1A:2B:3C:4D:5E", NAME="my_custom_interface"
```

### Note
- Ensure that no other rules are conflicting with your new rule, especially those that might rename interfaces.
- If you switch between different hardware, consider naming conventions that remain unique following your rules.
