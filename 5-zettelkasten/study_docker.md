### Meta
2024-10-03 19:51
**Tags:**
**Status:** #pending 

### Install Docker Engine on Ubuntu
**Prerequisites**
- Firewall limitations
	- If you use `ufw` or `firewalld` to manage firewall settings, be aware that when you expose container ports using Docker, these ports bypass your firewall rules.
	- Docker is only compatible with `iptables-nft` and `iptables-legacy`. Firewall rules created with `nft` are not supported on a system with Docker installed. Make sure that any firewall rulesets you use are created with `iptables` or `ip6tables`, and that you add them to the `DOCKER-USER` chain. See [docker packet filtering and firewalls]([[docker_packet_filtering_and_firewalls]])
- OS requirements
	- Ubuntu Noble 24.04 (LTS)
	- Ubuntu Jammy 22.04 (LTS)
	- Ubuntu Focal 20.04 (LTS)
	- Docker Engine for Ubuntu is compatible with `x86_64` (or `amd64`), `armfh`, `arm64`, `s390x`, and `ppc64le` (`ppc64el`) architectures.