RHEL goes through multiple phases during the boot process. 

![[Pasted image 20241125203314.png]]

| Boot Phase                     | Configuring It                                                                                  | Fixing It                                                                                |
| ------------------------------ | ----------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| POST                           | Hardware configuration (F2, Esc, F10, or another key).                                          | Replace hardware.                                                                        |
| Selecting the bootable device  | BIOS/UEFI configuration or hardware boot menu.                                                  | Replace hardware or use rescue system.                                                   |
| Loading the boot loader        | **grub2-install** and edits to /etc/defaults/grub.                                              | Use the GRUB boot prompt and edits to /etc/defaults/grub, followed by **grub2-mkconfig** |
| Loading the kernel             | Edits to the GRUB configuration and /etc/ dracut.conf.                                          | Use the GRUB boot prompt and edits to /etc/defaults/grub, followed by **grub2-mkconfig** |
| Starting /sbin/init            | Compiled into initramfs.                                                                        | Use the **init =** kernel boot argument, **rd.break** kernel boot argument.              |
| Processing initrd.target       | Compiled into initramfs.                                                                        | Use the **dracut** command. (You won’t often have to troubleshoot this.)                 |
| Switch to the root file system | Edits to the /etc/fstab file.                                                                   | Apply edits to the /etc/fstab file.                                                      |
| Running the default target     | Using **systemctl set-default** to create the /etc/systemd/system/default.target symbolic link. | Start the rescue.target as a kernel boot argument.                                       |

1. Performing POST: The machine is powered on. From the system firmware, which can be the modern Universal Extended Firmware Interface (UEFI) or the classical Basic Input/Output System (BIOS), the Power-On Self-Test (POST) is executed, and the hardware that is required to start the system is initialized.
2. Power On Self Test (POST) - Based on settings stored in stable, read-only memory, the BIOS/UEFI system performs a series of diagnostics to detect and connect the CPU and key controllers. As it finds them, installs drivers for the graphics card and the attached monitor, and begins exhibiting system messages on the video hardware. 
3. Once complete, the BIOS/UEFI passes control to the boot device, typically the first drive, loads the bootloader program into memory. Either from the UEFI boot firmware or from the BIOS, a bootable device is located.
4. Loading the boot loader: From the bootable device, a boot loader is located. On RHEL, this is usually GRUB 2.  Red Hat has implemented GRUB 2 as the only bootloader for its Linux distributions. It’s normally configured to boot into a configured default kernel. GRUB 2 finds the configuration in the /boot directory.
5. The first stage of the GRUB 2 bootloader is normally copied to the MBR or GPT. It serves as a pointer to the other information from the GRUB 2 menu.
6. The boot loader may present a boot menu to the user or can be configured to automatically start a default operating system.

![[Pasted image 20241127215652.png]]

6. If you press a key before those five seconds are complete, GRUB 2 will present a menu similar to that. 

![[Pasted image 20241127215839.png]]

7. If the system includes more than one Linux kernel, or more than one operating system, there may be multiple choices available, which you can highlight with the UP ARROW and DOWN ARROW keys. To boot Linux from the highlighted option, press ENTER.
9. **Loading the kernel:** To load Linux, the kernel is loaded together with the initramfs. The initramfs contains kernel modules for all hardware that is required to boot, as well as the initial scripts required to proceed to the next stage of booting. On RHEL 9, the initramfs contains a complete operational system (which may be used for troubleshooting purposes).
10. **Starting /sbin/init:** Once the kernel is loaded into memory, the first of all processes is loaded, but still from the initramfs. This is the /sbin/init process, which on RHEL is linked to Systemd. The **systemd-udevd** daemon is loaded as well to take care of further hardware initialization. All this is still happening from the initramfs image.
11. **Processing initrd.target:** The Systemd process executes all units from the initrd.target, which prepares a minimal operating environment, where the root file system on disk is mounted on the /sysroot directory. At this point, enough is loaded to pass to the system installation that was written to the hard drive.
12. **Switching to the root file system:** The system switches to the root file system that is on disk and at this point can load the Systemd process from disk as well.
13. **Running the default target:** Systemd looks for the default target to execute and runs all of its units. In this process, a login screen is presented, and the user can authenticate. Note that the login prompt can be prompted before all Systemd unit files have been loaded successfully. So, seeing a login prompt does not necessarily mean that your server is fully operational yet; services may still be loaded in the background.


