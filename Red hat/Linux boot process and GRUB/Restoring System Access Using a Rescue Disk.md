You need to be able to recover from a complete boot failure, such as if the GRUB 2 configuration file were corrupt or missing. In other words, if you’ve tried to boot directly from the grub> prompt described earlier and failed, you might need to resort to the option known as rescue mode. That requires access to the installation DVD or the network boot disk.

If you are lucky when you encounter trouble, you’ll still be able to boot from hard disk. If you are a bit less lucky, you’ll just see a blinking cursor on a system that does not boot at all. If that happens, you need a rescue disk. The default rescue image for Red Hat Enterprise Linux is on the installation disk. 

1. When booting from the installation disk, you’ll see a Troubleshooting menu item. Select this item to get access to the options you need to repair your machine.

![[Pasted image 20241201171134.png]]

2. After selecting the Troubleshooting option, you are presented with the following options:

![[Pasted image 20241201171220.png]]

- **Install Red Hat Enterprise Linux 9 in Basic Graphics Mode:** This option reinstalls your machine. Do not use it unless you want to troubleshoot a situation where a normal installation does not work and you need a basic graphics mode. Normally, you should never need to use this option to troubleshoot a broken installation.
- **Rescue a Red Hat Enterprise Linux System:** This is the most flexible rescue system. This should be the first option of choice when using a rescue disk.
- **Run a Memory Test:** Run this option if you encounter memory errors. It allows you to mark bad memory chips so that your machine can boot normally.
- **Boot from Local Drive:** If you cannot boot from GRUB on your hard disk, try this option first. It offers a boot loader that tries to install from your machine’s hard drive, and as such is the least intrusive option available.

3. Select the Rescue a Red Hat Enterprise Linux system option and press ENTER. Rescue mode runs a stable minimal version of the RHEL 9 operating system on the local machine. It’s in essence a text-only version of the “Live DVD” media available on other Linux distributions such as Knoppix or Ubuntu distributions.
4. After starting a rescue system, you usually need to enable full access to the on-disk installation.

![[Pasted image 20241201171454.png]]

5. The _Continue_ option, mounts all detected volumes as subdirectories of the /mnt/sysroot directory. 
	1. The _Read-Only Mount_ option mounts detected volumes in read-only mode. 
	2. The _Skip to Shell_ option moves straight to a command-line interface. 
6. Press 1 to accept the **Continue** option. After confirmation, you’ll be presented with a shell prompt.
7. If a valid Red Hat installation was found, you are prompted that your system has been mounted under /mnt/sysimage. At this point, you can press Enter to access the rescue shell.
8. Your Linux installation at this point is accessible through the /mnt/sysimage directory. Type **chroot /mnt/sysimage**. At this point, you have access to your root file system and you can access all tools that you need to repair access to your system.
9. Type **exit** to quit the **chroot** environment, and type **reboot** to restart your machine in a normal mode.

The **chroot** command changes the root directory, as if the /mnt/sysroot filesystem was mounted under /.