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