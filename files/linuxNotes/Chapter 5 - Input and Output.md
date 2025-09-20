#linuxNotes 
### Manual Pages

**Access Manuals:**

bash

```bash
man <command>
```

Example: `man grep`

**Searching in Manuals:**

- Type `/<string>` to search for text
- Press `n` to jump to next result
- Press `N` to jump to previous result

### Flags

Some commands accept flags. Flags are options that you can pass to a command to change its behavior.

For Example:
`ls -l` shows a "long" list of files
`ls -a` shows "all" files, including hidden ones
`ls -al` you can also combine flags

**Conventions:**

Whether or not a command takes flags, and what those flags are, is up to the developer of the command.

Common conventions:
- Single-character flags are prefixed with a single dash (e.g `-a`)
- Multi-character flags are prefixed with two dashes (e.g. `--help`)
- Sometimes the same flag can be used with a single dash or two dashes (e.g `h` or `help`)

### Help

Most CLI tools have a "help" option that prints out the information about the tool.
Usually accessed using:
- `--help`(flag)
- `-h`(flag)
- `help`(first positional argument)
The "help" output is often easier to parse than a full `man` page. It's more of a quick start guide than a full manual.

### Exit Codes

`0` exit code for success
`1` "catch all" error code

**Access Exit Code:**

`$?` in shell will access the exit code

bash

```bash
ls does/not/exist
echo $?
# returns non-zero error code (depends on your OS)
```

### Standard Error

"Standard Error", usually called "stderr", is a data stream just like stdout, but is intended to be used for error messages.

**Redirecting Streams:**

You can redirect stdout and stderr to different places using teh `>` and `2>` operators. `>` redirects stdout, and `2>` redirects stderr.

Redirect stdout to a file:

``` bash
echo "Hello world" > hello.txt
cat hello.txt
# Hello world
```

Redirect stderr to a file:

```bash
cat doesnotexist.txt 2> error.txt
cat error.txt
# cat: doesnotexist.txt: No such file or directory
```

### Standard Output

"Standard Output", usually called "standard out" or "stdout", is a default place where programs print their output.

In a shell it's the `echo` command

```bash
echo "Hello world"
```

### Standard In

"Standard Input", usually called "standard in" or "stdin", is the default place where programs read their output.

In shell we use `read`

```bash
echo "Input your name: "
read NAME
echo "Your name is $NAME"
# This will output whatever the user put in after the first echo
```

### Piping

The pipe operator is `|`. The pipe operator takes the stdout of the program on the left and "pipes" it into the stdin of the program on the right.

**Example: Printing word count**
```bash
echo "Have you heard of teh tragedy of Darth Plagueis the Wise?" | wc -w
# Ouput: 10
```

### Emergency commands

**Interrupt:**
Sometimes a program will get stuck and you'll want to stop it.

`ctrl + c` sends a "SIGINT" signal to the program, which tells it to stop.

**Kill:**
Sometimes a program is in such a bad state (or is so malicious) that it doesn't respond to the SIGINT, in which case the best option is to use another (new terminal window) to manually kill the program.

Syntax:
```bash
kill <PID>
```

`PID` stands for "process ID". Every process that's running on your machine has a unique ID. The `ps`, "process status" command can be used to list the processes running on your machin, and their IDs:
``` bash
ps aux
```
The `aux` options just mean "show all the processes, including those owned by other users, and show extra information about each process".

Check headers of `ps aux` table:
```bash
ps aux | head -n 1
```

To find a PID of a program:
```bash
ps aux | grep <file.name>
```
Note: You only need to put in file name (NOT the path/to/file)... Don't be like me :(
	Then finally you have the PID and you can kill the program >:)

### Unix Philosophy

**IMPORTANT:**
1. Write programs that do one thing and do it well
2. Write programs to work together
3. Write programs to handle text streams, because that is  a universal interface

### Top

`top` a powerful tool that allows you to see which programs are using the most resources on your computer.
- Much like task manager or Activity Monitor.

**Controls in `top`:** (May add more here later)

`M` - to sort by memory usage (macOS may have to use `o mem <ENTER>`)