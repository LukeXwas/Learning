When a user types a command, a shell job is started.

- By default, any executed command is started as a foreground job. That means that you cannot do anything on the terminal where the command was started until it is done.
- Sometimes it might prove useful to start commands in the background. This makes sense for processes that do not require user interaction and take significant time to finish. A process that does require user interaction will not be able to get that when running in the background, and for that reason will typically stall when moved to the background.

**Basic operations**

![[Pasted image 20241207204535.png]]

- **jobs** - shows which jobs are currently running from this shell
- If you know that a job will take a long time to complete, you can start it with an **&** behind it. This command immediately starts the job in the background.
- To move the last job that was started in the background back as a foreground job, use the **fg** command. If multiple jobs are currently running in the background, you can move a job back to the foreground by adding its job ID, as shown by the **jobs** command.
- Use **Ctrl-Z** to temporarily stop the job. This does not remove the job from memory; it just pauses the job so that it can be managed.
- Once the job is paused, you can continue it as a background job by using the **bg** command.
- An alternative key sequence that you can use to manage shell jobs is **Ctrl-C**. This key combination stops the current job and removes it from memory.
- **Ctrl-D** sends the End Of File (EOF) character to the current job. The result is that the job stops waiting for further input so that it can complete what it was currently doing. It is needed to complete in a proper way

