- command to start a container from image -> **docker run**

![[Pasted image 20241202202544.png]]

**Docker run** tells Docker to start a new container. 

- The **`--name`** flag told Docker to call this container **test**.
- The **`-it`** flags told Docker to make the container interactive and to attach your shell to the container’s terminal. 
- After that, the command told Docker to base the container on the **`ubuntu:latest`** image. 
- --publish 8080:8080
- bash -> it told Docker to start a Bash shell as the container’s main app, but you can specify commands, which container will start from


Press **`Ctrl-PQ`** to exit the container without terminating it. This will land your shell back at your local terminal, and your shell prompt will revert.

- how to check running containers - **docker ps**

![[Pasted image 20241202202914.png]]

**`docker ps`** command with the **`-a`** flag to list all containers, even those in the stopped state

![[Pasted image 20241202204123.png]]

- how to stop a container -> **docker stop <container_name>**

![[Pasted image 20241202203949.png]]

- how to kill the container -> **docker rm <container_name>**

![[Pasted image 20241202204053.png]]