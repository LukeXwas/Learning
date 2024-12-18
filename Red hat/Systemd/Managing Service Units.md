The _systemctl_ command offers several subcommands to manage service units, including starting, stopping, restarting, and checking their status.

Now, run the following command:

**systemctl status rsyslog.service**

If you specify a unit name without an extension, by default systemd assumes that it is a service unit. Hence, a short version of the previous command is

**systemctl status rsyslog**

![[Pasted image 20241212122103.png]]

- On line 1, it shows the service description (read from the _/usr/lib/systemd/system/atd.service_ file)
- Line 2 illustrates the load status, which reveals the current load status of the unit configuration file in memory. Other possibilities for “Loaded” include “error” (if there was a problem loading the file), "not-found" (if no file associated with this unit was found), "bad-setting" (if a key setting was missing), and "masked" (if the unit configuration file is masked).
- Line 2 also tells us whether the service is set (enabled or disabled) for autostart at system boot.
- Line 3 exhibits the current activation status and the time the service was started.

An activation status designates the current state of the service. Possible states include:

![[Pasted image 20241212113443.png]]

To disable the service from autostarting at the next system reboot:

**systemctl disable \<service>**

![[Pasted image 20241212114418.png]]

The **systemctl** command can do more. With that command, you can change the boot state of a particular service. For example, in a system with the Postfix e-mail server installed, the following command checks if the Postfix service is configured to start at boot:

![[Pasted image 20241212122519.png]]

use the **systemctl enable** and **systemctl disable** commands to add services to or remove services from targets.

##### To make sure that the required services are started when your server boots use the **systemctl enable** \<service> commnad

When you enable a service, the **systemctl enable** command creates a symbolic link in the directory /etc/systemd/system/multi-user.target.wants that points to the corresponding unit configuration file in /usr/lib/systemd/system.

When a service is disabled, you can still start and stop it manually via the **systemctl start** and **stop** commands.

**systemctl Service Control Commands

![[Pasted image 20241212121941.png]]
![[Pasted image 20241212121954.png]]