## Issues & Fixes

### Problem: Ctrl+Alt+Delete not working in VM
Solution:
Used VirtualBox menu:
Input → Keyboard → Insert Ctrl+Alt+Delete

---

### Problem: VM performance issues
Solution:
Reduced RAM allocation to 1024 MB per VM

---

## Issue: Windows 10 Home cannot join domain

Problem:
Client OS edition did not support domain join

Solution:
Reinstalled client using Windows 10 Pro

Learning:
OS edition determines available enterprise features


## Troubleshooting & Reset Summary

During the initial setup of the network project (DHCP, DNS, and basic client-server communication), several critical issues occurred that led to a complete breakdown of the environment.

### Key Issues

- **DNS & DHCP Misconfiguration**
  - Incorrect or incomplete DNS setup prevented proper name resolution.
  - DHCP was not correctly distributing DNS information to clients.
  - Result: Clients were unable to resolve hostnames (e.g. `server.labnet.local`).

- **Network Communication Issues**
  - Although IP assignment via DHCP worked, connectivity (e.g. ping) initially failed due to firewall restrictions and configuration gaps.

- **Configuration Inconsistencies**
  - Mismatched domain/zone names (e.g. `homenet.local` vs `labnet.local`) caused additional confusion.
  - Missing DHCP scope options (DNS server, domain name) led to incomplete client configuration.

### Root Cause

The combination of:
- incomplete DNS integration
- missing DHCP options
- and inconsistent naming

resulted in a non-functional network environment.

### Resolution

A full reset of the environment was performed:

- Reinstalled Windows Server 2022 and Windows 10 client VMs
- Reconfigured:
  - Static IP for server (`192.168.10.1`)
  - DHCP scope (`192.168.10.100 – 192.168.10.200`)
  - DNS server with forward lookup zone (`labnet.local`)
  - DHCP options:
    - DNS Server (Option 006)
    - Domain Name (Option 015)

After proper configuration:
- Clients successfully received correct IP and DNS settings
- Name resolution (`server.labnet.local`) worked as expected
- Network communication became stable

### Additional Note

Development was temporarily interrupted due to a **hardware failure** (primary machine became unusable), requiring migration to a new system and partial re-setup of the environment.

---

## Current Status

✔ DHCP working  
✔ DNS working  
✔ Client-server communication functional  
✔ Clean baseline restored  

Next step: Continue with Active Directory setup
