**chown** - command changes ownership for the file files to user

- chown who what - syntax
- The **chown** command has a few options, of which one is particularly useful: **-R**. It allows you to set ownership recursively, which allows you to set ownership of the current directory and everything below.

Example:
- command changes ownership for the file files to user linda: -> chown linda files
- command changes ownership for the directory /files and everything beneath it to user linda: -> chown -R linda /files

**Changing Group Ownership**

There are actually two ways to change group ownership. You can do it using **chown**, but there is also a specific command with the name **chgrp** that does the job. If you want to use the **chown** command, use a **.** or **:** in front of the group name.

examples:
- changes the group owner of directory /home/account to the group account: -> chown .account /home/account
- Sets user lisa as the owner of myfile -> chown lisa myfile
- Sets user lisa as user owner and group sales as group owner of myfile -> chown lisa.sales myfile
- Sets user lisa as user owner and group sales as group owner of myfile -> chown lisa:sales myfile
- Sets group sales as group owner of myfile without changing the user owner -> chown .sales myfile
- Sets group sales as group owner of myfile without changing the user owner -> chown :sales myfile

**chgrp** - command to change group ownership - chgrp account /home/account

You can use the option -R  with chgrp as well to change group ownership recursively.

**Applying Read, Write, and Execute Permissions**

To apply permissions, you use the **chmod** command.
- When using **chmod**, you can set permissions for user, group, and others
- You can use this command in two modes: the relative mode and the absolute mode.

![[Pasted image 20241125133116.png]]

In absolute mode, three digits are used to set the basic permissions. 
- The three digits apply to user, group, and others. 
- When setting permissions, calculate the value that you need. 
- The permissions are stored in four octal digits. This means that special permissions are stored in a number from 0 to 7, the same way user, group, and other permissions are stored, each one of them with a number from 0 to 7.
- **When you use _chmod_ in this way, all current permissions are replaced by the permissions you set.**

![[Pasted image 20241125130808.png]]
Example: chmod 755 file.txt

**Relative mode**

To change permissions using **chmod** in relative mode, we specify the changes with three characters:

- The first one, which determines whom the change affects:
    - **u**: User
    - **g**: Group
    - **o**: Others
- The second one to add or remove permissions:
    - **+**: Add
    - **-**: Remove
- The third one, which determines the permission to be changed:
    - **r**: Read
    - **w**: Write
    - **x**: Execute

chmod **+x** somefile -> adds the execute permission for all users if you not specif
y the “to whom” part

Example: 
- chmod g+w file.txt
- chmod g+w,o-r somefile

Files becoming executable in an uncontrolled way are a major security issue. For that reason, if you want to apply the execute permission in a recursive way, you should apply it as X, not x. So instead of using **chmod -R a+x files**, use **chmod -R a+X files**. This ensures that subdirectories will obtain the execute permission but the execute permission is not applied to any files.


