# Git Commands Guide

## Quick Navigation

- [[#Chapter 1 - Setup|Setup & Configuration]]
- [[#Chapter 2 - Repositories|Working with Repositories]]
- [[#Chapter 3 - Internals|Internals]]
- [[#Chapter 5 Branching|Branching Basics]]
- [[#Chapter 6 Merge|Merging]]
- [[#Chapter 7 Rebase|Rebasing]]
- [[#Chapter 9 Remote|Remote Repositories]]
- [[#Chapter 10 GitHub|GitHub Workflow]]
- [[#Chapter 11 gitignore|Gitignore Patterns]]

---

## Chapter 1 - Setup

Git commands are separated into 2 groups:

- **Porcelain** = high-level commands
- **Plumbing** = low-level commands

_We will mostly be using porcelain commands. Some examples of these are:_

- `git status`
- `git add`
- `git commit`
- `git push`
- `git pull`
- `git log`

### Configuration Commands

**Check username and email:**

bash

```bash
git config --get user.name
git config --get user.email
```

**Set username and email:**

bash

```bash
git config --add --global user.name "github_username"
git config --add --global user.email "email@example.com"
```

**Set default branch:**

bash

```bash
git config --global init.defaultBranch master
```

_Note: We change from master → main later_

**Check to see if it worked:**

bash

```bash
cat ~/.gitconfig
```

## Chapter 2 - Repositories

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

## Chapter 3: Internals

### Hash = SHA

- Might hear people call their commit hashes SHAs.
- Hashes are determined by the commit message, author's name and email, date and time, parent (previous) commit hashes.
- Hashes are almost always unique.

### Show objects in git:

bash

```bash
ls -al
```

To list the contents of the `.git/objects` directory.

### cat-file: (porcelain command)

bash

```bash
git cat-file -p <hash>
```

Allows us to see the contents of a commit without having to deal with the object files directly.

bash

```bash
git cat-file -p <hash> > /tmp/catfileout.txt
```

Create a temporary file to hold this information.

### Trees and Blobs:

- **Tree**: Git's way of storing a directory.
- **Blob**: Git's way of storing a file.

### Storing Data:

- Git stores an entire snapshot on a per-commit level. (Not just newly committed files)
- Git compresses and packs files to store them more efficiently.
- **Deduplication**: The elimination of duplicate or redundant information.
- Git deduplicates files that are the same across different commits. If a file does not change between commits, Git will only store it once.

## Chapter 4: Configuration

### Updating global Git config

bash

```bash
git config --add --global user.name "The Primeagen"
git config --add --global user.email "the.primeagen@aol.com"
```

**Command Breakdown:**

- `git config`: The command to interact with your Git Configuration
- `--add`: Flag stating you want to add a configuration
- `--global`: Flag stating you want this configuration to be stored globally in your `~/.gitconfig`. The opposite is `--local`, which stores the configuration in the current repository only.
- `user`: The section.
- `name`: The key within the section.

### Updating local Git config:

bash

```bash
git config --add --local webflyx.ceo ThePrimeagen
```

- `webflyx`: Section
- `ceo`: Section key (In this case key = ThePrimeagen)

bash

```bash
git config --list --local
```

Lists local git configuration.

### Additional config commands:

bash

```bash
git config --get <key>
```

Keys are in the format `<section>.<keyname>` For example: `user.name`

bash

```bash
git config --unset <key>
```

Used to remove a configuration value

bash

```bash
git config --unset-all <key>
```

Git doesn't care if you have duplicate Keys. To purge all instances of a key from your config.

bash

```bash
git config --remove-section <section>
```

Be careful with this

### Locations:

- **system**: `/etc/gitconfig`, a file that configures Git for all users on the system
- **global**: `~/.gitconfig`, a file that configures Git for a specific project
- **local**: `.git/config`, a file that configures Git for a specific project
- **worktree**: `.git/config.worktree`, a file that configures Git for part of a project

**Note**: 90% of the time we use `--global` to set things like username and email. 9% of the time we use `--local` to set project-specific configs. The last 1% is messing around with tree and workspace configs, but this is EXTREMELY rare.

**Overriding**: If you set a configuration in a more specific location, it will override the same configuration in a more general location. For example, if you set `user.name` in the local configuration, it will override the `user.name` set in the global configuration.

_Note: Specificity is in same order as in "Locations:" above._

## Chapter 5: Branching

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

## Chapter 6: Merge

**Merge** = merging other_branch into main. Git combines both branches by creating a new commit that has both histories as parents.

bash

```bash
git merge <head>
```

After merging you can delete the branch used to merge

bash

```bash
git branch -d <head>
```

### Fast forward merge:

When you create a new branch and instantly commit this will just "fast-forward merge" to main. This is because that new branch has the same previous commits as main.

### Nice way to view commit history:

bash

```bash
git log --oneline --graph --all
```

This will provide you with a nice ASCII representation of your commit history.

## Chapter 7: Rebase

**Rebase** = Changing the base at which the branch starts. This allows for better workflows with advanced git features.

bash

```bash
git switch -c <branch_name> <commit_hash>
```

This will create a branch at a desired commit location

bash

```bash
git rebase main
```

**What this does:** (branch jdsl is the branch being moved)

1. Identifies the latest commit from main and uses it as the temporary new base.
2. Replay each commit from the jdsl one at a time onto this temporary location.
3. Update the jdsl branch to point to the last replayed commit in the temporary location, making this the new permanent jdsl.
4. The rebase does not affect the main branch; jdsl now includes all changes from main.

### Merge vs. Rebase:

**MERGE:**

- **Advantages:**
    - Preserves the true history of the project
    - Shows when and where branches were merged
- **Disadvantage:**
    - Lots of merge commits can make the history harder to read and understand

**REBASE:**

- **Advantages:**
    - A linear history is generally easier to read, understand, and work on.
- **Disadvantages:**
    - NEVER rebase a public branch (like main) onto anything else.
        - If you do this other developers working on the branch will face problems
        - However, you can do this all you want with your own branch!

## Chapter 8: Reset

bash

```bash
git reset --soft <commit_hash>
```

`--soft` option will help if you want to go back to a previous commit but keep all of your changes. Will stay staged until committed.

bash

```bash
git reset --hard <commit_hash>
```

`--hard` option will reset the previously made changes and go back to a previous commit.

- **DANGEROUS!!!! yet powerful**
    - All commits made after the commit you reset to will be permanently deleted.

## Chapter 9: Remote

**Remote** = In git, another repo is called a "remote". The standard convention is that when you're treating the remote as the "true" repo (such as GitHub) you would name it the "origin".

bash

```bash
git remote add <name> <uri>
```

uri = (uniform resource identifier) path to the directory `Users/../../path_to_file`

You can use git log for more than just your local repo

bash

```bash
git log origin/branch
```

bash

```bash
git merge remote/branch
```

Just as we merged branches within a single local repo, we can also merge branches between local and remote repos

## Chapter 10: GitHub

**PUSH:**

bash

```bash
git push origin main
```

Sends local changes to any "remote" (for most of my cases to GitHub)

bash

```bash
git push <localbranch>:<remotebranch>
```

**PULL:**

bash

```bash
git pull [<remote>/<branch>]
```

Fetching only gives us the metadata. With pull we can receive the actual file changes from a remote repo.

**PULL REQUEST** = Allows team members to see what changes are being proposed and to discuss them before they are merged into the main codebase.

## Chapter 11: gitignore

**gitignore** = Prevents files from being tracked in git. This is very useful for automatically generated files.

bash

```bash
touch .gitignore
git add .
git commit -m "add .gitignore"
```

### Nested gitignore:

It's fairly common to have multiple `.gitignore` files in different directories throughout a project. A nested `.gitignore` file only applies to the directory it's in and its subdirectories.

### PATTERNS:

**Wildcards `*`:** The `*` character matches any number of characters except for a slash (`/`). For example, to ignore all `.txt` files you could use:

```
*.txt
```

**Rooted patterns:** Patterns starting with a `/` are anchored to the directory containing the `.gitignore` file. For example, this would ignore a `main.py` in the root directory, but not in any subdirectories:

```
/main.py
```

**Negation:** You can negate a pattern by prefixing it with a `!`. For example, to ignore all `.txt` files except for `important.txt`:

```
*.txt
!important.txt
```

**Comments:** You can add comments to your `.gitignore` file by starting a line with `#`. For example:

```
# Ignore all .txt files
*.txt
```

**Order Matters:**

```
temp/*
!temp/instructions.md
```

Everything in the `temp/` directory would be ignored except for `instructions.md`. If the order were reversed `instructions.md` would be ignored.

### What to Ignore:

1. Ignore things that can be generated (e.g. compiled code, minified files, etc.)
2. Ignore dependencies (e.g. node_modules, venv, packages, etc.)
3. Ignore things that are personal or specific to how you like to work (e.g. editor settings)
4. Ignore things that are sensitive or dangerous (e.g. .env files, passwords, API keys, etc.)