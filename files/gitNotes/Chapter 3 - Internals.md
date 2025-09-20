#gitNotes
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
