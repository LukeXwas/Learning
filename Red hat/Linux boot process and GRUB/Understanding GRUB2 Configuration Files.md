**Understanding GRUB2 Configuration Files**

- The GRUB2 configuration file, _grub.cfg_, is located in the _/boot/grub2_ directory.
- This file is referenced at boot time.
- This file is generated automatically when a new kernel is installed or upgraded, so it is not advisable to modify it directly, as your changes will be overwritten.
- The primary source file that is used to regenerate _grub.cfg_ is called _grub_, and it is located in the _/etc/default_ directory.
- This file defines the directives that govern how GRUB2 should behave at boot time. Any changes made to the _grub_ file will only take effect after the _grub2-mkconfig_ utility has been executed.

**The /etc/default/grub File**

- The _grub_ file defines the directives that control the behavior of GRUB2 at boot time.
- Any changes in this file must be followed by the execution of the _grub2-mkconfig_ command in order to be reflected in _grub.cfg_.
- **Generally, you do not need to make any changes to this file, as the default settings are good enough for normal system operation.**

![[Pasted image 20241127204052.png]]

| **Directive**         | **Description**                                                                               |
| --------------------- | --------------------------------------------------------------------------------------------- |
| GRUB_TIMEOUT          | Defines the wait time, in seconds, before booting off the default kernel. Default value is 5. |
| GRUB_DISTRIBUTOR      | Sets the name of the Linux distribution                                                       |
| GRUB_DEFAULT          | Boots the selected option from the previous system boot                                       |
| GRUB_DISABLE_SUBMENU  | Enables/disables the appearance of GRUB2 submenu                                              |
| GRUB_TERMINAL_OUTPUT  | Sets the default terminal                                                                     |
| GRUB_CMDLINE_LINUX    | Specifies the command line options to pass to the kernel at boot time                         |
| GRUB_DISABLE_RECOVERY | Lists/hides system recovery entries in the GRUB2 menu                                         |
| GRUB_ENABLE_BLSCFG    | Defines whether to use the new bootloader specification to manage bootloader configuration    |
**The grub.cfg File**

- The _grub.cfg_ is the main GRUB2 configuration file that supplies boot-time configuration information.
- This file is located in the _/boot/grub2_ directory on BIOS-based systems and in the _/boot/efi/EFI/redhat_ directory on UEFI-based systems.
- **This file can be recreated manually with the _grub2-mkconfig_ utility, or it is automatically regenerated when a new kernel is installed or upgraded.**
- In either case, this file will lose any previous manual changes made to it.
- During the recreation process, the _grub2-mkconfig_ command also uses the settings defined in helper scripts located in the _/etc/grub.d_ directory.

![[Pasted image 20241128114909.png]]
- 
The first script, _00_header_, sets the GRUB2 environment; the _10_linux_ script searches for all installed kernels on the same disk partition; the _30_os-prober_ searches for the presence of other operating systems; and _40_custom_ and _41_custom_ store user customizations. An example would be to add custom entries to the boot menu.

The _grub.cfg_ file also sources the _grubenv_ file located in the _/boot/grub2_ directory for kernel options and other settings. 

![[Pasted image 20241128115044.png]]

If a new kernel is installed, the existing kernel entries remain intact. All bootable kernels are listed in the GRUB2 menu, and any of the kernel entries can be selected to boot.

**grub2-mkconfig** - command to reproduce _grub.cfg_. After this command restart the system with _sudo reboot_.

example - In this exercise, you will change the default system boot timeout value to 8 seconds persistently, and validate:

1. Edit the _/etc/default/grub_ file and change the setting as follows:

![](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781835887325/files/html/images/264_1.jpg)

2. Execute the _grub2-mkconfig_ command to reproduce _grub.cfg_:

![](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781835887325/files/html/images/264_2.jpg)

3. Restart the system with _sudo reboot_ and confirm the new timeout value when GRUB2 menu appears.



