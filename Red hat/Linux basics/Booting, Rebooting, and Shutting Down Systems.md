Rebooting a server make sure that all processes and tasks that were running on your server have reread their configurations and initialized properly.

When you should reboot server:
- To recover from serious problems such as server hangs and kernel panics
- To apply kernel updates
- To apply changes to kernel modules that are being used currently and therefore cannot be reloaded easily

**Shutting down types:**
- When a server is rebooted, all processes that are running need to shut down properly. To issue a proper reboot, you have to alert the **Systemd process**. The Systemd process is the first process that was started when the server was started. 
- By pulling the power plug, much data will typically be lost. (The reason is that processes that have written data do not typically write that data directly to disk, but instead store it in memory buffers (a cache) from where it is committed to disk when it is convenient for the operating system)

Command:
- **systemctl reboot** or **reboot**
- **systemctl halt** or **halt**
- **systemctl poweroff** or **poweroff** 

To force a machine to reset, from a root shell you can type **echo b > /proc/sysrq-trigger**. This command immediately resets the machine without saving anything. Notice that this command should be used only if there are no other options!



