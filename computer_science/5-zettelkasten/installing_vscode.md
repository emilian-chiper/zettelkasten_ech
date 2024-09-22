### Meta
2024-09-17 21:16
**Tags:** [[linux_fundamentals]] [[linux_installations]]
**State:** #completed 

### What it looks like
```bash
sudo apt-get update && sudo apt updgrade -y
wget -O code-latest.deb 'https://code.visualstudio.com/sha/download?build=stable&os=linux-deb-x64'
sudo apt install ./code-latest.deb
rm code-latest.dev
```

### What it does
- Downloads and installs the VSCode text editor on Debian-based distros such as Ubuntu and its many flavors.
- Retrieves the `.deb` package from the web using `wget`.
- Uses the `apt` package manager.

### How it does it
- [VSCode Installation](https://www.theodinproject.com/lessons/foundations-text-editors#vscode-installation)
