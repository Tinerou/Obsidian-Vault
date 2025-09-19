# Command Line Guide

## Chapter 1: Terminals and Shells

### Terminal vs. Shell

- **Terminal** = A program that lets you type commands into a window on your computer
- **Shell** = Interprets the commands you type and executes them
    - Shells are often referred to as "REPLs"
    - **REPL** = Read Evaluate Print Loop
- **CLI** = Command Line Interface

### Variables

**Create a Variable:**

bash

```bash
name="Trey"
```

_Note: No spaces around the equals sign_

**Use a Variable:**

bash

```bash
echo $name
```

**Interpolate a Variable in a String:**

bash

```bash
echo "Hello $name"
```

### History Commands

- `history` - Shows your command history
- `clear` - Clears the terminal

## Chapter 2: Filesystems

### Navigation Commands

- `pwd` - Print working directory (shows current filepath)
- `ls [directory]` - Lists contents in directory
- `cd [path]` - Changes directory
    - `cd` alone takes you to the home directory
- `..` - Represents the parent directory
    - Common use: `cd ..` to go back one directory

### File Viewing Commands

- `cat <file> [file] [file]` - Concatenates and displays file contents
- `head -n 10 <file>` - Prints the first n lines (default: 10)
- `tail -n 10 <file>` - Prints the last n lines (default: 10)

### File and Directory Creation

- `touch <new_file> [new_file2] [new_fileN]` - Creates files
- `mkdir <new_directory> [new_directory2] [new_directoryN]` - Creates directories

### File Operations

**Moving/Renaming:**

- `mv file.txt file2.txt` - Renames a file
- `mv file.txt directory/file.txt` - Moves file to another directory
- `mv file.txt ../file.txt` - Moves file to parent directory

**Removing:**

- `rm <file>` - Removes a file
- `rm -r <directory>` - Removes directory and all contents recursively

**Copying:**

- `cp file.txt directory/` - Copies file to directory
- `cp -R old_directory new_directory` - Copies directory recursively

### Search Commands

**Text Search:**

- `grep "hello" <file> [fileN]` - Searches for text in files (case sensitive)
- `grep -r "hello" .` - Recursive search through entire directory

**File Search:**

- `find <directory> -name <file_name>` - Finds file by name
- `find <directory> -name "*.txt"` - Finds all .txt files
- `find <directory> -name "*gigachad*"` - Finds files containing "gigachad"
    - `*` is a wildcard that matches anything

### Directory Aliases

- `~` - Home directory (e.g., `/Users/username`)
- `.` - Current directory

## Chapter 3: Permissions

### Sudo

- `sudo` = superuser do
- Grants unrestricted access but can risk system damage if misused
- Always review commands before running with sudo

### Understanding Permissions

Permissions are represented as a 10-character string:

```
d rwx r-x r--
| |1| |2| |3|
```

**First Character:** 

- `d` = directory
- `-` = file

**Permission Groups:**

- **Section 1** = Owner permissions
- **Section 2** = Group permissions
- **Section 3** = Others permissions

**Permission Types:**

- `r` = read
- `w` = write
- `x` = execute
- `-` = permission not granted

### Changing Permissions

**View Permissions:**

bash

```bash
ls -l
```

**Modify Permissions:**

bash

```bash
chmod -R u=rwx,g=,o= <DIRECTORY>  # Owner: full access, Group/Others: no access
chmod -x program.sh               # Remove execute permission
chmod u+x program.sh              # Add execute permission for user
```

### Executables

**Shell Scripts:**

- Files with `.sh` extension are shell scripts
- Text files containing shell commands
- Run with: `./program.sh` (if in current directory)

### Environment Variables

**View Environment Variables:**

bash

```bash
env
```

**Set Environment Variable:**

bash

```bash
export NAME="Trey"
```

_Note: Only affects current shell session_

### PATH Variable

The PATH variable lists directories where the shell looks for executable commands.

**Adding to PATH:**

bash

```bash
export PATH="$PATH:/directory"
```

- `$PATH` references existing PATH
- `:` is the separator

**Permanent PATH Configuration:** Add `PATH="$PATH:/directory"` to your `.zshrc` or `.bashrc` file

## Chapter 5: Input/Output

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

**IMPORTANT**
1. Write programs that do one thing and do it well
2. Write programs to work together
3. Write programs to handle text streams, because that is  a universal interface

### Top

`top` a powerful tool that allows you to see which programs are using the most resources on your computer.
- Much like task manager or Activity Monitor.

**Controls in `top`**

`M` - to sort by memory usage (macOS may have to use `o mem <ENTER>`)
