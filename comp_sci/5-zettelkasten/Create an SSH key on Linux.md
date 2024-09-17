### Meta
- - -
- 2024-09-15 17:47
- Tags: [[snippets]] [[linux]] [[git basics]]
- Status: #completed 

### What it looks like
- - -
```bash file:example.sh
ls ~/.ssh/id_ed25519.pub
ssh-keygen -t ed25519
cat ~/.ssh/id_ed25519.pub
ssh -T git@github.com
```

### What it does
- - -
-  Check for an existing `Ed25519.pub` SSH key already installed.
- Creates a new SSH key. When prompted for a location and password, press `Enter` or specify these parameters explicitly.
- Displays the content of the SSH key in console.
- Tests the SSH connection.
