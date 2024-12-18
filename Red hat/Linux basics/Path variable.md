**$PATH variable**
PATH is a special environment variable that a shell that will search for executable commands. PATH contains a list of directories that are searched for the command that the user just typed at the command prompt. (you can type pwd instead of /bin/pwd)

echo $PATH - display directories for the current user account

The directories in the PATH for regular users and the root administrative user are slightly different.

The PATH is determined globally by current settings in the /etc/profile file or by scripts in the /etc/profile.d directory.

As well as the global settings, the PATH for individual users can be customized with an appropriate entry in that user’s home directory, in the hidden files named ~/.bash_profile or ~/.profile.

How to add path to .bashrc:

1. nano ~/.bashrc
2. In the text editor, scroll down to the end of the file
3. export PATH="$PATH:/path/to/your/directory"
4. Save and exit the file
5. source ~/.bashrc