# CCNA-Notes

## Day 1 Network Devices

**What is a client?**
A client is a device that requests a service or resource made available by a server.

----

**What is a server?**
A server is a device that provides a resource or service to clients.

A client can also act as a server in some situations. For example, when two computers are connected, one computer may host a resource (acting as the server), while the other computer requests access to that resource (acting as the client).

----

**What is a Switch?**
A switch is a device used to forward traffic (frames) within a LAN.

Switches provide connectivity to hosts within the same LAN. Layer 2 switches do not separate different networks. They connect and expand networks (via interfaces).

----

**What is a Router?**
A router is a device used to provide connectivity between different LANs. Routers are used to connect multiple networks.

Routers determine the best path to route traffic and are essential for sending data over the internet.

----

**What is a Firewall?**
A firewall is a network security device that filters incoming and outgoing network traffic based on rules.

Firewalls can be hardware or software-based and are used to protect networks from unwanted traffic.

------
## Day 6- Ethernet LAN Switching (part 2)
**What is ARP?** 
ARP is used to discover the Layer 2 address (MAC address) of a known Layer 3 address (IP address). In other words, ARP is used to learn the MAC address of a device, for which you already know the IP address

**The ARP process consists of two messages:** ARP Request, ARP Reply

ARP Request is sent as a broadcast ethernet frame. Broadcast means it is sent to all hosts on the network. Because the Layer 2 address of a destination host is unknown, it broadcasts the request and waits for a reply from the correct device. 

ARP Reply is unicast. Sent only to one host (the host that sent the ARP request).

**Example ARP REQUEST with a Broadcast address. (Both devices are on the same LAN)**

```
Ping 192.168.1.3

Src IP: 192.168.1.1  
Dst IP: 192.168.1.3  
Src MAC: 9D00  
Dst MAC: FFFF:FFFF:FFFF
```

**FFFF:FFFF:FFFF** = broadcast MAC address. This is the destination MAC address when a device wants to send ethernet frames to all other devices on the local network.

When a switch broadcasts a frame, the switch shoots out the frame to all of its interfaces except the one interface, in which the arp request came from. 

Switches learn MAC addresses through the ARP process by storing the source MAC address of incoming devices. This is how a switchs build their dynamic ARP table

------
**What is an ARP Table?** 
Used to store IP address to MAC address association (mapping of IP to MAC address) 

> Use arp –a to view the ARP table (Windows, macOS, Linux)

**Type of Entries in a ARP Tables: Static & Dynamic**

Type: Static = default entry

Dynamic = learned via ARP (This table is refreshed after 5 minutes)

-----
## Day 9 – Switches interface 
**CSMA/CD:** Carrier Sense Mutiple access with collision detection.
It describes how devices avoid collisions in a half-duplex situation, and how they react if collisions do occur. 

**Half-duplex:** Means device cannot send and receive data at the same time. If it is receiving a frame, it must wait before sending a frame.  (Example: Hubs Layer 1 devices, repeating whatever signals they receive)

**Full-duplex:** Means device can send and receive data at the same time. It does not have to wait (Example: Switches Layer 2)

-----
## Interface Errors the same on a switch and a router:
Switch1#show interface g0/1

- Runts: Frames that are smaller than the minimum frame size (64 bytes)

- Giants: Frames that are larger than the maximum frame size (1518 bytes)

- CRC: Frames that failed the CRC check (in the ethernet FCS trailer)

- Frame: Frames that have an incorrect format (due to an error)

- Input errors: Total of various counters, such as the above four. 

- Output errors: Frames the switch tried to send, but failed due to an error

--------

## Common CCNA Question 
What subnet does host 192.168.5.57/24 belong to?

subnet ID: ______/27

To find the network address we simply need to change all of the hosts bits to `0`

`**1100000| 10101000 | 000000101 | 001**11001`

 `192   .    168    .      5   .     57`

`**1100000| 10101000 | 000000101 | 001**00000` = **Answer: 192.168.5.32**

----






