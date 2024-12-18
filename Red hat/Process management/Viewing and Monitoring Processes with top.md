The other popular tool for viewing process information is the _top_ command. This command displays statistics in real time and continuously, and may be helpful in identifying possible performance issues on the system.

- Press q or Ctrl+c to quit
- Press “o” to re-sequence the process list 
- Press “f” to add or remove fields
- Press “F” to select the field to sort on
- Press “h” to obtain help
- Press  "**r**" command from the **top** utility to change the priority of a currently running process.
- type **k**; **top** then prompts for the PID of the process you want to send a signal to. By default, the most active process is selected. After you enter the PID, **top** asks which signal you want to send. By default, signal 15 for SIGTERM is used. However, if you want to insist on a bit more, you can type **9** for SIGKILL. Now press Enter to terminate the process.

**Top output explanation**

![[Pasted image 20241207211048.png]]

The _top_ output may be divided into two major portions: the summary portion and the tasks portion. The summary area spreads over the first five lines of the output, and it shows the information as follows:

- **Line 1**: Indicates the system uptime, number of users logged in, and system load averages over the period of 1, 5, and 15 minutes. See the description for the _uptime_ command output in
- **Line 2**: Displays the task (or process) information, which includes the total number of tasks running on the system and how many of them are in running, sleeping, stopped, and zombie states.
- **Line 3**: Shows the processor usage that includes the CPU time in percentage spent in running user and system processes, in idling and waiting, and so on.
- **Line 4**: Depicts memory utilization that includes the total amount of memory allocated to the system, and how much of it is free, in use, and allocated for use in buffering and caching.
- **Line 5**: Exhibits swap (virtual memory) usage that includes the total amount of swap allocated to the system, and how much of it is free and in use. The “avail Mem” shows an estimate of the amount of memory available for starting new processes without using the swap.

The second major portion in the _top_ command output showcases the details for each process in 12 columns as described below:
- **Columns 1 and 2**: Pinpoint the process identifier (PID) and owner (USER)
- **Columns 3 and 4**: Display the process priority (PR) and nice value (NI)
- **Columns 5 and 6**: Depict amounts of virtual memory (VIRT) and non-swapped resident memory (RES) in use
- **Column 7**: Shows the amount of shareable memory available to the process (SHR)
- **Column 8**: Represents the process status (S)
- **Columns 9 and 10**: Express the CPU (%CPU) and memory (%MEM) utilization
- **Column 11**: Exhibits the CPU time in hundredths of a second (TIME+)
- **Column 12**: Identifies the process name (COMMAND)

