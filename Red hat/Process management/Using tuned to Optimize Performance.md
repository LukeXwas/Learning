To offer the best possible performance right from the start, RHEL 9 comes with tuned. It offers a daemon that monitors system activity and provides some profiles. In the profiles, an administrator can automatically tune a system for best possible latency, throughput, or power consumption.

RHEL 9 comes with **tuned**, a daemon that simplifies the daunting and complex process to optimize a system for best performance.

1. The tuned service should be installed and enabled by default on every RHEL 9 system. If the package is not present, run **dnf -y install tuned**
2. You can enable and start the service with the following commands:
![[Pasted image 20241208163517.png]]

- The configuration of **tuned** is based on predefined profiles.
- Based on the properties of an installed system, a tuned profile is selected automatically at installation, and after installation it’s possible to manually change the current profile. 
- Administrators can also change settings in a tuned profile. 

**tuned-adm list** shows a list of all available profiles. This is overview of the most important default profiles:

![[Pasted image 20241208163144.png]]

use **tuned-adm** active to find out which profile currently is selected.

![[Pasted image 20241208164138.png]]

Switching to a different profile is achieved by the **tuned-adm profile** command.

![[Pasted image 20241208164219.png]]

The **tuned** service can also recommend a **tuned** profile for your system: use **tuned-adm recommend**

