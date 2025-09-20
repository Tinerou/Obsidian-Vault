#gitNotes 

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