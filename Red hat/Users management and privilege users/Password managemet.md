Password aging is a secure mechanism to control user passwords in Linux. The key advantages include setting restrictions on password expiry, account disablement, locking and unlocking users, and password change frequency. These controls are applied to all user accounts at the time of their creation and can be set explicitly on a per-user basis later. You can even choose to inactivate it completely for an individual user. Password aging information is stored in the _/etc/shadow_ file (fields 4 to 8) and its default policies in the _/etc/login.defs_ configuration file

**The chage command**

The _chage_ command is used to set or alter password aging parameters on a user account. This command changes various fields in the _shadow_ file depending on which option(s) you pass to it.

The **chage** command also has an interactive mode; if you type **chage anna**, for instance, the command will prompt for all the password properties you want to set interactively.

| **Option**        | **Description**                                                                                                                                                                                                                                                            |
| ----------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| -d (--lastday)    | Specifies an explicit date in the YYYY-MM-DD format, or the number of days since the UNIX time when the password was last modified. With -d 0, the user is forced to change the password at next login. It corresponds to field 3 in the shadow file.                      |
| -E (--expiredate) | Sets an explicit date in the YYYY-MM-DD format, or the number of days since the UNIX time on which the user account is deactivated. This feature can be disabled with -E -1. It corresponds to field 8 in the shadow file.                                                 |
| -I (--inactive)   | Defines the number of days of inactivity after the password expiry and before the account is locked. The user may be able to log in during this period with their expired password. This feature can be disabled with -I -1. It corresponds to field 7 in the shadow file. |
| -l                | Lists password aging attributes set on a user account.                                                                                                                                                                                                                     |
| -m (--mindays)    | Indicates the minimum number of days that must elapse before the password can be changed. A value of 0 allows the user to change their password at any time. It corresponds to field 4 in the shadow file.                                                                 |
| -M (--maxdays)    | Denotes the maximum number of days of password validity before the user password expires and it must be changed. This feature can be disabled with -M -1. It corresponds to field 5 in the shadow file.                                                                    |
| -W (--warndays)   | Designates the number of days for which the user gets alerts to change their password before it expires. It corresponds to field 6 in the shadow file.                                                                                                                     |
Examples:
- **chage -l** - to see current password management settings
- **chage -E 2025-12-31 bob** - to have the account for user bob expire on December 31, 2025

**The passwd command**

The common use of the _passwd_ command is to set or modify a user’s password; however, you can also use this command to modify the password aging attributes and lock or unlock their account.

| **Option**      | **Description**                                                                                                                                                 |
| --------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| -d (--delete)   | Deletes a user password without expiring the user account.                                                                                                      |
| -e (--expire)   | Forces a user to change their password upon next logon.                                                                                                         |
| -i (--inactive) | Defines the number of days of inactivity after the password expiry and before the account is locked. It corresponds to field 7 in the shadow file.              |
| -l (--lock)     | Locks a user account.                                                                                                                                           |
| -n (--minimum)  | Specifies the number of days that must elapse before the password can be changed. It corresponds to field 4 in the shadow file.                                 |
| -S (--status)   | Displays the status information for a user.                                                                                                                     |
| -u (--unlock)   | Unlocks a locked user account.                                                                                                                                  |
| -w (--warning)  | Designates the number of days for which the user gets alerts to change their password before it actually expires. It corresponds to field 6 in the shadow file. |
| -x (--maximum)  | Denotes the maximum number of days of password validity before the user password expires and it must be changed. It corresponds to field 5 in the shadow file.  |

Examples
- **passwd -n 30 -w 3 -x 90 linda** sets the password for user linda to a minimal usage period of 30 days and an expiry after 90 days, where a warning is generated 3 days before expiry.