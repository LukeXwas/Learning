The MBR resides on the first sector of the boot disk. MBR was the preferred choice for saving partition table information on x86-based computers. However, with the arrival of bigger and larger hard drives, a new firmware specification (UEFI) was introduced. MBR is still widely used, but its use is diminishing in favor of UEFI.

MBR allows the creation of three types of partition on single disk: 
- _primary_
- _extended
- _logical_

Of these, only primary and logical can be used for data storage; the extended is a mere enclosure for holding the logical partitions and it is not meant for data storage.

- MBR supports the creation of up to four primary partitions numbered 1 through 4 at a time. 
- In case additional partitions are required, one of the primary partitions must be deleted and replaced with an extended partition to be able to add logical partitions (up to 11) within that extended partition.
- Numbering for logical partitions begins at 5. 
- **MBR supports a maximum of 14 usable partitions (3 primary and 11 logical) on a single disk.

MBR cannot address storage space beyond 2TB. This is due to its 32-bit nature and its 512-byte disk sector size. The MBR is non-redundant; the record it contains is not replicated, resulting in an unbootable system in the event of corruption. If your disk is smaller than 2TB and you don’t intend to build more than 14 usable partitions, you can use MBR without issues.

**Logical Partitions

If three MBR partitions have been created already, there is room for one more primary partition, after which the partition table is completely filled up. If you want to go beyond four partitions on an MBR disk, you have to create an extended partition. Following that, you can create logical partitions within the extended partition.

If something goes wrong with the extended partition, you have a problem with all logical partitions existing within it as well. If you need more than four separate storage allocation units, you might be better off using LVM instead of logical partitions.

**An extended partition is used only for the purpose of creating logical partitions. You cannot create file systems directly on an extended partition!**