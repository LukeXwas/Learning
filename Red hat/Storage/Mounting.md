A **mount** is a connection between a device and a directory. In the process of mounting, a device is connected to a specific directory, such that after a successful mount this directory gives access to the device contents. 

**mount** - command gives an overview of all mounted devices.

**df -Th** - command was designed to show available disk space on mounted devices.

![[Pasted image 20241215162846.png]]

**findmnt** - command shows mounts and the relationship that exists between the different mounts.

![[Pasted image 20241215162912.png]]

**Filesystem:** The name of the device file that interacts with the disk device that is used. The real devices in the output start with /dev. 

![[Pasted image 20241215162927.png]]

**tmpfs** - These are kernel devices that are used to create a temporary file system in RAM.