The last of the important iteration loops is **case**. The **case** statement is used to evaluate a number of expected values.

In a **case** statement, you define every specific argument that you expect, which is followed by the command that needs to be executed if that argument was used.

**case** statement that was used in the service scripts in earlier versions of RHEL to start almost any service. This statement works on $1, which is the name of a startup script. Following the name of the script, the user can type **start**, **stop**, **restart**, and so on.

![[Pasted image 20241212194441.png]]

The **case** statement has a few particularities:
- To start, the generic syntax is **case _item-to-evaluate_ in**.
- This syntax is followed by a list of all possible values that need to be evaluated. Each item is closed with a closing parenthesis.
- This ) is followed by a list of commands that need to be executed if a specific argument was used. The list of commands is closed with a double semicolon. This ;; can be used directly after the last command, and it can be used on a separate line.
- the *) refers to all other options not previously specified. It is a “catchall” statement. The **case** statement is closed by an **esac** statement.

Notice that the evaluations in **case** are performed in order. When the first match is made, the **case** statement will not evaluate anything else.

Within the evaluation, wildcard-like patterns can be used. This shows in the *) evaluation, which matches everything. But you also could use evaluations like start|Start|START) to match the use of a different case.
