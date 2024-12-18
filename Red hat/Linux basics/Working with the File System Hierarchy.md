The layout of the Linux file system is defined in the **File system Hierarchy Standard (FHS)**, and this file system hierarchy is described in **man 7 file-hierarchy**.

- “Everything in Linux is a file.” 
- Partitions are associated with _filesystem device nodes_ such as **/dev/sda1.** 
- Hardware components are associated with node files such as **/dev/cdrom**. 
- Detected devices are documented as files in the /sys directory.

Every filesystem starts with the top-level root directory, also known by its symbol, the single forward slash (/). Unless they are mounted separately, you can also find their files on the same partition as the root directory.
![[Pasted image 20241021184208.png]]
![[Pasted image 20241021182820.png]]
![[Pasted image 20241105143239.png]]
Files in the /proc and /sys directories are filled only during the boot process and disappear when a system is shut down, and as such they are stored in a special in-memory virtual filesystem.

**The UNIX System Resources Directory (/usr)**

- **/usr/bin:** The _binary_ directory contains crucial user executable commands.
- **/usr/sbin:** Most commands are required at system boot, and those that require the _root_ user privileges in order to run are located in this _system binary_ directory. In other words, this directory contains crucial system administration commands that are not intended for execution by normal users (although they can still run a few of them). This directory is not included in the default search path for normal users because of the nature of data it holds.
- **/usr/lib** and **/usr/lib64:** The _library_ directories contain shared library routines required by many commands and programs located in the _/usr/bin_ and _/usr/sbin_ directories, as well as by the kernel and other applications and programs for their successful installation and operation. The _/usr/lib_ directory also stores system initialization and service management programs. The subdirectory _/usr/lib64_ contains 64-bit shared library routines.
- **/usr/include:** This directory contains header files for _C_ language.
- **/usr/local:** This directory serves as a system administrator repository for storing commands and tools downloaded from the web, developed in-house, or obtained elsewhere. These commands and tools are not generally included with the original Linux distribution. In particular, _/usr/local/bin_ holds executables, _/usr/local/etc_ holds configuration files, and _/usr/local/lib_ and _/usr/local/lib64_ holds library routines.
- **/usr/share:** This is the directory location for manual pages, documentation, sample templates, configuration files, etc., that may be shared with other Linux platforms.
- **/usr/src:** This directory is used to store source code.

**The Variable Directory (/var)** - contains data that frequently changes while the system is operational.

- **/var/log:** This is the storage for most system log files, such as system logs, boot logs, user logs, failed user logs, installation logs, cron logs, mail logs, etc.
- **/var/opt:** This directory stores log, status, and other variable data files for additional software installed in _/opt_.
- **/var/spool:** Directories that hold print jobs, cron jobs, mail messages, and other queued items before being sent out to their intended destinations are located here.
- **/var/tmp:** Large temporary files or temporary files that need to exist for longer periods of time than what is typically allowed in another temporary directory, _/tmp_, are stored here. These files survive system reboots and are automatically deleted if they are not accessed or modified for a period of 30 days.

**/tmp** - This directory is a repository for temporary files. Many programs create temporary files here during runtime or installation. These files survive system reboots and are automatically removed if they are not accessed or modified for a period of 10 days.

**Devices File System (/dev), virtual** - file system is accessible via the _/dev_ directory, and it is used to store device nodes for physical hardware and virtual devices. The Linux kernel communicates with these devices through corresponding device nodes located here.
- Character (raw) devices are accessed serially with streams of bits transferred during kernel and device communication. Examples of such devices are console, serial printers, mice, keyboards, terminals, etc.
- Block devices are accessed in a parallel fashion with data exchanged in blocks (parallel) during kernel and device communication. Data on block devices is accessed randomly. Examples of block devices are hard disk drives, optical drives, parallel printers, etc.

**The Procfs File System (/proc), Virtual** - file system is accessible via the _/proc_ directory, and it is used to maintain information about the current state of the running kernel. This includes the details for current hardware configuration and status information on CPU, memory, disks, partitioning, file systems, networking, running processes, and so on. This information is stored in a hierarchy of subdirectories that contain thousands of zero-length pseudo files. These files point to relevant data maintained by the kernel in the memory. This virtual directory structure simply provides an easy interface to interact with kernel-maintained information. The Procfs file system is dynamically managed by the system. The contents in _/proc_ are created in memory at system boot time, updated during runtime, and destroyed at system shutdown.


it is common to organize Linux file systems in different devices. Some directories are commonly mounted on dedicated devices:
- **/boot:** This directory is often mounted on a separate device because it requires essential information your computer needs to boot.
- **/var:** This directory is often on a dedicated device because it grows in a dynamic and uncontrolled way
- **/home:** This directory often is on a dedicated device for security reasons. By putting it on a dedicated device, you can mount it with specific options, such as **noexec** and **nodev**, to enhance the security of the server. When you are reinstalling the operating system, it is an advantage to have home directories in a separate file system. The home directories can then survive the system reinstall.
