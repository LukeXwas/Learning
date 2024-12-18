The **if … then … else** construction is common to evaluate specific conditions. This conditional loop is often used together with the **test** command to check whether a file exists. This command enables you to do many other things as well, such as compare files, compare integers, and much more.

Look at the man page of the **test** command.

The basic construction with **if** is **if ... then ... fi**. This construction is useful if many different values need to be checked.

![[Pasted image 20241212142907.png]]

Multiple conditions can be evaluated by contracting **else** with **if** to become **elif**.

**Test operators in bash

| **Operation on Integer Value** | **Description**                                      |
| ------------------------------ | ---------------------------------------------------- |
| integer1 -eq (-ne) integer2    | Integer1 is equal (not equal) to integer2            |
| integer1 -lt (-gt) integer2    | Integer1 is less (greater) than integer2             |
| integer1 -le (-ge) integer2    | Integer1 is less (greater) than or equal to integer2 |

| **Operation on String Value** | **Description**                                             |
| ----------------------------- | ----------------------------------------------------------- |
| string1=(!=)string2           | Tests whether the two strings are identical (not identical) |
| -l string or -z string        | Tests whether the string length is zero                     |
| string or -n string           | Tests whether the string length is non-zero                 |

| **Operation on File**               | **Description**                                                                                                                       |
| ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| -b (-c) file                        | Tests whether the file is a block (character) device file                                                                             |
| -d (-f) file                        | Tests whether the file is a directory (normal file)                                                                                   |
| -e (-s) file                        | Tests whether the file exists (non-empty)                                                                                             |
| -L file                             | Tests whether the file is a symlink                                                                                                   |
| -r (-w) (-x) file                   | Tests whether the file is readable (writable) (executable)                                                                            |
| -u (-g) (-k) file                   | Tests whether the file has the setuid (setgid) (sticky) bit                                                                           |
| file1 -nt (-ot) file2               | Tests whether file1 is newer (older) than file2                                                                                       |
|                                     |                                                                                                                                       |
| **Logical Operators**               | **Description**                                                                                                                       |
| !                                   | The logical NOT operator                                                                                                              |
| -a or && (two ampersand characters) | The logical AND operator. Both operands must be true for the condition to be true. Syntax: [ -b file1 && -r file1 ]                   |
| -o or \| (two pipe characters)      | The logical OR operator. Either of the two or both operands must be true for the condition to be true. Syntax: [ (x == 1 -o y == 2) ] |

**How to use test**

The **test** operator is sometimes used as a conditional within the **if**.

![Images](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781260462081/files/f0384-01.jpg)

is functionally equivalent to

![Images](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781260462081/files/f0384-02.jpg)

**How to compare two strings**

![[Pasted image 20241213141208.png]]

**Using || and &&

Instead of writing full **if ... then** statements, you can use the logical operators **||** and **&&**.

- || is a logical OR and will execute the second part of the statement only if the first part is not true
- && is the logical AND and will execute the second part of the statement only if the first part is true

![[Pasted image 20241212143145.png]]

 - In the first example, a test is performed (using the alternative **test** command syntax) to see whether $1 is empty. If that test is true (which basically means that the **test** command exits with the exit code 0), the second command is executed.
 - In the second example, a **ping** command is used to check the availability of a host. The logical OR is used in this example to echo the text “node is not available” in case the **ping** command was not successful.

You’ll often find that instead of fully written **if … then** statements, the **&&** and **||** constructions are used