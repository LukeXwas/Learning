Each file within a file system has a multitude of attributes assigned to it at the time of its creation. These attributes are collectively referred to as the file’s _metadata_, and they change when the file is accessed or modified. A file’s metadata includes several pieces of information, such as the file type, size, permissions, owner’s name, owning group name, last access/modification times, link count, number of allocated blocks, and pointers to the data storage location. This metadata takes 128 bytes of space for each file. This tiny storage space is referred to as the file’s _inode_ (_index node_).

An inode is assigned a unique numeric identifier that is used by the kernel for accessing, tracking, and managing the file. In order to access the inode and the data it points to, a filename is assigned to recognize it and access it. This mapping between an inode and a filename is referred to as a _link_. It is important to note that the inode does not store the filename in its metadata; the filename and corresponding inode number mapping is maintained in the directory’s metadata where the file resides.

Linking files or directories creates additional instances of them, but all of them eventually point to the same physical data location in the directory tree. Linked files may or may not have identical inode numbers and metadata depending on how they are linked.

There are two ways to create file and directory links in RHEL, and they are referred to as hard links and soft links. Links are created between files or between directories, but not between a file and a directory.

**Hard links**:
- **is a mapping between one or more filenames and an inode number, making all hard-linked files indistinguishable from one another.**
- all hard-linked files will have identical metadata
- **name of the file is referred to as hard link. So every file always has one hard link to start with, which is the name of the file. When you create a file, you give it a name. Basically, this name is a hard link.**
- Multiple hard links can be created to a file. This is useful if a file with the same contents needs to be available at multiple locations.
- If a change is applied to any one of the hard links, it will show in all other hard links as well, as all hard links point to the same data blocks.
- Hard links must exist all on the same device and you cannot create hard links to directories.
- When the last name (hard link) to a file is removed, access to the file’s data is also removed.
- if the first hard link that ever existed for a file is removed, that does not impact the other hard links that still exist.
- To be able to create hard links, you must be the owner of the item that you want to link to.

![[Pasted image 20241125133645.png]]

**Soft links**:
- A _soft_ link (a.k.a. a _symbolic_ link or a _symlink_) makes it possible to associate one file with another.
- The concept is analogous to that of a shortcut in Microsoft Windows where the actual file is resident somewhere in the directory structure, but there can be one or more shortcuts with different names pointing to it.
- With a soft link, you can access the file directly via the actual filename as well as any of the shortcuts.
- A symbolic link (also referred to as a soft link) does not link directly to the inode but to the name of the file.
- Symbolic links is that they can link to files on other devices, as well as on directories.
- When the original file is removed, the symbolic link becomes invalid and does not work any longer.
- Each soft link has a unique inode number that stores the pathname to the file it is linked with. For a symlink, the link count does not increase or decrease, rather each symlinked file receives a new inode number.
- The size of the soft link is the number of characters in the pathname to the target.

![[Pasted image 20241125134451.png]]

How to use links:
**ln** - command to create links.

![[Pasted image 20241022133553.png]]
![[Pasted image 20241022133640.png]]

The **ls** command will reveal whether a file is a link:
- In the output of the **ls -l** command, the first character is an l if the file is a symbolic link.
- If a file is a symbolic link, the output of **ls -l** shows the name of the item it links to after the filename.
- If a file is a hard link, **ls -l** shows the hard link counter. This is the number 3 that is right before root root for the hosts file.

**Differences between Copying and Linking**

| **Copying**                                                                                            | **Linking**                                                                                                                                                                                                                                                |
| ------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Creates a duplicate of the source file. If either file is modified, the other file will remain intact. | Creates a shortcut that points to the source file. The source can be accessed or modified using either the source file or the link.                                                                                                                        |
| Each copied file stores its own data at a unique location.                                             | All linked files point to the same data.                                                                                                                                                                                                                   |
| Each copied file has a unique inode number with its unique metadata.                                   | **Hard Link:** All hard-linked files share the same inode number, and hence the metadata. **Symlink:** Each symlinked file has a unique inode number, but the inode number stores only the pathname to the source.                                         |
| If a copy is moved, erased, or renamed, the source file will have no impact, and vice versa.           | **Hard Link:** If the hard link is weeded out, the other file and the data will remain untouched. **Symlink:** If the source is deleted, the soft link will be broken and become meaningless. If the soft link is removed, the source will have no impact. |
| Copy is used when the data needs to be edited independent of the other.                                | Links are used when access to the same source is required from multiple locations.                                                                                                                                                                         |
| Permissions on the source and the copy are managed independent of each other.                          | Permissions are managed on the source file.                                                                                                                                                                                                                |
