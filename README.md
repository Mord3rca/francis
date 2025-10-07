# Francis.lan

A light OpenVPN Home installation based on RPi4

## First setup

Use `dd` to copy **francis** image to an SD card:

```sh
# dd if=/path/to/francis.img of=/sd/block/device status=progress
```

Maybe [rpi-imager](https://github.com/raspberrypi/rpi-imager) can be used with a custom image.

## Additionnal configuration

RPi like configuration is planned but not yet on the product. So you gonna need to mount partition 2
and changes some files manually.

Assuming you have mounted partition 2 at **/mountpoint** for all useg/example.

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
