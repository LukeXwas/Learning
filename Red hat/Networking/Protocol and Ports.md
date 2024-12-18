A _protocol_ is a set of rules governing the exchange of data between two network entities. These rules include how data is formatted, coded, and controlled. The rules also provide error handling, speed matching, and data packet sequencing.

In other words, a protocol is a common language that all nodes on the network speak and understand. Protocols are defined in the _/etc/protocols_ file. An excerpt from this file is provided below:

![[Pasted image 20241208231450.png]]

**TCP and UDP Protocols**

TCP (_Transmission Control Protocol_) and UDP (_User Datagram Protocol_) protocols are responsible for transporting data packets between network entities.

- TCP is reliable, connection-oriented, and point-to-point. It inspects for errors and sequencing upon a packet’s arrival on the destination node, and returns an acknowledgement to the source node, establishing a point-to-point connection with the peer TCP layer on the source node. If the packet is received with an error or if it is lost in transit, the destination node requests a resend of the packet. This ensures guaranteed data delivery and makes TCP reliable. Due to its reliability and connection-oriented nature, TCP is widely implemented in network applications.
- UDP, in contrast, is unreliable, connectionless, and multi-point. If a packet is lost or contains errors upon arrival at the destination, the source node is unaware of it. The destination node does not send an acknowledgment back to the source node. A common use of this protocol is in broadcast-only applications where reliability is not sought.

**Well-Known Ports**

Both TCP and UDP use ports for data transmission between a client and its server program. Ports are either well-known or private.

- A well-known port is reserved for an application’s exclusive use, and it is standardized across all network operating systems. Well-known ports are defined in the _/etc/services_ file, an excerpt of which is presented below:
![[Pasted image 20241208231720.png]]

Some common services and the ports they listen on are FTP (_File Transfer Protocol_) 21, SSH (_Secure Shell_) 22, SMTP (_Simple Mail Transfer Protocol_) 25, DNS (_Domain Name System_) 53, HTTP (_HyperText Transfer Protocol_) 80, NTP (_Network Time Protocol_) 123, secure HTTP (_HyperText Transfer Protocol Secure_) 443, and rsyslog 514.

- A private port, on the other hand, is an arbitrary number generated when a client application attempts to establish a communication session with its server process. This port number no longer exists after the session has ended.


