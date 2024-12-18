_nmcli_ is a NetworkManager command line tool that is employed to create, view, modify, remove, activate, and deactivate network connections, and to control and report network device status. It operates on seven different object categories, with each category supporting several options to form a complete command.

Using **nmcli** might seem difficult. It’s not, because it offers excellent command-line completion features—just make sure that the **bash-completion** package has been installed. Try it by typing **nmcli**, but don’t press Enter! Instead, press the Tab key twice—you will see all available options that **nmcli** expects at this moment.

| **Object**                                                                  | **Description**                                                    |
| --------------------------------------------------------------------------- | ------------------------------------------------------------------ |
| **Connection: activates, deactivates, and administers network connections** |                                                                    |
| show                                                                        | Lists connections                                                  |
| up / down                                                                   | Activates/deactivates a connection                                 |
| add                                                                         | Adds a connection                                                  |
| edit                                                                        | Edits an existing connection or adds a new one                     |
| modify                                                                      | Modifies one or more properties of a connection                    |
| delete                                                                      | Deletes a connection                                               |
| reload                                                                      | Instructs NetworkManager to re-read all connection profiles        |
| load                                                                        | Instructs NetworkManager to re-read a connection profile           |
| **Device: displays and administers network interfaces**                     |                                                                    |
| status                                                                      | Exhibits device status                                             |
| show                                                                        | Displays detailed information about all or the specified interface |

**Required Permissions to Change Network Configuration**

- The root user can make modifications to current networking
- if an ordinary user is logged in to the local console, this user is able to make changes to the network configuration. As long as the user is using the system keyboard to enter either a graphical console or a text-based console, these permissions are granted.
- Regular users who have used **ssh** to connect to a server are not allowed to change the network configuration.

To check your current permissions, use the **nmcli general permissions** command:
![[Pasted image 20241209124258.png]]

RHEL 9 uses a service known as Network Manager to monitor and manage network settings. Using the **nmcli** command-line tool, you can interact with Network Manager and display the current status of network devices:

`# nmcli dev status`

The command should list configured and active devices. If a key device such as eth0 is not listed as connected, your network connection is probably down or the device is not configured. Key configuration files are located in the /etc/NetworkManager/system-connections directory.

Sometimes mistakes happen. If you’ve deactivated an adapter or just lost a wireless connection, try something simple: restart networking. The following command restarts networking with current configuration files:

![Pasted image 20241209125643.png](app://856eab8c45a34dd32ea74e1c02ed9d582efc/home/lwasiele/learning/Linux%20certification/Screenshot/Pasted%20image%2020241209125643.png?1733745403503)

**How to configure connections using nmcli**

Network Manager can store different profiles, also known as _connections_, for the same network interface. This allows you to switch from one profile to another. For example, you may have a home profile and a work profile for a laptop Ethernet adapter and switch between the two depending on the network to which you are attached.

You can display all the configured connections in Network Manager by running the following command:
![[Pasted image 20241209225322.png]]

- **nmcli con show enh0 - this command shows many properties followed by the name of the connection

**How to create new "static" connections**

![Images](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781260462081/files/f0103-03.jpg)

Then, a static IP address and default gateway can be configured, as shown here:

![[Pasted image 20241209225637.png]]

To add a DNS server to the eth-work connection, run
![[Pasted image 20241209225726.png]]

Add a DNS server to the static connection by using **nmcli con mod static ipv4.dns 10.0.0.10**. Notice that while adding a network connection, you use **ip4**, but while modifying parameters for an existing connection, you often use **ipv4** instead. This is not a typo; it is just how it works.

To add a second item for the same parameters, use a + sign. Test this by adding a second DNS server, using **nmcli con mod static +ipv4.dns 8.8.8.8**.

Finally, to switch to the new connection profile, run
![[Pasted image 20241209225746.png]]

You can prevent a connection from starting automatically at boot with the following command:
![[Pasted image 20241209225817.png]]

**How to create dynamic connections"

**nmcli con add con-name dhcp type ethernet ifname ens33 ipv4.method auto**.

To restore the original configuration, restore the *.nmconnection file to the /etc/NetworkManager/system-connections directory and run **nmcli conn reload**

Type **man nmcli-examples** to show this man page; you’ll notice that if you can find this man page, you can do almost anything with **nmcli**.