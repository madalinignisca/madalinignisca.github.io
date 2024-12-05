---
layout: post
title:  "How do I add a network interface to firewalld?"
date:   2024-12-05 22:00:00
categories: [howto]
tags: [firewalld,debian,ubuntu,centos,fedora,almalinux,rockylinux]
---

To add the `ens18` interface to the public zone of `firewalld` in Linux, you can follow these steps:

1. **Open a terminal** on your Linux machine.

2. **Check the current zones** and the configured interfaces using:
   ```bash
   sudo firewall-cmd --get-active-zones
   ```

3. **Add the `ens18` interface** to the public zone with the following command:
   ```bash
   sudo firewall-cmd --zone=public --add-interface=ens18 --permanent
   ```

   The `--permanent` option ensures that the change persists after a reboot.

4. **Reload the firewall** to apply the changes:
   ```bash
   sudo firewall-cmd --reload
   ```

5. **Verify that the interface has been added** to the public zone:
   ```bash
   sudo firewall-cmd --zone=public --list-interfaces
   ```

You should see `ens18` listed as part of the public zone. If you have any further questions or need assistance with anything else, feel free to ask!
