The **git init** command creates a new Git repository. It can be used to convert an existing, unversioned project to a Git repository or initialize a new, empty repository.

- Executing git init creates a .git subdirectory in the current working directory, which contains all of the necessary Git metadata for the new repository. 
- This metadata includes subdirectories for objects, refs, and template files.
- A **HEAD** file is also created which points to the currently checked out commit.

By default, **git init** will initialize the Git configuration to the **.git** subdirectory path.

How to create git repository:

All you have to do is cd into your project subdirectory and run **git init**, and you'll have a fully functional Git repository.

![[Pasted image 20241216115519.png]]

Executing this command will create a new .git subdirectory in your current working directory. This will also create a new main branch. 

**git init \<directory>** - Create an empty Git repository in the specified directory. Running this command will create a new subdirectory called ＜directory＞ containing nothing but the **.git** subdirectory.

**If you've already run `git init` on a project directory and it contains a `.git` subdirectory, you can safely run `git init` again on the same project directory. It will not override an existing `.git` configuration.


**Bare repositories --- git init --bare

![[Pasted image 20241216115701.png]]

Initialize an empty Git repository, but omit the working directory. Shared repositories should always be created with the --bare flag. Conventionally, repositories initialized with the --bare flag end in .git. For example, the bare version of a repository called my-project should be stored in a directory called my-project.git.

The **--bare** flag creates a repository that doesn’t have a working directory, making it impossible to edit files and commit changes in that repository. You would create a bare repository to git push and git pull from, but never directly commit to it. Central repositories should always be created as bare repositories because pushing branches to a non-bare repository has the potential to overwrite changes. 


![[Pasted image 20241216120119.png]]

**The most common use case for  `git init --bare` is to create a remote central repository.

**Git init has a few other command line options. A full list of them follows:

-Q

--QUIET - Only prints "critical level" messages, Errors, and Warnings. All other output is silenced.

--BARE - Creates a bare repository.

--TEMPLATE= - Specifies the directory from which templates will be used.

--SEPARATE-GIT-DIR=  - Creates a text file containing the path to . This file acts as a link to the .git directory. This is useful if you would like to store your .git directory on a separate location or drive from your project's working files. Some common use cases for --separate-git-dir are:

- to keep your system configuration "dotfiles" (.bashrc, .vimrc, etc.) in the home directory while keeping the .git folder elsewhere
- Your Git history has grown very large in disk size and you need to move it elsewhere to a separate high-capacity drive
- You want to have a Git project in a publicly accessible directory like `www:root`

**EXAMPLES

**Create a new git repository for an existing code base

![[Pasted image 20241216120434.png]]

**Create a new bare repository

![[Pasted image 20241216120453.png]]

**Create a git init template and initialize a new git repository from the template

![[Pasted image 20241216120511.png]]




