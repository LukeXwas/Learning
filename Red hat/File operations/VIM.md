**Editing Files with vim**

Vim is simple text editor. An important concept when working with **vim** is that it uses different modes. Two of them are particularly important: _command mode_ and _input mode_. 
- Command mode - use **Esc** to entre this mode
- _input mode_ - use **i** to entre this mode. In this mode u can write some text.

The most important options in command mode:
- **:wq** - Writes the current file and quits.
- **:q!** - Quits the file without applying any changes.
- **dd** - Deletes the current line.
- **yy** - Copies the current line
- **p** - Pastes the contents that have been cut or copied into memory.
- **u** - Undoes the last command.
- **gg** - Goes to the first line in the document.
- **G** - Goes to the last line in the document.
- **/text** - Searches for _text_ from the current cursor position forward.
- **:%s/old/new/g** - Replaces all occurrences of _old_ with _new_.
- **:set nu** - Shows line numbering
