The **set** command in Linux is used to display or modify shell environment settings. It is a built-in shell command available in **Bash** and other POSIX-compliant shells.

**Syntax

![[Pasted image 20241213143730.png]]

**set** - Lists all environment variables and functions defined in the current shell session

Enable shell options

![[Pasted image 20241213144226.png]]

![[Pasted image 20241213144239.png]]

**Common set options

- **`-e`** – Exit the script if any command returns a non-zero status.
- **`-x`** – Print each command before executing (debugging mode).
- **`-u`** – Treat undefined variables as errors.
- **`-v`** – Print each line of the script before executing it.
- **`-n`** – Check the script syntax without executing it.
- **`-o pipefail`** – A pipeline fails if any command in the pipeline fails.
- **`+<option>`** – Disable the specified option (e.g., `set +e` disables `-e`).

Example Script with set

![[Pasted image 20241213144437.png]]

**Options explained:**
- **`-e`** – Exit the script on any error.
- **`-u`** – Error if an undefined variable is used.
- **`-o pipefail`** – A pipeline fails if any command in the pipeline fails.


