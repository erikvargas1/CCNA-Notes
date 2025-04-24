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

------
## How to Calculate subnets Faster
![Screenshot 2025-04-24 002433](https://github.com/user-attachments/assets/1c110c3b-9f0e-48fe-8b4b-6bc4591cdc1e)

**Note: Borrowing 1 bit = can make 2 subnets** 

in this instance we need 5 subnets given a `192.168.255.0/24`, we will take 3 bits from the host bits to meet this requirement 3 bits will make 8 subnets. 2^3 = 8 subnets

**2^X = number of subnets 
(x = number of "borrowed" bits)**


`**1100000| 10101000 | 00000001| 111**00000`

 `192   .    168    .      255   .    0`  =  192.168.255.0/27


| Bit Value | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
|-----------|-----|----|----|----|---|---|---|---|
| Bit Set   |  1  | 1  | 1  | 0  | 0 | 0 | 0 | 0 |

Use the last octet of the network portion to calculate the next subnets. This is done by just adding the last octet over and over.

Starting with `192.168.255.0/27`, we increment by 32 for each new subnet:

### Subnet #2
```
192.168.255.0/24 + 32 = 192.168.255.32/27
```

### Subnet #3
```
192.168.255.32/24 + 32 = 192.168.255.64/27
```

### Subnet #4
```
192.168.255.64/24 + 32 = 192.168.255.96/27
```

### Subnet #5
```
192.168.255.128/24 + 32 = 192.168.255.128/27
```

Subnet 6 = 192.168.255.160/27

Subnet 7 = 192.168.255.192/27

Subnet 8  = 192.168.255.224/27

----
