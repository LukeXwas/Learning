**Shell Startup Files**

Modifications to the default shell environment can be stored in _startup_ (or _initialization_) files. These files are sourced by the shell following user authentication at the time of logging in and before the command prompt appears. When a user logs in, an environment is created for that user automatically. In addition, aliases, functions, and scripts can be added to these files as well. There are two types of startup files: _system-wide_ and _per-user_.

**System-wide Shell Startup Files**

_System-wide_ startup files set the general environment for all users at the time of their login to the system. These files are located in the _/etc_ directory and are maintained by the Linux administrator. System-wide files can be modified to include general environment settings and customizations.

**Per-user Shell Startup Files**

_Per-user_ shell startup files override or modify system default definitions set by the system-wide startup files. These files may be customized by individual users to suit their needs. By default, two such files, in addition to the _.bash_logout_ file, are located in the skeleton directory _/etc/skel_ and are copied into user home directories at the time of user creation.

**The order in which the system-wide and per-user startup files are executed is important to grasp. The system runs the _/etc/profile_ file first, followed by _.bash_profile_, _.bashrc_, and finally the _/etc/bashrc_ file.**

**/etc/bashrc**

The /etc/bashrc file is used for aliases and functions on a system-wide basis.
- It assigns a value of **umask**, which sets the default permissions for newly created files. It supports one set of permissions for root and system users (with user IDs below 200) and another for regular users.
- It assigns and defines a prompt, which is what you see just before the cursor at the command prompt.
- It includes settings from *.sh files in the /etc/profile.d/ directory.

The settings here are supplemented by the .bashrc file in each user’s home directory and, for login shells, by the /etc/profile, .bash_profile, and .bash_logout files.

**/etc/profile and /etc/profile.d**

The /etc/profile file is used for system-wide environments and startup files, and is sourced when bash is invoked as an interactive shell.

The first part of the file sets the PATH for searching for commands. Additional directories are added to the PATH with the **pathmunge** function. Then it exports the PATH, USER, LOGNAME, MAIL, HOSTNAME, HISTSIZE, and HISTCONTROL variables and finally runs the scripts in the /etc/profile.d directory. You can check the current value of any of these variables with the **echo $_variable_** command.

**/etc/profile.d**

The /etc/profile.d directory is designed to contain scripts to be executed in a login or interactive shell (that is, not in a script or a command that is run as **bash -c _command_**). If you performed a “Server with GUI” installation, the following is a partial listing of the files; those with .sh extensions apply to the default bash shell:

![Images](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781260462081/files/f0238-01.jpg)

In most cases, there are two versions of a script, customized for different shell environments. Look at the files in the /etc/profile.d script directory. You can see that any script in this directory that ends with .sh is included as part of the configuration sourced by /etc/profile. Scripts with other extensions, such as .csh, relate to the C shell.

There is also a per-user file _.bash_logout_ in the user’s home directory. This file is executed when the user leaves the shell or logs off. This file may be customized as well.

![[Pasted image 20241120232000.png]]

