If a project has already been set up in a central repository, the **git clone** command is the most common way for users to obtain a development copy. 

**Git makes no distinction between the working copy and the central repository—they're all full-fledged Git repositories.

![[Pasted image 20241216120649.png]]

**Git clone is primarily used to point to an existing repo and make a clone or copy of that repo at in a new directory, at another location. The original repository can be located on the local filesystem or on remote machine accessible supported protocols. The `git clone` command copies an existing Git repository.

**As a convenience, cloning automatically creates a remote connection called "origin" pointing back to the original repository. 
- This makes it very easy to interact with a central repository. 
- This automatic connection is established by creating Git refs to the remote branch heads under **refs/remotes/origin** and by initializing `remote.origin.url` and `remote.origin.fetch` configuration variables.

**Cloning to a specific folder

![[Pasted image 20241216120937.png]]

Clone the repository located at ＜repo＞ into the folder called ~＜directory＞! on the local machine.

**Cloning a specific branch

![[Pasted image 20241216121206.png]] 

**Cloning a specific tag

![[Pasted image 20241216121044.png]]

Clone the repository located at `＜repo＞` and only clone the ref for `＜tag＞`.

**Shallow clone

![[Pasted image 20241216121252.png]]

Clone the repository located at `＜repo＞` and only clone the  history of commits specified by the option depth=1. In this example a clone of `＜repo＞` is made and only the most recent commit is included in the new cloned Repo. Shallow cloning is most useful when working with repos that have an extensive commit history.

**git clone --bare

Similar to `git init --bare,` when the `-bare` argument is passed to `git clone,` a copy of the remote repository will be made with an omitted working directory. This means that a repository will be set up with the history of the project that can be pushed and pulled from, but cannot be edited directly. In addition, no remote branches for the repo will be configured with the `-bare` repository. Like `git init --bare,` this is used to create a hosted repository that developers will not edit directly.

**Git URL protocols

**SSH

Secure Shell (SSH) is a ubiquitous authenticated network protocol that is commonly configured by default on most servers. Because SSH is an authenticated protocol, you'll need to establish credentials with the hosting server before connecting. `ssh://[user@]host.xz[:port]/path/to/repo.git/`  

**GIT

A protocol unique to git. Git comes with a daemon that runs on port (9418). The protocol is similar to SSH however it has NO AUTHENTICATION. `git://host.xz[:port]/path/to/repo.git/`  
 
**HTTP

Hyper text transfer protocol. The protocol of the web, most commonly used for transferring web page HTML data over the Internet. Git can be configured to communicate over HTTP `http[s]://host.xz[:port]/path/to/repo.git/`
