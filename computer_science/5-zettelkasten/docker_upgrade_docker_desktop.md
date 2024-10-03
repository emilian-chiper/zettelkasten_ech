### Meta
2024-10-03 22:51
**Tags:** [[CI-CD]] [[docker]] [[docker_installation]]
**State:** #pending 

### Upgrade Docker Desktop
Once a new version for Docker Desktop is released, the Docker UI shows a notification. You need to download the new package each time you want to upgrade Docker Desktop and run:

```BASH title:script.sh
sudo apt-get install ./docker-desktop-<arch>.deb
```

Don't forget to substitute `<arch>` with the architecture you want.