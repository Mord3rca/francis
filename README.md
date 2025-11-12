# Francis.lan

A light OpenVPN Home installation based on RPi4

## First setup

### Writing image on sdcard

[rpi-imager](https://github.com/raspberrypi/rpi-imager) can be used, just set *Custom Image* in the OS field.
Also image customisation is not yet supported.

Or use `dd` to copy **francis** image to an SD card:

```sh
# dd if=/path/to/francis.img of=/sd/block/device status=progress
```

## Additionnal configuration

RPi like configuration is planned but not yet on the product. So you gonna need to mount partition 2
and changes some files manually.

Assuming you have mounted partition 2 at **/mountpoint** for all use/example.

### Allow SSH root connection

Copy you public key in **/mountpoint/root/.ssh/authorized_keys**:

```sh
# mkdir -p /mountpoint/root/.ssh
# cp /path/to/your/key.pub /mountpoint/root/.ssh/authorized_keys
```

SSH connection for root is key only, setting up a password for the account wont change anything.

### Configure DynDNS Updater

Your IPv4 may change ... It's recommended to setup DynDNS on your router
if it support it or on francis directly.

To do it, you can edit **/mountpoint/etc/dyndns-updater.conf** according to
[dyndns-updater](https://github.com/Mord3rca/dyndns-updater?tab=readme-ov-file#usage) secret file syntax.


### PiVPN Installer

Running `pivpn-installer` is required the first time on the target.

You can use */etc/pivpn/default-install-config* for the default configuration

```sh
# pivpn-installer --unattended /etc/pivpn/default-install-config
```

However, it is recommanded to modify the default file first to modify at least `pivpnHOST` key
so it watch the DynDNS entry configured or the WAN IPv4 of your router.

Once the installation is completed, just add a new user with:

```sh
# pivpn add [nopass]
```

**nopass** is should be used if your VPN client does not support password protected certs.

## Network Setup

### Static IP

In case of power cut, DHCP failure etc ... It is recommended to set a static IPv4 on **francis**.

To do so, you will have to modify the file **/etc/systemd/network/eth0.network** according to
[systemd.network(5)](https://man.archlinux.org/man/systemd.network.5) manual.

Example of static IP configuration:

```
[Match]
Name=eth0

[Network]
Address=192.168.1.100/24
Gateway=192.168.1.1
DNS=192.168.1.1
```

### NAT

There is 2 services running on **francis**, OpenVPN & SSH.

So, if you are behind a router, you will need to forward port 22 (TCP) and 1194 (UDP)

## Client configuration

List of tested clients to run with **francis**:

* [Opal GL-SFT1200](clients/gl-sft1200.md)
* [Network Manager](clients/network-manager.md)
