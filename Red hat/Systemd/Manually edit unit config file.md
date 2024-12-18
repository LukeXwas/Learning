When working with Systemd unit files, you risk getting overwhelmed by its many options. Every unit file can be configured with different options.

To figure out which options are available for a specific unit, use the **systemctl show** command.

To changing unit files use **systemctl edit** command.
- **systemctl edit httpd.service**

This command creates a subdirectory in /etc/systemd/system for the service that you are editing; for example, if you use systemctl edit sshd.service, you get a directory with the name /etc/systemd/systemd/sshd.service.d in which a file with the name override.conf is created. All settings that are applied in this file overwrite any existing settings in the service file in /usr/lib/systemd/system.

Zmiana edytora do konfiguracji plikow 

**export SYSTEMD_EDITOR=/bin/vim 

Enter **systemctl daemon-reload** to ensure that Systemd picks up the new configuration.

- **systemctl show sshd** command shows all Systemd options that can be configured in the sshd.service unit
![[Pasted image 20241212113909.png]]

