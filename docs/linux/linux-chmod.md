---
created: 17.10.2021
tags: linux cli
parent: Linux
---

# chmod - change file mode bits

| access |
| ------ | ------ |
| u      | user   |
| g      | group  |
| o      | others |
| a      | all    |

| file mode bits |
| -------------- | ---------- |
| r              | read       |
| w              | write      |
| x              | executable |

`chmod [ugoa] [-+=] [rwxXst]`

User write access
`chmod u+w <filename>`

Group write access
`chmod g+w <filename>`

All write access
`chmod a+w <filename>`

---

## Resources

* [https://linux.die.net/man/1/chmod](https://linux.die.net/man/1/chmod)
