Just like any other software that comes in the **rpm format** for RHEL, the software comprising the kernel is no different. There is a set of core kernel packages that must be installed on the system at a minimum to make it work. Additional packages providing supplementary kernel support are also available.

| **Kernel Package**   | **Description**                                                                                 |
| -------------------- | ----------------------------------------------------------------------------------------------- |
| kernel               | Contains no files, but ensures other kernel packages are accurately installed                   |
| kernel-core          | Includes a minimal number of modules to provide core functionality                              |
| kernel-devel         | Includes support for building kernel modules                                                    |
| kernel-headers       | Includes files to support the interface between the kernel and userspace libraries and programs |
| kernel-modules       | Contains modules for common hardware devices                                                    |
| kernel-modules-extra | Contains modules for not-so-common hardware devices                                             |
| kernel-tools         | Includes tools to manipulate the kernel                                                         |
| kernel-tools-libs    | Includes the libraries to support the kernel tools                                              |

Moreover, packages containing the source code for RHEL 9 are also available for those who wish to customize and recompile the code for their precise needs.

![[Pasted image 20241213200313.png]]

The output returns six kernel packages that were loaded during the OS installation.