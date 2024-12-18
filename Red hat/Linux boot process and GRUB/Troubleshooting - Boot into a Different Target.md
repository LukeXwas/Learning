When RHEL 9 is configured to boot into a GUI, it’s configured to boot into the graphical target by default. That target can be changed by appending a **systemd.unit=_name_.target** string to the end of the kernel command line.

- If you need direct access into a recovery shell, add the string **systemd.unit=rescue.target** to the end of the kernel command line. 
- In rare cases, some systems are so troubled, they don’t boot into the rescue target. In that case, you can boot the system into the emergency target by appending the string **systemd.unit=emergency.target** to the kernel command line. 
- The difference between rescue and emergency targets is that the former mounts the filesystems in read-write mode, while the latter does not mount any filesystems, apart from the root filesystem in read-only mode.

- The emergency and rescue targets require the root password to log in and get full root administrative privileges.
- If you have lost the root password, you will need to add the string **rd.break** to the end of the kernel command line
- As that supports full administrative privileges, including changes to the root administrative password, you may want to password-protect the GRUB 2 menu. Somebody who can change the boot order can achieve the same thing with a bootable USB drive, so it is also important to protect your BIOS or UEFI firmware to ensure the system only boots the local disk without a password. 

![[Pasted image 20241128233611.png]]

- **init=/bin/sh or init=/bin/bash:** This specifies that a shell should be started immediately after loading the kernel and initrd. This option provides the earliest possible access to a running system. You won’t have to enter the root password, but notice that only the root file system is mounted and it is still read-only.

**Boot into a Different Target** - how to do it:

1. Reboot your system using the **reboot** command.
2. When you see the following message, make sure to press any key to access the GRUB 2 menu:

`The selected entry will be started automatically in 5s.`

3.   Press E to edit the current menu entry.
4. Scroll down with the DOWN ARROW key to locate the line starting with **linux**. First, delete the kernel options **rhgb quiet**. Then, at the end of the line, type **systemd.unit=multi-user.target** and press CTRL-X to boot this kernel.

![[Pasted image 20241201173714.png]]

6. Enter the root password when you are prompted for it.
7. Type **systemctl list-units**. This shows all unit files that are currently loaded. You can see that a basic system environment has been loaded.
8. Type **systemctl show-environment**. This shows current shell environment variables.





