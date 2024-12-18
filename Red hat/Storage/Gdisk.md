The GPT partitioning scheme can hold up to 128 partitions.

Although you could use **fdisk** and select the **g** command to switch to a GPT partition table format, the **gdisk** utility was specifically designed for GPT partitions.

Do not ever use **gdisk** on a disk that has been formatted with **fdisk** and already contains **fdisk** partitions. **gdisk** will detect that an MBR is present, and it will convert this to a GPT (see the following code listing). Your computer most likely will not be able to boot after doing this! When you see the following message, use **q** to quit **gdisk** immediately, without saving anything!

![[Pasted image 20241215165317.png]]

**Creating GPT Partitions with gdisk

1. To create a partition with **gdisk**, open a root shell and type **gdisk /dev/sdc**. (Replace /dev/sdc with the exact device name used on your computer.) **gdisk** will try to detect the current layout of the disk, and if it detects nothing, it will create the GPT and associated disk layout.

![[Pasted image 20241214212323.png]]

2. Type the question mark (**?**) to get a list of commands:

![[Pasted image 20241215170034.png]]

3. Type **n** to enter a new partition. You can choose any partition number between 1 and 128, but it is wise to accept the default partition number that is suggested.

![[Pasted image 20241214212352.png]]

4. You now are asked to enter the first sector. By default, the first sector that is available on disk will be used, but you can specify an offset as well. This does not make sense, so just press Enter to accept the default first sector that is proposed.

![[Pasted image 20241214212425.png]]

5. When asked for the last sector, by default the last sector that is available on disk is proposed (which would create a partition that fills the entire hard disk). You can specify a different last sector, or specify the disk size using **+**, the size, and KMGTP. So to create a 1-GiB disk partition, use **+1G**.

![[Pasted image 20241214212454.png]]

6. You now are asked to set the partition type. If you do not do anything, the partition type is set to 8300, which is the Linux file system partition type. Other options are available as well. You can press **l** to show a list of available partition types.
- The relevant partition types are as follows:
		1. **8200:** Linux swap
		2. **8300:** Linux file system
		3. **8e00:** Linux LVM

- Notice that these are the same partition types as the ones that are used in MBR, with two 0s added to the IDs. You can also just press Enter to accept the default partition type 8300.

7. The partition is now created (but not yet written to disk). Press **p** to show an overview, which allows you to verify that this is really what you want to use.

![[Pasted image 20241214212632.png]]

8. If you are satisfied with the current partitioning, press **w** to write changes to disk and commit. This gives a warning which you can safely ignore by typing **Y**, after which the new partition table is written to the GUID partition table.

![[Pasted image 20241214212654.png]]

9. If at this point you get an error message indicating that the partition table is in use, type **partprobe** to update the kernel partition table.