## Chapter 6: Packages

### Package Managers

A package manager is a software tool that helps you install other software. 
Its primary functions include:
- Downloading software from official sources
- Installing software
- Updating software
- Removing software
- Managing dependencies

Examples of these are:
**APT (Ubuntu)
Brew (MacOS)**

### How does package manager work?

**When you type a command like `brew install neovim`, the package manager will:**
1. Check to see if the package is already installed.
2. If it's not installed, it will download the package from a repository.
3. It will install the package on your computer.
4. It will install any dependencies that the package needs to run.
5. It will (hopefully) add the package to you PATH if it should be there.

**You can see where your package manager installed a program on your filesystem using `which`:**
```bash
which <program>
```

### Webi

Webi lets you install command line tools directly from the web, with no need for a local command line tool like `apt` or `brew`. You don't need to install webi itself at all, instaead you just run a shell command that downloads and runs the tool's official installer script.

To try this out we downloaded lsd (LSDeluxe) a more modern and feature-rich version of `ls`.
**lsd (LSDeluxe) download
```bash
curl -sS https://webi.sh/lsd | sh; \
source ~/.config/envman/PATH.env
```


### lsd (LSDeluxe)

```bash
lsd path/to/directory
```

**Flags:**
- `--tree` - will show a nice tree file structure. Much like many GUI's
- `--classic` - classic`ls`/simplified look.