Managing Systemd units starts with starting and stopping units.

The primary tool for interaction in this command suite is _systemctl_. The _systemctl_ command performs administrative functions and supports plentiful subcommands and flags.

- **systemctl** - To list all units that are currently loaded in memory along with their status and description
	- You can use the --all option to include the inactive units too.

![[Pasted image 20241212002324.png]]

- UNIT column shows the name of the unit and its location in the tree
- LOAD column reflects whether the unit configuration file was properly loaded (other possibilities are not found, bad setting, error, and masked),
- ACTIVE column returns the high-level activation state (other possible states are active, reloading, inactive, failed, activating, and deactivating)
- SUB column depicts the low-level unit activation state (reports unit-specific information)
- DESCRIPTION column illustrates the unit’s content and functionality.

- **systemctl -t help** - to display a list of available units
- systemctl –t \<type of unit> - To list all units of type socket (or other type) currently loaded in memory
	- To list all (--all) active and inactive units of type (-t) socket (or other type)
- systemctl --failed -t \<type of unit> - wyswietlenie serwisow ktore sfailowaly
	- systemctl --failed -t service

- **systemctl list-unit-files** - command shows whether a unit is enabled or disabled at startup

![[Pasted image 20241212111617.png]]

- **systemctl cat _unitname_** - command to display the content of a system unit file

| **Subcommand**              | **Description**                                                                                                   |
| --------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| daemon-reload               | Re-reads and reloads all unit configuration files and recreates the entire user dependency tree.                  |
| enable (disable)            | Activates (deactivates) a unit for autostart at system boot                                                       |
| get-default (set-default)   | Shows (sets) the default boot target                                                                              |
| get-property (set-property) | Returns (sets) the value of a property                                                                            |
| is-active                   | Checks whether a unit is running                                                                                  |
| is-enabled                  | Displays whether a unit is set to autostart at system boot                                                        |
| is-failed                   | Checks whether a unit is in the failed state                                                                      |
| isolate                     | Changes the running state of a system                                                                             |
| kill                        | Terminates all processes for a unit                                                                               |
| list-dependencies           | Lists dependency tree for a unit                                                                                  |
| list-sockets                | Lists units of type socket                                                                                        |
| list-unit-files             | Lists installed unit files                                                                                        |
| list-units                  | Lists known units. This is the default behavior when systemctl is executed without any arguments.                 |
| mask (unmask)               | Prohibits (permits) auto and manual activation of a unit to avoid potential conflict                              |
| reload                      | Forces a running unit to re-read its configuration file. This action does not change the PID of the running unit. |
| restart                     | Stops a running unit and restarts it                                                                              |
| show                        | Shows unit properties                                                                                             |
| start (stop)                | Starts (stops) a unit                                                                                             |
| status                      | Presents the unit status information                                                                              |
