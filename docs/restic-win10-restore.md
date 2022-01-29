---
created: 2021121201
tags: restic backup win
---

# restic - Restore on Win 10

1. download restic repo
2. unzip
3. view snapshots
`restic.exe -r .\DockerVolumes\ snapshots`

4. restore a specific snapshot
`restic -r .\DockerVolumes restore 9794275e --target .\temp\`

---

## Resources

* [https://restic.readthedocs.io/en/stable/050_restore.html](https://restic.readthedocs.io/en/stable/050_restore.html)
