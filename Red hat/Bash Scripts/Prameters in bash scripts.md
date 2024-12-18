Linux Bash scripts are much more than just a list of sequentially executed commands. One of the nice things about scripts is that they can work with variables and input to make the script flexible.

In bash, a _parameter_ is something that can store a value. Hence, a variable is a parameter. It is in fact a type of parameter denoted by a name. However, there are also two other types of parameters:

- **Special parameters** - These parameters are represented by special characters, each with a specific meaning. For example, the special parameter $? stores the exit code of the last command executed.
- **Positional parameters** - A series of parameters, $0 to $9, that store the command-line arguments.

**Special parameters**

- **$@** refers to all arguments that were used when starting the script.

![[Pasted image 20241213135448.png]]

**Using Positional Parameters

- When starting a script, you can use arguments.
- An _argument_ is anything that you put behind the script command while starting it.
- for instance, the **useradd lisa** command. In this example, the command is **useradd**, and the argument **lisa** specifies what needs to be done.
- In a script, the first argument is referred to as **$1**, the second argument is referred to as **$2**, and so on.

![[Pasted image 20241212140815.png]]

If you use three arguments while using the script, it will work perfectly. If you use only two arguments, the third echo will print with no value for $3. If you use four arguments, the fourth value (which would be stored in $4) will never be used.

**How to use arguments in better way**

![[Pasted image 20241212140934.png]]

- **$#** is a counter that shows how many arguments were used when starting the script.
- **$@** refers to all arguments that were used when starting the script.

To evaluate the arguments that were used when starting this script, you can use a conditional loop with **for**. In conditional loops with **for**, commands are executed as long as the condition is true. In this script, the condition is **for i in $@**, which means “for each argument.” Each time the script goes through the loop, a value from the $@ variable is assigned to the $i variable. So, as long as there are arguments, the body of the script is executed.