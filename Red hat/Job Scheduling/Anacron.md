To ensure regular execution of the job, cron uses the anacron service. This service takes care of starting the hourly, daily, weekly, and monthly cron jobs, no matter at which exact time. To determine how this should be done, anacron uses the **/etc/anacrontab** file.

- You should reviews the contents of the /var/spool/anacron/cron.daily file to see if the **anacron** command has been run in the current day.
- If not, and if the system is not running on battery (for example, on a laptop disconnected from main power), the **/usr/sbin/anacron -s** command is executed, which runs scripts defined in the /etc/anacrontab configuration file.

![[Pasted image 20241208202913.png]]

The 0anacron script in the /etc/cron.hourly ( and other cron directories ) directory described earlier executes the **anacron** command after a system has been powered up. That command executes three scripts defined in the /etc/anacrontab file. This includes three environment variables that should seem familiar:

![[Pasted image 20241208203149.png]]
The following directive means that scripts are run at a random time of up to 45 minutes after the scheduled time:

![[Pasted image 20241208203213.png]]
With the following directive, anacron jobs are run only between the hours of 3 A.M. and 10:59 P.M.

While the format of /etc/anacrontab is similar to the format listed in a script for a regular cron job, there are differences. The order of data in each line is specified by the following comment:

![[Pasted image 20241208203240.png]]

The period in days is 1, 7, or @monthly, because the number of days in a month varies. The delay in minutes is associated with the **RANDOM_DELAY** directive. Since the /etc/anacrontab file is executed through the /etc/cron.d/0hourly script, the clock starts one minute after the hour, after the system has been started. The delay in minutes comes before the **RANDOM_DELAY** directive.

In other words, based on the following line, the scripts in the /etc/cron.daily directory may be run anywhere from 5 to 50 minutes after the **anacron** command is run, or 6 to 51 minutes after the hour:

![Images](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781260462081/files/f0373-02.jpg)