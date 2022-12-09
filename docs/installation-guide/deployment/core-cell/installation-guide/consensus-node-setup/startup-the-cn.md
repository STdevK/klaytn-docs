# Startup the CN

## CN Start/Stop <a href="#cn-start-stop" id="cn-start-stop"></a>

You can start/stop the Klaytn service with the following `systemctl` command.

**Note**: This requires root privileges.

**start**

```bash
$ systemctl start kcnd.service

```

**stop**

```bash
$ systemctl stop kcnd.service

```

**status**

```bash
$ systemctl status kcnd.service

```

## Troubleshooting <a href="#troubleshooting" id="troubleshooting"></a>

If you meet the following error,

```bash
Failed to start kcnd.service: Unit not found.
```

reload the systemd manager configuration with the following command.

```bash
$ systemctl daemon-reload
```