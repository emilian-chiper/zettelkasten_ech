### Meta
2024-10-04 11:59
**Tags:** [[dev-ops]] [[docker]] [[docker_installation]]
**Status:** #completed 

### Prerequisites
#### Firewall limitations
**Warning**
Before you install Docker, make sure you consider the following security implications and firewall incompatibilities.
- If you use `ufw` or `firewalld` to manage firewall settings, be aware that when you expose container ports using Docker, these ports bypass you firewall rules. For more info, see [Docker and ufw]().
- Docker is only compatible with `iptables-nft` and `iptables-legacy`. Firewall rules created with `nft` are not supported on a system with Docker installed. Make sure that any firewall rulesets you use are created with `iptables` or `ip6tables`, and that you add them to the `DOCKER-USER` chain, see [Packet filtering and firewalls].

#### OS requirements
To install Docker Engine, you need to 64-bit version of one of these Ubuntu versions:
- Ubuntu Noble 24.04 (LTS)
- Ubuntu Jammy 22.04 (LTS)
- Ubuntu Focal 20.04 (LTS)

Docker Engine for Ubuntu is compatible with `x86_64` (or `amd64`), `armhf`, `arm64`, `s390x`, and `ppc64le` (`ppc64el`) architectures.

#### Uninstall old versions
Before you can install Docker Engine, you need to uninstall any conflicting packages.

Distro maintainers provide unofficial distributions of Docker packages in APT. You must uninstall these packages before you can install the official version of Docker Engine.
The unofficial packages to uninstall are:
- `docker.io`
- `docker-compose`
- `docker-compose-v2`
- `docker-doc`
- `podman-docker`

Moreover, Docker Engine depends on `containerd` and `runc`. Docker Engine bundles these dependencies as one bundle: `containerd.io`. If you have installed `containerd` or `runc` previously, uninstall them to avoid conflicts with the versions bundled with Docker Engine.

Run the following command to uninstall all conflicting packages:

```BASH title:script.sh
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
```

`apt-get` might report that you have none of these packages installed.

Images, containers, volumes, and networks stored in `var/lib/docker` aren't automatically removed when you uninstall Docker. If you want to start with a clean installation, and prefer to clean up existing data, read the [uninstall Docker Engine]([[docker_uninstall_docker_engine]]) section.