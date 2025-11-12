# Configuration of NetworkManager

## Prerequisite

Generate a OVPN file with `pivpn add [nopass]` and copy it on your local machine

OVPN files can be found here: **/var/lib/pivpn-admin/ovpns**

In this case, Network Manager support password protected certificates, so *nopass* is not required

### Debian / Ubuntu

```sh
# apt install network-manager-openvpn-gnome
```

Note: For Debian 12 or less, you'll need to modify OpenVPN configuration on **francis** to use a less secure data cipher.

In file */etc/openvpn/server.conf* add/edit the following key:
```
data-ciphers AES-256-CBC
```

### Gentoo

You will need **net-misc/networkmanager** & **net-vpn/networkmanager-openvpn** packages

## Setup

### via CLI

Just run the following command with an account having nmcli admin rights:

```sh
$ nmcli connection import type openvpn file <file.ovpn>
```

### via GUI

Left click on your NM widget, go to *VPN Connection* and then left click *Configure VPN*.

Select *Import a saved VPN configuration* at the bottom, *Create* and then select you OVPN file.
