
## Start Eclipse fog05

The Eclipse fog05 installed components can be started and stopped using systemd, as follows:


### To start

```bash
sudo systemctl start zenoh
sudo systemctl start fos_agent
sudo systemctl start fos_linux
sudo systemctl start fos_linuxbridge
sudo systemctl start fos_lxd
```
### To stop

```bash
sudo systemctl stop fos_lxd
sudo systemctl stop fos_linuxbridge
sudo systemctl stop fos_linux
sudo systemctl stop fos_agent
sudo systemctl stop zenoh
```

Logs can be checked using:

```bash
journalctl
journalctl -u <fog05 component> -f
```

