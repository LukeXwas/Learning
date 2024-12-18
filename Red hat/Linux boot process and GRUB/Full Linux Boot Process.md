RHEL goes through a _boot_ process after the system has been powered up or restarted. The boot process lasts until all enabled services are started. A login prompt will appear on the screen, which allows users to log in to the system. The boot process is automatic, but you may need to interact with it to take a non-default action, such as booting an alternative kernel, booting into a non-default operational state, repairing the system, recovering from an unbootable state, and so on.

The boot process on an x86 computer may be split into four major phases: 
- (1) the firmware phase
- (2) the bootloader phase
- (3) the kernel phase
- (4) the initialization phase.

**The Firmware Phase (BIOS and UEFI)**

- The _firmware_ is the BIOS (_Basic Input/Output System_) or the UEFI (_Unified Extensible Firmware Interface_) code that is stored in flash memory on the x86-based system board.
- The BIOS is a small memory chip in the computer that stores system date and time, list and sequence of boot devices, I/O configuration, etc. This configuration is customizable. Depending on the computer hardware, you need to press a key to enter the BIOS setup or display a menu to choose a source to boot the system.
	- The computer goes through the hardware initialization phase that involves detecting and diagnosing peripheral devices.
	- It runs the _Power-On-Self-Test_ (POST) to detect, test, and initialize the system hardware components. 
	- As it finds them, installs drivers for the graphics card and the attached monitor, and begins exhibiting system messages on the video hardware.
	- It discovers a usable boot device, loads the bootloader program into memory, and passes control over to it.
- The UEFI is a new 32/64-bit architecture-independent specification that computer manufacturers have widely adopted in their latest hardware offerings replacing BIOS.
	- The Unified Extensible Firmware Interface (UEFI) is a newer standard and has replaced the Basic Input/Output System (BIOS) on many modern systems.
	- It has its own device drivers, is able to mount and read extended file systems, includes UEFI-compliant application tools, and supports one or more bootloader programs.
	- It comes with a boot manager that allows you to choose an alternative boot source.
	- If your system has a UEFI menu, it may include a Trusted Platform Module (TPM). Although TPM technology is built to enhance security on a system,
- Boot devices on most computers support booting from optical and USB flash devices, hard drives, network, and other media.

RHEL 9 supports the traditional MBR partitioning layout and the newer GPT format. Whereas the MBR partitioning scheme supports a maximum size of 2TB per disk, GPT does not have such limitation. However, to boot RHEL from a disk with a GPT partition layout, you need a system with the UEFI firmware interface rather than a traditional BIOS firmware. You should check with your hardware vendor if UEFI is supported by your system.

**The Bootloader Phase**

- Once the firmware phase is over and a boot device is detected, the system loads a piece of software called _bootloader_ that is located in the boot sector of the boot device.
- RHEL uses GRUB2 (_GRand Unified Bootloader_) version 2 as the bootloader program. GRUB2 supports both BIOS and UEFI firmware.
- **The GRUB 2 boot loader makes sure that you can boot Linux. GRUB 2 is installed in the boot sector of your server’s hard drive and is configured to load a Linux kernel and the initramfs**
- For UEFI-based systems, GRUB2 looks for the EFI system partition _/boot/efi_ instead, and runs the kernel based on the configuration defined in the _/boot/efi/EFI/redhat/grub.efi_ file.

1. The primary job of the bootloader program is to spot the Linux kernel code in the _/boot_ file system
2. Decompress Linux kernel code, load it into memory based on the configuration defined in the _/boot/grub2/grub.cfg_ file
3. Transfer control over to it to further the boot process.

**The Kernel Phase**

- The _kernel_ is the central program of the operating system, providing access to hardware and system services.
- After getting control from the bootloader, the kernel extracts the _initial RAM disk_ (initrd) file system image found in the _/boot_ file system into memory, decompresses it, and mounts it as read-only on _/sysroot_ to serve as the temporary root file system (tmpfs - These are kernel devices that are used to create a temporary file system in RAM).
- The kernel loads necessary modules from the initrd image to allow access to the physical disks and the partitions and file systems therein. It also loads any required drivers to support the boot process.
- Later, it unmounts the initrd image and mounts the actual physical root file system on _/_ in read/write mode.
- **At this point, the necessary foundation has been built for the boot process to carry on and to start loading the enabled services. The kernel executes the _systemd_ process with PID 1 and passes the control over to it.**

**The Initialization Phase**

- This is the fourth and the last phase in the boot process. _systemd_ takes control from the kernel and continues the boot process.
- It is the default system initialization scheme. It starts all enabled userspace system and network services and brings the system up to the preset boot target.
- The system boot process is considered complete when all enabled services are operational for the boot target and users are able to log in to the system.