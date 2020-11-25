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

After installing the agent is required to install at least the OS, Network Manager and one FDU plugin.




