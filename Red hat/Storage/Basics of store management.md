Data is stored on disks that are logically divided into partitions. A partition can exist on a portion of a disk, on an entire disk, or it may span multiple disks. Each partition is accessed and managed independent of other partitions and may contain a file system or swap space. Partitioning information is stored at special disk locations that the system references at boot time.

**Disk Partitions**

The space on a storage device can be sliced into partitions.

 - You should be careful when adding a new partition to avoid damaging data by overlapping with an existing partition or wasting space by leaving unused gaps between neighboring partitions.

RHEL offers a command called _lsblk_ to list disk and partition information. The following graphic illustrates the current storage status on _server1_:

![[Pasted image 20241213221341.png]]

It reveals the presence of one 20GB disk, _sda_, with two partitions: _sda1_ and _sda2_. The first partition holds _/boot_, and the second one is an LVM object encapsulating _root_ (17GB) and _swap_ (2GB) logical volumes within it. Both _sda1_ and _sda2_ partitions occupy the entire disk capacity. The _sr0_ represents the ISO image mounted as an optical medium.

Every hardware device such as a disk, CD/DVD, printer, and terminal has an associated device driver loaded in the kernel. The kernel communicates with hardware devices through their respective device drivers. Each device driver is assigned a unique number called the _major_ number, which the kernel uses to recognize its type.

Furthermore, there may be more than one instance of the same device type in the system. In that case, the same driver is used to control all those instances. For example, SATA device driver controls all SATA hard disks and CD/DVD drives. The kernel in this situation allots a _minor_ number to each individual device within that device driver category to identify it as a unique device. This scheme applies to disk partitions as well.