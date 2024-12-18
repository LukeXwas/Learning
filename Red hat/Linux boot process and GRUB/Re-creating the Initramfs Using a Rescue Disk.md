Occasionally, the initramfs image may get damaged as well. If this happens, you cannot boot your server into normal operational mode. To repair the initramfs image after booting into the rescue environment, you can use the **dracut** command. If used with no arguments, this command creates a new initramfs for the kernel currently loaded.

Alternatively, you can use the **dracut** command with several options to make an initramfs for specific kernel environments. The **dracut** configuration is dispersed over different locations:
- /usr/lib/dracut/dracut.conf.d/*.conf contains the system default configuration files.
- /etc/dracut.conf.d contains custom dracut configuration files.
- /etc/dracut.conf is now deprecated and should not be used anymore. Put your configuration in files in /etc/dracut.conf.d/ instead.

**Fixing the Initramfs**

In rare cases, the initramfs might get damaged. If you analyze the boot procedure carefully, you will learn that you have a problem with the initramfs because you’ll never see the root file system getting mounted on the root directory, nor will you see any Systemd units getting started. If you suspect that you are having a problem with the initramfs, it is easy to re-create it.

- To re-create it using all default settings (which is fine in most cases), you can just run the **dracut --force** command. (Without **--force**, the command will refuse to overwrite your existing initramfs.)

