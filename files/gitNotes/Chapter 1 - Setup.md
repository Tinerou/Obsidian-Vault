#gitNotes
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
