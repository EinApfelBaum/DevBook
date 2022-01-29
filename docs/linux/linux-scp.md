---
created: 17.10.2021
tags: linux cli
parent: Linux
---

# scp - secure copy (remote file copy program)

```bash
scp -P <port_number> <source> <destination>

# remote => local
scp root@192.168.123.1:/home/remoteUser/file.txt /home/localUser/file.txt

# local => remote
scp -P 123456 /home/localUser/test.sh root@192.168.123.1:/home/remoteUser/test.sh

# Enter password.
```

---

## Resources

* [https://linux.die.net/man/1/scp](https://linux.die.net/man/1/scp)
