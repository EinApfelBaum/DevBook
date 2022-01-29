---
created: 2021101204
tags: linux bash
parent: Linux
---

# Bash

## List all sub directories

```bash
cd "/my/path"
for index in *
do
 echo $index
done
```

## File exist

```bash
if [ -d "folderName" ]
then
 echo "exist"
else
 echo "does not exist"
fi
```
