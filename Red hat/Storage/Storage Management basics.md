Data is stored on disks that are logically divided into partitions. A partition can exist on a portion of a disk, on an entire disk, or it may span multiple disks. Each partition is accessed and managed independent of other partitions and may contain a file system or swap space. 

- A disk in RHEL can be carved up into several partitions.
- This partition information is stored on the disk in a small region, which is read by the operating system at boot time.
- **This region is referred to as the _Master Boot Record_ (MBR) on the BIOS-based systems, and _GUID Partition Table_ (GPT) on the UEFI-based systems.
- Though MBR and GPT are designed for different PC firmware types, their job is essentially the same: to store disk partition information and the boot code.

At system boot, the BIOS/UEFI scans all storage devices, detects the presence of MBR/GPT areas, identifies the boot disks, loads the bootloader program in memory from the default boot disk, executes the boot code to read the partition table and identify the _/boot_ partition, loads the kernel in memory, and passes control over to it.

Data is stored on disks that are logically divided into partitions. A partition can exist on a portion of a disk, on an entire disk, or it may span multiple disks. Each partition is accessed and managed independent of other partitions and may contain a file system or swap space. Partitioning information is stored at special disk locations that the system references at boot time.

**Disk Partitions**

Data is stored on disks that are logically divided into partitions. A partition can exist on a portion of a disk, on an entire disk, or it may span multiple disks. Each partition is accessed and managed independent of other partitions and may contain a file system or swap space. Partitioning information is stored at special disk locations that the system references at boot time.

The space on a storage device can be sliced into partitions.

 - You should be careful when adding a new partition to avoid damaging data by overlapping with an existing partition or wasting space by leaving unused gaps between neighboring partitions.

RHEL offers a command called _lsblk_ to list disk and partition information. The following graphic illustrates the current storage status on _server1_:

![[Pasted image 20241213221341.png]]

It reveals the presence of one 20GB disk, _sda_, with two partitions: _sda1_ and _sda2_. The first partition holds _/boot_, and the second one is an LVM object encapsulating _root_ (17GB) and _swap_ (2GB) logical volumes within it. Both _sda1_ and _sda2_ partitions occupy the entire disk capacity. The _sr0_ represents the ISO image mounted as an optical medium.


**Disk Device Types

Use the **lsblk** command to print a list of all disk devices available on your system

![[Pasted image 20241213224329.png]]