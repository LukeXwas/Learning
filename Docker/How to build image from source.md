All of the following steps:

- Clone an app from a GitHub repo
- Inspect the app’s _Dockerfile_
- _Containerize_ the app
- Run the app as a container

1. Clone an app from a GitHub repo

![[Pasted image 20241202204542.png]]

2. Inspect the app’s _Dockerfile_

The _Dockerfile_ is a plain-text document that tells Docker how to build the app and dependencies into an image.

List the contents of the application’s Dockerfile.
![[Pasted image 20241202204646.png]]

Each line represents an instruction Docker executes to build the app into an image

3. **Containerize the app**

Run the following **`docker build`** command to create a new image based on the instructions in the Dockerfile. It will create a new Docker image called **`test:latest`**

![[Pasted image 20241202204755.png]]


1. 
