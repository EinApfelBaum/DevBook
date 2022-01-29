---
created: 19.11.2021
tags: iobroker smarthome proxmox
---

# Install iobroker with ConBee2 in debian virtual machine

## deCONZ Installation

In the next step we will now install the just installed virtual machine with Debian, a few more prerequisites and programs to then install deCONZ.

* After the system is up, we establish an SSH connection via PUTTY and log in with the personal user ID and not `root`. Once you are logged in, type `su` to then enter the password of the "root user".
* Now install `sudo` with the following command: `apt-get install sudo`
* Now we have to install the package `gnupg`. We do this with the command: `apt-get install gnupg`
* The next step is to set the USB access rights for users. To do this, please enter the following command: `sudo gpasswd -a $USER dialout`
* With the following command we import the Phoscon public key:

```bash
wget -O - http://phoscon.de/apt/deconz.pub.key | sudo apt-key add -
```

* configure APT-Repository for deCONZ:

```bash
sudo sh -c "echo 'deb http://phoscon.de/apt/deconz \
$(lsb_release -cs) main' &gt; \
/etc/apt/sources.list.d/deconz.list"
```

* Update APT package list: `sudo apt update`
* install deCONZ `sudo apt install deconz`
* The following command defines that deCONZ will be started automatically when booting the VM: `sudo systemctl enable deconz`
* After a few seconds the operating system on the Raspberry will be restarted.
* As a last step please reboot the virtual machine best via proxmox;
* After a few seconds the start up process is finished and the gateway is available in your network.
* Now you can use your router to find out the assigned IP address or simply do the next step for the initial start up

## Initial commissioning

Calling up the Phoscon App via [http://phoscon.de/app](http://phoscon.de/app) in a browser. The gateway is displayed with the name Phoscon-GW and its current IP address. If not, the search for the gateway can be started directly via the Phoscon logo.

* When you call the gateway for the first time, a screen will appear where you have to enter a new password for security. Then click on Next;
* Next you will get to the page where you can learn new lights. Recommendation here would be to first click on Continue without lights in the upper right corner;
* Now you will be asked to define a first group. Also close this screen with X;
* Next, select the Gateway menu item to check if the gateway is available and if a firmware update is required. In my case the version was already up to date, because I already did an update during the installation in a Proxmox VM.
* With this, the basic setup of the Phoscon APP is also already done. The Phoscon App is a software to configure and control your smart light installations, no matter if small or big, specialized on the Zigbee wireless standard. The Phoscon App supports a constantly growing number of lights, sensors and switches from different manufacturers.
* A really comprehensive and good documentation can be found at the following link: [Documentation](https://phoscon.de/de/app/doc)

With this, all further actions such as teaching of lamps and other devices, definition of groups or scenarios should be possible without any problems.

---

## Resources

* [https://technikkram.net/blog/2020/04/18/conbee-ii-installation-des-universellen-zigbee-gateways-in-einer-vm-unter-proxmox/](https://technikkram.net/blog/2020/04/18/conbee-ii-installation-des-universellen-zigbee-gateways-in-einer-vm-unter-proxmox/)
