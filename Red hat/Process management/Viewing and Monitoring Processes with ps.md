A system may have hundreds or thousands of processes running concurrently depending on the purpose of the system. These processes may be viewed and monitored using various native tools such as **_ps_** (_process status_) and **_top_** (_table of processes_).

- _ps_ command offers plentiful switches that influence its output
- _top_ is used for real-time viewing and monitoring of processes and system resources

**Ps overview**

- Without any options or arguments, _ps_ lists processes specific to the terminal where this command is issued.
![[Pasted image 20241207210145.png]]
- If you are looking for a short summary of the active processes, use **ps aux**
![[Pasted image 20241207210549.png]]

- f you are looking for not only the name of the process but also the exact command that was used to start the process, use **ps -ef**
![[Pasted image 20241207210431.png]]

- **ps fax** shows hierarchical relationships between parent and child processes

- The _ps_ command with the -l option along with the -ef options can be used to list priority (PRI, column 7) and niceness (NI, column 8) for all processes:

![[Pasted image 20241208155314.png]]
**Listing Processes by User and Group Ownership**

A process can be listed by its ownership or owning group.

- For example, to list all processes owned by _user1_, specify the -U (or -u) option with the command and then the username:

![[Pasted image 20241208154147.png]]

- You can specify the -G (or -g) option instead and the name of an owning group to print processes associated with that group only:

![[Pasted image 20241208154241.png]]

- Another switch to look at with the _ps_ command is -C (command list). This option is used to list only those processes that match the specified command name. For example, run it to check how many _sshd_ processes are currently running on the system:

![[Pasted image 20241207210951.png]]

Column descriptions
![[Pasted image 20241207210603.png]]
- CMD- The command or program name
- The _ps_ output above pinpoints several daemon processes running in the background. These processes are not associated with any terminal, which is why there is a ? in the TTY column.

**Other options** - how to list a specific process

Linux also offers the **_pidof_** and **_pgrep_** commands to list only the PID of a specific process.

These commands have a few switches available to modify their behavior; however, their most elementary use is to pass a process name as an argument to view its PID. For instance, to list the PID of the _rsyslogd_ daemon, use either of the following:
![[Pasted image 20241208154041.png]]
Both commands produce an identical result if used without an option.

