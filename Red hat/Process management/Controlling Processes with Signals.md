Linux processes have a hierarchical relationship. Every process has a parent process, and as long as it lives, the parent process is responsible for the child processes it has created.

- if you kill a parent process, all of its child processes become children of the systemd process.

A system may have hundreds or thousands of processes running on it. **Sometimes it becomes necessary to alert a process of an event. This is done by sending a control signal to the process. Processes may use signals to alert each other as well.The receiving process halts its execution as soon as it gets the signal and takes an appropriate action as per the instructions enclosed in the signal. The instructions may include terminating the process gracefully, killing it abruptly, or forcing it to re-read its configuration.**

A list of available signals can be viewed with the _kill_ command using the -l option:

![[Pasted image 20241208161223.png]]
The most important signals:

- The signal SIGTERM (15) is used to ask a process to stop.
- The signal SIGKILL (9) is used to force a process to stop.
- The SIGHUP (1) signal is used to hang up a process. The effect is that the process will reread its configuration files, which makes this a useful signal to use after making modifications to a process configuration file.

![[Pasted image 20241208161758.png]]

To send a signal to a process, you use the **kill** command. The most common use is the need to stop a process, which you can do by using the **kill** command followed by the PID of the process. This sends the SIGTERM signal to the process, which normally causes the process to cease its activity and close all open files.

Sometimes the **kill** command does not work because the process you want to kill can ignore it. In that case, you can use **kill -9** to send the SIGKILL signal to the process.

Examples:

if the PID number of the main process associated with the Apache web server is 2059, the following command is functionally equivalent to the **systemctl reload httpd** command:

![[Pasted image 20241208162243.png]]


**pkill and killall**

- The **pkill** command is a bit easier to use because it takes the name rather than the PID of the process as an argument.
- You can use the **killall** command if multiple processes using the same name need to be killed simultaneously.

Example:

Sometimes, a number of processes are running under the same name. For example, the Apache web server starts several processes that run simultaneously. It’s at best inefficient to kill just one process; the following command would kill all currently running server processes, assuming no other issues:
![[Pasted image 20241208162613.png]]

![[Pasted image 20241208162938.png]]