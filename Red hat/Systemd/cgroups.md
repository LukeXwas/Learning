systemd spawns several processes during a service startup. It places the processes in a private hierarchy composed of _control groups_ (or _cgroups_ for short) to organize processes for the purposes of monitoring and controlling system resources such as processor, memory, network bandwidth, and disk I/O. This includes limiting, isolating, and prioritizing their usage of resources. This way resources can be distributed among users, databases, and applications based on need and priority, resulting in overall improved system performance.

On modern Linux systems, cgroups are used to allocate system resources. In cgroups, three system areas, the so-called _slices_, are defined:

- **system:** This is where all systemd-managed processes are running.
- **user:** This is where all user processes (including root processes) are running.
- **machine:** This optional slice is used for virtual machines and containers.

By default, all slices have the same CPUWeight. That means that CPU capacity is equally divided if there is high demand. All processes in the system slice get as much CPU cycles as all processes in the user slice, and that can result in surprising behavior. Within a slice, process priority can be managed by using **nice** and **renice**.

You can increase the priority of the system slice. Use **systemctl set-property system.slice CPUWeight=800** to set the CPUWeight of all processes in the system slices eight times as high as all processes in the user slice.

To address this limitation, systemd labels processes associated with a service using cgroups. In this way, systemd uses cgroups to kill all processes in a group, if required.

The command **systemd-cgls** displays the cgroup hierarchy in a tree format