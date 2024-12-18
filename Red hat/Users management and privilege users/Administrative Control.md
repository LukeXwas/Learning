It’s important for administrators to execute most actions as regular users because the root administrative user has full privileges on a system. Limits on regular users can help protect Linux systems from accidents. 

**The Ability to Log In**

The file /etc/security/access.conf regulates access by all users. By default, in RHEL 9 the file /etc/security/access.conf does not have any effect. To enable access.conf, add the following line to /etc/pam.d/password-auth and /etc/pam.d/system-auth:

- account required pam_access.so

The default version of this file is completely commented out. Be aware that the directives in this file are considered in order. So, if directives that allow access come first, then the following directive denies access.

Examples:
- -:ALL EXCEPT root:tty1 - shows how to disallow (with the -) logins to the first virtual console (tty1) to _all_ users but root

 ![Images](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781260462081/files/f0233-03.jpg)
The following lines (with the +) show how to allow the root user to access the system from three specific remote IP addresses and from the localhost address

If you’re protecting a system from outside networks, this type of limitation on direct root administrative access makes sense. As long as the **su** or **sudo** command allows it, users who log in remotely as regular users can still elevate their privileges accordingly. The following directive denies access to all other users from all other local and remote logins:
- -:ALL:ALL 

**Using su**

**su** - command to start a subshell in which you have another identity. If you want to become another user, you need to know password for that account. 
- If you type just the command **su**, the username root is implied.
- **Su** can be used to run tasks as another user as well, like **su linda** to become user Linda
- The subshell that is started when using **su** is an environment where you are able to work as the target user account, but environment settings for that user account have not been set. If you need complete access to the entire environment of the user account, you can use **su -** to start a login shell. If you start a login shell, all scripts that make up the user environment are processed, which makes you work in an environment that is exactly the same as when logging in as that user.
- The _root_ user can switch into any user account that exists on the system without being prompted for that user’s password.
- **su -c** command can be used to assume administrative privileges for one command (assuming the root administrative password is successfully entered in response to the prompt).
	- For example, use **sudo sh -c "rpm -qa | grep ssh"**

**Limit Access to su**

The ability to log in directly as the root administrative user can be regulated. You can limit the users who are allowed to run the **su** command, which requires two basic steps. 
1. First, you’ll need to list the users who should have access to the **su** command. Make them a part of the wheel group.
2. Second, this requires a change to the configuration of Pluggable Authentication Modules (PAM) /etc/pam.d/su
	1. # auth       required   pam_wheel.so
	2. If this line is activated, only users who are members of the wheel group are allowed to use the **su** command

**Superuser Access with the sudo Command**

You can limit access to the **sudo** command. Regular users who are authorized in /etc/sudoers can access administrative commands with their own password. **the sudo command requires you to type your own user account’s password.** If a non-root user needs to perform a specific system administration task, the user does not need root access; instead, the system administrator can configure **sudo** to give that user administrator permissions to perform the specific task. _The user then carries out the task by starting the command with **sudo** (and entering the user’s password when prompted)_.

The _sudo_ utility is designed to provide protected access to administrative functions as defined in the _/etc/sudoers_ file. 

Any normal user that requires privileged access to administrative commands or non-owning files is defined in the _sudoers_ file. This file may be edited with a command called **_visudo_**, which creates a copy of the file as _sudoers.tmp_ and applies the changes there. The **visudo** command locks the /etc/sudoers file against simultaneous edits and checks the syntax of the file before exiting. After the _visudo_ session is over, the updated file overwrites the original _sudoers_ file and _sudoers.tmp_ is deleted.

![[Pasted image 20241120232905.png]]

- The first field is to specify who is affected by the policy:
    - We can add users by simply putting the username in the first field.
    - We can add groups by using the **%** character before the name of the group in the first field.
- The second field is for where the policy applies:
    - We have so far used **ALL=(ALL)** to specify everything.
    - In the first part of this field, we can define a group of computers to be run, such as **SERVERS=10.0.0.0/255.255.255.0**.
    - In the second part, we can specify commands such as **NETWORK=/usr/sbin/ip**.
    - Between parentheses is the user account that can be used to run the command.
- The third field is to specify which commands will use the password and which won’t.

This allows the root user to run any command as any user:

![Images](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781260462081/files/f0235-01.jpg)

The **root** keyword indicates that this configuration applies to the root user. Thanks to this configuration, the root user can run any command (due to the last ALL on the line), from any host (thanks to the first ALL), as any user (the second ALL).

![Images](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781260462081/files/f0235-02.jpg)

Boris needs to do to run an administrative command is to preface it with the **sudo** command. For example, if boris runs the following command, he’s prompted for his own regular user password before the noted service is started.

**linda ALL=/usr/bin/useradd, /usr/bin/passwd, ! /usr/bin/passwd root**. This would allow user linda to change the password for all users, but not for root. ! before a command specifies that a given user cannot execute a given command using sudo (/usr/bin/passwd, ! /usr/bin/passwd root)

It is also possible to set up **sudo** privileges after installation by making the user a member of the group wheel.

**You can allow special users administrative access without a password**. As suggested by the comments in the file, the following directive in /etc/sudoers would allow all users who are members of the wheel group to run administrative commands without a password:

![Images](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781260462081/files/f0235-04.jpg)

**In many Linux configuration files, the % sign in front of a directive specifies a group.** For example, another directive shown in comments specifies a group of commands that can be run by users who are members of the %sys group:

![Images](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781260462081/files/f0235-06.jpg)

Each of the directives can be associated with a set of commands. PROCESSES directives:

![Images](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781260462081/files/f0235-07.jpg)

Predefined aliases

Cmnd_Alias	PKGCMD = /usr/bin/yum, /usr/bin/rpm -> command alias
User_Alias	PKGADM = user1, user100, user200 -> user alias
PKGADM	ALL = PKGCMD -> users of group PKGADM have acces to commands from PCGCMD alias

Append the above to the bottom of the _sudoers_ file and then run the _yum_ or _rpm_ command preceded by _sudo_ as one of the users listed.

![[Pasted image 20241120230127.png]]

This line enables the **/etc/sudoers.d** directory as a source for configuration files. We can drop a file in that folder and it will be used by **sudo**. For compatibility with **sudo** versions prior to 1.9.1, **#include** and **#includedir** are also accepted.

A better practice is to create a drop-in file in the directory /etc/sudoers.d. This drop-in file would have the exact same contents as the modification you would make to /etc/sudoers, with the benefit that the custom configuration is separated from the standard configuration that was created while installing Linux. Files in /etc/sudoers.d are always included while using **sudo**.

For cloud instances, the account root does not have a valid password assigned. To be able to manage the mentioned cloud instance, in some clouds such as **Amazon Web Services** (**AWS**), a user is created by default and added to the **wheel** group. In the case of AWS, the default user account is **ec2-user**. In other clouds, a custom user is also created and also added to the **wheel** group.