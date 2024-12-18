If a host is running the sshd service, that service can also be used to securely transfer files between systems. To do that, you can use the **scp** command if you want the file to be copied, or **rsync** if you want to synchronize the file. Also, the **sftp** command is a part of the SSH solution and enables users to use an FTP command-line syntax to transfer files using sshd.

**scp**
Use **scp** to copy files and subdirectories to and from remote hosts.
- scp /etc/hosts server2:/tmp - copy, for instance, the /etc/hosts file to the /tmp directory on server2, using current account
- scp root@server2:/etc/passwd ~ - connect to server2 as user root to copy the /etc/passwd file to your home directory
- scp -r server2:/etc/ /tmp - copy an entire subdirectory structure using -r option.
- scp -i ... - to use Key-Based Authentication method
- **-P** option followed by the port number you want to connect to nondefault port

**rsync**
The **rsync** command uses SSH to synchronize files between a remote directory and a local directory. The advantage of synchronizing files is that only differences need to be considered. So, for example, if you synchronize a 100-MiB file in which only a few blocks have changed since the previous sync, only the changed blocks will be synchronized.

![[Pasted image 20241023181036.png]]

