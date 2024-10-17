### Meta
2024-10-15 12:13
**Tags:** [[docker]] [[docker_installation]] [[docker_post-installation_steps]]
**Status:** #completed 

### Manage Docker as a non-root user
The Docker daemon binds to a Unix socket, not a TCP port. By default, it’s the `root` user that owns the Unix socked, and other users can only access it using `sudo`. The docker daemon always runs as the `root` user.

If you don’t want to preface the `docker` command with `sudo`, create a Unix group called `docker` and add users to it. When the Docker daemon starts, it creates a Unix socket accessible by members of the `docker` group. On some Linux distros, the system automatically creates this group when installing Docker Engine using a package manager. In this case, there’s no need to manually create the group.

**❗ Warning!**
The `docker` group grants root-level privileges to the user. For details on how this impacts security in your system, see [[[[docker_daemon_attack_surface|Docker Daemon Attack Surface]].

**ℹ️ Note**
To run Docker without root privileges, see [[docker_rootless_mode|Run the Docker daemon as a non-root user (Rootless mode)]].

To create the `docker` group and add your user:

1. Create the `docker` group:
```BASH title:script.sh
sudo groupadd docker
```

2. Add your user to the `docker` group:
```BASH title:script.sh
sudo usermod -aG docker $USER
```

3. Log out and log back in so that your group membership is re-evaluated.
	If you’re running Linux in a virtual machine, it may be necessary to restart the VM for changes to take effect.

	You can also run the following command to activate the changes to groups:
```BASH title:script.sh
newgrp docker
```

4. Verify that you can run `docker` commands without `sudo`:
```BASH title:script.sh
docker run hello-world
```

This command downloads a test image and runs it in a container. When the container runs, it prints a message and exits.

If you initially ran Docker CLI commands using `sudo` before adding your user to the `docker` group, you may see the following errror:
```BASH title:scri.sh
WARNING: Error loading config file: /home/user/.docker/config.json -
stat /home/user/.docker/config.json: permission denied
```

This error indicates that the permission settings for the `~/.docker` directory are incorrect due to having used the `sudo` command earlier.

To fix this problem, either remove the `~/.docker` directory (it’s recreated automatically, but any custom settings are lost), or change its ownership and permissions using the following commands:
```BASH title:script.sh
sudo chown "$USER":"$USER" /home/"$USER"/.docker -R
sudo chmod g+rwx "$HOME/.docker" -R
```