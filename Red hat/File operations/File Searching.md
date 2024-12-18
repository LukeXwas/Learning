The _find_ command recursively searches the directory tree, finds files that match the specified criteria, and optionally performs an action on the files as they are discovered. This powerful tool can be tailored to look for files in a number of ways. The search criteria may include tracking files by name or part of the name, ownership, owning group, permissions, inode number, last access or modification time in days or minutes, size, and file type.

![[Pasted image 20241125171925.png]]

With _find_, files that match the criteria are located and their full paths are displayed.

Examples:

- To search for a file called _file10_ (execute **touch file10** if it does not already exist) **by its name (name)** in _root_’s home directory, run the _find_ command as follows - 

![[Pasted image 20241125172304.png]]

-print is optional. The _find_ command, by default, displays the results on the screen. You do not need to specify this option.

- To perform a **case-insensitive (-iname) search** for files and directories in _/dev_ that begin with the string “usb” followed by any characters:

![[Pasted image 20241125172349.png]]

- To find files s**maller than 1MB (-1M) in size (-size)** in the _root_ user’s home directory (~):

![[Pasted image 20241125172440.png]]

- To search for files **larger than 40MB (+40M) in size (-size)** in the _/usr_ directory:
![[Pasted image 20241125172521.png]]
- To find files in the entire root file system (_/_) with **ownership (-user)** set to user _daemon_ and **owning group (-group)** set to any group other than ***(-not or ! for negation)*** _user1_:

![[Pasted image 20241125172611.png]]
- To search for **directories (-type)** by the name “src” (-name) in _/usr_ at **a maximum of two subdirectory levels below (-maxdepth)**:

![[Pasted image 20241125172708.png]]
- To find files in the _/etc_ directory that were **modified (-mtime) more than (the + sign) 2000 days ago**:

![[Pasted image 20241125172844.png]]
- To find files in the _/var/log_ directory that have been **modified (-mmin) in the past (the - sign) 100 minutes**:
![[Pasted image 20241125172938.png]]
To run the above search for files that have been modified exactly 25 minutes ago, replace “-100” with “25”.

- To search for **block device files (-type)** in the _/dev_ directory with **permissions (-perm) set to exactly 660**:
![[Pasted image 20241125174105.png]]
- Find empty files

$ find ~ -type f -empty
``
- Search a path

$ find / -type d -name 'img' -ipath "*public_html/example.com*" 

- To search for character device files (-type) in the _/dev_ directory with **at least (-222) world writable permissions** (this example would ignore checking the write and execute permissions):
![[Pasted image 20241125175404.png]]
prefix the number with `+` (more than) or `–` (less than).

- To search for symlinked files (-type) in _/usr_ with **permissions (-perm) set to read and write for the owner and owning group**:
![[Pasted image 20241125175506.png]]
**We can combine patterns with an "or," represented by `-o`**

![[Pasted image 20241125174656.png]]
**Using find with -exec and -ok Flags**

An advanced use of the _find_ command is to perform an action on the files as they are found based on any criteria outlined in the previous subsection and in the command’s manual pages. **This is done with the -exec switch. An equivalent option -ok may be used instead, which requires user confirmation before taking an action.**

To search for directories in the entire directory tree (/) by the name “core” (-name) and list them (ls -ld) as they are discovered without prompting for user confirmation (-exec):

![](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781835887325/files/html/images/132_3.jpg)

The _find_ command replaces {} for each filename as it is found. Use + to speed up command executions. The semicolon character (;) marks the termination of the command and it is escaped with the backslash character (\\).

In the next example, the _find_ command uses the -ok switch to prompt for confirmation (you need to enter a y) before it copies each matched file (-name) in _/etc/sysconfig_ to _/tmp_:

![[Pasted image 20241125180450.png]]

