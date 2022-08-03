---
created: 17.10.2021
tags: linux cli ssh
parent: Linux
---

# ssh - OpenSSH SSH client

## Generate a public/private key

```bash
# Generating public/private rsa key pair.
ssh-keygen -b 4096

# Test if the passphrase is correct
ssh-keygen -y -f ~/.ssh/id_rsa_file

# Copy public key to remote
ssh-copy-id -i .ssh/key_rsa.pub <USER>@<REMOTE IP>
```

## ssh into remote

```bash
ssh -p <port> -i <private key filename> <user>@<remote_IP>

ssh -p 123 -i /home/myHome/.ssh/myKey root@192.168.1.1

# Enter password

# Execute command on remote machine
sudo ssh -p 123 root@192.168.1.1 "cd /home/remoteUser; ls"
```

---

## Resources

* [https://linux.die.net/man/1/ssh](https://linux.die.net/man/1/ssh)
