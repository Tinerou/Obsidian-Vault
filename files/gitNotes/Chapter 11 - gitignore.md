#gitNotes 


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