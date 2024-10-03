### Meta
2024-10-03 22:32
**Tags:** [[CI-CD]] [[docker]] [[docker_installation]]
**State:** #completed 

### Launch Docker Desktop
Open a terminal and run:
```BASH title:script.sh
systemctl --user start docker-desktop
```

When Docker Desktop starts, it creates a dedicated [context]([[docker_contexts]]) that the Docker CLI can use as a target and sets it as the current context in use. This is to avoid a clash with a local Docker Engine that may be running on the Linux host and using the default context. On shutdown, Docker Desktop resets the current context to the previous one.

The Docker Desktop installer updates Docker Compose and the Docker CLI binaries on the host. It installs Docker Compose V2 and gives users the choice to link it as `docker-compose` from the settings panel. Docker Desktop installs the new Docker CLI binary that includes cloud-integration capabilities in `/usr/local/bin/com.docker.cli` and creates a symlink to the classic Docker CLI at `/usr/local/bin`.

After you've successfully installed Docker Desktop, you can check the versions of these binaries by running the following commands:

```BASH title:script.sh
docker compose version

docker --version

docker version
```

To enable Docker desktop to start on sign in, open a terminal and run:

```BASH title:script.sh
systemctl --user enable docker-desktop
```

To stop Docker Desktop, open a terminal and run:

```BASH title:script.sh
systemctl --user stop docker-desktop
```