Installing kernel packages requires extra care because it could leave your system in an unbootable or undesirable state.

It is advisable to have the bootable medium handy prior to starting the kernel install process. **By default, the _dnf_ command adds a new kernel to the system, leaving the existing kernel(s) intact. It does not replace or overwrite any existing kernel files.

**Always install a new version of the kernel instead of upgrading it. The upgrade process removes any existing kernel and replaces it with a new one. In case of a post-installation issue, you will not be able to revert to the old working kernel.

A new version of the kernel is typically required if an application needs to be deployed on the system that requires a different kernel to operate. When deficiencies or bugs are identified in the existing kernel, it can hamper the kernel’s smooth operation. In either case, the new kernel addresses existing issues as well as adds bug fixes, security updates, new features, and improved support for hardware devices.

**The _dnf_ command is the preferred tool to install a kernel, as it resolves and installs any required dependencies automatically.

**Download and Install a New Kernel**

1. Check the version of the running kernel - uname -r
2. List the kernel packages currently installed:

![[Pasted image 20241213202407.png]]

There are five kernel packages on the system as reported.

3. Install new kernel - **dnf install kernel**
4. Confirm the installation: **dnf list installed kernel*

![[Pasted image 20241213202934.png]]

The output indicates that packages for a higher kernel version 5.14.0-162.12.1.el9_1 have been installed. It also shows the presence of the previous kernel packages.

5. The _/boot/grub2/grubenv_ file now has the directive “saved_entry” set to the new kernel, which implies that this new kernel will boot on the next system restart:

![[Pasted image 20241213203045.png]]

6. Reboot the system. You will see the new kernel entry in the GRUB2 boot list at the top. The system will autoboot this new default kernel.

![[Pasted image 20241213203104.png]]

7. Run the _uname_ command after the system has been booted up to confirm the loading of the new kernel:

![](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781835887325/files/html/images/276_4.jpg)

8. The new kernel is active.