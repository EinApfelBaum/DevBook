---
created: 12.04.2022
tags: linux thunderbolt
parent: Linux
---

# Enable thunderbolt device on linux

My problem: The monitor was working, but the connected USB mouse and keyboard did not work.

> boltctl - control the thunderbolt device manager

```bash
# On linux mint bolt is already installed
sudo apt-get install bolt

# For more information
man boltctl

# Show thunderbolt devices, copy the UUID for later
boltctl
```

The yellow dot means that the device is currently not fully authorized.

![Thunderbolt device manager - device not authorized](/assets/images/linux/linux-bolt-thunderbolt-not-authorized.png)

```bash
# Authorize the thunderbolt device with the device UUID from above
sudo boltctl enroll --policy auto DEVICE_UUID
```

![Thunderbolt device manager - device fully authorized](/assets/images/linux/linux-bolt-thunderbolt-authorized.png)

From the manpage:
> enroll [--policy policy] DEVICE
       Authorize and record the device with the unique id DEVICE in the
       database. If the domain supports secure connection a new key will be
       generated and stored in the database alongside the device name and
       vendor name. The key, if created, will be used in the future to
       securely authorize the device.
> --policy {default | auto | manual}
           Specify the policy to be used for the newly enrolled device.
           auto: Automatically authorize this device whenever it is connected.

---

## Resources

* [https://forums.linuxmint.com/viewtopic.php?t=299991](https://forums.linuxmint.com/viewtopic.php?t=299991)
