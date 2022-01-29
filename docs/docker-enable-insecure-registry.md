---
created: 17.10.2021
tags: docker registry
---

# Enable insecure registry

```bash
  sudo nano /etc/docker/daemon.json
```

## If the file does not exist, create it and insert

```json
  {
    "insecure-registries" : ["<IP>:<PORT>"]
  }
```

## Restart docker

```bash
sudo systemctl restart docker
```
