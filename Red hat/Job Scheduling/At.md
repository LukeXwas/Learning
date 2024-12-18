**The _at_ command is used to schedule a one-time execution of a program in the future.** All submitted jobs are spooled in the _/var/spool/at_ directory and executed by the _atd_ daemon at the specified time. Each submitted job will have a file created containing the settings for establishing the user’s shell environment to ensure a successful execution. This file also includes the name of the command or program to be run. There is no need to restart the daemon after a job submission.

1. To run a job through the atd service, you would use the **at** command, followed by the time the job needs to be executed.
2. This can be a specific time, as in at 14:00, but it can also be a time indication like at teatime or at noon. 
3. After you type this, the at shell opens. From this shell, you can type several commands that will be executed at the specific time that is mentioned.
4. After entering the commands, press Ctrl-D to quit the at shell.

![[Pasted image 20241208191832.png]]
You may supply a filename with the _at_ command using the -f option. The command will execute that file at the specified time. For instance, the following will run _/home/user1/.bash_profile_ file for _user1_ 2 hours from now:

![](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781835887325/files/html/images/210_1.jpg)

- After scheduling jobs with at, you can use the **atq** command (_q_ for _queue_) or **at -l** to get an overview of all jobs currently scheduled.
- It is also possible to remove current at jobs. To do this, use the **atrm** command, optionally followed by the number of the at job that you want to remove