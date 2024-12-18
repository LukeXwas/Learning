On an average Linux system, hundreds of commands are available—way too many to ever be able to remember all of them, which is why using the help resources on your computer is so very important.

**Using --help**
The quickest way to get an overview of how to use a command is by running the command with the **--help** option. You’ll see all options that can be used with the command.

**Using man**
If you do not know how a command is used, the man page of that command will provide valuable information.

The most important parts of the man page in general are at the bottom of the man page. The topics you find here are related man pages, which is useful if you have just not hit the right man page.

**man -k** -  This command looks in the summary of all man pages that are stored in the mandb database (man- k partition). **Man -k** is giving you, you can probably identify the man page that you need to access to do whatever you want to accomplish.

Man pages are categorized in different sections. The most relevant sections for system administrators are as follows:

- **1:** Executable programs or shell commands
- **5:** File formats and conventions
- **8:** System administration commands

example:
man 5 /etc/crontab

When you use the **man -k** command, the mandb database is consulted. This database is automatically created through a scheduled job. Occasionally, you might look for something that should obviously be documented, but all you get is the message “nothing appropriate.” If that happens, you might need to update the mandb database manually. Doing that is easy: Just run the **mandb** command as root without any arguments.

**whatis** - command searches for a short description of the specified command or file in the manual database.

**Using /usr/share/doc Documentation Files**

A third source of information consists of files that are sometimes copied to the /usr/share/doc directory. Some services store very useful information in this directory, like rsyslog, bind, Kerberos, and OpenSSL. For some services, even sample files are included.

