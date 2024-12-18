**A Networking Primer**

TCP/IP is a series of protocols organized in layers, known as a protocol suite. It was developed for Unix and eventually adopted as the standard for communication on the Internet. IP addresses identify a network interface in an IP network, and IP addressing is one of the most important concepts of TCP/IP. A number of TCP/IP tools and configurations are available to help you manage a network.

To set up networking on a server, your server needs a unique address on the network. For this purpose, Internet Protocol (IP) addresses are used. Currently, two versions of IP addresses are relevant:

- **IPv4 addresses:** These are based on 32-bit addresses and have four octets, separated by dots, such as 192.168.10.100.
- **IPv6 addresses:** These are based on 128-bit addresses and are written in eight groups of hexadecimal numbers that are 16 bits each and separated by colons. An IPv6 address may look like fe80:badb:abe01:45bc:34ad:1313:6723:8798.


**IP Addresses**

Originally, IP addresses were assigned to computers and routers. Nowadays, many other devices also need IP addresses to communicate, such as smartphones, industrial equipment, and almost all other devices that are connected to the Internet.

To make it easier for computers to communicate with one another, every IP address belongs to a specific network, and to communicate with computers on another network, a router is used. A router is a machine (often dedicated hardware that has been created for that purpose) that connects networks to one another.

- Every network interface that communicates on a network needs its own IP address. Some addresses are assigned permanently to a network interface; these are known as _static_ IP addresses. 

- Others are leased from a Dynamic Host Configuration Protocol (DHCP) server for a limited amount of time; these are known as _dynamic_ IP addresses.

To communicate on the Internet, every computer needs a worldwide unique IP address. These addresses are scarce; a theoretical maximum of four billion IP addresses is available, and that is not enough to provide every device on the planet with an IP address. IPv6 is the ultimate solution for that problem, because a very large number of IP addresses can be created in IPv6. Because many networks still work with IPv4, though, another solution exists: private network addresses.

The loopback interface is used for communication between processes. Some processes use the IP protocol for internal communications. For that reason, you’ll always find a loopback interface, and the IP address of the loopback interface is always set to 127.0.0.1.

**_default gateway_**

Related to networking and routing is the concept of the _default gateway_. It’s a host that defines the junction between the local network and all other networks that your machine does not know how to reach. Although the gateway IP address is part of the local network, that address is assigned to a router, which may have an IP address on a different network, such as the public Internet. The default gateway IP address is normally configured in the routing table for the local system.

**ip route** command described the routing table for the local system

**IPv6 Addresses**

Let’s look at a valid IPv6 address, such as 02fb:0000:0000:0000:90ff:fe23:8998:1234. In this address, you can see that a long range of zeros occurs. To make IPv6 addresses more readable, you can replace one range of zeros with :: instead. Also, if an IPv6 address starts with a leading zero, you can omit it. So the previously mentioned IPv6 address can be rewritten as 2fb::90ff:fe23:8998:1234.

