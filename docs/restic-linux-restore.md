---
created: 2021121201
tags: restic backup linux
---

# restic - Restore using mount¶

Browsing your backup as a regular file system is also very easy. First, create a mount point such as `/mnt/restic` and then use the following command to serve the repository with FUSE:

```bash
$ mkdir /mnt/restic
$ restic -r /srv/restic-repo mount /mnt/restic
enter password for repository:
Now serving /srv/restic-repo at /mnt/restic
When finished, quit with Ctrl-c or umount the mountpoint.
```

---

## Resources

* [https://restic.readthedocs.io/en/stable/050_restore.html](https://restic.readthedocs.io/en/stable/050_restore.html)
