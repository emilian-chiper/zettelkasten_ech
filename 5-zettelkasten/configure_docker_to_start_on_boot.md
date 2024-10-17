### Meta
2024-10-15 12:27
**Tags:** [[docker]] [[docker_installation]] [[docker_post-installation_steps]]
**Status:** #completed

### Configure Docker to start on boot with systemd
Many modern Linux distros use systemd to manage which services to start when the system boots. On Debian and Ubuntu, the Docker service starts on boot by default. To automatically start Docker and containerd on boot for other Linux distros using systemd, run the following commands:

```BASH title:script.sh
sudo systemctl enable docker.service
sudo systemctl enable containerd.service
```

To stop this behavior, use `disable` instead.

```BASH title:script.sh
sudo systemctl disable docker.service
sudo systemctl disable containerd.service
```

You can use systemd unit files to configure the Docker service on startup, for example to add an HTTP proxy, set a different directory or partition for the Docker runtime files, or other customizations. For example, see [[docker_configure_daemon_for_proxy_use|Configure the daemon to use a proxy]].