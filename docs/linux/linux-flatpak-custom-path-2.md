---
created: 22.10.2021
tags: linux flatpak
parent: Linux
---

# Custom installation path 2

It's best (not mandatory) if the following conditions are adhered to ...

* Its is best to have a separate partition on your internal hard disk (preferable) dedicated to installing flatpak applications.
* It is best to configure you linux OS to auto mount partition on boot ...
* Its is best to let the partitions mount at their default locations ... some OSes mount it in /media/user and some mount it in `/mnt`
* It is best to name/label the partition

The following commands are written assuming the default location being /media/user and partitions get auto mounted at this location.
Make changes according to your own systems. I have a separate partition labelled it as flatpak (name of the partition not the folder).

```bash
sudo mkdir /media/Flatpak/flatpak
sudo mkdir /etc/flatpak
sudo mkdir /etc/flatpak/installations.d

sudo gedit /etc/flatpak/installations.d/extra.conf
```

Custom install location : **myFlatpaks**

Paste the following block in the `extra.conf` file and save it ...

```bash
[Installation "myFlatpaks"]
Path=/media/Flatpak/flatpak/
DisplayName=myFlatpaks Installation
StorageType=harddisk
```

Add the flathub remote to this custom install location

```bash
flatpak --installation=myFlatpaks remote-add flathub https://flathub.org/repo/flathub.flatpakrepo
```

Check the environment variable `XDG_DATA_DIRS`, if the custom path was added.

```bash
echo $XDG_DATA_DIRS
```

If not, add the path to `XDG_DATA_DIRS`.
In your `.profile` file (`${HOME}/.profile`). This is the default situation on most Unix installations, and in particular on Debian.

If your login shell is bash and these following files exist, you can use `.bash_profile` (`${HOME}/.bash_profile`) or .bash_login instead.

```bash
# append XDG_DATA_DIRS so it includes custom path to flatpak if it exists
if [ -d "/media/Flatpak/flatpak/exports/share" ] ; then
    XDG_DATA_DIRS="/media/Flatpak/flatpak/exports/share:$XDG_DATA_DIRS"
fi
```

## Advantages of using a Separate partition dedicated ONLY for flatpak applications

* In cases where the OS is reinstalled from scratch which involves formatting /root and /home partition. (Tested and Works)
* In cases where you are switching from one linux distro to another. (not yet tested as such a situation hasn't been encountered by me).

## Commands to manage applications at this custom install location

```bash

# Install
flatpak --installation=myFlatpaks install flathub org.application.name

# Uninstall
flatpak --installation=myFlatpaks uninstall org.application.name

# Update
flatpak --installation=myFlatpaks update org.application.name

# List
# to list all applications
flatpak list 
# to list applications only from a specific installation location.
flatpak --installation=myFlatpaks list 

# Run flatpak 
run flathub org.application.name

```

---

## Resources

* [https://github.com/flatpak/flatpak/issues/2337](https://github.com/flatpak/flatpak/issues/2337)
