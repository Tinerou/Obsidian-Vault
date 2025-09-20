#gitNotes
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