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

- Use **arp –a** to view the ARP table (Windows, macOS, Linux)

**Type of Entries in a ARP Tables: Static & Dynamic**

Type: Static = default entry

Dynamic = learned via ARP (This table is refreshed after 5 minutes)

----
## Day 16 VLANs (part 1)

**What is a LAN?** 
The simple answer is: A LAN is a group of devices in a single location.

A more specific definition: A LAN is a single **broadcast domain**, including all devices in that broadcast domain. 

**A broadcast domain:** is the group of devices, which will receive a broadcast frame (dest MAC FFFF:FFFF:FFFF) sent by any one of its members.

<img width="500" alt="image" src="https://github.com/user-attachments/assets/ae653aec-7140-44fd-b9bc-8fc8aa4c6484">

**NOTES broadcast traffic** 
- Performance: Lots of unnecessary broadcast traffic can reduce network performance. 
- Security: In a LAN computers by default can reach each other directly without traffic passing through the routers (LAN traffic). This is a problem because the security policies we apply on a router/firewall wont have any effect, since the device can talk to each other without the need of a router.   

---------

**What is a VLAN?**
Its essentially a way to logically split up a Layer 2 broadcast domain to make multiple separate broadcast domains. 

**What is the purpose of VLANs?**
- Improves performance and security.
- VLANs help to reduce unnecessary broadcast traffic, which helps prevent network congestion, and therefore improve network performance.
- VLANs improves network security by limiting broadcast and unknown unicast traffic. Since these messages won't be received by devices outside of the VLAN. 
 
**VLANS (Virtual Local Area Network)**
- VLANs are configured on switches on a per-interface basis
- VLANS Logically separate end hosts at layer 2

A switch WILL NOT forward traffic between VLANs, the switches must forward the traffic to a router. Routers are used to route between VLANs. 

- **Default VLAN:** this is the VLAN that all interfaces are assigned to by default

- VLANs 1,1002-1005 exist by default and **cannot be deleted**
 
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
802.1Q is a tag inserted into the Ethernet frame and is used to identify which VLAN the frame belongs to when sent over a trunk. VID (Vlan ID) - identifies the VLAN the frame belongs to 

802.1Q has a feature called the **native VLAN.** 
**The native VLAN is VLAN 1** by default on all trunk ports, However this can be changed manually on each trunk port. 

Switches DO NOT add a 802.1Q tag to frames in the native VLAN. 
When a switch receives a untagged frame on a trunk port, it assumes the frame belongs to the native VLAN.

**its very important that the native VLAN matches between swtiches.** Switches will still forward traffic if there is native VLAN mismatch, which will cause traffic problems.

<img width="500" alt="image" src="https://github.com/user-attachments/assets/df6105cb-5a5d-4301-8d24-d372129c165e">


------
## Day 20 Spanning tree protocol

`Since STP is so important switches from ALL vendors run STP by default.`

STP prevents Layer 2 **loops** (broadcast storm) by placing redundant ports in a **blocking state**, essentialy disabling the interface. These interfaces act as backups that can enter a forwarding state if an active (currently forwarding) interface fails.

Interfaces in a **forwarding state** behave normally. They send and receive all normal traffic. 

However, **Interfaces in a blocking state** only send or receive **STP messages** called `(BPDUs = Bridge Protocol Data Units)`, and some other specific traffic.

By selecting which ports are **forwarding** and which ports are **blocking,** STP creates a single path to/from each point in the network. This prevents layer 2 loops. 

-------
##  Spanning tree protocol

STP-enabled switches send/receive **Hello BPDUs** out of all interfaces, the default timer is 2 seconds. If a switch receives a *Hello BPDU* on an interface, it knows that the interface is connected to another switch.. `(routers, PCs, etc do not use STP, so they do not send Hello BPDUs).`

**What are these BPDUs used for?**
- Switches use the STP BPDU **Bridge ID** field, to elect a **root bridge** for the network.
- The switch with the **lowest Bridge ID** becomes the root bridge


So, as I mentioned previously STP puts switch ports in either a **blocking** or **forwarding** state, to avoid Layer 2 loops in the network. 

`However ALL ports on the root bridge are put in a forwarding state, and other switches in the topology must have a path to reach the root bridge.`

<img width="500" alt="image" src="https://github.com/user-attachments/assets/add81076-e56d-4e6e-9b34-57f681d9046a">

> The bridge priority has been updated to be made of two parts, the bridge priority which is 4 bits, and the ‘extended system ID’, which is just the VLAN ID, which is 12 bits

<img width="500" alt="image" src="https://github.com/user-attachments/assets/5241ef3a-8a2f-47b6-b8ab-b86f9e359734">

----

All interfaces on the root bridge are **designated ports.** Designated ports are in a forwarding state. 

When a switch is powered on, it assumes it is the root bridge. It will only give up its position if it receives a "superior BPDU" (lower bridge ID). Once the topology has converged and all switches agree on the root bridge, only the root bridge sends BPDUs. 

The reason all switches send BPDUs at first is because they all think they are the root bridge.


## The first criteria for root port selection is the port with the lowest root cost.

The interface with the lowest root cost will be the root port. Root ports are also in a forwarding state.

**Now let’s talk about what that ‘root cost’ is?**

**Remember these path costs for the exam** 

<img width="500" alt="image" src="https://github.com/user-attachments/assets/8e2fa1da-8210-487b-a357-4cb884203636">

-----
## Explains how switches determine their root port based on root cost 

<img width="500" alt="image" src="https://github.com/user-attachments/assets/18ff38ea-e03b-4868-95d8-76b3f13bb603">

The root cost is the total cost of the outgoing interfaces along the path to the root bridge. SW1 is the **root bridge**, so it has a cost of 0 on all interfaces. The ports connected to another switch's root port MUST be designated. Because the root port is the swtich's path to the root bridge, another switch must not block it. 

----

So far we have covered the first step of the spanning-tree’s process. To Review:

`Step 1:` The switch with the lowest bridge ID is elected as the **root bridge.** All ports on the root bridge are **designated ports,** so they are in a forwarding state. It’s important that this is the first step that spanning tree takes, because the rest of the steps depend on knowing which switch is the root bridge. 

**Root Bridge selection:**

**1: Lowest bridge ID**

----

`Step 2:` All other switches will select **ONE** of its ports to be its **‘root port’ (forwarding state).** So, that means there is **one root port on each switch in the network**, EXCEPT on the root bridge. **Ports across from the root port** are always "Designated ports".

**Root port selection: **

**1: Lowest root cost**

**What if a switch has multiple ports with the same root cost?** In that case, the interface connected to the neighbor with the lowest bridge ID will be selected as the root port.

**2) Lowest neighbor bridge ID (priority)**

**What if two switches have two connections between them, so both the root coost and the neighbor bridge ID are the same?**

**3) Lowest neighbor port ID**

<img width="500" alt="image" src="https://github.com/user-attachments/assets/e78e60b1-b92c-45bc-8bcb-ac56928951b4">

STP Port ID = port priority (default 128) + port number. In this case the port number is used as a tiebreaker if the priorities tie. Usually you dont need to worry about it, so you can just look at the port number. 


<img width="500" alt="image" src="https://github.com/user-attachments/assets/222c3241-416d-4486-a459-f937a5430aa3">

-------

*Every collision domain has a single SPT designated port.* Which we use switches each link is a separate collison domain. 

<img width="500" alt="image" src="https://github.com/user-attachments/assets/f2789ce3-5faf-4a63-a5a3-5ed86b9fbb58">

-----
## OVERVIEW STP Proccess 
So, here is the process for selecting the different port roles and states in spanning tree.

<img width="500" alt="image" src="https://github.com/user-attachments/assets/ae5700f5-5eaf-42c5-b644-c89bffd65994">

------

<img width="500" alt="image" src="https://github.com/user-attachments/assets/9d12a61e-a801-4113-be36-c2ccaacb661d">

-----
## Day 21 Spanning tree protocol (PART 2)

**Remember these for the Exam**

<img width="500" alt="image" src="https://github.com/user-attachments/assets/880050c4-0714-4379-9603-fe5360ae104a">

<img width="500" alt="image" src="https://github.com/user-attachments/assets/535e5e31-dec4-4503-a71d-5ac80fd91a83">

Cisco’s PVST+ uses the destination MAC address of ```01:00.0c:cc:cc:cd``` for its BPDUs. Modern Cisco switches run rapid-PVST by default, and usually there is no reason to change it.

Regular STP (NOT Cisco's PVST+) uses a destination MAC address of ```0180.c200.0000```

------

**Port Fast**

<img width="500" alt="image" src="https://github.com/user-attachments/assets/c6bea762-3be7-4b67-8013-4afdf41f6441">

PortFast allows a port to move immediately to the Forwarding state, bypassing **Listening and Learning.** If used, it must be enabled only on ports **connected to end hosts.** (this can save time because Listening and Learning takes a total of 15 seconds each)
If enabled on a port connected to another switch it could cause a Layer 2 loop.

So, PortFast is a great feature for getting a switchport connected to an end host running quickly without having to wait 30 seconds. However, it can still be a risk. What if an employee plugs another switch into the network like this?

<img width="500" alt="image" src="https://github.com/user-attachments/assets/a5ce033f-88e4-4001-b4a1-c12512444049">

This employee doesn’t necessarily have malicious intent, they could just be unaware of exactly what they are doing. Because PortFast is putting these interfaces into a forwarding state, a Layer 2 loop is formed. PortFast can also cause loops if the network cabling is changed without proper caution, perhaps a host is moved to a different switchport and a switch is connected to its old port.

However, there is an additional spanning tree optional feature that we can enable to protect against such loops. It’s called **BPDU Guard.**

------
**BPDU Guard**

<details>
Not part of the CCNA. At least know the name and basic purpose of, just in case they are mentioned in the exam.

<img width="500" alt="image" src="https://github.com/user-attachments/assets/64bf6f98-67cd-4367-bf65-3a9c9904f1c4">

</details>

What is BPDU Guard? 
If an interface with BPDU Guard enabled receives a BPDU from another switch, the interface will be shut down to prevent a loop from forming.

<img width="500" alt="image" src="https://github.com/user-attachments/assets/b3ec38d1-39d0-44cd-80c7-afde94864f82">

----

**Primary & Secondary root bridge**

You can see what happens when a BPDU arrives on a BPDU guard-enabled port. The port is disabled, it is effectively shut down.
**What if you want to enable the port again?** To enable a port that was disabled by BPDU guard, simply **SHUTDOWN**, and then **NO SHUTDOWN**

You can also manually configure the root bridge by manipulating the bridge priority of a switch. With these MAC addresses and the default priority values, SW1 is the root bridge. However, we could configure SW3 to be the root bridge. We could also configure something called a ‘secondary’ root bridge, which will be next in line to become the root bridge if the current root bridge fails.

<img width="500" alt="image" src="https://github.com/user-attachments/assets/ac7a6a24-2f95-473d-97b8-481f50755e05">


