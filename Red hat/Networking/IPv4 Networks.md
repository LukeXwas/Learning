IPv4 addresses are 32-bit binary numbers and are usually expressed in “dot-decimal” notation (such as 172.16.0.100), with each decimal octet representing 8 bits. 

An IP address is made up of two parts: a network (or _subnet_) address and a host part.

Three key IP components define a network:

![Images](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781260462081/files/square.jpg)   **Network address** Always the first IP address in a range

![Images](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781260462081/files/square.jpg)   **Broadcast address** Always the last address in the same range. This is the address that can be used to address all nodes in the network.

![Images](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781260462081/files/square.jpg)   **Subnet mask** Helps your computer define the network portion and the host portion of an IP address

You can assign IP addresses between the network and broadcast addresses (not including these addresses) to any computer on the network.

Private network addresses are addresses that are for use in internal networks only. Some specific IP network addresses have been reserved for this purpose:

- 10.0.0.0/8 (a single Class A network)
- 172.16.0.0/12 (16 Class B networks)
- 192.168.0.0/16 (256 Class C networks)

When private addresses are used, the nodes that are using them cannot access the Internet directly, and nodes from the Internet cannot easily access them.

Because that is not very convenient, **Network Address Translation (NAT)** is commonly used on the router that connects the private network to the Internet. In NAT, the nodes use a private IP address, but when accessing the Internet, this private IP address is replaced with the IP address of the NAT router. Hence, nodes on the Internet think that they are communicating with the NAT router, and not with the individual hosts.

The NAT router in its turn uses tables to keep track of all connections that currently exist for the hosts in the network. Based on this table, the NAT router helps make it possible for computers with a private IP address to connect to hosts on the Internet anyway. The use of NAT is very common; it is embedded in most routers that are used in home and small business networks to connect computers and other devices in those networks to the Internet.

Today, IP addresses are usually analyzed using a classless logic. That means that the subnet mask, rather than the address class, is used to determine the network and host parts of an IP address.

![[Pasted image 20241208225028.png]]

In addition, a number of private IP addresses are not to be assigned to any computer that is directly connected to the Internet. 

The most common private network ranges are defined in RFC 1918 and are associated with network addresses 
- 10.0.0.0–10.255.255.255
- 172.16.0.0–172.31.255.255
- 192.168.0.0–192.168.255.255. 
- In addition, network addresses 127.0.0.0 through 127.255.255.255 are reserved for loopback communication on a local host.

**Networks and Routing

IP address has two parts: a network part and a host identifier. To determine the network part and the host part, IP addresses are associated with a _subnet mask_ (also known as a _netmask_ or _prefix_). This is a 32-bit number made of a sequence of binary ones followed by zeros.

The subnet mask can be represented in the same dot-decimal notation used for IPv4 addresses. For example, 255.255.255.0 is a subnet mask made of 24 binary ones and 8 zeros. An alternative notation is known as Classless Inter-Domain Routing (CIDR) notation and consists of a slash character (/) followed by a number that indicates the amount of one bits in the netmask. As an example, the subnet mask 255.255.255.0 can be written as /24 in CIDR notation.

**Given an IP address and a subnet mask, all you have to do to determine the network portion of the IP address is provide a logical AND between the IP address and the netmask.**

As an example, suppose you are defining the range of addresses for a private network. Start with the private network address 192.168.56.0 and a subnet mask of 255.255.255.0. Based on this information, the broadcast address is 192.168.56.255, and the range of IP addresses that you can assign on that particular network is 192.168.56.1 through 192.168.56.254. That subnet mask is also defined by the number of associated bits, 24. In other words, the given network can be represented by 192.168.56.0/24.

![[Pasted image 20241208230913.png]]

To determine the subnet address for an arbitrary IP address, such as 192.168.12.72 with netmask 255.255.255.224, write the IP address in binary format. Then write the subnet mask in binary format with all network and subnet bits set to 1 and all node bits set to 0. Then perform a logical AND operation. For each matching 1 you get a 1, otherwise you get a 0. The following highlights the ANDed bits: