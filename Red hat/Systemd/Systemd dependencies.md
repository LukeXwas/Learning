Units can have dependency relationships among themselves based on a sequence (ordering) or a requirement. A sequence outlines one or more actions that need to be taken before or after the activation of a unit (the Before and After directives). A requirement specifies what must already be running (the Requires directive) or not running (the Conflicts directive) in order for the successful launch of a unit.

In general, there are two ways to manage Systemd dependencies:

- Unit types such as socket, timer, and path are directly related to a service unit. **Systemd can make the connection because the first part of the name is the same: cockpit.socket works with cockpit.service. Accessing either of these unit types will automatically trigger the service type.**
- Dependencies can be defined within the unit, using keywords like **Requires**, **Requisite**, **After**, and **Before**.

![[Pasted image 20241212111859.png]]

To ensure accurate dependency management, you can use different keywords in the \[Unit] section of a unit:

- **Requires:** If this unit loads, units listed here will load also. If one of the other units is deactivated, this unit will also be deactivated.
- **Requisite:** If the unit listed here is not already loaded, this unit will fail.
- **Wants:** This unit wants to load the units that are listed here, but the unit is not forced to fail activation if a required unit fails to start.
- **Before:** This unit will start before the unit specified with **Before**.
- **After:** This unit will start after the unit specified with **After**.

For instance, the _graphical.target_ unit file tells us that the system must already be operating in the multi-user mode and not in rescue mode in order for it to boot successfully into the graphical mode. 

This means that a target can include another target. In this case, graphical.target is a superset of multi-user.target. After all systemd units in multi-user.target have started, graphical.target activates display-manager.service, as indicated by the Wants directive in the graphical.target configuration file.

Systemd can activate services in parallel by keeping track of all dependencies between units. The **systemctl list-dependencies** command displays a tree with all dependencies between units.

You can show the dependencies for any available unit. Dependent units must be started first. For example, the following command shows the units that must be started before the **rsyslog** service:

![[Pasted image 20241212010801.png]]

![[Pasted image 20241212112318.png]]