To work with servers that are not physically accessible, Secure Shell (SSH) is normally used. On modern Linux distributions, Secure Shell is the common method to gain access to other machines over the network. In SSH, cryptography is used to ensure that you are connecting to the intended server. Also, traffic is encrypted while being transmitted.

- To access a server using SSH, you need the sshd server process, as well as an SSH client.
- On the remote server that you want to access, the sshd service must be running and offering services, (22 port needs to be open)
- Red Hat Enterprise Linux starts the sshd process automatically, and by default

Configuration file:
- user-specific agent config file -> .ssh/config
- global specific agent config file -> /etc/ssh/ssh_config

more info -> man ssh_config

SSH command:
- type **ssh** followed by the name or IP address of the other Linux machine, when remotely connecting to a Linux server, the SSH client tries to do that as the user account you are currently logged in with on the local machine. After connecting, you will be prompted for a password if a default configuration is used.
- type **ssh username@remoteserver** - to connect using a different user account
- The **ssh** command by default tries to reach the sshd process on the server port 22. If you have configured the sshd process to offer its services on a different port, use **ssh -p** followed by the port number you want to connect to.
- If you have a Windows version that does not have the Windows subsystem for Linux, you need to use PuTTY.

On some occasions, using **ssh** to get access to a server will be slow. If you want to know why, use the **-v** (more verbosity use **-vvv**) option with the **ssh** command.

![[Pasted image 20241023170817.png]]

The security message is displayed because the remote server has never been contacted before and therefore there is no way to verify the identity of the remote server. After you connect to the remote server, a public key fingerprint is stored in the file ~/.ssh/known_hosts. The next time you connect to the same server, this fingerprint is checked with the encryption key that was sent over by the remote server to initialize contact. If the fingerprint matches, you will not see this message anymore.

In some cases, the remote host key fingerprint does not match the key fingerprint that is stored locally. That is a potentially dangerous situation. Instead of being connected to the intended server, you might be connected to the server of an evildoer. It does, however, also happen if you are connecting to an IP address that you have been connected to before but that is now in use by a different server, or if the sshd service has been deleted and reinstalled. If you encounter such a mismatch between the host key that is presented and the one that you’ve cached, you just have to remove the key fingerprint from the ~/.ssh/known_hosts file on the client computer.

**Graphical Applications in an SSH Environment**
From an SSH session, by default you cannot start graphical applications. There are two requirements for starting graphical applications through an SSH connection:
- An X server must be running on the client computer. The X server is the software component that creates the graphical screens.
- The remote host must be allowed to display screens on the local computer. To allow the remote host to display graphical screens on your computer is by adding the **-Y** option to the **ssh** command.

As an administrator, you can also create a systemwide configuration that allows you to use _X forwarding_. As root, open the configuration file /etc/ssh/ssh_config and make sure it includes the line "ForwardX11 yes".

**Configuring Key-Based Authentication for SSH**
SSH is more secure when using public/private keys for authentication. The only thing you need to do to enable key-based login is to create a key pair. 

When using public/private key-based authentication, the user who wants to connect to a server generates a public/private key pair. 
- The private key needs to be kept private and will never be distributed. 
- The public key is stored in the home directory of the target user on the SSH server in the file **.ssh/authorized_keys**.

The permissions for private keys are set to 600 (rw-------) and for public keys are set to 644 (rw-r--r--). In addition, the permissions of the ~/.ssh directory should be 700 (rwx------).

When authenticating using key pairs, the user generates a hash derived from the private key. This hash is sent to the server, and if on the server it proves to match the public key that is stored on the server, the user is authenticated.

When creating a public/private key pair, you are prompted for a passphrase. If you want maximal security, you should enter a passphrase. You are prompted for that passphrase each time that you are using the private key to authenticate to a remote host. press the Enter key twice when generating the public/private key pair to confirm that you do not want to set a passphrase. This is a typical configuration that is used for authentication between servers in a trusted environment where no outside access is possible anyway.

To add the private key to my session keyring (active terminal), use two commands:
- exec /usr/bin/ssh-agent $SHELL
- ssh-add

You cannot pass passphrase only in terminal, where you type this commands. once you close the client machine’s terminal window that you used for logging in, the private key will be removed from your session keyring.

**Log with key**
- ssh -i ~/.ssh/id_ed25519 donnie@192.168.0.17 - log to remote server authenticate with id_ed25519 algorithm. Without the **-i** option defaults to transmitting the most recently created public key.

How to create key pair:
- To create a key pair, use the **ssh-keygen** command. If you want to specify algorithm use -t option (-t ed25519)
- When asked for the filename in which to store the (private) key, accept the default filename ~/.ssh/id_rsa.
- When asked to enter a passphrase, press Enter twice.
- The private key now is written to the ~/.ssh/id_rsa file and the public key is written to the ~/.ssh/id_rsa.pub file.

How to copy public keys to remote server:
- **ssh-copy-id server2** to copy to server2 the public key you have just created. You are then asked for the password on the remote server one last time.
- type **ssh server2**. You should now authenticate without having to enter the password for the remote user account.

After you copy the public key to the remote host, it will be written to the ~/.ssh/authorized_keys file on that host. Notice that if multiple users are using keys to log in with that specific account, the authorized_keys file may contain a lot of public keys. Make sure never to overwrite it because that will wipe all keys that are used by other users as well!