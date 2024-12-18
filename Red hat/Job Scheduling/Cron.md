The **crond** service is started by default on every RHEL system. Managing the **crond** service itself is easy: it does not need much management. 

- Where other services need to be reloaded or restarted to activate changes to their configuration, this is not needed by **crond**. The **crond** daemon wakes up every minute and checks its configuration to see whether anything needs to be started. So, if you want to make sure your job is executed as fast as possible, allow for a safe margin of three minutes between the moment you save the cron configuration and the execution time.
- To monitor the current status of the **crond** service, you can use the **systemctl status crond** command

**Managing cron Configuration Files**

The main configuration file for cron is /etc/crontab, but you will not change this file directly. It does give you a convenient overview, though, of some time specifications that can be used in cron. It also sets environment variables that are used by the commands that are executed through cron.

![[Pasted image 20241208193439.png]]
 - The /etc/crontab file is set up in a specific format. Each line can be blank, a comment (which begins with #), a variable, or a configuration line. Naturally, blank lines and comments are ignored
 - In RHEL 9, the default crontab file just includes the format for other related configuration files.
 - Variables can be set in the /etc/crontab and other cron files (in /etc/cron.d, /etc/cron.daily, and so on).
 ![[Pasted image 20241208194605.png]]
 
 **Understanding cron Timing**

When scheduling services through cron, you need to specify when exactly the services need to be started.

The _/etc/crontab_ file specifies the syntax that each user cron job must comply with in order for _crond_ to interpret and execute it successfully. Based on this structure, each line in a user crontable with an entry for a scheduled job is comprised of six fields.

**Fields 1 to 5 are for the schedule, field 6 may contain the login name of the executing user, and the rest for the command or program to be executed.**

![[Pasted image 20241208195212.png]]

![[Pasted image 20241208195729.png]]

![[Pasted image 20241208195310.png]]

**In any of these fields, you can use an * as a wildcard to refer to any value.**

Examples:

![[Pasted image 20241208195708.png]]

**How to use cron**

To make modifications to the cron jobs, there are other locations where cron jobs should be specified. Instead of modifying /etc/crontab, different cron configuration files are used:

- cron files in /etc/cron.d
- Scripts in /etc/cron.hourly, cron.daily, cron.weekly, and cron.monthly
- User-specific files that are created with **crontab -e**

**Crontab**

Each user can use the **crontab** command to create and manage cron jobs for their own accounts. Four switches are associated with the **crontab** command:

![Images](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781260462081/files/square.jpg)   **-u _user_** Allows the root user to edit the crontab of another specific user.
![Images](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781260462081/files/square.jpg)   **-l** Lists the current entries in the crontab file.
![Images](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781260462081/files/square.jpg)   **-r** Removes cron entries.
![Images](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781260462081/files/square.jpg)   **-e** Edits an existing **crontab** entry.

1. To start, cron jobs can be started for specific users. 
2. To create a user-specific cron job, type **crontab -e** after logging in as that user, or as root type **crontab -e -u username**. 
3. These user-specific cron jobs are the most common way for scheduling additional jobs through cron. By default, **crontab** uses vi, unless a different editor is specified via the **EDITOR** environment variable.
4. Create cron job

![[Pasted image 20241208200756.png]]

5. After you edit the cron configuration, the temporary file is moved to its final location in the directory /var/spool/cron. Save and exit. When the file is saved by **crontab -e**, it is activated automatically.
6. Run **crontab -l** and confirm the existence of the user cron file in the /var/spool/cron directory. That file should have the same name as the user.

**Cron files in /etc/cron.d**

Example cron Jobs in /etc/cron.d.
![[Pasted image 20241208201042.png]]

You need to create file with .cron.

This example starts by setting environment variables. These are the environment variables that should be considered while running this specific job. On the last line the job itself is defined. The first part of this definition specifies when the job should run. In this case it will run 1 minute after each hour, each day of the month, each month, and each day of the week. The job will be executed as the root user, and the job itself involves the **run-parts** command, which is responsible for running the scripted cron jobs in /etc/cron.hourly.

After file creations you do not need use chmod and 

**The last way to schedule cron jobs is through the following directories:**

- /etc/cron.hourly
- /etc/cron.daily
- /etc/cron.weekly
- /etc/cron.monthly

In these directories, you typically find scripts (not files that meet the crontab syntax requirements). When opening these scripts, notice that no information is included about the time when the command should be executed. The reason is that the exact time of execution does not really matter. The only thing that does matter is that the job is launched once an hour, once a day, a week, or a month.

In every of this locations there is 0anacorn scripts

Consult the manual pages of the _crontab_ configuration file (**man 5 crontab**) for more details on the syntax.