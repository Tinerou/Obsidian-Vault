#gitNotes
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