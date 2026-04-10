## Server Setup

1. Created VM in VirtualBox
2. Attached ISO
3. Installed Windows Server 2022 (Desktop Experience)
4. Assigned static IP:
   - 192.168.100.10


## DNS Suffix Configuration

- Configured DHCP option 015 (DNS Domain Name)
- Value: homelab.local

### Result:
Clients can resolve hostnames without full domain name

Example:
ping server → resolves to server.homelab.local


## Active Directory Setup

* Installed Active Directory Domain Services (AD DS)
* Promoted server to Domain Controller
* Created new forest:

  * Domain: homelab.local
  * NetBIOS: HOMELAB

### Result:

* Centralized authentication available
* Server acts as Domain Controller
