A common scenario for a Linux administrator is that the root password has gone missing. If that happens, you need to reset it. The only way to do that is by booting into minimal mode, which allows you to log in without entering a password. To do so, follow these steps:

1. When you see the following message, press a key to access the GRUB 2 menu:

![[Pasted image 20241129000421.png]]

2. Press E to edit the current menu entry.
3. Scroll down with the DOWN ARROW key to locate the line starting with **linux**. Press CTRL-E or END to move to the end of the line, and then type the string **rd.break**.
4. Press CTRL-X to boot the system.
5. The **rd.break** directive interrupts the boot sequence before the root filesystem is properly mounted. Confirm this by running **ls /sysroot**. If you know the contents of the root filesystem, the output should look familiar.
6. Remount the root /sysroot filesystem as read-write and change the root directory to /sysroot
	1. Type two commands:

![[Pasted image 20241201173218.png]]

7. Now you can enter **passwd** and set the new password for the user root.
8. Because SELinux is not running, the **passwd** command does not preserve the context of the /etc/passwd file. To ensure that the /etc/passwd file is labeled with the correct SELinux context, instruct Linux to relabel all files at the next boot with the following command:

![[Pasted image 20241129000651.png]]

7. Type **exit** to close the chroot jail, and then type **exit** again to reboot the system.
8.  It may take a few minutes for SELinux to relabel all files. Once you get a login prompt, confirm that you are able to log in as the root user.
