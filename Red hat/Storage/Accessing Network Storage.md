The classic network file system is the **Network File System (NFS)**. It is a protocol that was developed for UNIX by Sun in the early 1980s, and it has been available on Linux forever. Its purpose is to make it possible to mount remote file systems into the local file system hierarchy.

**Understanding NFS Security

You should use NFS together with a centralized authentication service. Commonly, a combination of the Lightweight Directory Access Protocol (LDAP) and Kerberos is used to provide this functionality.

**RHEL NFS Versions

On Red Hat Enterprise Linux, NFS 4 is the default version of NFS. If when making an NFS mount the NFS server offers a previous version of NFS, the client falls automatically back to that version. On Red Hat Enterprise Linux, NFS 4 is the default version of NFS. If when making an NFS mount the NFS server offers a previous version of NFS, the client falls automatically back to that version.

**Setting Up NFS

To do so, you need to go through a few tasks:

1. Create a local directory you want to share.
2. Edit the /etc/exports file to define the NFS share.
3. Start the NFS server.
4. Configure your firewall to allow incoming NFS traffic

Example - you need a second server to do this exercise:

1. Type **mkdir -p /nfsdata /users/user1 /users/user2** to create some local directories that are going to be shared.
2. Copy some random files to this directory, using **cp /etc/\[a-c]* /nfsdata**
3. Use **vim** to create the **/etc/exports** file and give it the following contents:

![[Pasted image 20241213212402.png]]

4.  Type **dnf install -y nfs-utils** to install the required packages.
5. Type **systemctl enable --now nfs-server** to start and enable the NFS server.
6. Type **firewall-cmd --add-service nfs --permanent** to add the nfs service. Also type **firewall-cmd --add-service rpc-bind --permanent** and **firewall-cmd --add-service mountd --permanent** to add the bind and mountd services.
7. To make the newly added services effective at this point, type **firewall-cmd --reload**.

**Mounting the NFS Share

To mount an NFS share, you first need to find the names of the shares. To discover which shares are available, you have multiple options:

- If NFSv4 is used on the server, you can use a root mount. That means that you just mount the root directory of the NFS server, and under the mount point you’ll only see the shares that you have access to.
- Use the **showmount -e nfsserver** command to find out which shares are available.

**Mounting an NFS Share

1. On server1, type **dnf install -y nfs-utils** to install the RPM package that contains the **showmount** utility.
2. Type **showmount -e server2.example.com** to see all exports available from server2.
3. On server1, type **mount server2.example.com:/ /mnt**. (Note the space between the slashes in the command.) This performs an NFSv4 pseudo root mount of all NFS shares.
4. Type **mount | grep server2** to verify the mount has succeeded.
5. Still on server1, type **ls /mnt**. This shows the subdirectories data and home, which correspond to the mounts offered by the NFS server.





