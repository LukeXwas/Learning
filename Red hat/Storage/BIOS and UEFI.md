The _firmware_ is the BIOS (_Basic Input/Output System_) or the UEFI (_Unified Extensible Firmware Interface_) code that is stored in flash memory on the x86-based system board.

1. The firmware scans the available storage devices to locate a boot device, starting with a 512-byte image that contains 446 bytes of the bootloader program, 64 bytes for the partition table, and the last two bytes with the boot signature.
2. This 512-byte tiny area is referred to as the _Master Boot Record_ (MBR) and it is located on the first sector of the boot disk.As soon as it discovers a usable boot device, it loads the bootloader into memory and passes control over to it.

The BIOS is a small memory chip in the computer that stores system date and time, list and sequence of boot devices, I/O configuration, etc.

**UEFI

The UEFI is a new 32/64-bit architecture-independent specification that computer manufacturers have widely adopted in their latest hardware offerings replacing BIOS.

- This mechanism delivers enhanced boot and runtime services, and superior features such as speed over the legacy 16-bit BIOS. It has its own device drivers, is able to mount and read extended file systems, includes UEFI-compliant application tools, and supports one or more bootloader programs.
- It comes with a boot manager that allows you to choose an alternative boot source. Most computer manufacturers have customized the features for their hardware platform. You may find varying menu interfaces among other differences.