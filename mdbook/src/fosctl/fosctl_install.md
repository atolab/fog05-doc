# Install fosctl

Eclipse fog05 command line `fosctl` can be installed both for source and from its debian package

## Install from source

Eclipse fog05 `fosctl` is written in `rust`, hence to build it from source you need a functional rust environment.

Installing the rust environment is quite trival:

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs -o /tmp/rust.sh && chmod +x /tmp/rust.sh
/tmp/rust.sh --default-toolchain nightly -y
```

Once we have our rust environment we need to clone the Eclipse fog05 repository and to build `fosctl`

```bash
git clone https://github.com/eclipse-fog05/fog05 -b 0.2.x
cd src/utils/fosctl
make
sudo install -m 0755 ./fosctl /usr/local/bin/
```

## Install from debian package

It is sufficient to download the debian package from fog05's release page and install it.

```bash
wget https://github.com/eclipse-fog05/fog05/releases/download/v0.2.2/fog05-fosctl_0.2.2-1_amd64.deb
sudo apt install ./fog05-fosctl_0.2.2-1_amd64.deb
```
