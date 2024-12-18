_NetworkManager_ is the default interface and connection configuration, administration, and monitoring service used in RHEL 9. This service has a daemon program called _NetworkManager_, which is responsible for keeping available interfaces and connections up and active.

- It offers a powerful command line tool called _nmcli_ to manage interfaces and connections, and to control the service. This utility offers many options for their effective management.
- The _NetworkManager_ service also furnishes a text-based interface called _nmtui_
- a graphical equivalent called _nm-connection-editor_

You can use the **systemctl status NetworkManager** command to verify its current status.

When NetworkManager comes up, it reads the network card configuration scripts, which are in /etc/NetworkManager/system-connections and have a name that starts with the name of the network interface the configuration applies to, like ens160.nmconnection.

**Understanding Interface Connection Profile**

The difference between a device and a connection:

- A **device** is a network interface card.
- A **connection** is the configuration that is used on a device.

- Each network connection has a configuration file that defines IP assignments and other relevant parameters for it. 
- The networking subsystem reads this file and applies the settings at the time the connection is activated.
- Connection configuration files (or _connection profiles_) are stored in a central location under the **_/etc/NetworkManager/system-connections_** directory.
- The filenames are identified by the interface connection names with nmconnection as the extension. Some instances of connection profiles are _enp0s3.nmconnection_, _ens160.nmconnection_, and _em1.nmconnection_.

In RHEL 9, you can create multiple connections for a device. This makes sense on mobile computers, for example, to differentiate between settings that are used to connect to the home network and settings that are used to connect to the corporate network. Switching between connections on devices is common on end-user computers but not so common on servers. To manage the network connections that you want to assign to devices, you use the **nmtui** command or the **nmcli** command.

##### If you want to make your configuration persistent, use **nmtui** or **nmcli** or **nm-connection-editor**.

**Working on Network Configuration Files**

Every connection that you create is stored as a configuration file in the directory /etc/NetworkManager/system-connections. The name of the configuration files starts with the name of the connection, followed by .nmconnection.

Example of a NetworkManager Connection File
![[Pasted image 20241209130407.png]]

- The file has multiple sections.
- Each section defines a set of networking properties for the connection.
- The output above shows five sections—connection, ethernet, ipv4, ipv6, and proxy.

![[Pasted image 20241209130937.png]]

There are hundreds of other properties that may be defined in connection profiles depending on the type of interface. Run **man nm-settings** for a description of additional properties.

Network Manager includes **nmcli** to control the status of the service and apply network configuration changes. Rather than modifying the configuration via **nmcli**, you can change a device configuration file directly.

After saving the file, you still have to notify Network Manager of the changes. This is achieved by running the following commands (**con** is short for **connection**):

![Images](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781260462081/files/f0102-03.jpg)

You have also applied the **ip addr add** command to temporarily set an IP address on a network interface. Everything you do with the **ip** command, though, is nonpersistent. 

###### If you want to make your configuration persistent, use **nmtui** or **nmcli** or **nm-connection-editor**.


