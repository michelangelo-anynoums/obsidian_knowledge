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

=========================== 4 lesson ==================================

Explain binary numbers.
Explain how to convert decimal numbers to binary numbers and vice-versa in a simple form.

=====================================================================

========================= 5 lesson ====================================

255.255.255.0 = classic subnet mask
It can have 256 IP addresses (2 IP are reserved = 254)

11111111.11111111.11111111.00000000

00000000 = last octet is the available IP addresses

2^(# of 0) = available IP addresses

We can get more!

11111111.11111111.11111110 <-- change it .00000000
Now we get 2^9 = 512 IP

=====================================================================

