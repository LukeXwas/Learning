**Controlling User Access**

By default, all users are allowed to schedule jobs using the at and cron services. However, this access may be controlled and restricted to specific users only. This can be done by listing users in the allow or deny file located in the _/etc_ directory for either service. 

**These files are named /etc/cron.allow and /etc/cron.deny for cron service.**

These files are named /etc/_at.allow_ and /etc/_at.deny_ for the at service.

- You only need to list usernames that are to be allowed or denied access to these scheduling tools. 
- Each file takes one username per line. 
- The _root_ user is always permitted; it is affected neither by the existence or non-existence of these files nor by the inclusion or exclusion of its entry in these files.

![[Pasted image 20241208191320.png]]


Examples

if you include the following entries in /etc/cron.deny, and the /etc/cron.allow file does not exist, users elizabeth and nancy aren’t allowed to set up their own cron scripts:

![[Pasted image 20241208190536.png]]

