---
created: 22.10.2021
tags: linux flatpak
parent: Linux
---

# Install flatpak dbeaver extension

To create a database dump/backup you need to install an extension to load the specific client library.

```bash
# mmaradb
flatpak install flathub io.dbeaver.DBeaverCommunity.Client.mariadb

# postgres
flatpak install flathub io.dbeaver.DBeaverCommunity.Client.pgsql
```

---

## Resources

* [https://github.com/dbeaver/dbeaver/issues/5008](https://github.com/dbeaver/dbeaver/issues/5008)
