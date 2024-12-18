Linux is a multitasking operating system. It runs numerous processes on a single processor core by giving each process a slice of time. The process scheduler on the system performs rapid switching of processes, giving the notion of concurrent execution of multiple processes.

- A process is spawned at a certain priority, which is established at initiation based on a numeric value called _niceness_ (a.k.a. a _nice_ value).
- A process running at a higher priority gets more CPU attention. A child process inherits the niceness of its calling process in its priority calculation.
- There are 40 niceness values, **with -20 being the highest or the most favorable to the process, and +19 being the lowest or the least favorable to the process.** By applying a negative niceness, you increase the priority. Use a positive niceness to decrease the priority.
- The default niceness of a process is set to 0.
- Regular users can only decrease the priority of a running process. You must be root to give processes increased priority by using negative **nice** values.

**_nice_** -  command to launch a program at a non-default priority
**_renice_** - command to alter the priority of a running program.

- Changing process priority may make sense in two different scenarios. Suppose, for example, that you are about to start a backup job that does not necessarily have to finish fast. Typically, backup jobs are rather resource intensive, so you might want to start the backup job in a way that does not annoy other users too much, by lowering its priority.
- Another example is where you are about to start a very important calculation job. To ensure that it is handled as fast as possible, you might want to give it an increased priority, taking away CPU time from other processes.
- Do not set process priority to –20; it risks blocking other processes from getting served.

**Start Processes at Non-Default Priorities**

1. Check the priority and niceness for the command

![[Pasted image 20241208155717.png]]
2. Launch command at a lower priority with a nice value of +2:
![[Pasted image 20241208155934.png]]
3. Launch command at a higher priority with a nice value of -10. Use _sudo_ for _root_ privileges.
![[Pasted image 20241208160046.png]]
4. Increase command priority by renicing it to -5 in Terminal 2. Use the command substitution to get the PID of _top_. Prepend the _renice_ command by _sudo_.

![[Pasted image 20241208160211.png]]
