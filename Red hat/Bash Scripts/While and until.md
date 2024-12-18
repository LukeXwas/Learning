Whereas the **for** statement that you just read about is useful to work through ranges of items, the **while** statement is useful if you want to monitor something like the availability of a process.

![[Pasted image 20241212172348.png]]

- First, there is the **while** loop.
- Second, there is everything that needs to be executed when the **while** loop no longer evaluates to true.
- The commands that need to be executed if the statement evaluates to true follow after the **while** statements. In this case, the command is **sleep 5**, which will basically pause the script for 5 seconds.
- As long as the **while** command evaluates to true, it keeps on running. If it does no longer (which in this case means that the process is no longer available), it stops and the commands that follow the **while** loop can be executed.

The core of the **while** loop is the **ps** command, which is grepped for the occurrence of $1. Notice the use of **grep -v grep**, which excludes lines containing the **grep** command from the result. Keep in mind that the **ps** command will include all running commands, including the **grep** command that the output of the **ps** command is piped to. This can result in a false positive match. The results of the **ps aux** command are redirected to the file ~/output.txt. That makes it possible to read the results later from ~/output.txt if that is needed, but they do not show by default.

**Until**

The counterpart of **while** is **until**, which opens an iteration that lasts until the condition is true. 

![[Pasted image 20241212194106.png]]

**until** is used to filter the output of the **users** command for the occurrence of $1, which would be a username. Until this command is true, the iteration continues. When the username is found in the output of **users**, the iteration closes and the commands after the **until** loop are executed.
