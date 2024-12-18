As a Linux server administrator, you need to manage network addresses and network interfaces. The network addresses can be assigned in two ways:

- **Fixed IP addresses:** Useful for servers and other computers that always need to be available at the same IP address.
- **Dynamically assigned IP addresses**: Useful for end users’ devices, and for instances in a cloud environment. To dynamically assign IP addresses, you usually use a Dynamic Host Configuration Protocol (DHCP) server.

**Network device**

_Network Interface Cards_ (NICs) are hardware adapters that provide one or more Ethernet ports for network connectivity.

- NICs may also be referred to as _network adapters_ and individual ports as _network interfaces_ or _network devices_.
- NICs may be built-in to the system board or are add-on adapters. They are available in one, two, and four port designs on a single adapter.
- For a long time, network cards in Linux have had default names, such as eth0, eth1, and eth2. This naming is assigned based on the order of detection of the network card.
- By default, Red Hat Enterprise Linux 9 names network interfaces based on their physical location, such as enoX for onboard Ethernet interfaces and enpXsY for PCI slots.
- RHEL 9 uses the traditional enumeration method of eth0, eth1, etc., only as a fallback choice.

The first onboard network interface to be named _eno1_, while an interface located on PCI bus 3, slot 0, would be named _enp3s0_

![[Pasted image 20241209122226.png]]

In RHEL 9, the default names for network cards are based on firmware, device topology, and device types. This leads to network card names that always consist of the following parts:

- Ethernet interfaces begin with _en_, WLAN interfaces begin with _wl_, and WWAN interfaces begin with _ww_.
- The next part of the name represents the type of adapter. An _o_ is used for onboard, _s_ is for a hotplug slot, and _p_ is for a PCI location. Administrators can also use _x_ to create a device name that is based on the MAC address of the network card.
- Then follows a number, which is used to represent an index, ID, or port.
- If the fixed name cannot be determined, traditional names such as eth0 are used.

Based on this information, device names such as eno16777734 can be used, which stands for an onboard Ethernet device, with its unique index number.
