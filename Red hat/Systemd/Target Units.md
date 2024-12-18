cdThe unit files are used to build the functionality that is needed on your server. To make it possible to load them in the right order and at the right moment, you use a specific type of unit: **the target unit**

- Some targets are used to define the state a server should be started in.
- Targets by themselves can have dependencies on other targets. These dependencies are defined in the target unit. An example of such a dependency relation is the basic.target. This target defines all the units that should always be started.
- Each target may be associated with several systemd units. Each unit can start or stop Linux services such as printing (**cupsd**). When configured, the boot process starts and stops the systemd units of your choice. These units are known as dependencies.

A Target Unit File
![[Pasted image 20241212000831.png]]

- You can see that by itself the target unit does not contain any information about the units that it should start.
- It just defines what it requires and which services and targets it cannot coexist with.
- It also defines load ordering, by using the **After** statement in the \[Unit] section.
- The target file does not contain any information about the units that should be included; that is defined in the \[Install] section of the different unit files.

When you add a unit to a target, under the hood a symbolic link is created in the target directory in /etc/systemd/system. If, for instance, you enabled the vsftpd service to be automatically started, you’ll find that a symbolic link /etc/systemd/system/multi-user.target/wants/vsftpd.service has been added, pointing to the unit file in /usr/lib/systemd/system/vsftpd.service and thus ensuring that the unit will automatically be started. In Systemd terminology, this symbolic link is known as a **want**, as it defines what the target wants to start when it is processed.

**Understanding Wants

**_Wants_ in Systemd define which units Systemd wants when starting a specific target.** Wants are created when Systemd units are enabled using **systemctl enable**, and this happens by creating a symbolic link in the /etc/systemd/system directory. In this directory, you’ll find a subdirectory for every target, containing wants as symbolic links to specific services that are to be started. The multi-user.target, for instance, contains its wants in /etc/systemd/system/multi-user.target.wants/.