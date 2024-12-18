A parameter’s value can be manipulated using some string substitution techniques known as _parameter expansion_.

define a variable as shown next:

![[Pasted image 20241213135723.png]]

The first parameter expansion construct is **${_parameter_:-_word_}**.

This gives the value of **${_parameter_}** if the parameter is defined; otherwise, **_word_** is substituted:

![[Pasted image 20241213135855.png]]

Another useful parameter expansion construct is **${_parameter_/_pattern_/_string_}**. This replaces the longest match of **_pattern_** with **_string_**. As an example, suppose that you want to change the .gz extension to .tar.gz for the filename stored in the variable ch9:

![[Pasted image 20241213140317.png]]

You can remove a matching suffix pattern with the parameter expansion sequences **\${_parameter_#_word_}** and **${_parameter_##_word_}**. These remove, respectively, the shortest or longest occurrence of **_word_**, starting the search from the beginning of the value of **_parameter_**. An example is shown next:

![[Pasted image 20241213140423.png]]

the parameter expansion sequences **\${_parameter_\%_word_}** and **\${_parameter_\%%_word_}** remove the shortest or longest occurrence of **_word_**, but starting the search from the end of the value of **_parameter_**. This is exemplified here:

![Images](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781260462081/files/f0381-03.jpg)

![[Pasted image 20241213140756.png]]

