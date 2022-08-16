---
created: 17.10.2021
tags: linux cli ssh server
parent: Linux
---

# SSH - OpenSSH SSH client (remote login program)

The `id_type.pub` file is for the public key. This is the part you have to share with remote devices you want to connect to via an SSH key. On those remote devices, the public key will be saved in the `authorized_keys` file.

The `authorized_keys` file is for public keys of all devices that are allowed to connect to the device via an SSH key. The format of this file is one key per line. It is not possible to connect to a remote device via an SSH key, unless the public key is in this file.

`known_hosts` - This file is needed when you connect to another device. Every remote device has a unique fingerprint that is saved in this file.

## SSH logs

```bash
journalctl -t sshd
```

## Generate a public/private key

```bash
# Generating public/private rsa key pair.
ssh-keygen -b 4096 -f ~/.ssh/<ssh_key_filename>

# Test if the passphrase is correct
ssh-keygen -y -f ~/.ssh/<ssh_key_filename>

# Copy public key to remote
ssh-copy-id -i .ssh/<ssh_key_filename>.pub <USER>@<REMOTE IP>
```

## Connect to remote via SSH

```bash
ssh -p <port> -i <shh_key_filename> <user>@<remote_IP>

ssh -p 123 -i /home/myHome/.ssh/myKey root@192.168.1.1
# Enter passphrase

# Execute command on remote machine
sudo ssh -p 123 root@192.168.1.1 "cd /home/remoteUser; ls"
```

## Configuration

After the configuration in `/etc/ssh/sshd_config` is changed, restart sshd.

```bash
sudo systemctl restart sshd
```

### Deactivate SSH root login

If you want to prohibit direct SSH root login under Debian, you need at least one other user besides the root user who is allowed to log in to the server.

> :warning: If you have not created another user, you lock yourself out of the system! :warning:

Change in the `/etc/ssh/sshd_config` the property `PermitRootLogin` to `no`.

```bash
PermitRootLogin     no
```

### Deactivating password authentication

> :warning: Do not disable password authentication, if you are using a password to connect to your server. Otherwise, you will no longer be able to connect to your server. :warning:

Change in the `/etc/ssh/sshd_config` the property `PasswordAuthentication` to `no`.

```bash
PasswordAuthentication     no
```

---

## Resources

* [https://linux.die.net/man/1/ssh](https://linux.die.net/man/1/ssh)
* [https://community.hetzner.com/tutorials/howto-ssh-key]([https://](https://community.hetzner.com/tutorials/howto-ssh-key))
