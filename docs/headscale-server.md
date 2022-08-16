---
created: 11.08.2022
tags: server headscale
---

# Headscale - a selfhosted tailscale

## Logs

```bash
sudo journalctl -t headscale
```

## Directories

* Executable - `/usr/local/bin/headscale`
* Configuration - `/etc/headscale` - `/etc/headscale/config.yaml`
* Database, and other variable data (like certificates) - `/var/lib/headscale`

## Commands

* Start headscale `sudo headscale serve`
* List nodes `sudo headscale nodes list`
* Connect client `sudo tailscale up --login-server http://<my server>:8080`

## Hints

```bash
useradd \
    --create-home \
    --home-dir /var/lib/headscale/ \
    --system \
    --user-group \
    --shell /sbin/nologin \
    headscale

    # Debian: /sbin/nologin
    # Ubuntu: /usr/bin/nologin
```

Note: If your OS does not provide `/sbin/nologin`, you can set the shell to a NOOP command such as `/bin/false`.

## Tailscale client in LXC

These are steps how to enable TUN/TAP on Proxmox LXC containers:

1. Make sure your container is PRIVILEGED, if not, then make a backup of the container, then restore it and check “Privileged Container”.
2. Shutdown container and edit its configuration file located under /etc/pve/lxc/CTID.conf (CTID is the ID of your container)
3. Add following lines at the end of file:

    ```config
    lxc.cgroup.devices.allow: c 10:200 rwm
    lxc.hook.autodev: sh -c “modprobe tun; cd ${LXC_ROOTFS_MOUNT}/dev; mkdir net; mknod net/tun c 10 200; chmod 0666 net/tun”
    ```

4. Save configuration file and start the container.
5. Make sure TUN is enabled by running following command:
`cat /dev/net/tun`
This should output the following:
`cat: /dev/net/tun: File descriptor in bad state`
Now you can run VPN.

---

## Resources

* [Tailscale client in LXC](https://discuss.linuxcontainers.org/t/no-dev-net-tun-inside-lxc-container/8344/13)
