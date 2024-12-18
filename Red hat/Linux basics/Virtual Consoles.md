Terminal - is an environment that is opened on the console and provides access to a nongraphical shell, typically Bash. This is the command-line environment that can be used to type commands. A terminal can be offered through a window while using a graphical console, but it can also be opened as the only thing that you see in a textual console. You can also open a remote terminal, using SSH.

Console is basically what you see when you are looking at your computer screen. Think of it like this: You can have multiple terminals open on a console. This means that in a textual environment, the words _console_ and _terminal_ are more or less equivalent. In a graphical environment, they are not.

**Logging In to a Local Console**
- the Linux console and interactively log in from the login prompt that is presented
	- Linux server boots with a graphical environment (graphical target) or text-based console.
	- To log in from a text console, you need to know which user account you should use.
- remote connection using ssh

**System root user**
On many installations, the unrestricted system administrator user root is available. The user root has no limitations to access the system. On RHEL 9, you can indicate while installing if the root user should have a password or not. **If the root user doesn’t get a password, you’ll only be able to log in with an administrator user. This is a user that will only obtain root superpowers while using the sudo command.**

**If the root user, is enabled, you shouldn’t use it.** Two type of getting root account:
- If you do need root access anyway, you can use the **sudo -i** command from the local user environment to open a root shell. Note that you are allowed to do this only if you have **sudo** privileges, and you’ll have to type your current user password after using the command.
- If you know the root user password, use **su -** to open a root shell. This command will prompt for the root user password, and you’ll be able to work as root until you type **exit**.

**Switching Between Terminals
- When you’re working in a graphical environment, type **term**, which presents an icon to open a terminal. Because terminals are opened as a **subshell**, you do not have to log in to each terminal again, and will get access as the same user account that was originally used to log in to the graphical environment. When you’re working from a graphical environment, it is also possible to open different virtual consoles. (use Ctrl-Alt-F(1-6))
- In a nongraphical environment, you have only one terminal interface that is available. To offer an option that makes working from several consoles on the same server possible, Linux uses the concept of a **_virtual terminal_**. This feature allows you to open six different terminal windows from the same console at the same time and use key sequences to navigate between them (use the key sequences Alt-F1 through Alt-F6).
	- **F1:** Gives access to the GNOME Display Manager (GDM) graphical login
	- **F2:** Provides access to the current graphical console
	- **F3:** Gives access back to the current graphical session
	- **F4–F6:** Gives access to nongraphical consoles

Of these virtual consoles, the first one is used as the default console. It is commonly known as the _virtual console tty1_. and it has a corresponding device file that has the name /dev/tty1.

**Pseudo Terminal Devices**
For terminal windows that are started from a graphical environment, pseudo terminals are started. These pseudo terminals are referred to using numbers in the **/dev/pts** directory. So, the first terminal window that is started from a graphical environment appears as /dev/pts/1.

**clear** - command to clear the terminal screen


