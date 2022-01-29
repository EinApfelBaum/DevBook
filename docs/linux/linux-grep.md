---
created: 17.10.2021
tags: linux cli
parent: Linux
---

# grep, egrep, fgrep - print lines matching a pattern

```bash
grep -rnw '/path/to/somewhere/' -e 'pattern'
# -r or -R is recursive,
# -n is line number, and
# -w stands for match the whole word.
# -l (lower-case L) can be added to just give the file name of matching files.
# -i, --ignore-case Ignore case distinctions in  both  the  PATTERN  and  the  input files.

# Along with these, --exclude, --include, --exclude-dir or --include-dir flags could be used for efficient searching:

# This will only search through those files which have .c or .h extensions:
grep --include=\*.{c,h} -rnw '/path/to/somewhere/' -e "pattern"

# This will exclude searching all the files ending with .o extension:
grep --exclude=*.o -rnw '/path/to/somewhere/' -e "pattern"

# Just like exclude files, it's possible to exclude/include directories through --exclude-dir and --include-dir parameter. For example, this will exclude the dirs dir1/, dir2/ and all of them matching *.dst/:
grep --exclude-dir={dir1,dir2,*.dst} -rnw '/path/to/somewhere/' -e "pattern"
```

---

## Resources

* [https://linux.die.net/man/1/grep](https://linux.die.net/man/1/grep)
