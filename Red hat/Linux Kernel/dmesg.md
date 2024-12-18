The first utility to consider if you require detailed information about the kernel activity is **dmesg**. This utility shows the contents of the kernel ring buffer, an area of memory where the Linux kernel keeps its recent log messages.

Analyzing Kernel Activity Using **dmesg**

![[Pasted image 20241213204034.png]]

In the **dmesg** output, all kernel-related messages are shown:

- Each message starts with a time indicator that shows at which specific second the event was logged. This time indicator is relative to the start of the kernel, which allows you to see exactly how many seconds have passed between the start of the kernel and a particular event.