Boot loader code does not disappear just like that, but on occasion it can happen that the GRUB 2 boot code gets damaged. In that case, you should know how to reinstall GRUB 2. The exact approach depends on whether your server is still in a bootable state.

- If it is in bootable state, reinstalling GRUB 2 is fairly easy. Just type **grub2-install** followed by the name of the device to which you want to install it. The command has many different options to fine-tune what exactly will be installed, but you probably will not need them because, by default, the command installs everything you need to make your system bootable again.

- Reinstalling GRUB 2 becomes a little bit more complicated if your machine is in a nonbootable state. 
	- If that happens, you first need to start a rescue system and restore access to your server from the rescue system.
	- After mounting your server’s file systems on /mnt/sysimage and using **chroot /mnt/sysimage** to make the mounted system image your root image
	- Run **grub2-install** to install GRUB 2 to the desired installation device.
	- If you are in a KVM virtual machine, run **grub2-install /dev/vda**, and if you are on a physical disk, run **grub2-install /dev/sda**.