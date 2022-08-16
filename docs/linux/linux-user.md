---
created: 17.10.2021
tags: linux cli users
parent: Linux
---

# Users

## Add

```bash
    useradd <username>

    # With no login
    useradd -r <username>
    # -r, --system
    # create a system account
    # The -r flag will create a system user - one which does not have a password, a home dir and is unable to login.
```

## Add to sudo group

```bash
    # add user to sudo group
    # as root
    usermod -aG sudo <username>
    # -a helps to append the user to a specific group
    # -G indicates the group name to which the new user will be added
```

## Switch user

```bash
su - <username>
# You need to enter the password
```

## Remove

```bash
userdel <username> -r
# -r (--remove) 
# force userdel to remove the user’s home directory and mail spool
```

## List

The term “getent” is a short form for “get entries from the administrative database.” As it suggests, getent can work with various administrative databases. Check out all the supported administrative databases.

```bash
# info about all the users in the system
getent passwd | sort

# check if user exists
getent passwd <username>

# list all the users from a particular user group
getent group <group_name>
```

---

## Resources

* [https://linux.die.net/man/1/ssh](https://linux.die.net/man/1/ssh)
* [https://community.hetzner.com/tutorials/howto-initial-setup-ubuntu#step-3---giving-a-user-administrative-privileges](https://community.hetzner.com/tutorials/howto-initial-setup-ubuntu#step-3---giving-a-user-administrative-privileges)
