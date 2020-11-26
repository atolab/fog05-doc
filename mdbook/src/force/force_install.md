# FOrcE Installation

Before getting started with Eclipse fog05 orchestation we need to install and start it

We have three possibilities for installing Eclipse fog05 FOrcE:

- Install FOrcE from source
- Install FOrcE from debian packages
- Install FOrcE using a docker image


## Install FOrcE from source

We can clone the Eclipse fog05 repository and build the orchestation engine, as follows:

```bash
git clone https://github.com/eclipse-fog05/fog05 -b 0.2.x
cd fog05/src/force
make
sudo install -m 0755 /usr/local/bin
```


## Install FOrcE from debian packages

For each release `.deb` files are generated for Ubuntu 18.04 LTS, and works also with newer versions of Ubuntu. Those files can be found in the [release](https://github.com/eclipse-fog05/fog05/releases) page on GitHub, and are available for `x86_64` and `aarch64` architectures.

To install the force we can simply run:

```bash
wget https://github.com/eclipse-fog05/fog05/releases/download/v0.2.2/fog05-force_0.2.2-1_amd64.deb
sudo apt install ./fog05-force_0.2.2-1_amd64.deb
```

It will create the folder `/etc/fos` in which we can found the configuration file force.json and the force, and configures the systemd service force to start it. The configuration file contains the address of the zenoh router used by the orchestrator.


## Install FOrcE using a docker image

If you have docker and docker-compose enable in you machine you can download the `docker-compose.yaml` file, as follows:

```bash
wget https://raw.githubusercontent.com/eclipse-fog05/fog05/0.2.x/src/force/docker-compose.yaml

```

And deploy it using:

```bash
docker stack deploy -c docker-compose.yaml force
```
