#gitNotes

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
