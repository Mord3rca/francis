# Router configuration of Opal GL-SFT1200

## Prerequisite

Generate an OVPN file with `pivpn add nopass` and copy it on your local machine

OVPN files can be found here: **/var/lib/pivpn-admin/ovpns**

Note: *nopass* is not optional here

## Setup

* Acces you router admin panel

* In the side menu to the left, go to VPN - OpenVPN Client

* Click on **+ New Group** and name it as you like

* Select (or drag) the OVPN file in the according dialog box to the right side

* Once done, click on the three dots and then *Start*

After this, a green dot should appear near the server, *OpenVPN Client* and *VPN Dashboard* items.

Every machines connected to the router would use the VPN tunnel transparently.
