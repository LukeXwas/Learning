The Tape ARchiver (**tar**) utility is used to archive files. four important tasks with **tar**:

- Create an archive
	- **tar -cf archivename.tar /files-you-want-to-archive** - create an archive, to put files in an archive, you need at least read permissions to the file and execute permissions on the directory the file resides in.
	- **tar -rvf /root/homes.tar /etc/hosts** - add a file to an archive. -r option.
	- **tar -uvf /root/homes.tar /home** - To update a currently existing archive file, **-u** option
- List the contents of an archive
	- **tar -tvf /root/homes.tar** - list the contents of the tar archive, -t option.
- Extract an archive
	- **tar -xvf /archivename.tar** - extract the contents of an archive. This extracts the archive in the _current_ directory.
	- **tar -xvf homes.tar -C /tmp** - Use the option **-C /targetdir** to specify the target directory where you want to extract the file to.
	- **tar -xvf /archivename.tar file-you-want-to-extract** - extract specyfic file out of the archive.

| **Option** | **Definition**                                                                                                       |
| ---------- | -------------------------------------------------------------------------------------------------------------------- |
| -c         | Creates a tarball.                                                                                                   |
| -f         | Specifies a tarball name.                                                                                            |
| -p         | Preserve file permissions. Default for the root user. Specify this option if you create an archive as a normal user. |
| -r         | Appends files to the end of an extant uncompressed tarball.                                                          |
| -t         | Lists contents of a tarball.                                                                                         |
| -u         | Appends files to the end of an extant uncompressed tarball provided the specified files being added are newer.       |
| -v         | Verbose mode.                                                                                                        |
| -x         | Extracts or restores from a tarball.                                                                                 |

**Using Compression**

Many files contain a lot of redundancy. Compression programs allow you to make files take less disk space by taking out that redundancy. Originally, after you created the archive, it had to be compressed with a separate compression utility, such as gzip or bzip2. 

- **gzip home.tar** - replaces home.tar with its compressed version, home.tar.gz.
- **bzip2 home.tar** - replaces home.tar with its compressed version
- **gunzip** or **bunzip2** - use it to decompres

As an alternative to using these utilities from the command line, you can include the **-z** (**gzip**), **-J** (**xz**), or **-j** (**bzip2**) option while creating the archive with **tar**. This will immediately compress the archive while it is created. There is no need to use this option while extracting. The **tar** utility will recognize the compressed content and automatically decompress it for you.

Example:
- **tar cjvf homes.tar /home** - creates a compressed archive of the home directory to the home directory of user root using xz utility.
