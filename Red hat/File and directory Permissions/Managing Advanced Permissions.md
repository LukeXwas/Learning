There are three advanced permissions. 

**Set user ID (SUID) - Understanding and applying SUID

On some very specific occasions, you may want to apply this permission to executable files. By default, a user who runs an executable file runs this file with their own permissions. 

- **SUID permission applied to a file**: When applied to an executable file, this file will run as if the owner of the file was running it, applying the permissions.
- **SUID permission applied to a directory**: No effect.

You can see the SUID permission with **ls -l** as an **s** at the position where normally you would expect to see the **x** for the user permissions (the lowercase **s** means that both SUID and execute are set, whereas an uppercase **S** would mean that only SUID is set)

![[Pasted image 20241125135256.png]]

Be very careful when assigning SUID to files as **root**. If you leave write permissions on the file, any user will be able to change the content and execute anything as **root**.

Example:

User needs to change their password. To do this, the user needs to write their new password to the /etc/shadow file. This file, however, is not writeable for users who do not have root permissions. The SUID permission offers a solution for this problem. On the /usr/bin/passwd utility, this permission is applied by default. That means that when a user is changing their password, the user temporarily has root permissions because the /usr/bin/passwd utility is owned by the root user, which allows the user to write to the /etc/shadow file.

**Set group ID (SGID) - Understanding and applying SGID**

You can use it to set default group ownership on files and subdirectories created in that directory. By default, when a user creates a file, the user’s effective primary group is set as the group owner for that file.

- **SGID permission applied to a file**: When applied to an executable file, this file will run with the group permissions of the file.
- **SGID permission applied to a directory**: New files created in that directory will have the group of the directory applied to them.

The SGID permission shows in the output of **ls -l** as an **s** at the position where you normally find the group execute permission (a lowercase **s** indicates that both SGID and execute are set, whereas an uppercase **S** means that only SGID is set)

![[Pasted image 20241125140023.png]]

Example:

- Imagine a situation where users linda and lori work for the accounting department and are both members of the group account. By default, these users are members of the private group of which they are the only member. Both users, however, are members of the accounting group as well but as a secondary group setting.
- The default situation is that when either of these users creates a file, the primary group becomes owner. So by default, user linda cannot access the files that user lori has created and vice versa. However, if you create a shared group directory (say, /groups/account) and make sure that the SGID permission is applied to that directory, and that the group account is set as the group owner for that directory, all files created in this directory and all its subdirectories also get the group accounting as the default group owner. For that reason, the SGID permission is a very useful permission to set on shared group directories.

**Using the sticky bit**

This permission is useful to protect files against accidental deletion in an environment where multiple users have write permissions in the same directory. If sticky bit is applied, a user may delete a file only if they are the user owner of the file or of the directory that contains the file. It is for that reason that sticky bit is applied as a default permission to the **/tmp** directory, and it can be useful on shared group directories as well.

When you apply sticky bit, a user can delete files only if one of the following is true:
- The user has root access.
- The user is owner of the file.
- The user is owner of the directory where the file exists.

When using **ls -l**, you can see sticky bit as a **T** at the position where you normally see the execute permission for others (a lowercase **t** indicates that sticky bit as well as the execute permission for the others entity are set, whereas uppercase **T** indicates that only sticky bit is set)

![[Pasted image 20241125140614.png]]

![[Pasted image 20241125161751.png]]

**Applying Advanced Permissions**

To apply SUID, SGID, and sticky bit, you can use **chmod** as well. SUID has numeric value 4, SGID has numeric value 2, and sticky bit has numeric value 1. If you want to apply these permissions, you need to add a four-digit argument to **chmod**, of which the first digit refers to the special permissions.

It is rather impractical if you have to look up the current permissions that are set before working with **chmod** in absolute mode. (You risk overwriting permissions if you do not.) Therefore, I recommend working in relative mode if you need to apply any of the special permissions.

- For SUID, use **chmod u+s**
- For SGID, use **chmod g+s**
- For sticky bit, use **chmod +t**, followed by the name of the file or the directory that you want to set the permissions on

Example:
- chmod 2755 /somedir


