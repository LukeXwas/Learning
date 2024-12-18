**RHEL supports three fundamental user account types: _root_, _normal_, and _service_.**

**Privileged users**
- The default privileged user is root. 
- This user is created by default during installation.
- This user account has full access to everything on a Linux server and is allowed to work in system space without restrictions. 
- On modern Linux distributions like RHEL 9, the root user account is often disabled. While installing RHEL 9, you have a choice of what to do with the root user. If you create a regular user and choose the option Make This User Administrator, you don’t have to set a root password and you’ll be able to use sudo when administrator privileges are needed. If you want to be able to log in as root directly, you can set a password for the root user.

Methods to Run Tasks with Elevated Permissions:

**Other users**

**Normal users:** 
- have user-level privileges; they cannot perform any administrative functions but can run applications and programs that have been authorized. 
- These user accounts typically have a password that is used for authenticating the user to the system.
**Service accounts:**
- take care of their respective services, which include apache, ftp, mail, and chrony.
- denied access to users
- The _nologin_ shell is a special purpose program that can be employed for user accounts that do not require login access to the system.

User account information for local users is stored in four files that are located in the _/etc_ directory. These files—_passwd, shadow_, _group_, and _gshadow_—are updated when a user or group account is created, modified, or deleted. The same files are referenced to check and validate the credentials.
