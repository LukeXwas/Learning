Kernel and its support files are stored at different locations in the directory hierarchy, of which three locations:
- **_/boot_,
- **_/proc_,
- **_/usr/lib/modules_

**The /boot Location**

_/boot_ is essentially a file system that is created at system installation. It houses the Linux kernel, GRUB2 configuration, and other kernel and boot support files. A long listing produces the following output for this file system:

![[Pasted image 20241213201335.png]]
The output displays several files, five of which are for the kernel and two for its rescue version. **The _vmlinuz_ is the main kernel file with _config_**, _initramfs_, _symvers_, and _System.map_ storing the kernel’s configuration, boot image, CRC values of all the variables used in the kernel and modules, and mapping, respectively.

The files for the rescue version have the string “rescue” embedded within their names.

The _efi_ and _grub2_ subdirectories under _/boot_ hold bootloader information specific to firmware type used on the system: UEFI or BIOS.

![[Pasted image 20241213201611.png]]

The files _grub.cfg_ and _grubenv_ contain critical data with the former holding bootable kernel information and the latter stores the environment information that the kernel uses.

The subdirectory _loader_ under _/boot_ is the storage location for configuration of the running and rescue kernels. The configuration is stored in files under the _entries_ subdirectory, as shown below:

![[Pasted image 20241213201711.png]]
The files are named using the machine id of the system as stored in the _/etc/machine-id_ file and the kernel version they are for. The content of the kernel file is presented below:

![[Pasted image 20241213201738.png]]

The “title” is displayed on the bootloader screen where the countdown to autoboot a selected kernel entry runs. Other than the kernel version, and the default kernel and boot image filenames, the environment variables “kernelopts” and “tuned_params” supply various values to the booting kernel to control its behavior.

**The /proc Location**

_/proc_ is a virtual, memory-based file system. Its contents are created and updated in memory at system boot and during runtime, and they are destroyed at system shutdown.

- It maintains information about the current state of the kernel, which includes hardware configuration and status information about processor, memory, storage, file systems, swap, processes, network interfaces and connections, routing, etc
- This data is kept in tens of thousands of zero-byte files organized in a hierarchy of hundreds of subdirectories. A long directory listing of _/proc_ is provided below:

![[Pasted image 20241213201909.png]]
Some subdirectory names are numerical and contain information about a specific process, and the process ID matches the subdirectory name. Within each subdirectory are other files and subdirectories containing a plethora of information, such as memory segments for processes and configuration data for system components.

The following show selections from the _cpuinfo_ and _meminfo_ files that hold processor and memory information:
![[Pasted image 20241213201957.png]]

The data stored under _/proc_ is referenced by many system utilities, including _top_, _ps_, _uname_, _free_, _uptime_, and _w_ to produce their output.

**The /usr/lib/modules Location**

This directory holds information about kernel modules. Underneath it are subdirectories specific to the kernels installed on the system. For example, the long listing of _/usr/lib/modules_ below shows that there is only one kernel installed. The name of the subdirectory corresponds with the installed kernel version.

![[Pasted image 20241213202033.png]]

And this subdirectory contains:

![[Pasted image 20241213202112.png]]

There are several files and a few subdirectories here; they hold module-specific information for the kernel version.

One of the key subdirectories is _/usr/lib/modules/5.14.0-162.6.1.el9_1.x86_64/kernel/drivers_, which stores modules for a variety of hardware and software components in various subdirectories, as shown in the listing below:

![[Pasted image 20241213202136.png]]
Additional modules may be installed on the system to support more components.