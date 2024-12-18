**whoami** - command returns the effective (current) username

**users** - output who is currently logged in.

**logname** - command reports the user’s real (original) username

**who** - command to list users who are currently logged on

**tty** - command to identify your current active terminal session.

**w** - command to give an overview of all users who are currently logged in.

**last** - list all user login, logout, and system reboot occurrences.

![[Pasted image 20241107130749.png]]

- **Column 1:** Login name of the user
- **Column 2:** Terminal name assigned upon logging in
- **Column 3:** Terminal name or IP address from where the connection was established-
- **Column 4 to 7:** Day, month, date, and time when the connection was established
- **Column 8:** Log out time. If the user is still logged on, it will say “still logged in”
- **Column 9:** Duration of the login session

**last reboot** - list system reboot details

**lastb** - command reports the history of unsuccessful user login attempts

**lastlog** - command reports the most recent login evidence information for every user account that exists on the system.
- **Column 4:** Timestamp for the latest login or “Never logged in” if the user never signed in

**id** - command displays the calling user’s UID (User IDentifier), username, GID (Group IDentifier), group name, all secondary groups the user is a member of, and SELinux security context

**The useradd, usermod, and userdel Commands**

This set of commands is used to add, modify, and delete a user account from the system. The _useradd_ command adds entries to the four user authentication files for each account added to the system. It creates a home directory for the user and copies the default user startup files from the _skeleton_ directory _/etc/skel_ into the user’s home directory. It can also be used to update the default settings that are used at the time of new user creation for unspecified settings.

_useradd_ (options) login
- example: **useradd -m -u 1201 -G sales,ops linda** to create a user linda who is a member of the secondary groups sales and ops with UID 1201 and add a home directory to the user account as well.

For nonlogin user:
- **useradd -s /sbin/nologin** username - create nologin user account

| **Option**         | **Description**                                                                                                                                                                                                                                                                                                                                                                                                     |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| -b (--base-dir)    | Defines the absolute path to the base directory for placing user home directories. The default is /home.                                                                                                                                                                                                                                                                                                            |
| -c (--comment)     | Describes useful information about the user.                                                                                                                                                                                                                                                                                                                                                                        |
| -d (--home-dir)    | Defines the absolute path to the user home directory.                                                                                                                                                                                                                                                                                                                                                               |
| -D (--defaults)    | Displays the default settings from the /etc/default/useradd file and modifies them.                                                                                                                                                                                                                                                                                                                                 |
| -e (--expiredate)  | Specifies a date on which a user account is automatically disabled. The format for the date specification is YYYY-MM-DD.                                                                                                                                                                                                                                                                                            |
| -f (--inactive)    | Denotes maximum days of inactivity between password expiry and permanent account disablement.                                                                                                                                                                                                                                                                                                                       |
| -g (--gid)         | Specifies the primary GID. Without this option, a group account matching the username is created with the GID matching the UID.                                                                                                                                                                                                                                                                                     |
| -G (--groups)      | Specifies the membership to supplementary groups.                                                                                                                                                                                                                                                                                                                                                                   |
| -k (--skel)        | Specifies the location of the skeleton directory (default is /etc/skel), which stores default user startup files. These files are copied to the user’s home directory at the time of account creation. Three hidden bash shell files—.bash_profile, .bashrc, and .bash_logout—are available in this directory by default. You can customize these files or add your own to be used for accounts created thereafter. |
| -m (--create-home) | Creates a home directory if it does not already exist.                                                                                                                                                                                                                                                                                                                                                              |
| -o (--non-unique)  | Creates a user account sharing the UID of an existing user. When two users share a UID, both get identical rights on each other’s files. This should only be done in specific situations.                                                                                                                                                                                                                           |
| -r (--system)      | Creates a service account with a UID below 1000 and a never-expiring password.                                                                                                                                                                                                                                                                                                                                      |
| -s (--shell)       | Defines the absolute path to the shell file. The default is /bin/bash.                                                                                                                                                                                                                                                                                                                                              |
| -u (--uid)         | Indicates a unique UID. Without this option, the next available UID from the /etc/passwd file is used.                                                                                                                                                                                                                                                                                                              |
| login              | Specifies a login name to be assigned to the user account.                                                                                                                                                                                                                                                                                                                                                          |
_usermod_ - can modify the attributes of a user account. 
- **usermod -aG** newgroup username - will add users to new groups that will be used as their secondary group.
- **deluser**  username group - will remove user from newgroup parameter

The common use of the **_usermod_** command is to modify a user’s attribute, but it can also lock or unlock their account.
- -L - Locks a user account by placing a single exclamation mark (!) at the beginning of the password field and before the hashed password string.
- -U - Unlocks a user’s account by removing the exclamation mark (!) from the beginning of the password field.

| **Option**       | **Description**                                                           |
| ---------------- | ------------------------------------------------------------------------- |
| -a (--append)    | Adds a user to one or more supplementary groups                           |
| -l (--login)     | Specifies a new login name                                                |
| -m (--move-home) | Creates a home directory and moves the content over from the old location |
_userdel_ (options) username

The _userdel_ command is straightforward. It removes entries for the specified user from the authentication files, and deletes the user’s home directory if the -r flag is also specified. The -f option may be used to force the removal even if the user is still logged in.

**If you don't want to use user* commands, you can edit the contents of the /etc/passwd and /etc/shadow configuration files directly in an editor, using the _vipw_ command (with the risk of making an error that could make logging in impossible to anyone).**
