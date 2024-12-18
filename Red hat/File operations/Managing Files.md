Basic file wilcards:
![[Pasted image 20241021184844.png]]
**Absolute paths and relative paths**
- Absolute paths - is a complete path reference to the file or directory you want to work with. This pathname starts with the root directory, followed by all subdirectories up to the actual filename.
- Relative paths - is relative to the current directory as shown with the **pwd** command. It contains only the elements that are required to get from the current directory up to the item you need.

Basic commands:

- **pwd** command identifies the current directory.
- The dot symbol ".” signifies the current directory.
- **cd** - change directories in Linux. **cd** command with no arguments navigates to your home directory. **cd ..** moves to the parent directory of the current working directory.
- **touch** - create a new empty file.
- **mv _file1 file2_** command changes the name of _file1_ to _file2_. Moreover, **mv** command can also be used to move files and directories into the directory specified as the last argument.
- **mkdir somefiles** - create directory name somefile. 
	- -p switch creates a series of directories ( test1/test2/test3 )
	- use {1..5} to create few directories, example mkdir test_{1..3}
- **tree** - lists a hierarchy of directories and files. 
	- -a	Includes hidden files in the output
	- -d	Excludes files from the output
	- -h	Displays file sizes in human-friendly format
	- -f	Prints the full path for each file
	- -p	Includes file permissions in the output

While working with files and directories, it is useful to show the contents of the current directory. For this purpose, you can use the **ls** command.

![[Pasted image 20241021190338.png]]
ls -Z - returns SELinux file contexts.
ls -1 - returns only files without directories (use when u want to sum files without current and parent directories)

The **cp** (copy) command allows you to take the contents of one file and place a copy with the same or different name in the directory of your choice. One of the dangers of **cp** is that it can easily overwrite files in different directories 

cp -a  /etc /tmp -> supports recursive changes and preserves all file attributes, such as permissions, ownerships, and timestamps.

**rm** - delete files. 
- - r - option removes directories with its context.
- -f - switch overrides any safety precautions, such as the **-i** switch. It’s still quite a dangerous command.

