# Charmed Kafka ROCK

[![Container Registry](https://img.shields.io/badge/Container%20Registry-published-blue)](https://github.com/canonical/charmed-kafka-rock/pkgs/container/charmed-kafka)
[![Release](https://github.com/canonical/charmed-kafka-rock/actions/workflows/publish.yaml/badge.svg)](https://github.com/canonical/charmed-kafka-rock/actions/workflows/publish.yaml)

This repository contains the packaging metadata for creating a Charmed Kafka ROCK. This ROCK image is based on the [Charmed Kafka Snap](https://github.com/canonical/charmed-kafka-snap)  

For more information on ROCKs, visit the [rockcraft Github](https://github.com/canonical/rockcraft). 

## Building the ROCK
The steps outlined below are based on the assumption that you are building the ROCK with the latest LTS of Ubuntu.  
If you are using another version of Ubuntu or another operating system, the process may be different. 
To avoid any issue with other operating systems you can simply build the image with [multipass](https://multipass.run/):
```bash
sudo snap install multipass
multipass launch 22.04 -n rock-dev
multipass shell rock-dev
``` 

### Clone Repository
```bash
git clone https://github.com/canonical/charmed-kafka-rock.git
cd charmed-kafka-rock
```
### Installing Prerequisites
```bash
sudo snap install rockcraft --edge --classic
sudo snap install docker
sudo snap install lxd
sudo snap install skopeo --edge --devmode
```
### Configuring Prerequisites
```bash
sudo usermod -aG docker $USER 
sudo lxd init --auto
```
*_NOTE:_* You will need to open a new shell for the group change to take effect (i.e. `su - $USER`)
### Packing and Running the ROCK
```bash
rockcraft pack
sudo skopeo --insecure-policy copy oci-archive:charmed-kafka*.rock docker-daemon:<username>/charmed-kafka:<tag>
docker run --rm -it <username>/charmed-kafka:<tag>
```
## License
The Charmed Kafka ROCK is free software, distributed under the Apache
Software License, version 2.0. See
[LICENSE](https://github.com/canonical/charmed-kafka-rock/blob/main/LICENSE)
for more information.
