On some occasions, you might need to know specific information about the RHEL version you are using. To get that information, run the **cat /etc/redhat-release** command and review its output; it will tell you which Red Hat version you are using and which update level is applied.

**_lscpu_** - show the CPU information. The output indicates the architecture of the CPU (x86_64), supported modes of operation (32-bit and 64-bit), number of CPUs (2), vendor ID (GenuineIntel), model name (Intel …), threads per core (1), cores per socket (2), number of sockets (1), the amount and levels of cache memory (L1d, L1i, L2, and L3), and other information.

**_lsblk_ ** -  list disk and partition information

**uptime** - command display the system’s current time, length of time it has been up for, number of users currently logged in, and the average CPU (processing) load over the past 1, 5, and 15 minutes.

As a rule of thumb, the load average should not be higher than the number of CPU cores in your system. You can find out the number of CPU cores in your system by using the **lscpu** command. **If the load average over a longer period is higher than the number of CPUs in your system, you may have a performance problem.**

To learn more, disable the **quiet** directive for the desired kernel in the GRUB configuration file. Boot your system. Watch as the messages pass quickly through the screen. After logging in, you can review these messages by running the **dmesg** command.