A convenient feature of the Bash shell is the Bash history. Bash is configured by default to keep the last 1,000 commands a user used. When a shell session is closed, the history of that session is updated to the history file. The name of this file is .bash_history and it is created in the home directory of the user who started a specific shell session. Notice that the history file is written to only when the shell session is closed; until that moment, all commands in the history are kept in memory.

- **history** - show a list of all commands in the Bash history
- Press **Ctrl-r** to open the prompt from which you can do backward searches in commands that you have previously used.
- Type **!number** - execute a command with a specific number from history.
- **history -d number** - delete a specific command from history
- **history -c** - commands from this session won’t be written to the history file when you exit the current session

If you want to remove both the current history and the contents of the .bash_history file, then type **history -w** immediately after running the **history -c** command.

**History variables**

- There are three variables—HISTFILE, HISTSIZE, and HISTFILESIZE—that control the location and history storage. 
- HISTFILE defines the name and location of the history file to be used to store command history, and the default is _.bash_history_ in the user’s home directory. 
- HISTSIZE dictates the maximum number of commands to be held in memory for the current session. 
- HISTFILESIZE sets the maximum number of commands allowed for storage in the history file at the beginning of the current session and are written to the HISTFILE from memory at the end of the current terminal session.

The values of any of these variables may be altered for individual users by editing the _.bashrc_ or _.bash_profile_ file in the user’s home directory.