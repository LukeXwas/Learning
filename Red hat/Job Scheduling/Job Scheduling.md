_Job scheduling_ allows a user to submit a command for execution at a specified time in the future. The execution of the command could be one time or periodic based on a pre-determined time schedule. A one-time execution may be scheduled for an activity that needs to be performed at a time of low system usage.

RHEL 9 offers different solutions for scheduling tasks:

- Systemd timers are now the default solution to ensure that specific tasks are started at specific moments.
- **cron** is the legacy scheduler service. It is still supported and responsible for scheduling a few services.
- **at** is used to schedule an occasional user job for future execution.

**Controlling User Access**

By default, all users are allowed to schedule jobs using the at and cron services. However, this access may be controlled and restricted to specific users only. This can be done by listing users in the allow or deny file located in the _/etc_ directory for either service. 

- You only need to list usernames that are to be allowed or denied access to these scheduling tools. 
- Each file takes one username per line. 
- The _root_ user is always permitted; it is affected neither by the existence or non-existence of these files nor by the inclusion or exclusion of its entry in these files.


