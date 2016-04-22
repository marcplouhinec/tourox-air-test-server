Test server for Tourox Air
==========================

Introduction
------------

This project is a test server for the Tourox Air applications available at the following repositories:
* [Tourox Air for Android](https://github.com/marcplouhinec/tourox-air-android)
* [Tourox Air for iOS](https://github.com/marcplouhinec/tourox-air-ios)

Because Tourox Air is a client application, it needs a WIFI router and a VoIP server to run.
The goal of this project is to explain how to configure a WIFI router and setup a Voip server in order to
test the mobile applications. However, this project is limited for a testing purpose: the basis are the
same as the ones we use for our Tourox platform, but the later includes more features like a statistic
collecting system for billing, specific tools for tour guides, etc.

If you are a professional working in the tourism industry and are interested in buying or selling
our Tourox platform, please contact us via email at contact@tourox.io.

For more information, please look at our website: http://www.tourox.io.

Setup guide
-----------

Because the goal of Tourox Air is being an application that "just work" with the less configuration
as possible from the user side, the router and server configuration must follow strict rules in order to
correctly work with the mobile applications.

The first step is to prepare a WIFI router with the following configuration:
* SSID: tourox-test
* Encryption: none
* Mode: access point
* IPv4 configuration: router address = 192.168.85.254, netmask = 255.255.255.0
* DHCP server: enabled - provide IP addresses in the following range: 192.168.85.100 to 192.168.85.110

Theses are the main configuration properties in order to have a compatible environement the the
smartphone apps. If applicable for your router, we recommend using [OpenWrt](https://openwrt.org) as it
provides great flexibility. [Here is a step-by-step guide](https://wiki.openwrt.org/doc/recipes/guest-wlan-webinterface)
explaining WIFI congiguration with OpenWrt.

The second step is to configure a VoIP server. We have chosen [Asterisk](http://www.asterisk.org) version 11 or greater, because
of its big community and its large documentation.
* Configure a computer with a Linux distribution (like [Arch Linux](https://www.archlinux.org));
* Connect the computer via WIFI to the router you just configured with a static IP: 192.168.85.1;
* Install Asterisk. The procedure depends on your Linux distribution; for Arch Linux, the "yaourt asterisk" command will do the trick ([here is a nice guide for Arch Linux](https://wiki.archlinux.org/index.php/asterisk));
* Once installed, several configuration files are available in the /etc/asterisk/ folder. Backup and replace the files sip.conf and extensions.conf by the ones included in this repository;
* Start Asterisk with the command: asterisk -cvvv

Testing guide
-------------

In order to test Tourox Air we need two devices: the smartphone/tablet with Tourox Air installed on it and another device
(computer or smartphone) with a SIP client installed on it (for Android we recommend
[CSipSimple](https://play.google.com/store/apps/details?id=com.csipsimple&hl=fr), for iOS
we recommend https://itunes.apple.com/us/app/join-softphone-voip-sip-client/id566525840?mt=8).

The first step is to configure the device with a SIP client:
* Connect the device via WIFI to the router you just configured with a dynamic IP address;
* Open the SIP client aplication and create a user with the following configuration: username = test, password = test, host/domain = 192.168.85.1;
* The SIP client must confirm that the user is successfully registered;
* Dial the number "2" and start the call.

Now it's time for the real test:
* Connect your smartphone/tablet via WIFI to the router you just configured with a dynamic IP address;
* Open Tourox Air;
* After few seconds the other device with the SIP client should ring;
* After answering, the voice of the user of the SIP client must be heard on the smartphone/tablet with Tourox Air.

Hope everything is fine and the test succeeded! :-) Here are the steps to properly clean your testing environment:
* Hangup on your SIP client and turn it off;
* Turn off Tourox Air by pressing on the back button on Android, or by double pressing the physical button on iOS and swipe up on the app preview;
* On your computer, turn off Asterisk by pressing CTRL+C on the console.

If you have problems during the test, please contact us via email at contact@tourox.io.

Licence
-------
Copyright (C) 2016, Marc Plouhinec (marc.plouhinec@tourox.io)

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>.

![GPL-v3 logo](http://www.gnu.org/graphics/gplv3-127x51.png)

Credits
-------
The application is based on:
* [OpenWrt](https://openwrt.org), a highly extensible GNU/Linux distribution for embedded devices (typically wireless routers).
* [Asterisk](http://www.asterisk.org), a software implementation of a telephone private branch exchange (PBX).
* [Arch Linux](https://www.archlinux.org), a simple an lightweight Linux distribution. It is also available for the [Raspberry PI](https://wiki.archlinux.org/index.php/Raspberry_Pi).
