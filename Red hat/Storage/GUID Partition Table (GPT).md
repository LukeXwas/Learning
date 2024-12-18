With the increasing use of disks larger than 2TB on x86 computers, a new 64-bit partitioning standard called _Globally Unique Identifiers_ (GUID) _Partition_ _Table_ (GPT) was developed and integrated into the UEFI firmware.

This new standard introduced plenty of enhancements, including the ability to construct up to 128 partitions (no concept of extended or logical partitions), utilize disks larger than 2TB, use 4KB sector size, and store a copy of the partition information before the end of the disk for redundancy.

Moreover, this standard allows a BIOS-based system to boot from a GPT disk using the bootloader program stored in a protective MBR at the first disk sector. In addition, the UEFI firmware also supports the secure boot feature, which only allows signed binaries to boot.