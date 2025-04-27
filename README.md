# CCNA-Notes

**Day 13 Subnetting PART 1**

The IETF (Internet Engineering Task Force) introduced **CIDR** in 1993 to replace the "Classful" addressing system. With CIDR the classful requirments of: `Class A = /24, Class B = /16, Class C = /24` were removed. 

**CIDR allows for larger networks to be split into smaller networks**, allowing for greater efficiency. CIDR allows us to assign different prefix lengths `EX: /21 instead of /24 for a Class C.`

These smaller networks are called "subnetworks" or "subnets".

----
## Common CCNA Question 
What subnet does host 192.168.5.57/24 belong to?

subnet ID: ______/27

To find the network address we simply need to change all of the hosts bits to `0`

`**1100000| 10101000 | 000000101 | 001**11001`

 `192   .    168    .      5   .     57`

`**1100000| 10101000 | 000000101 | 001**00000` = **Answer: 192.168.5.32**

----






