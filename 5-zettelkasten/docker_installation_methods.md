### Meta
2024-10-04 12:14
**Tags:** [[dev-ops]] [[docker]] [[docker_installation]]
**Status:** #completed 

### Install using the `apt` repository
Before you install Docker Engine for the first time on a new host or machine, you need to set up the Docker repository. Afterward, you can install and update Docker from the repository.

While these packages are not part of Docker's core functionality, they must be available on Your Pop_OS 22.04 system as they are needed to import the official Docker repository smoothly into your system.

```BASH title:script.sh
sudo apt install apt-transport-https ca-certificates curl
```

1. Set up Docker's `apt` repository.

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

2. Install the Docker packages.

```BASH title:script.sh
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

3. Verify that the Docker Engine installation is successful by running the `hello-world` image.

```BASH title:script.sh
sudo docker run hello-world
```