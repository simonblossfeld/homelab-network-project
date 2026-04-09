# Homelab Network Project (Windows Server + Client)

## Goal

This project demonstrates the setup of a basic internal network using virtualization.

The focus is on:

* Understanding core networking concepts
* Setting up a Windows Server
* Connecting a client machine
* Testing communication within a controlled environment

---

## Concepts Covered

* IP (Internet Protocol)
* DHCP (Dynamic Host Configuration Protocol)
* DNS (Domain Name System)
* Static vs Dynamic IP addressing
* Internal networks (LAN simulation)

---

## Environment

### Host System

* OS: Windows 11
* RAM: 8 GB (limited resources → optimization required)

### Virtualization

* Tool: Oracle VM VirtualBox

---

## Virtual Machines

### Server

* OS: Windows Server 2022 (Desktop Experience)
* Role: future DHCP / DNS server
* IP Address: 192.168.100.10 (static)

### Client

* OS: Windows 10
* IP Address: dynamic (DHCP planned)

---

## Network Configuration

* Network Type: Internal Network
* Network Name: lab-net

### IP Scheme

| Device | IP Address     | Type    |
| ------ | -------------- | ------- |
| Server | 192.168.100.10 | Static  |
| Client | DHCP (planned) | Dynamic |

---

## Tests

### Connectivity Test

Command used:

```
ping 192.168.100.10
```

Result:

* 4/4 packets received 
* Successful communication between client and server

---

## ⚙️ Challenges & Solutions

### Problem: Limited RAM

* Host system has only ~6 GB usable RAM
* Running two VMs caused instability

### Solution:

* Reduced VM memory to 1024 MB per machine
* Started/stopped VMs as needed

---

## Current Status

* [x] Virtual machines created
* [x] Internal network configured
* [x] Windows Server installed (GUI)
* [x] Static IP configured on server
* [x] Client installed
* [x] Ping test successful

---

## Next Steps

* Set up DHCP server on Windows Server
* Configure DNS
* Automate IP assignment
* Expand network (additional clients, Linux VM)

---

## Learning Outcome

This project builds a foundation in:

* Network configuration
* System administration basics
* Troubleshooting real-world issues

---

## Note

This is a learning project built in a resource-constrained environment.
Performance is limited but functionality is the main focus.
