---
created: 12.10.2021
tags: synology cli
---

# Commands for handling DSM Services

> Note that you need elevated permissions to issue these commands, use `sudo -i` for simplicity.

```bash
synoservicecfg –list
synoservice –status
synoservicecfg –stop <service>
synoservicecfg –hard-stop <service>
synoservicecfg –start <service>
synoservicecfg –hard-start <service>
synoservice –restart <service>
synoservicectl –restart <service>[/code]
```

For example, this will restart WebStation altogether:

```bash
synoservice --restart pkgctl-WebStation
```

or Docker:

```bash
synoservice --restart pkgctl-Docker
```

---

## Resources

* [https://tech.setepontos.com/2018/03/25/control-synology-dsm-services-via-terminal-ssh/](https://tech.setepontos.com/2018/03/25/control-synology-dsm-services-via-terminal-ssh/)
