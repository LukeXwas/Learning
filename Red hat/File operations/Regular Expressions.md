A regular expression is a search pattern that allows you to look for specific text in an advanced and flexible way.

**man 7 regex**

grep - the general regular expression parser, use it to search specific string in file. **When you use grep, always use escaping (' ') to prevent regular expressions from being interpreted by the shell.**

Example: 
- grep '^anna' /etc/passwd

**Using Extended Regular Expressions**
There are different sets of regular expressions. The base regular expressions as discussed so far are supported by tools like **grep**. When used with **grep**, you’ll have to add the **-E** option to indicate it is an extended regular expression, like +.

### When used in **grep**, don’t forget to use **grep -E** to ensure that these are interpreted as extended regular expressions! ###

![[Pasted image 20241022210316.png]]
![[Pasted image 20241022210355.png]]
Example: 
- grep -E '/web(/.*)?' /etc/x.txt

In this regular expression, the text _/web_ is referred to. This text string can be followed by the regular expression (/.*)?. To understand the regular expression, start with the ?, which refers to the part between braces and indicates that the part between braces may occur zero times or one time. Within the braces, the pattern starts with a slash, which is just a slash, followed by zero or more characters. So this means that just the directory name gives a match, but also the directory name followed by just a slash, or a slash that is followed by a filename.

**More grep options**
![[Pasted image 20241022224809.png]]
