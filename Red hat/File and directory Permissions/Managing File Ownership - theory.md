File and directory ownership are vital for working with permissions. 

These owners are set when a file or directory is created. On creation, the user who creates the file becomes the user owner, and the primary group of that user becomes the group owner. To determine whether you as a user have permissions to a file or a directory, the shell checks ownership. This happens in the following order:

1. The shell checks whether you are the user owner of the file you want to access, which is also referred to as the user of the file. If you are the user, you get the permissions that are set for the user, and the shell looks no further.
2. If you are not the user owner, the shell checks whether you are a member of the group owner, which is also referred to as the group of the file. If you are a member of the group, you get access to the file with the permissions of the group, and the shell looks no further.
3. If you are neither the user owner nor the group owner and have not obtained permissions through access control lists (ACLs), you get the permissions of the others entity.

**Displaying Ownership**

- On Linux, every file and every directory has two owners: **a user owner and a group owner**. Apart from that, there is the “others” entity, which also is considered to be an entity to determine the permissions a user has.
- Collectively, the user, group, and others (ugo) owners are shown when listing permissions with the **ls -l** command

Example: **ls -la /usr/bin/bash**

The blocks are as follows:

![[Pasted image 20241124211534.png]]
- **Block 1** is for the special permissions that the file may have. If it is a regular file and has no special permissions (as in this case), it will appear as **-**:
	- - Directories will appear with **d**.
	- Links, usually symbolic links, will appear with an **l**.
	- Special permissions to run a file as a different user or group, called **setuid** or **setgid**, will appear as **s**.
	- Special permissions for directories so that the owner can only remove or rename the file, called a **sticky bit**, will appear as **t**.
- **Block 2** is the permissions for the _user_ owning the file, and consists of three characters:
	- The first one, **r**, is the read permission assigned.
	- The second one, **w**, is the write permission assigned.
	- The third one, **x**, is the executable permission (note that the executable permission for directories means being able to enter them.)
- **Block 3** is permissions for the _group_. It consists of the same three characters for read, write, and execute (**rwx**). In this case, write is missing.
- **Block 4** is the permissions for _others_. It also consists of the same three characters for read, write, and execute (**rwx**) as before. As in the previous block, write is missing.
- **Block 5** indicates that there is an **SELinux** context applied to the file.

**Understanding Read, Write, and Execute Permissions**

This basic permission system uses three permissions that can be applied to files and directories.

![[Pasted image 20241125125801.png]]
The execute permission will never be set by default, which makes Linux almost completely immune to viruses. Only the user owner and the root user can apply the execute permission. This means that execute is an important permission for directories, and you will see that it is normally applied as the default permission to directories.

