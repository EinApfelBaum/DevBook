---
created: 22.10.2021
tags: linux
parent: Linux
---

# Clean up linux

```bash
sudo apt-get autoremove
sudo apt-get autoclean

# clean trash of root
sudo rm -rf /root/.local/share/Trash/files/*

# clean docker
docker system prune --all
```

---

## Resources

* [https://docs.docker.com/engine/reference/commandline/system_prune/](https://docs.docker.com/engine/reference/commandline/system_prune/)

