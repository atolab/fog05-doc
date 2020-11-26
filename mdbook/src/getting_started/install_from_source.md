# Install Eclipse fog05

Before getting started with Eclipse fog05 we need to install and start it

We have two possibilities for installing Eclipse fog05

- Installing from source
- Instlaling from debian packages

## Installing from source

### Pre-requisites

Eclipse fog05 core component is written in `OCaml` language, hence to build it we need a functional OCaml environment, luckily installing OCaml compiler and build system is not that complicated.

```bash
sudo apt install jq libev-dev libssl-dev m4 pkg-config rsync unzip bubblewrap -y
sh <(curl -sL https://raw.githubusercontent.com/ocaml/opam/master/shell/install.sh)
opam init -c 4.09.0
eval $(opam env)
```


After that we can install all the OCaml dependencies:


```bash
opam install dune.1.11.4 atdgen.2.0.0 conf-libev ocp-ocamlres -y
opam pin add apero-core https://github.com/atolab/apero-core.git#0.4.6 -y
opam pin add dynload-sys https://github.com/atolab/apero-core.git#0.4.6 -y
opam pin add apero-net https://github.com/atolab/apero-net.git#0.4.6 -y
opam pin add apero-time https://github.com/atolab/apero-time.git#0.4.6 -y
opam pin add zenoh-proto https://github.com/atolab/zenoh.git#0.3.0 -y
opam pin add zenoh-ocaml https://github.com/atolab/zenoh.git#0.3.0 -y
opam pin add yaks-common https://github.com/atolab/yaks-common.git#0.3.0 -y
opam pin add yaks-ocaml https://github.com/atolab/yaks-ocaml.git#0.3.0 -y
opam pin add fos-sdk https://github.com/eclipse-fog05/sdk-ocaml.git#0.2.x -y
opam pin add fos-fim-api https://github.com/eclipse-fog05/api-ocaml.git#0.2.x  -y
```

Then we need to get the [Eclipse Zenoh](http://zenoh.io) daemon, fog05 uses version `0.3.0` building instruction can be found [here](https://github.com/atolab/fog05_debs/blob/master/zenoh/generate_deb.sh)


### fog05's Agent

Now, we can clone the Eclipse fog05 agent repository. Build and install the agent as follows:

```bash
git clone https://github.com/eclipse-fog05/agent
cd agent
make
sudo make install
```

The installation creates the folder `/etc/fos` in which we can found the configuration file `agent.json` and the agent itself. It creates as well the `systemd` files for starting and stopping the service fos_agent

> **Note:** After installing the agent, it is required to install at least one of the following:
>
> - the Linux OS plugin
> - the Network Manager (Linux Bridge Plugin)
> - an FDU plugin.


### Linux OS Plugin

To install the OS plugin, we need Python3 and a set of dependencies

***pre-requisites***

```bash
sudo apt install python3 python3-dev python3-pip cmake build-essential python3-lxml
git clone https://github.com/atolab/zenoh-c -b 0.3.0 && cd zenoh && make && sudo make install && cd ..
pip3 install yaks==0.3.0.post1 zenoh==0.3.0 psutil netifaces pyangbind sphinx jinja2 packaging
git clone https://github.com/eclipse-fog05/sdk-python -b 0.2.x cd sdk-python && make && sudo make install && cd ..
```

Then we can clone and install the Linux Plugin as follows:

```bash
git clone https://github.com/eclipse-fog05/plugin-os-linux -b 0.2.x
cd plugin-os-linux
sudo make install
```

After the installation the directory `/etc/fos/plugins/plugin-os-linux` is created and the plugin configuration `/etc/fos/plugins/plugin-os-linux/linux_plugin.json` is populated with the `/etc/machine-id` as nodeid value. The systemd service `fos_linux` is created.


### The Network Manager (Linux Bridge) Plugin

To install the Network Manager (a.k.a. Linux Bridge) plugin, we need the same dependencies as the Linux OS Plugin.

***pre-requisites***

```bash
sudo apt install python3 python3-dev python3-pip cmake build-essential python3-lxml
git clone https://github.com/atolab/zenoh-c -b 0.3.0 && cd zenoh && make && sudo make install && cd ..
pip3 install yaks==0.3.0.post1 zenoh==0.3.0 psutil netifaces pyangbind sphinx jinja2 packaging
git clone https://github.com/eclipse-fog05/sdk-python -b 0.2.x cd sdk-python && make && sudo make install && cd ..
```

Then, we can clone and install the Network Manager Plugin as follows:

```bash
git clone https://github.com/eclipse-fog05/plugin-net-linuxbridge -b 0.2.x
cd plugin-os-linux
sudo make install
```

After the installation the directory `/etc/fos/plugins/plugin-net-linuxbridge` is created and the plugin configuration `/etc/fos/plugins/plugin-net-linuxbridge/linuxbridge_plugin.json` is populated with the `/etc/machine-id` as nodeid value. The systemd service `fos_linuxbridge` is created.

### The FDUs Plugin

For this user guide we show how to install the LXD plugin, the steps are similar for the others plugins.

First, we install the dependencies as follows:

```bash
sudo pip3 install pylxd
sudo snap install lxd
```

Then we clone and install the plugin:

```bash
git clone https://github.com/eclipse-fog05/plugin-fdu-lxd -b 0.2.x
cd plugin-os-linux
sudo make install
```
After the installation the directory `/etc/fos/plugins/plugin-fdu-lxd` is created and the plugin configuration `/etc/fos/plugins/plugin-fdu-lxd/LXD_plugin`.json is populated with the `/etc/machine-id` as nodeid value. The systemd service `fos_lxd` is created.


