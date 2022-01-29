---
created: 17.10.2021
tags: linux cli
parent: Linux
---

# ssh - OpenSSH SSH client (remote login program)

```bash
ssh -p <port> <user>@<remote_IP>

ssh -p 123 root@192.168.1.1

# Enter password

# Execute command on remote machine
sudo ssh -p 123 root@192.168.1.1 "cd /home/remoteUser; ls"
```

---

## Resources

* [https://linux.die.net/man/1/ssh](https://linux.die.net/man/1/ssh)
