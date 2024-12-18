**_Systemd_ (short for _system daemon_) is the system initialization and service management mechanism. _Systemd_ is the first process with PID 1 that spawns at boot and it is the last process that is terminated at shut down.** It is responsible for starting not only services but also a variety of other items.

To describe it in a generic way, the Systemd system and service manager is used to start stuff.

First, at boot, systemd activates only the services that are strictly required, whereas others are started on demand. As an example, systemd starts the CUPS printing service only when a print job is sent to the /var/spool/cups queue. In addition, systemd parallelizes the initialization of services.

Some Linux developers have argued that systemd does too much and breaks the Unix philosophy of writing programs that “do one thing and do it well.” However, as of today, systemd has been adopted by most of the major Linux distributions.