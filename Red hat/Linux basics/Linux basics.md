A _shell_ is a user interface. A text-based shell is also used as a command-line interpreter. In Linux, the shell is the interpreter that allows you to interact with the operating system using various commands.

Users can choose between four command-line shells in RHEL 9. Although bash is the default, longtime Linux and Unix users may prefer something else. This is a partial list of the most common shells:
1. **bash** The default Bourne-again shell, based on the command-line interpreter originally developed by Stephen Bourne
2. **ksh** The Korn shell, developed by David Korn at Bell Labs in the 1980s, to incorporate the best features of the Bourne-again and C shell
3. **tcsh** An enhanced version of the Unix C shell
4. **zsh** A sophisticated shell, similar to the Korn shell

Kolejnosc wykonywania komend:
1. Aliasy 
	1. komenda: alias newcommand="ls -la"
2. Komendy wbudowane w shella
3. Zewnetrzne komendy (programy znajdujace sie na dysku)

**type** - komenda okreslajaca czy komenda jest wbudowana czy zewnetrzna
**which** - komenda okreslajaca czy polecenie jest w zmiennej path oraz wyswietla sciezke bezwzgledna polecenia

These shells are located in the /bin directory.

**Differences Between Regular and Administrative Users

What you can do at the command line depends on the privileges associated with the login account.

regular user:
`[michael@server1 ~]$`

administrator user:
`[root@server1 ~]#`

**Tilde**

If ~ is used as a standalone character, the shell refers to the $HOME directory of the user running the command.

![[Pasted image 20241205203816.png]]

If the plus sign (+) follows the ~, the shell refers to the current directory. For example, if _user1_ is in the _/usr/bin_ directory and does ~+, the output exhibits the user’s current directory location:

![[Pasted image 20241205203854.png]]

Tilde substitution can also be used with commands such as _cd_ and _ls_. For instance, to _cd_ into the home directory of _user1_ (or any other user for that matter) from anywhere in the directory structure, specify the login name with the ~. This command is only successful if _user1_ has the right permissions to navigate into the target user’s home directory.

![[Pasted image 20241205203938.png]]

**How to assign the result of a command to variable

VAR1= $( commands )

for example:
- **TODAY=$(date +%d-%m-%y)**

**How to assign result of last command in bash**

To request the exit status of the last command, from the parent shell, use the **echo $?** command.

**Special parameters**

![[Pasted image 20241213135448.png]]

**Bash Completion**

Bash completion is useful when you’re working with commands. Just type the beginning of a command and press the Tab key. If there is only one option for completion, Bash will complete the command automatically for you. If there are several options, you need to press Tab once more to get an overview of all the available options.

**Command line is too long**

When the command line is too long, the \ character can be added, then press Enter and continue the command on a new line

**Prefixing with a Backslash \**

The backslash character (\), also referred to as the _escape_ character in shell terminology, instructs the shell to mask the meaning of any special character that follows it.


