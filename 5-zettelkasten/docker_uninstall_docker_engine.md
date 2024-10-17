### Meta
2024-10-15 12:07
**Tags:** [[docker]] [[docker_installation]]
**Status:** #pending 

### Uninstall Docker Engine
1. Uninstall the Docker Engine, CLI, containerd, and Docker compose packages:

```BASH title:script.sh
sudo apt-get purge docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin docker-ce-rootless-extras
```

2. Images, containers, volumes, or custom configuration files on your host aren’t automatically removed. To delete all images, containers, and volumes:

```BASH title:script.sh
sudo rm -rf /var/lib/docker
sudo rm -rf /var/lib/containerd
```

You must delete any edited configuration files manually.