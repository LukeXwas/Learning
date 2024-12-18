The **for** conditional provides an excellent solution for processing ranges of data.

![[Pasted image 20241212143737.png]]

- In conditional loops with for, commands are executed as long as the condition is true. 
- In this script, the condition is for i in $@, which means “for each argument.” Each time the script goes through the loop, a value from the $@ variable is assigned to the $i variable. 
- As long as there are arguments, the body of the script is executed. 
- The body of a for loop always starts with **do and is closed with done**, and between these two, the commands that need to be executed are listed
- when you use **break** loop is terminated immediately

![[Pasted image 20241212143307.png]]
1. A **for** conditional statement always starts with **for**, which is followed by the condition that needs to be checked.
2. Then comes **do**, which is followed by the commands that need to be executed if the condition is true
3. The conditional statement is closed with **done**.

The condition is a range of numbers assigned to the variable COUNTER. The variable first is initialized with a value of 100, and as long as the value is higher than 1, in each iteration, 1 is subtracted. As long as the condition is true, the value of the $COUNTER variable is displayed, using the echo commands.

![[Pasted image 20241212143737.png]]

![[Pasted image 20241213141558.png]]

**For one-liner

![[Pasted image 20241212144234.png]]

Notice how the range is defined: You specify the first number, followed by two dots and closed with the last number in the range.

- With **for i in**, each of these numbers is assigned to the variable **i**. For each of these numbers, a **ping** command is executed, where the option **-c 1** makes sure that only one ping request is sent.


