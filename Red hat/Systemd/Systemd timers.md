
**Using Systemd Timers**

Since its initial appearance in RHEL 7, systemd has been replacing many services. Since the release of RHEL 9 it is also responsible for scheduling tasks.

- It is now the primary mechanism to do so, which means that if ever you are trying to find out how future tasks are executed, you should consider systemd timers first.
- **A systemd timer is always used together with a service file, and the names should match.** For example, the logrotate.timer file is used to modify the logrotate.service file. The service unit defines _how_ the service should be started, and the timer defines _when_ it will be started.
- If you need a service to be started by a timer, you enable the timer, not the service

To check all options in timer config file use - **man systemd.time**

logrotate.timer file

![[Pasted image 20241208165505.png]]

To define how the timer should be started, the timer unit contains a \[Timer\] section. In the code in Example 12-1, you can see that it lists three options:

- **OnCalendar:** Describes when the timer should execute. In this case it is set to daily, which ensures daily execution.
- **AccuracySec:** Indicates a time window within which the timer should execute. It is set to 1 hour. If the timer needs to be executed at a more specific time, it is common to set it to a lower value. Use 1us for the best accuracy.
- **Persistent:** A modifier to OnCalendar=daily, it specifies that the last execution time should be stored on disk, so that the next time it executes is exactly one day later.

In systemd timers, different options can be used to indicate when the related service should be started.

![[Pasted image 20241208165945.png]]Using Systemd Timers

![[Pasted image 20241208170315.png]]