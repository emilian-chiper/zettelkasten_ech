### Meta
- - -
- 2024-09-15 17:26
- Tags: [[snippets]] [[linux]] [[linux installations]]
- Status: #completed 

### What it looks like
- - -
```bash file:example.sh
sudo apt-get update && apt update -y
wget -O code-latest.deb 'https://code.visualstudio.com/sha/download?build=stable&os=linux-deb-x64'
sudo apt install ./code-latest.deb
rm code-latest.dev
code .
```

### What it does
- - -
- Downloads and installs the VSCode text editor on Debian-based distros such as Ubuntu and its many flavors.
- Retrieves the `.deb` package from the web using `wget`.
- Uses the `apt` package manager.
