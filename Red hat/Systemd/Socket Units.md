Another type of unit that is interesting to look at is the socket. A socket creates a method for applications to communicate with one another. 

- A socket may be defined as a file but also as a port on which Systemd will be listening for incoming connections.
- That way, a service doesn’t have to run continuously but instead will start only if a connection is coming in on the socket that is specified.
- Every socket needs a corresponding service file.

cockpit.socket file

![[Pasted image 20241211174956.png]]

- The important option in is **ListenStream**. This option defines the TCP port that Systemd should be listening to for incoming connections. 
- Sockets can also be created for UDP ports, in which case you would use **ListenDatagram** instead of **ListenStream**.