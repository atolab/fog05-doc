# Start Eclipse fog05 FOrcE

- If Eclipse fog05 FOrcE was installed by source if shall be started by hand:

```bash
$ ZENOH=<ip address of a dedicated zenoh router> force
```

- If Eclipse fog05 FOrcE was installed by `.deb` file it can be started using the systemd

To start:

```bash
$ sudo systemctl start force
```

To stop FOrcE do:

```bash
$ sudo systemctl stop force
```

**Interaction is described in fosctl usage.**

Logs can be checked using `journalctl` and, `journalctl -u force -f`
