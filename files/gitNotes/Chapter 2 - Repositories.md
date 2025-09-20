#gitNotes
### Initializing new repo:

bash

```bash
mkdir newDirectory
cd newDirectory
git init
```

`git init` will create a new repo and place a hidden `.git` directory in newDirectory

### States of a git repo:

- **Untracked**: Not being tracked by Git
- **Staged**: Marked for inclusion in the next commit
- **Committed**: Saved to the repo's history

bash

```bash
git status
```

Command that shows you the current state of your repo

### Table of contents:

All good repos have a table of contents

bash

```bash
touch contents.md
```

### Staging:

bash

```bash
git add <path-to-file | pattern>
```

For example: `git add i-use-arch.btw`

### Commit:

After staging a file we can commit it.

bash

```bash
git commit -m "Your message here"
```

### Git Log:

- **Commit Hash**: Long string of characters that uniquely identifies the commit.
    - For convenience you can use the first 7 chars to refer to the hash.

bash

```bash
git log
```

Shows a history of commits in a repo. You can scroll through the log using arrow keys and exit using 'q'.

bash

```bash
git --no-pager log -n 10
```

Limit the max number of commits shown. Runs without interactive pager.

bash

```bash
git log --oneline
```

Shows commits with less hash digits