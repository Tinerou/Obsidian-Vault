#linuxNotes
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
