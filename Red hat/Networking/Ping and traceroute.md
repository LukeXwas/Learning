**ICMP Protocol**

The _Internet Control Message Protocol_ (ICMP) is a key protocol. It is primarily used for testing and diagnosing network connections. Commands such as _ping_ uses this protocol to send a stream of messages to remote network devices to examine their health and report statistical and diagnostic information.

The report includes the number of packets transmitted, received, and lost; a round-trip time for individual packets with an overall average; a percentage of packets lost during the communication; and so on.

Normally, **ping** works continuously on Linux; you’ll need to press CTRL-C to stop this command. If you need to verify a proper connection to a LAN, **ping** the IP address of the local network interface:

`# ping 192.168.56.100`

If possible, **ping** the address of the network’s connection to the Internet, which would be on the other side of the gateway. It may be the public IP address of your router on the Internet. Finally, **ping** the address of a computer that you know is active on the Internet.

**-c options set number of packets**

![[Pasted image 20241208232603.png]]

**Traceroute**

The traceroute command is provided by the traceroute RPM package. 

- traceroute automates the process just described by tracking the route path to a destination. For example, the following command finds the path to the IP address 192.168.20.5:

![[Pasted image 20241208232118.png]]

Look at the **-n** option in this command. This tells **traceroute** to display IP addresses rather than hostnames. The command also shows the round-trip time (RTT) to reach each hop along the path. By default, three different probes are sent for each hop.

Please note that some **traceroute** command options require root privileges.

**By default,** traceroute **relies on UDP probe packets with an increasing time-to-live (TTL) value in the IP header in order to find the route path to a given destination. Sometimes, a firewall along the path may block UDP packets. In that case, you may try to run** traceroute **with the** -I **or** -T **option to enable ICMP or TCP probe packets, respectively.**