---
created: 12.10.2021
tags: docker cli cheatSheet
parent: Cheat sheets
---

# Docker cli commands

```bash
# This one is particularly interesting, removes all the images that are not tagged `<none>`
docker rmi $(docker images -q -f dangling=true) -- force


# It is like the above command, only with grep
docker images | grep SEARCH_STRING | awk '{print $3}' | sort -u | xargs docker rmi --force

# List all containers, includes also detached containers
docker ps -a
```
