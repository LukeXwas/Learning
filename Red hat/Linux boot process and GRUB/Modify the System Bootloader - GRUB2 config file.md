How to configure GRUB 2 in detail?

- Normally, GRUB 2 works just fine and does not need much maintenance.
- In some cases, though, you might have to change its configuration. To apply changes to the GRUB 2 configuration, the starting point is the **/etc/default/grub** file, which has options that tell GRUB what to do and how to do it.

**GRUB 2 config file**

Based on the configuration files **/etc/default/grub and configuration files in /etc/grub.d**, the main configuration of GRUB 2 file is created

- If your system is a **BIOS system**, the name of the GRUB 2 config file is **/boot/grub2/grub.cfg**
- On a **UEFI system** the the GRUB 2 config file is written to **/boot/efi/EFI/redhat/grub.cfg** on RHEL and **/boot/efi/EFI/centos/grub.cfg** on CentOS.

**You should know the name of the GRUB 2 config file that applies to your system architecture**, **do not manually edit the /boot/grub2/grub.cfg file. Use** grub2-mkconfig **and the /etc/default/grub file to make modifications to grub.cfg.**

**Modifying Default GRUB 2 Boot Options**

The primary source file that is used to regenerate _grub.cfg_ is called _grub_, and it is located in the _/etc/default_ directory. The right approach is to generate a new version of this file with the **grub2-mkconfig** tool, based on the /etc/default/grub configuration file and on the scripts in the /etc/grub.d/ directory.

Once you have made a modification to /etc/default/grub, generate the new GRUB configuration file by running:

![[Pasted image 20241128175127.png]]
- On a BIOS system, the command would be **grub2-mkconfig -o /boot/grub2/grub.cfg**
- UEFI system the command would be **grub2-mkconfig -o /boot/efi/EFI/redhat/grub.cfg**.

**Restart the system with _sudo reboot_ and confirm the new timeout value when GRUB2 menu appears.**

Apart from the configuration in /etc/default/grub, there are a few configuration files in /etc/grub.d. In these files, you’ll find rather complicated shell code that tells GRUB what to load and how to load it. You typically do not have to modify these files. You also do not need to modify anything if you want the capability to select from different kernels while booting. GRUB 2 picks up new kernels automatically and adds them to the boot menu automatically, so nothing has to be added manually.

**/etc/default/grub**

- The _grub_ file defines the directives that control the behavior of GRUB2 at boot time.
- The most important part that it configures is the **GRUB_CMDLINE_LINUX** option. This line contains boot arguments for the kernel on your server.
- **Any changes in this file must be followed by the execution of the _grub2-mkconfig_ command in order to be reflected in _grub.cfg_.**
- Generally, you do not need to make any changes to this file, as the default settings are good enough for normal system operation.

![[Pasted image 20241128175918.png]]

| **Directive**         | **Description**                                                                                                                                                                                                                                                                                                  |
| --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| GRUB_TIMEOUT          | Defines the wait time, in seconds, before booting off the default kernel. Default value is 5. If this variable is set to 0, GRUB 2 will not display a list of bootable kernels, unless you press and hold an alphanumeric key during the BIOS initial screen.                                                    |
| GRUB_DISTRIBUTOR      | The value of the GRUB_DISTRIBUTOR variable returns “Red Hat Enterprise Linux” on a standard RHEL installation, and is displayed before each kernel-bootable entry. You can modify this entry to any string of your choice if you wish.                                                                           |
| GRUB_DEFAULT          | The next variable is GRUB_DEFAULT and is related to the default kernel that GRUB 2 loads at boot. The value “saved” instructs GRUB 2 to look at the saved_entry variable in the file /boot/grub2/grubenv. This variable is updated with the name of the latest kernel every time that a new kernel is installed. |
| GRUB_DISABLE_SUBMENU  | Enables/disables the appearance of GRUB2 submenu                                                                                                                                                                                                                                                                 |
| GRUB_TERMINAL_OUTPUT  | Sets the default terminal                                                                                                                                                                                                                                                                                        |
| GRUB_CMDLINE_LINUX    | Specifies the command line options to pass to the kernel at boot time                                                                                                                                                                                                                                            |
| GRUB_DISABLE_RECOVERY | Lists/hides system recovery entries in the GRUB2 menu                                                                                                                                                                                                                                                            |
| GRUB_ENABLE_BLSCFG    | Defines whether to use the new bootloader specification to manage bootloader configuration                                                                                                                                                                                                                       |
The variable GRUB_CMDLINE_LINUX is more interesting. It specifies the options to pass to the Linux kernel. For example, **rd.lvm.lv** tells the name of the logical volumes where the root filesystem and swap partition are located. The **crashkernel** option is used to reserve some memory for **kdump**, which is invoked to capture a kernel core dump if the system crashes. Finally, at the end of the line, the **rhgb quiet** directives enable the Red Hat graphical boot and hide the boot messages by default. If you want to enable verbose boot messages, remove the **quiet** option from this line.

**Example**
In this exercise, you will change the default system boot timeout value to 8 seconds persistently, and validate:

1. Edit the _/etc/default/grub_ file and change the setting as follows:

![](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781835887325/files/html/images/264_1.jpg)

2. Execute the _grub2-mkconfig_ command to reproduce _grub.cfg_:

![](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781835887325/files/html/images/264_2.jpg)

3. Restart the system with _sudo reboot_ and confirm the new timeout value when GRUB2 menu appears.