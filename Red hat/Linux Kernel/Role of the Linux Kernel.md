The Linux kernel is the heart of the operating system. It is the layer between the user who works with Linux from a shell environment and the hardware that is available in the computer on which the user is working.

**Kernel functions:

- It manages hardware, enforces security, regulates access to the system, as well as handles processes, services, and application workloads.
- The kernel manages the I/O instructions it receives from the software and translates them into the processing instructions that are executed by the central processing unit and other hardware in the computer.
- The kernel also takes care of handling essential operating system tasks. One example of such a task is the scheduler that makes sure any processes that are started on the operating system are handled by the CPU.

**Default kernel

**RHEL 9 is shipped with kernel version 5.14.0 for the 64-bit Intel/AMD processor architecture computers with single, multi-core, and multi-processor configurations.

The default kernel installed during the installation is usually adequate for most system needs; however, it requires a rebuild when a new functionality is added or removed. The new functionality may be introduced by installing a new kernel, upgrading an existing one, installing a new hardware device, or changing a critical system component.