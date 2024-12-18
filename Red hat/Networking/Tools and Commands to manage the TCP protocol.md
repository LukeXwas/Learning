In older versions of Red Hat Enterprise Linux, some of the most important network management commands were **ifconfig**, **arp**, **netstat**, and **route**. Those commands have been deprecated, in favor of the **ip** tool, which supports more advanced features.

![[Pasted image 20241208230835.png]]

With the **ip** utility, you can monitor many aspects of networking:
- Use **ip addr** to configure and monitor network addresses.
- Use **ip route** to configure and monitor routing information.
- Use **ip link** to configure and monitor network link state.

To show current network settings, you can use the **ip addr show** command (which can be abbreviated as **ip a s** or even as **ip a**)

![[Pasted image 20241208232840.png]]

In the result of this command, you see a listing of all network interfaces in your computer. The command shows the following items about its current status:

- **Current state:** The most important part of this line is the text state UP, which shows that this network card is currently up and available.
- **MAC address configuration:** This is the unique MAC address that is set for every network card. You can see the MAC address itself (00:0c:29:50:9e:c9), as well as the corresponding broadcast address.
- **IPv4 configuration:** This line shows the IP address that is currently set, as well as the subnet mask that is used. You can also see the broadcast address that is used for this network configuration. Notice that on some interfaces you may find multiple IPv4 addresses.
- **IPv6 configuration:** This line shows the current IPv6 address and its configuration. Even if you haven’t configured anything, every interface automatically gets an IPv6 address, which can be used for communication on the local network only. 

Run the **ip link show** command to review the link status of the active network adapters on the system.

![[Pasted image 20241208233917.png]]

**Routing Tables with ip route**

On every network that needs to communicate to nodes on other networks, routing is a requirement. Every network has, at least, a default router (also called the default gateway) that is set, and you can see which router is used as the default router by using the command **ip route show**

![[Pasted image 20241208233232.png]]

the most important part is the first line. It shows that the default route goes through (“via”) IP address 192.168.4.2, and also shows that network interface ens33 must be used to address that IP address. The line shows that this default route was assigned by a DHCP server. The metric is used in case multiple routes are available to the same destination. In that case, the route with the lowest metric will be used.

Next you can see lines that identify the local connected networks. When you’re booting, an entry is added for each local network as well, and in this example this applies to the networks 192.168.4.0 and 192.168.122.0. These routes are automatically generated and do not need to be managed.

**ARP**

- The Address Resolution Protocol (ARP) associates the hardware address of a network interface (MAC) with an IP address. 
- The **ip neigh** command displays a table of hardware and IP addresses on the local computer.
- This command can help detect problems such as duplicate addresses on the network. Such problems may happen with improperly configured systems or cloned virtual machines.
- If needed, you can use the **ip neigh** command to set or modify ARP table entries manually

Here’s sample output from the command, showing all ARP entries in the local database:

![[Pasted image 20241208233025.png]]

The first column in the output lists known IP addresses on the LAN, followed by the interface to which the neighbor is attached and its link layer address (MAC address). The last entry shows whether or not the neighbor’s hardware address is reachable. A STALE entry may indicate that its ARP cache timeout has expired since a packet was last seen from that host. If the ARP table is empty, no recent connections exist to other systems on the local network.

**Configure a Network Adapter with ip**

You can also use **ip** to assign IP address information. For example, the following command adds the noted IP address and network mask to the eth0 network adapter:

![[Pasted image 20241208234520.png]]

The first argument, **172.16.0.50/24**, specifies the new IP address and netmask. The next argument, **dev eth0**, tells you which device is being configured. To make sure the change worked, run the **ip addr show eth0** command again.

![[Pasted image 20241208234541.png]]

**The ip** command is useful for troubleshooting or to temporarily configure an IP address for troubleshooting a network problem. It is not the appropriate tool to make changes that persist after a system reboot, because any changes made with the **ip** command are, by definition, temporary. To configure permanent changes to the network configuration, use **nmcli** or manually modify the configuration files in the /etc/NetworkManager/system-connections directory, described shortly.

You have also applied the **ip addr add** command to temporarily set an IP address on a network interface. Everything you do with the **ip** command, though, is nonpersistent. 

**Activate and Deactivate Network Adapters**

It’s possible to use the **ip** command to activate and deactivate network adapters. For example, the following commands deactivate and reactivate the first Ethernet adapter:

![Images](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781260462081/files/f0099-02.jpg)