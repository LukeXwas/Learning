A mount unit specifies how a file system can be mounted on a specific directory. Mount units are an alternative for mounting file systems through /etc/fstab.

A Mount Unit File - tmp.mount unit file:

![[Pasted image 20241211173829.png]]

- **\[Unit]** The **Conflicts** statement is used to list units that cannot be used together with this unit. Use this statement for mutually exclusive units.
- **\[Mount]** This section defines exactly where the mount has to be performed. Here you see the arguments that are typically used in any **mount** command.
