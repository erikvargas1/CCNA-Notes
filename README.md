# CCNA-Notes

--------

## Common CCNA Question 
What subnet does host 192.168.5.57/24 belong to?

subnet ID: ______/27

To find the network address we simply need to change all of the hosts bits to `0`

`**1100000| 10101000 | 000000101 | 001**11001`

 `192   .    168    .      5   .     57`

`**1100000| 10101000 | 000000101 | 001**00000` = **Answer: 192.168.5.32**



-------

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

----
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
---------
**FFFF:FFFF:FFFF** = broadcast MAC address. This is the destination MAC address when a device wants to send ethernet frames to all other devices on the local network.

When a switch broadcasts a frame, the switch shoots out the frame to all of its interfaces except the one interface, in which the arp request came from. 

Switches learn MAC addresses through the ARP process by storing the source MAC address of incoming devices. This is how a switchs build their dynamic ARP table

------
**What is an ARP Table?** 
Used to store IP address to MAC address association (mapping of IP to MAC address) 

> Use arp –a to view the ARP table (Windows, macOS, Linux)

------------
**Type of Entries in a ARP Tables: Static & Dynamic**

Type: Static = default entry

Dynamic = learned via ARP (This table is refreshed after 5 minutes)

-----
## Day 9 – Switches interface 
**CSMA/CD:** Carrier Sense Mutiple access with collision detection.
It describes how devices avoid collisions in a half-duplex situation, and how they react if collisions do occur. 

**Half-duplex:** Means device cannot send and receive data at the same time. If it is receiving a frame, it must wait before sending a frame.  (Example: Hubs Layer 1 devices, repeating whatever signals they receive)

**Full-duplex:** Means device can send and receive data at the same time. It does not have to wait (Example: Switches Layer 2)

## Interface Errors the same on a switch and a router:
Switch1#show interface g0/1

- Runts: Frames that are smaller than the minimum frame size (64 bytes)

- Giants: Frames that are larger than the maximum frame size (1518 bytes)

- CRC: Frames that failed the CRC check (in the ethernet FCS trailer)

- Frame: Frames that have an incorrect format (due to an error)

- Input errors: Total of various counters, such as the above four. 

- Output errors: Frames the switch tried to send, but failed due to an error

----
## Day 16 VLANs (part 1)

**What is a LAN?** 
The simple answer is: A LAN is a group of devices in a single location.

A more specific definition: A LAN is a single **broadcast domain**, including all devices in that broadcast domain. 

**A broadcast domain:** is the group of devices, which will receive a broadcast frame (dest MAC FFFF:FFFF:FFFF) sent by any one of its members.

![Screenshot 2025-04-28 221449](https://github.com/user-attachments/assets/ae653aec-7140-44fd-b9bc-8fc8aa4c6484)

**NOTES broadcast traffic** 
- Performance: Lots of unnecessary broadcast traffic can reduce network performance. 
- Security: In a LAN computers by default can reach each other directly without traffic passing through the routers (LAN traffic). This is a problem because the security policies we apply on a router/firewall wont have any effect, since the device can talk to each other without the need of a router.   

---------

**What is a VLAN?**
Its essentially a way to logically split up a Layer 2 broadcast domain to make mutiple separate broadcast domains. 

**What is the purpose of VLANs?**
- Improve Performance and Security.
- VLANs help to reduce unnecessary broadcast traffic, which helps prevent network congestion, and therefore improve network performance.
- VLANs improves network security by limiting broadcast and unknown unicast traffic. Since these messages won't be received by devices outside of the VLAN. 
 
**VLANS (Virtual Local Area Network)**
- VLANs are configured on switches on a per-interface basis
- VLANS Logically separate end hosts at layer 2

A switch WILL NOT forward traffic between VLANs, the switches must forward the traffic to a router. Routers are used to route between VLANs. 

Different types of VLANs
- **Default VLAN:** this is the VLAN that all interfaces are assigned to by default
- ?

> VLANs 1,1002-1005 exist by default and **cannot be deleted**
 
----
## Day 17 VLANs (part 2)

**What is a trunk port?** 

It's a switch interface that carries traffic over multiple VLANs  


**What is the purpose of a Trunk port?**

It allows switches to forward traffic from multiple VLANs over a single physical interface, instead of having to use a separate physical interface for every single VLAN


**VLAN Tagging**

Switches will **tag** all frames that they send over a trunk link. This allows the receiving switch to know which VLAN the frame belongs to. 

> Truck ports = "tagged" ports
> Access ports = "untagged" ports 

**802.1Q (dot1q)**
802.1Q is a tag inserted into the Ethernet frame and is used to identify which VLAN the frame belongs to when sent over a trunk.
The tag is inserted between the source and type/length fields of the ethernet frame. VID (Vlan ID) - identifies the VLAN the frame belongs to 

802.1Q has a feature called the **native VLAN.** 
**The native VLAN is VLAN 1** by default on all trunk ports, however this can be changed manually on each trunk port. 

Switches DO NOT add a 802.1Q tag to frames in the native VLAN. 
When a switch receives a untagged frame on a trunk port, it assumes the frame belongs to the native VLAN.

**its very important that the native VLAN matches between swtiches.** Switches will still forward traffic if there is native VLAN mismatch, which will cause traffic problems.

![Screenshot 2025-04-28 232948](https://github.com/user-attachments/assets/df6105cb-5a5d-4301-8d24-d372129c165e)


------





