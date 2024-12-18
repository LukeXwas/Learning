The **ss** command replaces the deprecated **netstat** tool to display network connections. With the right combination of command switches, it can show listening and nonlistening TCP and UDP sockets. 

**Socket is a communication method that allows two processes on the same or different systems to talk.**

During the operational state, systemd maintains the sockets and uses them to reconnect other daemons and services that were interacting with an old instance of a daemon before that daemon was terminated or restarted. Likewise, services that use activation based on D-Bus (_Desktop Bus_) are started when a client application attempts to communicate with them for the first time. Additional methods used by systemd for activation are device-based and path-based, with the former starting the service when a specific hardware type such as USB is plugged in, and the latter starting the service when a particular file or directory alters its state.

One command we like to use is:

![[Pasted image 20241208234043.png]]

- which shows all (**-a**) network sockets using IPv4 (**-4**) and both the TCP (**-t**) and UDP (**-u**) protocols in numeric (**-n**) format. If the **-p** switch is specified, **ss** also shows the process ID (PID) of the process using each socket.

![[Pasted image 20241209120554.png]]

At the end of the output, note the peer address of 192.168.122.1:47068. The 47068 port number is just the source port on the remote server. The corresponding local address of 192.168.122.100:22 specifies a port number of 22 (the local SSH service) for a connection from 192.168.122.1. You may also see a second entry with the same port number, which identifies the associated SSH daemon listening for connections. Other lines in this output identify other listening services.