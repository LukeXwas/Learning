A variable is a label that is used to refer to a specific location in memory that contains a specific value. 

The following example illustrates how you can assign a variable from the command line:

![[Pasted image 20241212195525.png]]

How to display variables - use **echo** to show the value of each variable. Notice that to request the current value of a variable, the script refers to the variable name, preceded by a $ sign.

- Variables can be defined statically by using **NAME=value
- Variables can be defined in a dynamic way. There are two solutions to define a variable dynamically:
	- Use **read** in the script to ask the user who runs the script for input.
	- Use command substitution to use the result of a command and assign that result to a variable. For example, the **date +%d-%m-%y** command shows the current date in day-month-year format. To assign that date to a variable in a script, you could use the **TODAY=$(date +%d-%m-%y)** command.

**Variable operations

You can also add braces around the variable name to avoid ambiguous expressions. For example, without braces, the following command would retrieve the value of the variable **\$todayth** rather than the value of **$today**:

![[Pasted image 20241212195654.png]]

You can use variables as part of arithmetic expressions. In bash, arithmetic expressions are enclosed in the **$((_expression_))** syntax. Here’s an example:

![[Pasted image 20241212195754.png]]

Variables can also store the output of a command. There are two ways to do so: using the **$(_command_)** syntax and with backticks, **`_command_`**. Here’s an example of each:

![[Pasted image 20241212195829.png]]

**The Scope of Variables

The variables that we declare in bash can be passed as arguments to other commands

example:

create a script with the following lines:

![[Pasted image 20241213134937.png]]
Save the content to a file (for example, testvar), make it executable, assign a value to myvar, and then run the script:

![[Pasted image 20241213135032.png]]

The script’s output is empty, so the value of myvar was not available to the script.

**To use shell variables with any command, you need to export those variables as _environment variables_, as shown next:**

![[Pasted image 20241213135157.png]]

Then, if you run the script again, you will find that the value of the myvar variable is now passed to the script:
![[Pasted image 20241213135206.png]]

Environment variables are usually declared in either the ~/.bashrc file or ~/.bash_profile file on a user’s home directory, or in the corresponding global files, /etc/basrhc or /etc/profile. An example is the LANG environment variable, which tells programs which language and local setting to use.

**Environment variables are useful to define variables that should be globally available to all programs. However, they are not very practical if you want to pass to a program parameters that change often. For that purpose, you can use command arguments, or positional parameters.