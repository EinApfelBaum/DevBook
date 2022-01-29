---
created: 17.10.2021
tags: docker
---

# Enable remote API for dockerd

## Overview

The best way to include the required startup options without editing the systemd unit file in place is to use a systemd drop-in file.

## Resolution

After completing these steps, you will have enabled the remote API for dockerd, without editing the systemd unit file in place:

Create a file at `/etc/systemd/system/docker.service.d/startup_options.conf` with the below contents:

```config
# /etc/systemd/system/docker.service.d/override.conf
[Service]
ExecStart=
ExecStart=/usr/bin/dockerd -H fd:// -H tcp://0.0.0.0:2376
```

> Note: The -H flag binds dockerd to a listening socket, either a Unix socket or a TCP port. You can specify multiple -H flags to bind to multiple sockets/ports. The default -H fd:// uses systemd's socket activation feature to refer to /lib/systemd/system/docker.socket.

Reload the unit files

```bash
sudo systemctl daemon-reload
```

Restart the docker daemon with new startup options:

```bash
sudo systemctl restart docker.service
```


Ensure that anyone that has access to the TCP listening socket is a trusted user since access to the docker daemon is root-equivalent.

https://docs.docker.com/engine/security/

---

## Resources

* [https://success.docker.com/article/how-do-i-enable-the-remote-api-for-dockerd](https://success.docker.com/article/how-do-i-enable-the-remote-api-for-dockerd)
