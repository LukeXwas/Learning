**Understanding the Shell Environment**
When you are working from a shell, an **environment** is created. This environment consists of variables that define the user environment, such as the **$PATH**. **Variables** are fixed names that can be assigned dynamic values. 

**Shell and Environment Variables**

- A _variable_ is a transient storage for data in memory. It retains information that is used for customizing the shell environment and referenced by many programs to function properly. The shell stores a value in a variable, and one or more white space characters must be enclosed within quotation marks.
- There are two types of variables: _local_ (or _shell_) and _environment_.
- A local variable is private to the shell in which it is created, and its value cannot be used by programs that are not started in that shell. This introduces the concept of _current_ shell and _sub_-shell (or _child_ shell). **The current shell is where a program is executed, whereas a sub-shell (or child shell) is created within a shell to run a program. The value of a local variable is only available in the current shell.**
- The value of an environment variable is inherited from the current shell to the sub-shell during the execution of a program. In other words, the value stored in an environment variable is accessible to the program, as well as any sub-programs that it spawns during its lifecycle.

The advantage of working with variables for scripts and programs is that the program only has to use the name of the variable without taking interest in the specific value that is assigned to the variable. Because different users have different needs, the variables that are set in a user environment will differ.

**Basic commands**

- **env** - overview of the current variables defined in your shell environment
- **set** - to view both local and environment variables
- To define a variable, you type the name of the variable, followed by an equal sign (**=**) and the value that is assigned to the specific variable. To read the value of a variable, you can use the **echo** command (among others), followed by the name of the variable, as in **echo $PATH**
- **export** - To make this variable an environment variable, use the _export_ command.
- **unset** - To undefine this variable and erase it from the shell environment.
- To define and make the variable an environment variable at the same time:
![[Pasted image 20241125182250.png]]


