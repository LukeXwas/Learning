User account information for local users is stored in four files that are located in the _/etc_ directory. These files—_passwd, shadow_, _group_, and _gshadow_—are updated when a user or group account is created, modified, or deleted. The same files are referenced to check and validate the credentials.

These files are so critical to the operation of the system that the system creates their automatic backups by default as _passwd-_, _shadow-_, _group-_, and _gshadow-_ in the _/etc_ directory.

Two of the files—_gshadow_ and _shadow_—along with their backups have no access permissions for any user, not even for _root_.

Default settings for user accounts are stored in the /etc/login.defs file.

**The passwd File**

The _passwd_ file is a simple plaintext file but it contains vital user login data. Each row in the file holds information for one user account.

**Permissions and ownership on the _passwd_ file**

![[Pasted image 20241108161147.png]]

The access permissions on the file are 644 (world-readable and owner-writable), and it is owned by the _root_ user.

![[Pasted image 20241108134316.png]]

- **Username:** This is a unique name for the user. Usernames are important to match a user to their password, which is stored separately in /etc/shadow. On Linux, there can be no spaces in the username, and in general it’s a good idea to specify usernames in all lowercase letters.
- **Password:** Can contain an “x” (points to the _/etc/shadow_ file for the actual password), an asterisk * to identify a disabled account, or a hashed password.
- **UID:** Comprises a numeric UID between 0 and approximately 4.2 billion. UID 0 is reserved for the _root_ account, UIDs between 1 and 200 are used by Red Hat to statically assign them to core service accounts, UIDs between 201 and 999 are reserved for non-core service accounts, and UIDs 1000 and beyond are employed for normal user accounts. By default, RHEL begins assigning UIDs to new users at 1000. The range of UIDs that are used to create regular user accounts is set in /etc/login.defs.
- **GID:** On Linux, each user is a member of at least one group. By default, RHEL creates a group for every new user matching their login name and the same GID as their UID. This group is referred to as the _primary group_, and this group plays a central role in permissions management. Users can be a member of additional groups, which are administered in the file /etc/group.
- **Comments** Called GECOS (_General Electric Comprehensive Operating System_ and later changed to GCOS), optionally stores general comments about the user that may include the user’s name, phone number, location, or other useful information to help identify the person for whom the account is set up.
- **Home Directory:** Defines the absolute path to the user home directory. A _home_ directory is the location where a user is placed after signing in and it is used for personal storage. The default location for user home directories is _/home_.
- **Shell:** This is the program that is started after the user has successfully connected to a server. For most users this will be **/bin/bash**, the default Linux shell. For system user accounts, it will typically be a shell like **/sbin/nologin**. The **/sbin/nologin** command is a specific command that silently denies access to users.. Optionally, you can create an /etc/nologin.txt file, in which case only root will be able to log in but other users will see the contents of this file when their logins are denied.

**The shadow File**

RHEL has a secure password control mechanism in place that provides an advanced level of password security for local users. This control is referred to as the _shadow password_. With this control mechanism in place, user passwords are hashed and stored in a more secure file _/etc/shadow_. The _shadow_ file contains user authentication and password aging information. The _shadow_ file has no access permissions at all. With the shadow password mechanism active, a user is initially checked in the _passwd_ file for existence and then in the _shadow_ file for authenticity.

**Permissions and ownership on the _shadow_ file**

![[Pasted image 20241108161111.png]]

The access permissions on the file are 000 (no permissions at all), and it is owned by the _root_ user. There is a special mechanism in place that is employed in the background to update this file when a user account is added, modified, deleted, or the password changed.

![[Pasted image 20241108160504.png]]
![[Pasted image 20241108160537.png]]

Password explanation:
\$6$tOT/cvZ4PWRcl8XX$0v3.ADE/ibzlUGbDLer0ZYaMPNRJ5gK17LeKnoMfKK 9.nFz8grN3IafmHvoHPuh3XrU81nJu0.is5znztB64Y/
- **$6**: The algorithm used to encrypt the file. In this case, the value **6** indicates that it is SHA-512. The number **1** is for the old, now insecure, MD5 algorithm.
- **$tOT/cvZ4PWRcl8XX**: The **salt** password. This token is used to improve password encryption.
- **$0v3.ADE/ibzlUGbDLer0ZYaMPNRJ5gK17LeKnoMfKK9.nFz8grN3IafmHvoHPuh3XrU81nJu0.is5znztB64Y/**: An encrypted password hash. Using **salt** and the SHA-512 algorithm, this token is created. When the user validates, the process is run again and if the same hash is generated, the password is validated and access is granted.

**The group File**

The _group_ file is a simple plaintext file and contains critical group information. Each row in the file stores information for one group entry. Every user on the system must be a member of at least one group, which is referred to as the _User Private Group_ (UPG). By default, a group name matches the username it is associated with. Additional groups may be set up, and users with common file access requirements can be added to them.

**Permissions and ownership on the _group_ file**

![[Pasted image 20241108161246.png]]

The access permissions on the file are 644 (world-readable and owner-writable), and it is owned by the _root_ user.

![[Pasted image 20241108160839.png]]

- **Group name:** As is suggested by the name of the field, it contains the name of the group.
- **Group password:** Where applicable, this field contains a group password, a feature that is hardly used anymore. A group password can be used by users who want to join the group on a temporary basis, so that access to files the group has access to is allowed. If a group password is used, it is stored in the /etc/gshadow file, as that file is root accessible only.
- **Group ID:** This field contains a unique numeric group identification number.
- **Members:** Here you find the names of users who are a member of this group as a secondary group. Note that this field does not show users who are a member of this group as their primary group.

**The gshadow File**

The shadow password implementation also provides an added layer of protection at the group level. With this mechanism in place, the group passwords are hashed and stored in a more secure file _/etc/gshadow_. Unlike the _group_ file, which is world-readable and owner-writable, the _gshadow_ file has no access permissions at all. This is done to safeguard the file’s content.

**Permissions and ownership on the _gshadow_ file**

![[Pasted image 20241108161659.png]]

The access permissions on the file are 000 (no permissions at all) and it is owned by the _root_ user.

![[Pasted image 20241108161537.png]]

![[Pasted image 20241108161738.png]]

**The useradd and login.defs Configuration Files**

The _/etc/login.defs_ and from the _/etc/default/useradd_ file provides the baseline for a number of parameters in the shadow password suite. The _login.defs_ file is also consulted by the _usermod_, _userdel_, _chage_, and _passwd_ commands. if you change any settings, those are effective only for new users, not for existing ones.

- MAIL_DIR - Specifies the mail directory location
- UMASK - Defines the permissions to be set on the user home directory at creation based on this umask value
- HOME_MODE - The mode for new user home directories. The umask value is used if not specified with the command.
- PASS_MAX_DAYS, PASS_MIN_DAYS, and PASS_WARN_AGE - Define password aging attributes.
- UID_MIN, UID_MAX, GID_MIN, and GID_MAX - Identify the ranges of UIDs and GIDs to be allocated to new users and groups
- SYS_UID_MIN, SYS_UID_MAX, SYS_GID_MIN, and SYS_GID_MAX - Identify the ranges of UIDs and GIDs to be allocated to new service users and groups
- ENCRYPT_METHOD - Specifies the encryption method for user passwords
- USERGROUPS_ENAB - If set to yes, (1) the useradd command will create a group matching the name of the user and (2) the userdel command will delete a user’s group if it contains no more members.
- CREATE_HOME - Defines whether to create a home directory
- ENV_PATH - Defines the $PATH variable, a list of directories that should be searched for executable files after logging in.

/etc/default/useradd

![[Pasted image 20241123170608.png]]

**Home Directories**

All normal users will have a home directory. For people, the home directory is the directory where personal files can be stored. For system accounts, the home directory often contains the working environment for the service account. **When creating home directories (which happens by default while you’re creating users), the content of the “skeleton” directory is copied to the user home directory. The skeleton directory is /etc/skel, and it contains files that are copied to the user home directory at the moment this directory is created.** These files will also get the appropriate permissions to ensure that the new user can use and access them.

By default, the skeleton directory contains mostly configuration files that determine how the user environment is set up. If in your environment specific files need to be present in the home directories of all users, you take care of that by adding the files to the skeleton directory.



