# CCNA-Notes

**Day 13 Subnetting PART 1**

The IETF (Internet Engineering Task Force) introduced **CIDR** in 1993 to replace the "Classful" addressing system. With CIDR the classful requirments of: Class A = /24, Class B = /16, Class C = /24 were removed. 

**CIDR allows for larger networks to be split into smaller networks**, allowing for greater efficiency. CIDR allows us to assign different prefix lengths EX: /21 instead of /24 for a Class C.

These smaller networks are called "subnetworks" or "subnets".

---------
How to calculate how many usable host address in a network 

2^N - 2 = usable addresses

N = number of host bits 
-2 = For the Network address and the Broadcast address

NOTES: /31 subnet mask can be used for a point-to-point Router connection. /32 can be used when you want to create a static route not to a network but to a specific host.

I like using /30 for PTP Router connections. Since you will have 4 addresses: one for the network and one for the broadcast. And the last 2 for each interface 

