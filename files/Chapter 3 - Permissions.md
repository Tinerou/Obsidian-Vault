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