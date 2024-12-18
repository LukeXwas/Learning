The **fdisk** utility has been around for a long time and can be used to create and manage MBR as well as GPT partitions.

**The MBR partitioning scheme supports a maximum of 15 partitions for data (3 primary and 12 logical), plus an extended partition, which is simply a “container” for logical partitions.

After a new drive is installed on Linux, that drive normally isn’t configured with partitions. The **fdisk** utility can be used to configure partitions on physical or virtual disks attached to the system.

Type **fdisk -l** to display partitions.

**Creating MBR Partitions with fdisk**

1. Open a root shell and type **lsblk**. This lists the block devices that are available.
2. Open a root shell and run the **fdisk** command. This command needs as its argument the name of the disk device where you want to create the partition. This exercise uses /dev/sdb. Change that, if needed, according to your hardware.

![[Pasted image 20241213231659.png]]

3. When you start **fdisk**, type **m** to list basic **fdisk** commands:

![[Pasted image 20241215163106.png]]. 

4. Before you do anything, it is a good idea to check how much disk space you have available. Press **p** to see an overview of current disk allocation:

![[Pasted image 20241213231742.png]]

In the output of this command, in particular look for the total number of sectors and the last sector that is currently used. If the last partition does not end on the last sector, you have available space to create a new partition. In this case, that shouldn’t be an issue because you are supposed to use a new disk in this exercise.

5. Type **n** to add a new partition:

![[Pasted image 20241213231908.png]]

6. Press **p** to create a primary partition. Accept the partition number that is now suggested, which should be /dev/sdb1.
7. Specify the first sector on disk that the new partition will start on. The first available sector is suggested by default, so press Enter to accept.
8. Type **+1G** to make this a 1-GiB partition. If you were to just press Enter, the last sector available on disk would be suggested. If you were to use that, after this exercise you would not have any disk space left to create additional partitions or logical volumes, so you should use another last sector. To use another last sector, you can do one of the following:
	1. Enter the number of the last sector you want to use.
	2. Enter **+number** to create a partition that sizes a specific number of sectors.
	3. Enter **+number(K,M,G)** to specify the size you want to assign to the partition in KiB, MiB, or GiB.

![[Pasted image 20241213232104.png]]
After you enter the partition’s ending boundary, **fdisk** will show a confirmation.

9. At this point, you can define the partition type. By default, a Linux partition type is used. If you want the partition to be of any other partition type, use **t** to change it. For this exercise there is no need to change the partition type. Common partition types include the following:

![[Pasted image 20241215163300.png]]

You can then list available partition types with the **L** command. Unless you’re making a change, type in identifier **83**. You’ll be returned to the **fdisk** command prompt.

Example:
![[Pasted image 20241215164847.png]]
10. If you want to make this partition bootable press **a

![[Pasted image 20241215165543.png]]

11. If you are happy with the modifications, press **w** to write them to disk and exit **fdisk**.

![Images](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781260462081/files/f0263-02.jpg)

The **fdisk** utility doesn’t actually write the changes to disk until you run the write (**w**) command. Alternatively, you can cancel these changes with the quit (**q**) command. If you don’t see any error messages, the changes are written to disk.

12. When partitions are added or changed, you generally don’t have to reboot to get Linux to read the new partition table, unless another partition on that drive has been formatted and mounted. If so, an attempt to write the partition table with the **w** command fails temporarily with the following message:

![[Pasted image 20241215163602.png]]

13. Run **partprobe /dev/sdb**, the kernel will read the new partition table and you’ll be able to use the newly created partition.
14. Type **lsblk** to verify that the new partition has been created successfully.

**Creating Logical Partitions

If you need more than four partitions on the new physical disk, configure the first three partitions as primary partitions, and then configure the fourth partition as an extended partition. That extended partition should typically be large enough to fill the rest of the disk; all logical partitions must fit in that space.

1. In a root shell, type **fdisk /dev/sdb** to open the **fdisk** interface.
2. Type **n** to create a new partition. To create a logical partition, when **fdisk** prompts which partition type you want to create, enter **e**. This allows you to create an extended partition, which is necessary to later add logical partitions.

![[Pasted image 20241213232635.png]]

3. If the extended partition is the fourth partition that you are writing to the MBR, it will also be the last partition that can be added to the MBR. For that reason, it should fill the rest of your computer’s hard disk. Press Enter to accept the default first sector and press Enter again when **fdisk** prompts for the last sector (even if this is not the fourth partition yet).

![[Pasted image 20241213232714.png]]

4. Now that the extended partition has been created, you can create a logical partition within it. Still from the **fdisk** interface, press **n** again. Because all of the space in the drive has been allocated to partitions, the utility will by default suggest adding a logical partition with partition number 5.

![[Pasted image 20241213232747.png]]

5. Press Enter to accept the default first sector. When asked for the last sector, enter **+1G**:

![[Pasted image 20241213232818.png]]

6. Now that the logical partition has been created, enter **w** to write the changes to disk and quit **fdisk**.

**Delete a Partition

**_Do not perform this action on any partition where you need the data_

Assuming only one partition exists on this drive, it is selected automatically after you run the **d** command.

![[Pasted image 20241215164235.png]]

This is the last chance to change your mind before deleting the current partition. To avoid writing the change, exit from **fdisk** with the **q** command. If you’re pleased with the changes that you’ve made and want to make them permanent, proceed with the **w** command:

![Images](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781260462081/files/f0262-03.jpg)

You should now have an empty hard drive.

**Create a Swap Partition

To set up that partition for swap space. Once you have a swap partition of the desired size, run the **t** command to select a partition, and then run the **l** command to show the partition ID types

In this case, at the following prompt, type in **82** for a Linux swap partition:

![Images](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781260462081/files/f0263-01.jpg)

**Sequence of commands to set up a new swap partition

![[Pasted image 20241215165753.png]]