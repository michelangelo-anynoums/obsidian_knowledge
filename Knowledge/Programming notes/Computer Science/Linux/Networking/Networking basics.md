============================ 1 lesson =============================

windows: ipconfig
linux: ip a or ifconfig

every network devices have an IP address

IPv4, SubnetMask, DefaultGateway

IP address has 4 octets x.x.x.x
0-255 range

192.168.1 = network portion
0 = host

192.168.1.0 = reserved IP address = network address
192.168.1.255 = broadcast IP = reserved IP address
192.168.1.1 = gateway IP = reserved IP address
Possible IP address of 255.255.255.0 subnet mask is 253 combinations.



=================================================================

======================== 2 lesson ==================================

IPv4 has over 4.3 billions of possible IPs (2^32)

There are different classes of IP: A, B, C, D and E ranges

Loop back IP has over 16 millions of IPs...

===================================================================

======================== 3 lesson ====================================

RFC 1918 = bandage for the problem of the lack of IP address.

What happened? NAT and private IPs

NAT = Network Address Translation
> Explain how it works

So basically, there are private network with ONE public IP (NAT) and many private IP in your network.

IPv4 = x.x.x.x = 4 numbers
IPv6 = x.x.x.x.x.x = 8 numbers = 2^128...








====================================================================