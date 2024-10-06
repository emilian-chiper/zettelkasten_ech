### Meta
2024-10-04 13:30
**Tags:** [[docker]] [[docker_engine]] [[docker_engine_security]]
**Status:** #pending 

### How it works
Rootless mode executes the Docker daemon and containers inside a user namespace. This is very similar to `userns-remap` mode, except that with `userns-remap` mode, the daemon itself is running with root privileges, whereas in rootless mode, both the daemon and the container are running without root privileges.

Rootless mode does not use binaries with `SETUID` bits or file capabilities, except `newuidmap` and `newgidmap`, which are needed to allow multiple UIDs/GIDs to be used in the user namespace.

### Prerequisites
- You must install `newuidmap` and `newgidmap` on the host. These commands are provided by the `uidmap` package on most distros.
- `/etc/subuid` and `/etc/subgid` should contain at least 65,536 subordinate UIDs/GIDs for the user.

```BASH title:script.sh
id -u
1001
whoami
testuser
grep ^$(whoami): /etc/subuid
testuser:231072:65536
grep ^$(whoami): /etc/subgid
testuser:231072:65536
```

### Ubuntu
Install `dbus-user-session` package if not installed. Run `sudo apt-get install -y dbus-user-session` and relogin.

Install `uidmap` package if not installed. Run `sudo apt-get install -y uidmap`.

If running in a terminal where the user was not directly logged into, you will need to install `system-container` with `sudo apt-get install -y systemd-container`, then switch to TheUser with the command `sudo machinectl shell TheUser@`.

`overlay` storage driver is enabled by default.

If you install `docker-ce-rootless-extras` using the deb package(`apt-get install docker-ce-rootless-extras`), then the AppArmor profile for `rootlesskit` is already bundled with the `apparmor` deb package. With this installation method, you don't need to add any manual AppArmor configuration.

### Known limitations
Only the following storage drivers are supported:
- `overlay2` (only running with kernel)
- `fuse-overlayfs` (only if running with kernel 4.18 or later, and `fuse-overlayfs` is installed).
- `btrfs` (only if running with kernel 4.18 or later, or `~/.local/share/docker` is mounted with `user_subvol_rm_allowed` mount options)
- `vfs`

Cgroup is supported only when running with cgroup v2 and systemd.

Following features are not supported:
- AppArmor
- Checkpoint
- Overlay network
- Exposing SCTP ports

To use the `ping` command, see [Routing ping packets]([[docker_routing_ping_packets]]).

To expose privileged TCP/UDP ports (<1024), see [Exposing privileged ports]([[docker_exposing_privileged_ports]]).

`IPAddress` shown in `docker inspect` is namespaced inside RootlessKit's network namespace. This means the IP address is not reachable from the host without `nsenter`-ing into the network namespace.

Host network (`docker run --net=host`) is also namespaced inside RootlessKit.

NFS mounts as the docker 'data-root' is not supported. This limitation is not specific to rootless mode.

### Install
**Note?**
If the system-wide Docker daemon is already running, consider disabling it:

```BASH title:script.sh
sudo systemctl disable --now docker.service docker.socket
sudo rm /var/run/docker.sock
```

Should you choose not to shut down the `docker` service and socket, you will need to use the `--force` parameter in the next section. There are no known issues, but until you shutdown and disable you're still running rootful Docker.

#### Using packages (rpb/deb)
If you installed Docker 20.10 or later with rpm/deb packages, you should have `docker-rootless-setuptool.sh` in `/usr/bin`.

Run `dockerd-rootless-setuptool.sh install` as a non-root user to set up the daemon:

```BASH title:script.sh
dockerd-rootless-setuptool.sh install
[INFO] Creating /home/testuser/.config/systemd/user/docker.service
...
[INFO] Installed docker.service successfully.
[INFO] To control docker.service, run: `systemctl --user (start|stop|restart) docker.service`
[INFO] To run docker.service on system startup, run: `sudo loginctl enable-linger testuser`

[INFO] Make sure the following environment variables are set (or add them to ~/.bashrc):

export PATH=/usr/bin:$PATH
export DOCKER_HOST=unix:///run/user/1000/docker.sock
```

If `dockerd-rootless-setuptool.sh` is not present, you may need to install the `docker-ce-rootless-extras` package manually, e.g.,

```BASH title:script.sh
sudo apt-get install -y docker-ce-rootless-extras
```

### Uninstall
To remove the systemd service of the Docker daemon, run `docker-rootless-setuptool.sh uninstall`:

```BASH title:script.sh
dockerd-rootless-setuptool.sh uninstall
+ systemctl --user stop docker.service
+ systemctl --user disable docker.service
Removed /home/testuser/.config/systemd/user/default.target.wants/docker.service.
[INFO] Uninstalled docker.service
[INFO] This uninstallation tool does NOT remove Docker binaries and data.
[INFO] To remove data, run: `/usr/bin/rootlesskit rm -rf /home/testuser/.local/share/docker`
```

Unset environment variables PATH and DOCKER_HOST if you have added them to `~/.bashrc`.

To remove the data directory, run `rootleskit rm -rf ~/.local/share/docker`.

To remove the binaries, remove `docker-ce-rootless-extras` package if you installed docker with package managers.