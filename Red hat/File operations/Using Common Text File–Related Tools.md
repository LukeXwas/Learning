![[Pasted image 20241022174516.png]]
**less** - less /etc/passwd:
- press **q** to quit
- **/sometext** for a forward search, **?sometext** for a backward search, **n** next search
- **zless** - can read text files compressed in gzip format
**head & tail** - text file shows the last ten lines by default, you can adjust the number of lines that are shown by adding **-n** followed by the number you want to see.
- **tail -f /var/log/messages** - This is convenient for monitoring log files. This option starts by showing you the last ten lines of the file you’ve specified, but it refreshes the display as new lines are added to the file.
**cut** - To filter out a specific field (column) from text file, the **-d** option to specify the field delimiter followed by **-f** with the number of the specific field you want to filter out (**cut -d : -f 1 /etc/passwd**)
**sort** - this command sorts text, By default, sorts in order in which the characters appear in the ASCII text table, 
- **-n** - numerical order, 
- **-u** - display unique values
- **-r** - reverse the result of comparisons
- You can also use the **sort** command and specify which column you want to sort. To do this, use **sort -k3 -t : /etc/passwd**, for instance, which uses the field separator : to sort the third column
**wc** - count lines and words and the number of characters, -l count only lines (wc -l)
**nl** - number lines
**sed** - very powerful utility for filtering text from text files, default **sed** behavior is to write the output to STDOUT, but the option **-i** will write the result directly to the file.
- sed -i s/old-text/new-text/g ~/myfile - used to search for the text _old-text_ in ~/myfile and replace all occurrences with the text _new-text_
- sed -i -e '2d' ~/myfile - delete a line based on a specific line number
**diff** - find the difference between files. 
- The **-u** option in the diff command represents the “unified format.” This format not only highlights the differences between files but also displays several surrounding lines for context. This contextual view facilitates a clearer understanding of the variations in relation to the adjacent content.
**tr** - use to perform different text transformations, including case conversion, squeezing or deleting characters, and basic text replacement.
- syntax: tr \[options] SET1 \[SET2]

**tr examples**

**Convert Lowercase to Uppercase:

cat baeldung.url
www.baeldung.com

tr 'a-z' 'A-Z' < baeldung.url
WWW.BAELDUNG.COM

we redirected a file _baeldung.url_ to _stdin_ and asked _tr_ to do the case conversion

**Basic Find and Replace - _tr_ can do multiple character replacement

![[Pasted image 20241216130202.png]]


**Squeeze Repeating Characters - example of converting multiple continuous spaces to a single space:

![[Pasted image 20241216130334.png]]

**Delete Specific Characters - we can pass the “-d” option to tr to delete characters in SET1

![[Pasted image 20241216130457.png]]

**To remove all the digits from the string, you can use

**How to complement the sets using -c option - we would like to match any character that is not a lowercase letter and translate it into whitespace:

![[Pasted image 20241216130536.png]]

**We can also combine the “-c” option with “-d” or “-s”. The next example shows how can we extract the id number from the customer.csv file:

![[Pasted image 20241216130606.png]]
