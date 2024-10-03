### Meta
2024-10-03 22:24
**Tags:** [[CI-CD]] [[docker]] [[docker_installation]]
**State:** #completed 

### Install Docker Desktop
Recommended approach to install Docker Desktop on Ubuntu:
1. Set up Docker's package repository.

```BASH title:script.sh
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

2. Downloand the latest DEB package.
3. Install the package with apt. Substitute `<arch>` with the architecture you want.

```BASH title:script.sh
sudo apt-get update
sudo apt-get install ./docker-desktop-<arch>.deb
```

**Note:** At the end of the installation process, `apt` displays an error due to installing a downloaded package. You can ignore this error message.

By default, Docker Desktop is installed at `/opt/docker-desktop`.

There are a few post-install configuration steps done through the post-install script contained in the deb package.

The post-install script:
- Sets the capability on the Docker Desktop binary to map privileged ports and set resource limits.
- Adds a DNS name for Kubernetes to `/etc/hosts`.
- Creates a symlink for `usr/local/bin/com.docker.cli` to `/user/bin/docker`. This is because the classic Docker CLI is installed at `/usr/bin/docker`. The Docker Desktop installer also installs a Docker CLI binary that includes cloud-integration capabilities and is essentially a wrapper for the Compose CLI, at `/usr/local/bin/com.docker.cli`. The symlink ensures that the wrapper can access the classic Docker CLI.