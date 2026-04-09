# IPv4, DHCP Range and Subnet Mask - Theory Notes

## 1. IPv4 (Internet Protocol Version 4)

### Definition

IPv4 (Internet Protocol Version 4) is a network layer protocol used to identify devices in an IP network and to enable communication between them.

An IPv4 address is a **32-bit address**.

---

## 2. Structure of an IPv4 address

An IPv4 address consists of:

* 32 bits total
* divided into 4 octets
* each octet contains 8 bits

Example:

```text
192.168.100.10
```

Binary form:

```text
11000000.10101000.01100100.00001010
```

Each octet can represent a decimal value from:

```text
0 to 255
```

because 8 bits can store:

```text
00000000 = 0
11111111 = 255
```

---

## 3. Network part and host part

An IPv4 address does not only identify one device. It also contains information about:

* the network
* the host inside that network

Which part belongs to the network and which part belongs to the host is defined by the **subnet mask**.

---

## 4. Subnet Mask

### Definition

A subnet mask defines which bits of an IPv4 address belong to the network portion and which bits belong to the host portion.

Example:

```text
IP address:   192.168.100.10
Subnet mask:  255.255.255.0
```

Binary subnet mask:

```text
11111111.11111111.11111111.00000000
```

Meaning:

* first 24 bits = network part
* last 8 bits = host part

This is also written as:

```text
/24
```

So:

```text
192.168.100.10/24
```

means:

* Network: `192.168.100.0`
* Host ID: `10`

---

## 5. Why 255.255.255.0?

`255.255.255.0` is one of the most common subnet masks in small internal networks.

It means:

* all devices in the network share the first three octets
* the last octet is used for individual device addresses

So in this lab network, all devices belong to:

```text
192.168.100.x
```

Examples inside the same subnet:

* `192.168.100.10`
* `192.168.100.20`
* `192.168.100.50`
* `192.168.100.100`

These devices can communicate directly with each other because they are in the same network.

---

## 6. Why was the server assigned 192.168.100.10?

The server was configured with a **static IP address**:

```text
192.168.100.10
```

### Reason

A server should have a fixed, predictable address.

Clients and services must always know where to find the server.

If the server IP changed dynamically, network services such as:

* DHCP (Dynamic Host Configuration Protocol)
* DNS (Domain Name System)
* later possibly Active Directory

could become unreliable or unreachable.

A static IP ensures consistency.

---

## 7. Why was the DHCP range set from 192.168.100.50 to 192.168.100.100?

Example DHCP scope:

```text
Start IP: 192.168.100.50
End IP:   192.168.100.100
```

### Reason

This is not a technical requirement. It is a **design decision for structure and clarity**.

The address space is deliberately divided into sections.

### Example layout

```text
192.168.100.1 - 192.168.100.19    reserved / infrastructure
192.168.100.10                    server (static)
192.168.100.20 - 192.168.100.49   free for future static devices
192.168.100.50 - 192.168.100.100  DHCP client range
192.168.100.101 - 192.168.100.254 reserved for later expansion
```

### Why this is useful

This separation helps to avoid confusion.

Benefits:

* servers can keep fixed addresses
* clients receive addresses only from a defined pool
* troubleshooting becomes easier
* the network remains organized as the lab grows

So the reason is not “the server needs 50 addresses”.
The real reason is:

**Keep static addresses and dynamic addresses separated.**

That is standard good practice.

---

## 8. Why not let DHCP use the whole subnet?

Technically, DHCP could use a much larger range.

Example:

```text
192.168.100.2 - 192.168.100.254
```

But that would be less structured.

Problems:

* static devices could accidentally overlap with DHCP leases
* documentation becomes less clear
* future expansion becomes messy

Therefore a smaller, clean DHCP range is often better.

---

## 9. Special addresses in a /24 network

In the network:

```text
192.168.100.0/24
```

some addresses have special meanings.

### Network address

```text
192.168.100.0
```

This identifies the network itself and cannot be assigned to a host.

### Broadcast address

```text
192.168.100.255
```

This is used to send traffic to all hosts in the subnet and cannot be assigned to a host.

### Usable host range

```text
192.168.100.1 - 192.168.100.254
```

These addresses can be assigned to devices.

---

## 10. Why was no default gateway configured?

At the current stage of the lab, both virtual machines are in the same isolated internal network:

```text
lab-net
```

There is currently:

* no router
* no connection to another network
* no internet access

Because of that, a default gateway is not yet required.

A default gateway is only needed when a device wants to send traffic to a different network.

Inside the same subnet, devices communicate directly.

---

## 11. Why is 127.0.0.1 not correct as DHCP DNS server option?

### Definition

`127.0.0.1` is the loopback address.

It always means:

```text
this device itself
```

So:

* on the server, `127.0.0.1` = the server itself
* on the client, `127.0.0.1` = the client itself

If DHCP gives `127.0.0.1` to clients as DNS server, every client would try to use itself as DNS server.

That is wrong unless a DNS server is actually running on each client.

Therefore, clients must receive the real server IP:

```text
192.168.100.10
```

---

## 12. Summary

### Current lab design

Network:

```text
192.168.100.0/24
```

Server:

```text
192.168.100.10
```

DHCP range:

```text
192.168.100.50 - 192.168.100.100
```

Subnet mask:

```text
255.255.255.0
```

### Purpose of this design

* fixed address for the server
* structured DHCP range
* clean separation between static and dynamic addresses
* easier troubleshooting
* easier expansion later
