
The **git config** command is a convenience function that is used to set Git configuration values on a global or local project level. These configuration levels correspond to **.gitconfig** text files. Executing git config will modify a configuration text file.

**git config levels and files

The git config command can accept arguments to specify which configuration level to operate on. The following configuration levels are available:

- **--local

By default, git config will write to a local level if no configuration option is passed. Local level configuration is applied to the context repository git config gets invoked in. Local configuration values are stored in a file that can be found in the repo's .git directory: **.git/config**

To list local (repository) properties: **git config --list --local

- **--global

Global level configuration is user-specific, meaning it is applied to an operating system user. Global configuration values are stored in a file that is located in a user's home directory. **~ /.gitconfig 

To list global properties: **git config --list --global

- **--system

System-level configuration is applied across an entire machine. This covers all users on an operating system and all repos. The system level configuration file lives in a gitconfig file off the system root path. **/etc/gitconfig on unix systems.

To list **system** properties: **git config --list --system

**Thus the order of priority for configuration levels is: local, global, system. This means when looking for a configuration value, Git will start at the local level and bubble up to the system level.  

The follow command will have Git config show the user.email property used by a repository for local commits:

![[Pasted image 20241216122819.png]]

**Writing a value

1. Add username and email - This is a mandatory setting, which you must provide to start using Git. our username and e-mail will be included in every commit you perform.

![[Pasted image 20241216123141.png]]

2. Choose the default editor for Git

![[Pasted image 20241216122323.png]]

3. Git pruning during fetch

Pruning during fetch is a cleanup method that deletes outdated remote references in your **.git** directory when you do a **git fetch --prune**

![[Pasted image 20241216122434.png]]

With this in place, pruning will occur whenever you do a git fetch.




