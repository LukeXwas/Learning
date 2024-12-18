**Modules**

Kernel is a collection of software components called _modules_ that work in tandem to provide a stable and controlled platform. Modules are _device drivers_ that control hardware devices—the processor, memory, storage, controller cards, and peripheral equipment, and interact with software subsystems, such as storage management, file systems, networking, and virtualization.

A modular kernel consists of a relatively small core kernel and provides driver support through modules that are loaded when required. Modular kernels are very efficient, as they include only those modules that really are needed.

Some of these modules are static to the kernel and are integral to system functionality, while others are loaded dynamically as needed, making the kernel speedier and more efficient in terms of overall performance and less vulnerable to crashes.

**How to control modules?

To control the behavior of the modules, and the kernel in general, a variety of tunable parameters are set that define a baseline for kernel functionality. Some of these parameters must be tuned to allow certain applications and database software to be installed smoothly and operate properly.

RHEL allows you to generate and store several custom kernels with varied configuration and required modules, but only one of them can be active at a time. A different kernel may be loaded by interacting with GRUB2.

**Understanding Hardware Initialization

The loading of drivers is an automated process that roughly goes like this:

1. During boot, the kernel probes available hardware.
2. Upon detection of a hardware component, the **systemd-udevd** process takes care of loading the appropriate driver and making the hardware device available.
3. To decide how the devices are initialized, **systemd-udevd** reads rules files in /usr/lib/udev/rules.d. These are system-provided rules files that should not be modified.
4. After processing the system-provided udev rules files, **systemd-udevd** goes to the /etc/udev/rules.d directory to read any custom rules if these are available.
5. As a result, required kernel modules are loaded automatically, and status about the kernel modules and associated hardware is written to the sysfs file system, which is mounted on the /sys directory. The Linux kernel uses this pseudo file system to track hardware-related settings.

The **systemd-udevd** process is not a one-time-only process; it continuously monitors plugging and unplugging of new hardware devices. To get an impression of how this works, as root you can type the command **udevadm monitor**. This lists all events that are processed while activating new hardware devices.

if you plug in a USB device while this command is active, you can see exactly what’s happening. Press Ctrl-C to close the **udevadm monitor** output.

**Managing Kernel Modules

Linux kernel modules normally are loaded automatically for the devices that need them, but you will on rare occasions have to load the appropriate kernel modules manually. A few commands are used for manual management of kernel modules.

![[Pasted image 20241213205404.png]]

The first command to use when working with kernel modules is **lsmod**. This command lists all kernel modules that currently are used, including the modules by which this specific module is used.

![[Pasted image 20241213205512.png]]

If you want to have more information about a specific kernel module, you can use the **modinfo** command. This gives complete information about specific kernel modules, including two interesting sections: the alias and the parms.

- A module alias is another name that can also be used to address the module.
- The parms lines refer to parameters that can be set while loading the module.

example: **modinfo e1000**

To manually load and unload modules, you can use the **modprobe** and **modprobe -r** commands.

Managing Kernel Modules from the Command Line:

1. Open a root shell and type **lsmod | less**. This shows all kernel modules currently loaded.
2. Type **modprobe vfat** to load the vfat kernel module.
3. Verify that the module is loaded by using the **lsmod | grep vfat** command. You can see that the module is loaded, as well as some of its dependencies.
4. Type **modinfo vfat** to get information about the vfat kernel module. Notice that it does not have any parameters.
5. Type **modprobe -r vfat** to unload the vfat kernel module again.
6. Type **modprobe -r xfs** to try to unload the xfs kernel module. Notice that you get an error message because the kernel module currently is in use.






