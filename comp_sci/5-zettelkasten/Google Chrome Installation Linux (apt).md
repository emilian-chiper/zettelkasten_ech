### Meta
- - -
- 2024-09-13 23:26
- Tags: [[snippets]] [[linux]] [[linux installations]]
- Status: #pending

### What it looks like
- - -
```bash file:example.sh
sudo apt-get update && apt update -y
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo apt install ./google-chrome-stable_current_amd64.deb
rm google-chrome-stable_current_amd64.deb
```

### What it does
- - -
-  Downloads and installs the Google Chrome web browser on Debian-based distros such as Ubuntu and its many flavors.
- Retrieves the `.deb` package from the web using `wget`.
- Uses the `apt` package manager to install
