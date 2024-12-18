An error in grub.cfg can result in an unbootable system. For example, if GRUB 2 identifies the wrong volume as the root partition (/), Linux will hang during the boot process. Other configuration errors in /boot/grub2/grub.cfg can lead to a kernel panic during the boot process.

![[Pasted image 20241128213931.png]]

- The grub> command prompt appears when you press Ctrl+c while in the edit window or a _c_ from the main menu. The command mode provides you with the opportunity to execute debugging, recovery, and many other tasks. You can view available commands by pressing the TAB key.
- Command completion is also available. For example, if you don’t remember the name of the kernel file, type **linux /** and then press the TAB key to review the available files in the /boot directory.

**Example - boot RHEL 9 manually**

1. Boot the system. When you see the following line at the top of the screen, press any key to access the GRUB 2 menu:

`The selected entry will be started automatically in 5s.`

2. Press c for a GRUB-based command-line interface. You should see the grub> prompt.
3. Load the LVM module:

`grub> insmod lvm`

4. 4.   List all partitions and logical volumes:

`grub> ls`

5. Identify the root partition. This may be named something like “lvm/rhel-root.” You may need to use some trial and error to find out (for example, by trying to display the /etc/fstab file from all the device names previously listed by GRUB 2).

`grub> cat (lvm/rhel-root)/etc/fstab`

6.   Set the root variable to the device that you have identified as that containing the root filesystem:

`grub> set root=(lvm/rhel-root)`

7.   Enter the **linux** command, which specifies the kernel and root directory partition. Yes, this is a long line; however, you can use command completion (press the TAB key) to make it faster. In addition, the only important parts of the line are the kernel file and the location of the top-level root directory.

![Images](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781260462081/files/f0187-04.jpg)

8.   Enter the **initrd** command, which specifies the initial RAM disk command and file location. Again, you can use the TAB key for filename completion.

![Images](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781260462081/files/f0187-05.jpg)

![Images](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781260462081/files/f0187-05.jpg)

9.   Now enter the **boot** command. If this command is successful, Linux should now boot the selected kernel and initial RAM disk just as if you selected that option from the GRUB 2 configuration menu.
