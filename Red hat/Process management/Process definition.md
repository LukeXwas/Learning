A _process_ is a unit for provisioning system resources. It is any program, application, or command that runs on the system. it can use multiple threads. A thread is a task started by a process and that a dedicated CPU can service. The Linux shell does not offer tools to manage individual threads.

Every process has a unique numeric identifier, and it is managed by the kernel through its entire lifespan. **_Process IDentifier_ (PID),**

A major distinction can be made between three process types:
- _Shell jobs_ are commands started from the command line. They are associated with the shell that was current when the process was started. Shell jobs are also referred to as _interactive processes_.
- _Daemons_ are processes that provide services. They normally are started when a computer is booted and often (but certainly not in all cases) run with root privileges. **These background system processes are called _daemons_ and are critical to system operation.**
- _Kernel threads_ are a part of the Linux kernel. You cannot manage them using common tools, but for monitoring of performance on a system, it’s important to keep an eye on them. **When managing processes, you can easily recognize the kernel processes because they have a name that is between square brackets.**

**Processes and Priorities**

- Processes are organized in a hierarchical fashion.
- Each process has a _parent process_ (a.k.a. a _calling process_) that spawns it. A single parent process may have one or many _child processes_ and passes many of its attributes to them at the time of their creation.
- When a process completes its lifespan or is terminated, this event is reported back to its parent process, and all the resources provisioned to it (cpu cycles, memory, etc.) are then freed and the PID is removed from the system.

**Process States**

A process changes its operating state multiple times during its lifecycle. Many factors, such as load on the processor, availability of free memory, priority of the process, and response from other applications, affect how often a process jumps from one operating state to another.

**There are five basic process states: _running_, _sleeping_, _waiting_, _stopped_, and _zombie_. Each process is in one state at any given time.**

![[Pasted image 20241207205703.png]]

- **Running:** The process is being executed by the system CPU.
- **Sleeping:** The process is waiting for input from a user or another process.
- **Waiting:** The process has received the input it was waiting for and is now ready to run as soon as its turn comes.
- **Stopped:** The process is currently halted and will not run even when its turn comes unless a signal is sent to change its behavior.
- **Zombie:** The process has been stopped but could not be removed by its parent, which has put it in an unmanageable state.
