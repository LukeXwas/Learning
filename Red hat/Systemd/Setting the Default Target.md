The _systemctl_ command is also used to manage the target units. It can be used to view or change the default boot target, switch from one running target into another, and so on.

Four targets can be used while booting:
- **emergency.target:** In this target only a minimal number of units are started, just enough to fix your system if something is seriously wrong. You’ll find that it is quite minimal, as some important units are not started.
- **rescue.target:** This target starts all units that are required to get a fully operational Linux system. It doesn’t start nonessential services though.
- **multi-user.target:** This target is often used as the default target a system starts in. It starts everything that is needed for full system functionality and is commonly used on servers.
- **graphical.target:** This target also is commonly used. It starts all units that are needed for full functionality, as well as a graphical interface.
- **default.target**: A special soft link that points to the default system boot target (multi-user.target or graphical.target)
- **halt.target** - Shuts down and halts the system
- **poweroff.targey** - Shuts down and powers off the system
- **shutdown.target** - Shuts down the system
- **reboot.target** - Shuts down and reboots the system
- **hibernate.target** - Puts the system into hibernation by saving the running state of the system on the hard disk and powering it off. When powered up, the system restores from its saved state rather than booting up.

**The default target is specified as a symbolic link from the /etc/systemd/system/default.target file to either multi-user.target or graphical.target.** Don’t change files in the /usr/lib/systemd/system directory. Any software updates may overwrite those files.

To check the current default boot target - **systemctl get-default**

![[Pasted image 20241212005437.png]]

The system knows that graphical.target is the default thanks to a symbolic link from the /etc/systemd/system/default.target file to the graphical.target file in /usr/lib/system/system

**Other services started by graphical.target may be listed in the graphical.target.wants subdirectory in /etc/systemd/system or /usr/lib/systemd/system. In a default RHEL 9 installation, we see the following file:**

![[Pasted image 20241212112011.png]]

command to set the desired default target - **systemctl set-default multi-user.target**

![[Pasted image 20241212010114.png]]

Reboot system after that

**Switch Between Targets

Some of those targets have a special role because they can be isolated. These are also the targets that you can set as the targets to get into after system start. By isolating a target, you start that target with all of its dependencies. Only targets that have the **isolate** option enabled can be isolated. We’ll explore the **systemctl isolate** command.

Of the targets on your system, a few have an important role because they can be started (isolated) to determine the state your server starts in. These are also the targets that can be set as the default targets.

After logging in as the administrative user, you can move to a different target with the **systemctl isolate** command. For example, the following command moves the system to the multi-user target:

Aby zmienic na chwile system na inny target uzyj komendy

![[Pasted image 20241212010205.png]]

After that command is complete, rerun the **systemctl get-default** command. The output confirms that the default target has not changed:

![Images](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781260462081/files/f0193-03.jpg)

After reboot you back to default target.

