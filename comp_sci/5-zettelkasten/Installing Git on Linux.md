### Meta
- - -
- 2024-09-15 17:36
- Tags: [[snippets]] [[linux]] [[linux installations]]
- Status: #completed 

### What it looks like
- - -
```bash file:example.sh
sudo apt-get update && apt update -y
sudo add-apt-repository ppa:git-core/ppa
sudo apt update
sudo apt install git
git --version
```

### What it does
- - -
-  Downloads and installs the Git distributed version control system from the it's `ppa` directory.
- Checks the version.
