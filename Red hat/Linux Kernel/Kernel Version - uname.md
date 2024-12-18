Sometimes you need to ascertain the version of the kernel running on the system to check for compatibility with an application or database that you need to deploy. RHEL has a basic tool available to extract the version.

A useful source of information is the **uname** command. This command gives different kinds of information about your operating system.

**uname** - command identifies elementary information about the system.

**uname -m** - reveals the architecture of the system

**uname -a** command for an overview of all relevant parameters:

| Linux                                               | Kernel name                       |
| --------------------------------------------------- | --------------------------------- |
| [server1.example.com](http://server1.example.com)   | Hostname of the system            |
| 5.14.0-162.6.1.el9_1.x86_64                         | Kernel release                    |
| #1 SMP PREEMPT_DYNAMIC Fri Sep 30 07:36:03 EDT 2022 | Date and time of the kernel built |
| x86_64                                              | Machine hardware name             |
| x86_64                                              | Processor type                    |
| x86_64                                              | Hardware platform                 |
| GNU/Linux                                           | Operating system name             |

**uname -r** - print the kernel version which currently is used

![[Pasted image 20241213200449.png]]
From left to right:

- 5 - major version of the Linux kernel. It changes when significant alterations, enhancements, and updates to the previous major version are made.
- 14 - minor revision of the 5th major version
- 0 - represents patched version of 5.14 with minor bug and security hole fixes, minor enhancements, and so on.
- 162.6.1 - Red Hat customized version of 5.14.0
- el9_1 - Enterprise Linux this kernel is built for
- x86_6 -) architecture this kernel is built for

A further analysis designates that 5.14.0 holds the general Linux kernel version information, the numbers and letters (162.6.1.el9_1) represent the Red Hat specific information, and x86_64 identifies the hardware architecture type.