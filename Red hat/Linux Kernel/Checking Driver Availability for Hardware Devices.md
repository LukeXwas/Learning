On modern Linux servers, many hardware devices are supported. On occasion, you might find that some devices are not supported properly because their modules are not currently loaded.

The best way to find out whether this is the case for your hardware is by using the **lspci** command. 
- If used without arguments, it shows all hardware devices that have been detected on the PCI bus.
- A very useful argument is **-k**, which lists all kernel modules that are used for the PCI devices that were detected.

![[Pasted image 20241213210835.png]]

If you discover that PCI devices were found for which no kernel modules could be loaded, you are probably dealing with a device that is not supported. You can try to find a closed source kernel module, but you should realize that doing so might endanger the stability of your kernel. A much better approach is to check with your hardware vendor that Linux is fully supported before you purchase specific hardware.

**Managing Kernel Module Parameters

Occasionally, you might want to load kernel modules with specific parameters. To do so, you first need to find out which parameter you want to use. If you have found the parameter you want to use, you can load it manually, specifying the name of the parameter followed by the value that you want to assign. To make this an automated procedure, you can create a file in the /etc/modprobe.d directory, where the module is loaded, including the parameter you want to be loaded.

Loading Kernel Modules with Parameters:

1. Type **lsmod | grep cdrom**. If you have used the optical drive in your computer, this module should be loaded, and it should indicate that it is used by the sr_mod module.
2. Type **modprobe -r cdrom**. This will not work because the module is in use by the sr_mod module.
3. Type **modprobe -r sr_mod; modprobe -r cdrom**. This should unload both modules, but it will most likely fail. (It won’t fail if currently no optical device is mounted.)
4. Type **umount /dev/sr0** to unmount the mounted cdrom file system and use **modprobe -r sr_mod**. This should now work.
5. Type **modinfo cdrom**. This shows information about the cdrom module, including the parameters that it supports. One of these is the **debug** parameter, which supports a Boolean as its value.
6. Type **modprobe cdrom debug=1**. This loads the cdrom module with the **debug** parameter set to on.
7. Type **dmesg**. For some kernel modules, load information is written to the kernel ring buffer, which can be displayed using the **dmesg** command. Unfortunately, this is not the case for the cdrom kernel module.
8. Create a file with the name /etc/modprobe.d/cdrom.conf and give it the following contents:

![[Pasted image 20241213211130.png]]

9. This enables the parameter every time the cdrom kernel module loads.
