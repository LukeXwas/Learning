The most common are _service units_, which have a **.service** extension and activate a system service. It is used to start processes. You can start any type of process by using a service unit, including daemon processes and commands.

Service Unit File

![[Pasted image 20241211173535.png]]

Systemd _service_ unit files typically consist of the following three sections:

- **\[Unit]** Describes the unit and defines dependencies. This section also contains the important **After** statement and optionally the **Before** statement. These statements define dependencies between different units, and they relate to the perspective of this unit. The **Before** statement indicates that this unit should be started before the unit that is specified. The **After** statement indicates that this unit should be started after the unit that is specified.
- **\[Service]** Describes how to start and stop the service and request status installation. Normally, you can expect an ExecStart line, which indicates how to start the unit, or an ExecStop line, which indicates how to stop the unit. Note the **Type** option, which is used to specify how the process should start. The **forking** type is commonly used by daemon processes, but you can also use other types, such as **oneshot** and **simple**, which will start any command from a Systemd unit.
- **\[Install]** Indicates in which target this unit has to be started. This section is optional, but units that don’t have an **\[Install]** section cannot be started automatically.
- Finally, the **WantedBy directive tells us that this service will be activated at boot when the system enters into the multi-user target.**

See **man 5 systemd.service** for more details.