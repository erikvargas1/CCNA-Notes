# CCNA-Notes

**Day 13 Subnetting PART 1**

The IETF (Internet Engineering Task Force) introduced **CIDR** in 1993 to replace the "Classful" addressing system. With CIDR the classful requirments of: `Class A = /24, Class B = /16, Class C = /24` were removed. 

**CIDR allows for larger networks to be split into smaller networks**, allowing for greater efficiency. CIDR allows us to assign different prefix lengths `EX: /21 instead of /24 for a Class C.`

These smaller networks are called "subnetworks" or "subnets".

---------
**How to calculate # of usable host addresses in a network?**

`2^N - 2 = usable addresses`

N = number of host bits 
-2 = For the Network address and the Broadcast address

NOTES: /31 subnet mask can be used for a point-to-point Router connection. /32 can be used when you want to create a static route not to a network but to a specific host.

I like using /30 for PTP Router connections. Since you will have 4 addresses: one for the network and one for the broadcast. And the last 2 for each interface 

---------
**How to find the remaining subnets?**

- Subnet 1: 192.168.1.0/26
- Subnet 2: ?
- Subnet 3: ?
- Subnet 4: ?

HINT: Find the broadcast address of Subnet 1. The next address is the network address of Subnet 2. Repeat the proccess for Subnet 3 and 4. 

**To find the broadcast address flip all the host bits to** `1`


`**1100000| 10101000 | 00000001| 00**000000`
  
  `192   .    168    .      1   .     0`


`**1100000| 10101000 | 00000001| 00**111111`

**broadcast addresss= 192.168.1.63** Therefore the subnet range is: **192.168.1.0 - 192.168.1.63**

The network address of Subnet 2 will be `1` higher than the broadcast address

----

**Subnet 2 Network Address = 192.168.1.64**

                              
`**1100000| 10101000 | 00000001| 01**000000`

  `192   .    168    .      1   .     64`
  
`**1100000| 10101000 | 00000001| 01**111111`

**broadcast addresss= 192.168.1.127** Therefore the subnet range is: **192.168.1.64 - 192.168.1.127**

-----

**Subnet 3 Network Address = 192.168.1.128**

                              
`**1100000| 10101000 | 00000001| 10**000000`

  `192   .    168    .      1   .     128`
  
`**1100000| 10101000 | 00000001| 10**111111`

**broadcast addresss= 192.168.1.191** Therefore the subnet range is: **192.168.1.128 - 192.168.1.191**

-----
This time the borrowed bits are `all 1`, so this is our last subnet, we don’t have any room for more.

**Subnet 4 Network Address = 192.168.1.192**

`**1100000| 10101000 | 00000001| 11**000000`

 `192   .    168    .      1   .     192`

`**1100000| 10101000 | 00000001| 11**111111`

**broadcast addresss= 192.168.1.255** Therefore the subnet range is: **192.168.1.192 - 192.168.1.255**

