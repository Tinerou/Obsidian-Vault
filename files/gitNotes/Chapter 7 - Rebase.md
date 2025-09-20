#gitNotes

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