If your server does not boot normally, the GRUB boot prompt offers a convenient way to stop the boot procedure and pass specific options to the kernel while booting. You may want to interact with GRUB2 before the autoboot times out to boot with a non-default kernel, boot to a different target, or customize the kernel boot string. 

- The GRUB2 main menu shows a list of bootable kernels at the top. You can change the selection using the Up or Down arrow key. The default value is 5 seconds. If you press no keys within the 5 seconds, the highlighted kernel will boot automatically.

![[Pasted image 20241125213108.png]]

- Pressing a key before the timeout expires allows you to interrupt the autoboot process and interact with GRUB2. 

**Accessing the Boot Prompt**

- It lets you edit a selected kernel menu entry by pressing an _e_ or go to the grub> command prompt by pressing a _c_.
- In the edit mode, GRUB2 loads the configuration for the selected kernel entry from the _/boot/grub2/grub.cfg_ file in an editor, enabling you to make a desired modification before booting the system.
- ![[Pasted image 20241127203157.png]]

- If you do not wish to boot the system at this time, you can press ESC to discard the changes and return to the main menu.

This is the line that tells GRUB how to start a kernel, and by default it looks like this:

![[Pasted image 20241128211633.png]]

To start, it is a good idea to remove the **rhgb** and **quiet** parts from this line; these arguments hide boot messages for you, and typically you do want to see what is happening while booting.

**After entering the boot options you want to use, press Ctrl-X to start the kernel with these options. Notice that these options are used one time only and are not persistent.**

To make them persistent, you must modify the contents of the /etc/default/grub configuration file and use **grub2-mkconfig -o /boot/grub2/grub.cfg** to apply the modification.

