#gitNotes
**Branch** = A named pointer to a specific commit. When you create a branch, you are creating a new pointer to a specific commit. The commit that the branch points to is called the tip of the branch.

### Rename a branch:

bash

```bash
git branch -m <oldname> <newname>
```

Git config names are case INSENSITIVE

### Create a branch:

bash

```bash
git switch -c <new_branch>
```

This will create and set you to that new branch.

- `-c` flag tells Git to create a new branch if it doesn't already exist.
- When you create a new branch, it uses the current commit you are on as the branch base.

### Switch branch:

bash

```bash
git switch <branch>
```

Newer and easier way.

bash

```bash
git checkout <branch>
```

Older and less intuitive way.

### Log flags:

**Using --decorate:**

- short (default)
- full (shows the full ref name)
- no (no decoration)

Example: `git log --decorate=full`

**Using --oneline:**

- Compact view of the log (Just one line per commit).

Example: `git log --oneline`