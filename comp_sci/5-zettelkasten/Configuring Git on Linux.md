### Meta
- - -
- 2024-09-15 17:39
- Tags: [[snippets]] [[linux]] [[git basics]]
- Status: #completed 

### What it looks like
- - -
```bash file:example.sh
git config --global user.name "Your Name"
git config --global user.email "yourname@example.com"
git config --global init.defaultBranch main
git config --global color.ui auto
git config --global pull.rebase false
git config --get user.name
git config --get user.email
```

### What it does
- - -
-  Configures credentials.
- Changes the default branch to `main`.
- Enables colorful output with `git`.
- Sets the default branch reconciliation behavior to merging.
- Verifies credentials.
