- _Docker Engine_ is jargon for the server-side components of Docker that run and manage containers.
- When Docker was first released, the Docker Engine had two major components:
	- The Docker daemon (sometimes referred to as just “the daemon”)
	- LXC - did the hard work of interfacing with the Linux kernel and constructing the required namespaces and cgroups to build and start containers.
	- To improve the experience and help the project evolve more quickly, Docker replaced LXC with its own tool, _libcontainer_. The goal of libcontainer was to be a platform-agnostic tool that gave Docker access to the fundamental container building blocks in the host kernel.
- The Docker Engine is made from many specialized tools that work together to create and run containers — the API, image builder, high-level runtime, low-level runtime, shims, etc.

![[Pasted image 20241202211056.png]]

- This work of breaking apart the Docker daemon is an ongoing process, and all of the code for building images and executing containers has been removed and refactored into small, specialized tools.
- Notable examples include removing the high-level and low-level runtime functionality and re-implementing them in separate tools called containerd and runc, both of which are used by many different projects including Docker, Kubernetes, Firecracker, and Fargate.
- Docker has removed image management from the daemon and now uses containerd’s image management capabilities.

**The influence of the Open Container Initiative (OCI)**

Around the same time that Docker, Inc. was refactoring the Engine, the OCI was in the process of defining three container-related standards:
- Image Specification (image-spec)
- Runtime Specification (runtime-spec)
- Distribution Specification (distribution-spec) - governing how images are distributed via registries

All versions of Docker since 2016 have implemented the OCI specifications. For example, Docker uses _runc_, the reference implementation of the OCI runtime-spec, to create OCI-compliant containers (runtime-spec). It also uses BuildKit to build OCI-compliant images (image-spec), and Docker Hub is an OCI-compliant registry (registry-spec).

**runc**

Docker uses runc as its low-level runtime. This means you get OCI-compliant containers **and** the feature-rich Docker user experience. Runc operates at the _OCI layer_, and we often refer to it as a _low-level runtime._

Docker and Kubernetes both use runc as their default low-level runtime, and both pair it with the containerd high-level runtime:

- containerd operates as the high-level runtime _managing_ lifecycle events
- runc operates as the low-level runtime _executing_ lifecycle events by interfacing with the kernel to do the work of actually building containers and deleting them

**containerd**

We refer to containerd as a _high-level runtime_ as it _manages_ lifecycle events such as starting, stopping, and deleting containers. However, it needs a low-level runtime to perform the actual work. Most of the time, containerd is paired with runc as its low-level runtime.

The original plan was for containerd to be a small specialized tool for managing container lifecycle events. However, it has since grown to include the ability to manage images, networks, and volumes.

**How everything work by starting a new container example"

1. The most common way of starting containers is using the Docker CLI: "docker run -d --name ctr1 nginx" 
2. When you run commands like this, the Docker client converts them into API requests and sends them to the API exposed by the daemon.
3. The daemon can expose the API on a local socket or over the network. On Linux, the local socket is **/var/run/docker.sock** and on Windows it’s **\pipe\docker_engine**
4. The daemon receives the request, interprets it as a request to create a new container, and passes it to containerd. Remember that the daemon no longer contains any code to create containers.
5. The daemon communicates with containerd via a CRUD-style API over gRPC.
6. Despite its name, even containerd cannot create containers. It converts the required Docker image into an OCI bundle and tells runc to use this to create a new container. Runc interfaces with the OS kernel to pull together all the constructs necessary to create a container (namespaces, cgroups, etc.). The container is started as a child process of runc, and as soon as the container starts, runc exits.

![[Pasted image 20241202214836.png]]
Decoupling the container creation and management from the Docker daemon and implementing it in containerd and runc makes it possible to stop, restart, and even update the daemon without impacting running containers.

**shims**

Shims are a popular software engineering pattern, and the Docker Engine uses them in between containerd and the OCI layer, bringing the following benefits:

- Daemonless containers
- Improves efficiency
- Makes the OCI layer pluggable

On the efficiency front, containerd forks a shim and a runc process for every new container. However, each runc process exits as soon as the container starts running, leaving the shim process as the container’s parent process. The shim is lightweight and sits between containerd and the container. It reports on the container’s status and performs low-level tasks such as keeping the container’s STDIN and STDOUT streams open.

**How it’s implemented on Linux**

On a Linux system, Docker implements the components we’ve discussed as the following separate binaries:

- /usr/bin/docker - (the Docker daemon)
- /usr/bin/containerd`
- /usr/bin/containerd-shim-runc-v2`
- /usr/bin/runc

**Do we still need the daemon

Docker has stripped most of the functionality out of the daemon, leaving the daemon to focus on serving the API.