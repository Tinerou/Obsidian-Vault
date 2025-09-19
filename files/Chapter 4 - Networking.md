### Shebang
A "shebang" is a special line at the top of a script that tells your shell which program to use to execute files.
**The format for shebang:**
```
#! interpreter [optional-arg]
```
For example in python you might use:
```
#!/usr/bin/python3
```

### Shell Configuration

Both Bash and Zsh have configuration files that run automatically each time you start a new shell session. They can be used to set up aliases, functions, and environment variables.

`.bashrc`- if you're using bash
`zshrc` - if your using zsh
### Environment Variables

**View Environment Variables:**

bash

```bash
env
```

**Set Environment Variable:**

bash

```bash
export NAME="Trey"
```

_Note: Only affects current shell session_

### PATH Variable

The PATH variable lists directories where the shell looks for executable commands.

**Adding to PATH:**

bash

```bash
export PATH="$PATH:/directory"
```

- `$PATH` references existing PATH
- `:` is the separator

**Permanent PATH Configuration:** Add `PATH="$PATH:/directory"` to your `.zshrc` or `.bashrc` file
