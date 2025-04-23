# CCNA-Notes

## 🟢 Day 1 – Network Devices

### What is a Client?
A client is a device that requests a service or resource made available by a server.

### What is a Server?
A server is a device that provides a resource or service to clients.  
> A client can also act as a server in some situations. For example, when two computers are connected, one computer may host a resource (acting as the server), while the other computer requests access to that resource (acting as the client).

---

### What is a Switch?
A switch is a device used to forward traffic (frames) within a LAN.

- Provides connectivity to hosts within the same LAN.
- Layer 2 switches do **not** separate different networks.
- Used to **connect and expand** networks (via interfaces).

---

### What is a Router?
A router is a device used to provide connectivity between different LANs.

- Connects multiple networks.
- Determines the best path to route traffic.
- Essential for sending data over the internet.

---

### What is a Firewall?
A firewall is a network security device that filters network traffic based on rules.

- Can be hardware or software-based.
- Used to **protect networks** from unwanted traffic.

---

## 🟡 Day 6 – Ethernet LAN Switching (Part 2)

### What is ARP?
ARP (Address Resolution Protocol) is used to discover the **MAC address** (Layer 2) of a known **IP address** (Layer 3).

- Learns MAC address of a device whose IP is already known.
- Consists of two messages:
  - **ARP Request**
  - **ARP Reply**

#### ARP Request
- Sent as a **broadcast** Ethernet frame.
- Since destination MAC is unknown, it’s broadcasted to all devices on the local network.

#### ARP Reply
- Sent as a **unicast** message to the requester only.

---

### Example ARP Request with Broadcast Address

```
Ping 192.168.1.3

Src IP: 192.168.1.1  
Dst IP: 192.168.1.3  
Src MAC: 9D00  
Dst MAC: FFFF:FFFF:FFFF
```

- `FFFF:FFFF:FFFF` is the **broadcast MAC address**.
- Switches forward broadcast frames to **all interfaces** except the one from which the frame originated.

---

### What is an ARP Table?

Used to store **IP-to-MAC address** mappings.

- Command: `arp –a` (Windows/macOS/Linux)
- **Types:**
  - Static = Default entry
  - Dynamic = Learned via ARP
- **Refresh interval:** Every 5 minutes

---

## 🔵 Day 8 – IPv4 Addressing

*(No notes provided yet.)*

---

## 🟣 Day 9 – Switch Interfaces

### CSMA/CD: Carrier Sense Multiple Access with Collision Detection

- Helps devices **avoid** and **handle** collisions in half-duplex environments.

#### Half-Duplex
- Device **cannot** send and receive at the same time.
- Must **wait** to send if it's receiving.
- Example: **Hubs** (Layer 1)

#### Full-Duplex
- Device **can** send and receive **simultaneously**.
- Example: **Switches** (Layer 2)

---

### Interface Errors (Same on Switch and Router)

**Command:**
```bash
Switch1# show interface g0/1
```

**Error Types:**

- **Runts:** Frames smaller than 64 bytes  
- **Giants:** Frames larger than 1518 bytes  
- **CRC:** Frames failed CRC check (FCS trailer error)  
- **Frame:** Frames with incorrect format  
- **Input errors:** Total of all input error types  
- **Output errors:** Frames the switch tried to send but failed

---
