Every Linux user is assigned to a _primary group_, which is the group corresponding to the GID defined in /etc/passwd. By default, in RHEL 9 every user gets his own private group, with the same name as their username. A user may also be a member of other groups, which are usually referred to as _supplementary groups_ to distinguish them from a user’s primary group.

Members of the same group possess the same access rights on files and directories. Other users and members of other groups may optionally be given access to those files.

Group information is stored in the _/etc/group_ file and the default policies in the _/etc/login.defs_configuration file. Furthermore, the _/etc/gshadow_ file stores group administrator information and group-level passwords.

- When a user creates a file, the user’s primary group becomes the group owner of the file.
- Users can also access all files their primary group has access to.
- If the group a user is a member of has access to specific files, the user will get access to those files also.
- Working with secondary groups is important, in particular in environments where Linux is used as a file server to allow people working for different departments to share files with one another.

**The group File** - /etc/group

The _group_ file is a simple plaintext file and contains critical group information. Each row in the file stores information for one group entry. Every user on the system must be a member of at least one group, which is referred to as the _User Private Group_ (UPG). By default, a group name matches the username it is associated with. Additional groups may be set up, and users with common file access requirements can be added to them.

![[Pasted image 20241121215203.png]]

- **Field 1 (Group Name):** Holds a group name that must begin with a letter.
- **Field 2 (Encrypted Password):** Can be empty or contain an “x” (points to the _/etc/gshadow_ file for the actual password), or a hashed group-level password. Where applicable, this field contains a group password, a feature that is hardly used anymore. A group password can be used by users who want to join the group on a temporary basis, so that access to files the group has access to is allowed. If a group password is used, it is stored in the /etc/gshadow file, as that file is root accessible only.
-  **Field 3 (GID):** Holds a GID, which is also placed in the GID field of the _passwd_ file. By default, groups are created with GIDs starting at 1000 and with the same name as the username.
- **Field 4 (Group Members):** Lists the membership for the group. Note that a user’s primary group is always defined in the GID field of the _passwd_ file.

**The permissions and ownership on the _group_ file**

![[Pasted image 20241121215523.png]]

The access permissions on the file are 644 (world-readable and owner-writable), and it is owned by the _root_ user.

**The gshadow File**

The shadow password implementation also provides an added layer of protection at the group level. With this mechanism in place, the group passwords are hashed and stored in a more secure file _/etc/gshadow_.

![[Pasted image 20241121215831.png]]

- **Field 1 (Group Name):** Consists of a group name as appeared in the _group_ file.
- **Field 2 (Encrypted Password):** Can contain a hashed password, which may be set with the _gpasswd_ command for non-group members to access the group temporarily using the _newgrp_ command. A single exclamation mark (!) or a null value in this field allows group members passwordless access and restricts non-members from switching into this group.
- **Field 3 (Group Administrators):** Lists usernames of group administrators that are authorized to add or remove members with the _gpasswd_ command.
- **Field 4 (Members):** Holds a comma-separated list of members.

**The permissions and ownership on the _gshadow_ file**

![[Pasted image 20241121220045.png]]

The access permissions on the file are 000 (no permissions at all), and it is owned by the _root_ user.

**The groupadd, groupmod, and groupdel Commands**

This set of management commands is used to add, modify, and delete a group from the system. The _groupadd_ command adds entries to the _group_ and _gshadow_ files for each group added to the system.

**groupadd**

groupadd (options) groupname

| **Option**        | **Description**                                                                                                                                                                                                      |
| ----------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| -g (--gid)        | Specifies the GID to be assigned to the group                                                                                                                                                                        |
| -o (--non-unique) | Creates a group with a matching GID of an existing group. When two groups have an identical GID, members of both groups get identical rights on each other’s files. This should only be done in specific situations. |
| -r                | Creates a system group with a GID below 1000                                                                                                                                                                         |
| groupname         | Specifies a group name                                                                                                                                                                                               |
The _groupadd_ command picks up the default values from the _login.defs_ file.

**groupmod**

You can modify the attributes of a group with the _groupmod_ command. The syntax of this command is very similar to the _groupadd_ with most options identical. The only flag that is additional with this command is -n, which can change the name of an existing group.

**groupdel**

The _groupdel_ command is straightforward. It removes entries for the specified group from both _group_ and _gshadow_ files.

To edit the contents of the /etc/group file where groups are defined, you can use a similar command with the name **vigr**

**Gpasswd**

The gpasswd command is used to add group administrators, add or delete group members, assign or revoke a group-level password, and disable the ability of the newgrp command to access a group. This command picks up the default values from the /etc/login.defs file.

To show the current primary group, a user can use the **groups** command. Of the groups listed, the primary group is the **first name** after the : character:
- **groups** USERNAME - print group memberships for each USERNAME

**Understanding Default Ownership in group**

When a user creates a file, default ownership is applied. The user who creates the file automatically becomes user owner, and the primary group of that user automatically becomes group owner. Normally, this is the group that is set in the /etc/passwd file as the user’s primary group.

**newgrp** - command to change the effective primary group of file (directory) if the user is a member of more groups. **New files will get the new primary group as group owner.**

![[Pasted image 20241125121348.png]]

After you change the effective primary group, all new files that the user creates will get this group as their group owner. To return to the original primary group setting, use **exit**.

**Lid command**
To see which users are a member of a group, use the **lid** command. For example, use **lid -g sales** to check which users are a member of the group sales.