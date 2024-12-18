Basically, a shell script is a list of commands that is sequentially executed, with some optional scripting logic in it that allows code to be executed under specific conditions only.

**After writing a script, make sure that it can be executed. The most common way to do this is to apply the execute permission to it. So, if the name of the script is hello, use chmod +x hello to make it executable.**

You can basically store the script anywhere you like, but if you are going to store **it in a location that is not included in the $PATH, you need to execute it with a ./ in front of the script name.**

So, just typing **hello** is not enough to run your script; type **./hello** to run it. Note that ./ is also required if you want to run the script from the current directory. When you are in other locations use full path to the script.


![[Pasted image 20241212140308.png]]

When a script is started from a parent shell environment, it opens a subshell. In this subshell, different commands are executed. These commands can be interpreted in any way, and to make it clear how they should be interpreted, the shebang is used.

This basic script contains a few elements that should be used in all scripts:
- **To start, there is the shebang**. This is the line #!/bin/bash. In this case, the shebang makes clear that the script is a Bash shell script. Other shells can be specified as well. For instance, if your script contains Perl code, the shebang should be #!/usr/bin/perl.
- On RHEL 9, the **/bin/sh** path is symbolically linked to **/bin/bash**. This means that using **/bin/sh** or **/bin/bash** will lead to the same result, and they can be used interchangeably.

It is good practice to start a script with a shebang; if it is omitted, the script code will be executed by the shell that is used in the parent shell as well. Because your scripts may also be executed by, for instance, users of ksh, using a shebang to call /bin/bash as a subshell is important to avoid confusion.

- Right after the shebang, there is a part that explains what the script is about. It is a good idea in every script to include a few comment lines. In a short script, it is often obvious what the script is doing.

- You can include comment lines, starting with a #. Include them not only in the beginning of the script but also at the start of every subsection of the script. **You can also use comments within lines. No matter in which position the # is used, everything from the # until the end of the line is comment text.**

- Next is the body of the script. The body is just a simple script containing a few commands that are sequentially executed. The body may grow as the script develops.

- At the end of the script, I included the statement **exit 0**. An **exit** statement tells the parent shell whether the script was successful. A 0 means that it was successful, and anything else means that the script has encountered a problem.

