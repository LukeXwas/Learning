RHEL supports seven types of files: regular, directory, block special device, character special device, symbolic link, named pipe, and socket. Linux does not require an extension to a file to identify its type.

**file or stat** - commands to identify type of a file.

1. **Regular_files** may contain text or binary data. These files may be shell scripts or commands in the binary form. Character (-) represent regular files.
2. **Directories** are logical containers that hold files and subdirectories. Character (d) represent directories.
3. **Block and Character Special Device Files** 
	1. Each piece of hardware in the system has an associated file in the _/dev_ directory that is used by the system to communicate with that device. This type of file is called a _device file_.
	2. There are two types of device files: _character_ (or _raw_) and _block_.
	3. “c” for character and a “b” for block
4. **Symbolic Links** - a shortcut to another file or directory. Character (l) represent links.