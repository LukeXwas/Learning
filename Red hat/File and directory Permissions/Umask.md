- When creating a new file, some default permissions are set. These permissions are determined by the **umask** setting. This shell setting is applied to all users when logging in to the system.
- In the **umask** setting, a numeric value is used that is subtracted from the maximum permissions that can be set automatically to a file; the maximum setting for files is 666, and for directories is 777.
- Of the digits used in the **umask**, like with the numeric arguments for the **chmod** command, the first digit refers to user permissions, the second digit refers to the group permissions, and the last refers to default permissions set for others. 
- The default **umask** setting of 022 gives 644 for all new files and 755 for all new directories that are created on your server.

**umask** - show the value of default permissions

umask –S - display the umask in symbolic form

![[Pasted image 20241125165301.png]]

![[Pasted image 20241125164755.png]]

**Calculating Default Permissions**

1. Calculate the default permission values on files

![[Pasted image 20241125165402.png]]

This is an indication that every new file will have read and write permissions assigned to the owner, and a read-only permission to the owning group and others.

2. To calculate the default permission values on directories

![[Pasted image 20241125165722.png]]

This indicates that every new directory created will have read, write, and execute permissions assigned to the owner, and read and execute permissions to the owning group and everyone else.

**Set new permissions**

If you want different default permissions set on new files and directories, you will need to modify the umask. The new value becomes effective right away, and it will only be applied to files and directories created thereafter. The umask value set at the command line will be lost as soon as you log off.

![[Pasted image 20241125170814.png]]

There are two ways to change the **umask** setting: for all users and for individual users. If you want to set the **umask** for all users, you must make sure the **umask** setting is considered when starting the shell environment files as directed by /etc/profile. The right approach is to create a shell script with the name umask.sh in the /etc/profile.d directory and specify the **umask** you want to use in that shell script. If the **umask** is changed in this file, it applies to all users after logging in to your server.