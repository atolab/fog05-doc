# Install Eclipse fog05 from debian packages

For each Eclipse fog05 release, the respective `.deb` files are generated for Ubuntu 18.04 LTS. It also works with newer versions of Ubuntu. Those files can be found in the fog05 [release page](https://github.com/eclipse-fog05/fog05/releases) on GitHub, and are available for `x86_64` and `aarch64` architectures.


## fog05's Agent

Installing the fog05's agent can be done by simply running:

```bash
wget https://github.com/eclipse-fog05/fog05/releases/download/v0.2.1/zenoh_0.3.0-1_amd64.deb
sudo apt install ./zenoh_0.3.0-1_amd64.deb
wget https://github.com/eclipse-fog05/fog05/releases/download/v0.2.1/fog05_0.2.1-1_amd64.deb
sudo apt install ./fog05_0.2.0-1_amd64.deb
```

It will create the folder `/etc/fos` in which we can found the configuration file `agent.json` and the agent, and configures the systemd service `fos_agent` and the Zenoh systemd service `zenoh`

## Linux Plugin

Installing the Linux Plugin can be done by simply running:

```bash
wget https://github.com/eclipse-fog05/fog05/releases/download/v0.2.1/libzenoh-0.3.0-Linux.deb
sudo apt install ./libzenoh-0.3.0-Linux.deb
sudo pip3 install fog05-sdk==0.2.1 zenoh==0.3.0 yaks==0.3.0.post1
wget https://github.com/eclipse-fog05/fog05/releases/download/v0.2.1/fog05-plugin-os-linux_0.2.1-1_amd64.deb
sudo apt install ./fog05-plugin-os-linux_0.2.1-1_amd64.deb
```

After the installation the directory `/etc/fos/plugins/plugin-os-linux` is created and the plugin configuration `/etc/fos/plugins/plugin-os-linux/linux_plugin.json` is populated with the `/etc/machine-id` as nodeid value. The systemd service `fos_linux` is created.


## Network Manager (Linux Bridge) Plugin

To install the Network Manager (a.k.a. Linux Bridge) Plugin we can simply run:

```bash
wget https://github.com/eclipse-fog05/fog05/releases/download/v0.2.1/fog05-plugin-net-linuxbridge_0.2.1-1_amd64.deb
sudo apt install ./fog05-plugin-net-linuxbridge_0.2.1-1_amd64.deb
```

After the installation the directory `/etc/fos/plugins/plugin-net-linuxbridge` is created and the plugin configuration `/etc/fos/plugins/plugin-net-linuxbridge/linuxbridge_plugin.json` is populated with the `/etc/machine-id` as nodeid value. The systemd service `fos_linuxbridge` is created.


### FDUs plugin

For this user guide we show how to install the LXD plugin, the steps are similar for the others plugins.

First, install the dependencies as follows:

```bash
sudo snap install lxd
```

Then, install the plugin as follows:

```bash
wget https://github.com/eclipse-fog05/fog05/releases/download/v0.2.1/fog05-plugin-fdu-lxd_0.2.1-1_amd64.deb
sudo apt install ./fog05-plugin-fdu-lxd_0.2.1-1_amd64.deb
```

After the installation the directory `/etc/fos/plugins/plugin-fdu-lxd` is created and the plugin configuration `/etc/fos/plugins/plugin-fdu-lxd/LXD_plugin`.json is populated with the `/etc/machine-id` as nodeid value. The systemd service `fos_lxd` is created.







