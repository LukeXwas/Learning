**Disk Partitions**

Data is stored on disks that are logically divided into partitions. A partition can exist on a portion of a disk, on an entire disk, or it may span multiple disks. Each partition is accessed and managed independent of other partitions and may contain a file system or swap space. Partitioning information is stored at special disk locations that the system references at boot time.

The space on a storage device can be sliced into partitions.

 - You should be careful when adding a new partition to avoid damaging data by overlapping with an existing partition or wasting space by leaving unused gaps between neighboring partitions.

RHEL offers a command called _lsblk_ to list disk and partition information. The following graphic illustrates the current storage status on _server1_:

![[Pasted image 20241213221341.png]]

It reveals the presence of one 20GB disk, _sda_, with two partitions: _sda1_ and _sda2_. The first partition holds _/boot_, and the second one is an LVM object encapsulating _root_ (17GB) and _swap_ (2GB) logical volumes within it. Both _sda1_ and _sda2_ partitions occupy the entire disk capacity. The _sr0_ represents the ISO image mounted as an optical medium.

Almost all disk device names end with the letter _a_. The reason is that it is the first disk that was found in your server. The second SCSI disk, for instance, would have the name /dev/sdb. If many disks are installed in a server, you can have up to /dev/sdz and even beyond. After /dev/sdz, the kernel continues creating devices with names like /dev/sdaa and /dev/sdab. Notice that on NVMe devices, numbers are used instead of letters. So the first NVMe disk is nvme0n1, the second NVMe disk is nvme0n2, and so on.

Types of utilities

Two different types of partitions can be used on RHEL. To match the different partition types, there are also two different partitioning utilities:

- The **fdisk** utility has been around for a long time and can be used to create and manage MBR as well as GPT partitions.
- The **gdisk** utility is used to create GPT partitions.
- Apart from **fdisk** and **gdisk**, there are other partitioning utilities as well, of which **parted** is relatively easy to use, but at the same time it hides some of the more advanced features.

**Notice that you can only decide which type of partition table to create when initializing an unused disk. Once either MBR or GPT partitions have been created on a disk, you cannot change its type.