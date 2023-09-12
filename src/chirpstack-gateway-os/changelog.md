# Changelog

## v4.2.0

### Features

This is a very exciting release, as this release migrates the ChirpStack Gateway OS
from [Yocto](https://www.yoctoproject.org/) to [OpenWrt](https://openwrt.org/).
Thanks to [LuCI](https://github.com/openwrt/luci/) and the [UCI configuration system](https://openwrt.org/docs/guide-user/base-system/uci)
it is now possible to configure the provided ChirpStack components as well
things like network configuration through a web-interface instead of a CLI.
This release also splits the [packages](https://github.com/chirpstack/chirpstack-openwrt-feed)
from the ChirpStack Gateway OS [configuration](https://github.com/chirpstack/chirpstack-openwrt-config/)
such that these can be integrated in other OpenWrt based projects.
Main features that this release brings:

#### Web-interface

There is no need to configure the ChipStack Gateway OS using a terminal.
Powered by [LuCI](https://github.com/openwrt/luci/)), the ChirpStack Gateway OS
now provides an easy-to-use web-interface to configure ChirpStack components and
system configuration.

#### Custom packages

Through the web-interface (and cli) it is possible to install additional
software using the OpenWrt package repositories. This has been requested
several times, but until now would require to compile a custom ChirpStack
Gateway OS image which would take several hours to complete.

### Updates

* Update ChirpStack to v4.4.3.
* Update ChirpStack Concentratord to v4.2.3.
* Update ChirpStack UDP Forwarder to v4.1.2.
* Update ChirpStack MQTT Forwarder to v4.1.0.
* Update Node-RED to v3.0.2.

### Upgrade notes

Unfortunately it is not possible to migrate from ChirpStack Gateway OS v4.1.1
to ChirpStack Gateway OS v4.2.0. You need to re-flash your SD-Card with the
ChirpStack Gateway OS v4.2.0 image. 

## v4.1.1

### New shields

* Add support for Dragino PG1302 (EU868 + US915).

### Updates

* Update ChirpStack to v4.3.0.
* Update ChirpStack Concentratord to v4.1.1.
* Update ChirpStack UDP Forwarder to v4.1.1.

### Bugfixes

* Change `band_` to `_region_` after rename in Concentratord repo. ([#97](https://github.com/chirpstack/chirpstack-gateway-os/issues/97))

## v4.1.0

### Features

#### ChirpStack MQTT Forwarder

This release replaces the ChirpStack Gateway Bridge with the ChirpStack MQTT
Forwarder. The following MQTT configuration values will be automatically migrated
from the `chirpstack-gateway-bridge.toml` configuration file:

* `server`
* `topic_prefix` (detected based on `event_topic_template`)
* `username`
* `password`
* `ca_cert`
* `tls_cert`
* `tls_key`

### Updates

* ChirpStack to v4.2.0.
* ChirpStack Concentratord to v4.1.0.
* ChirpStack UDP Forwarder to v4.1.0.

## v4.0.2

### Updates

* ChirpStack to v4.1.1.
* ChirpStack Gateway Bridge to v4.0.3.
* Node-RED to v3.0.2.

### Bugfixes

* Fix NodeJS / Node-RED crashing with "Bus error" error message. ([#95](https://github.com/chirpstack/chirpstack-gateway-os/issues/95))

## v4.0.1

### Updates

* ChirpStack to v4.0.3.
* ChirpStack Concentratord to v4.0.1.
* The Things Network [lorawan-devices](https://github.com/TheThingsNetwork/lorawan-devices) to latest version.

### New shields

* Waveshare SX1302 LoRaWAN Gateway HAT

### Bugfixes

* Add missing `/etc/fw_env.config` file (see upgrade note below).
* Fix missing Wiregard binaries. ([#93](https://github.com/chirpstack/chirpstack-gateway-os/issues/93))

### Update note

If upgrading from v4.0.0 using the `software-update` utility, you must run the
following command first because of the missing `/etc/fw_env.config` file:

```
sudo echo "/boot/uboot.env 0x0000    0x4000" > /etc/fw_env.config
```

## v4.0.0

### Main changes

#### ChirpStack v4

This release replaces ChirpStack Network Server (v3) and ChirpStack Application
Server (v3) with ChirpStack v4.0.0.

#### MQTT certificates

If using the _full_ image, MQTT TLS certificates will be automatically generated on
first boot and configured in ChirpStack. For consuming device events throug the
MQTT integration, you can generate certificates in the web-interface under
the application integrations.

**Note:** localhost connections (e.g. if using Node-RED) to the MQTT do not
need TLS certificates for authentication and authorization.

#### gateway-config improvements

If using the _full_ ChirpStack Gateway OS image, which includes the ChirpStack
Network Server, the `gateway-config` script will automatically create the
gateway in the ChirpStack database for you.

#### Region configuration

The _full_ image contains update region configuration for the common regions.
The desired region can be selected using the `gateway-config` configuration script.

#### New shields

Support for the following shields has been added:

- RAK2247
- RAK5147
- Seeed WM1302

#### Yocto Kirkstone

ChirpStack Gateway OS has been updated to Yocto Kirkstone. This should fix
boot problems on some Pi 4 revisions, as this release contains an updated
bootloader.

### Other updates

* ChirpStack Concentratord to v4.0.0
* ChirpStack Gateway Bridge to v4.0.0
* Node-RED to v2.1.6

## v3.6.0

### Updates

* [ChirpStack Application Server](https://www.chirpstack.io/application-server) to v3.17.7
* [ChirpStack Gateway Bridge](https://www.chirpstack.io/gateway-bridge) to v3.14.2
* [ChirpStack Network Server](https://www.chirpstack.io/network-server) to v3.16.3

**Note:** The ChirpStack Gateway Bridge version included is compatible with
ChirpStack v4 which will soon be released.

## v3.5.1

### Updates

* Update [ChirpStack Concentratord](https://www.chirpstack.io/concentratord/) to v3.3.1.

### Improvements

* Additional region configurations
	* IMST Lite
		* RU864
		* IN865
	* Pi Supply - LoRa Gateway HAT
		* AU915
	* RAK2245
		* IN865
		* RU864
	* RAK2246(G)
		* IN865
		* RU864

### Bugfixes

* Fix configuration for RisingHF RHF0M301 shield (GPIO7 issue). [#72](https://github.com/brocaar/chirpstack-gateway-os/issues/72)

## v3.5.0

### Features

#### Node-RED integration

This release includes [Node-RED](https://nodered.org/) into the *full* image
version, with the [node-red-contrib-chirpstack](https://github.com/brocaar/node-red-contrib-chirpstack/)
package pre-installed. Please note that it must be enabled using the
`gateway-config` configuration utility first.

### Updates

* Update [ChirpStack Concentratord](https://www.chirpstack.io/concentratord/) to v3.3.0.
* Update [ChirpStack Gateway Bridge](https://www.chirpstack.io/gateway-bridge/) to v3.13.1.
* Update [ChirpStack Network Server](https://www.chirpstack.io/network-server/) to v3.15.0.
* Update [ChirpStack Application Server](https://www.chirpstack.io/application-server/) to v3.17.0.
* Update [Yocto](https://www.yoctoproject.org/) BSP and open-embedded layers from *dunfell* to *hardknott*.

### Notes

As this release increases the size of the rootfs and data partitions, updating
using a `.swu` image is not possible.

## v3.4.0

### Features

* Add support for Semtech 2.4 GHz gateway module.
* Add support for RAK2287 gateway module.

### Updates

* Update [ChirpStack Concentratord](https://www.chirpstack.io/concentratord/) to v3.2.0.
* Update [ChirpStack Network Server](https://www.chirpstack.io/network-server/) to v3.12.2.
* Update [ChirpStack Application Server](https://www.chirpstack.io/application-server/) to v3.14.0.

### Improvements

* Disable append only in Redis configuration.
* Align US915 and AU915 config examples (https://github.com/brocaar/chirpstack-docs/issues/38).
* Cleanup ChirpStack Gateway OS recipe structure.

### Bugfixes

* Fix disabling bluetooth on Raspberry Pi 3 (so that UART pins can be used for GNSS module).

## v3.3.3

### Features

* Add test-version of [ChirpStack UDP Bridge](https://github.com/brocaar/chirpstack-udp-bridge).

### Updates

* All meta-layers have been updated.
* Update [ChirpStack Concentratord](https://www.chirpstack.io/concentratord/) to v3.0.3.
* Update [ChirpStack Network Server](https://www.chirpstack.io/network-server/) to v3.11.0.
* Update [ChirpStack Application Server](https://www.chirpstack.io/application-server/) to v3.13.2.

### Bugfixes

* Fix bootfiles path in rpi-config. ([#63](https://github.com/brocaar/chirpstack-gateway-os/pull/63))
* Remove libubootenv. ([#64](https://github.com/brocaar/chirpstack-gateway-os/pull/64/))
* Update u-boot `CONFIG_SYS_BOOTM_LEN` to 16M.

## v3.3.2

### Updates

* [ChirpStack Concentratord](https://www.chirpstack.io/concentratord/) is updated to v3.0.2.

## v3.3.1

### Updates

* [ChirpStack Concentratord](https://www.chirpstack.io/concentratord/) is updated to v3.0.1.
* [ChirpStack Application Server](https://www.chirpstack.io/application-server/) is updated to v3.12.1.
* [ChirpStack Gateway Bridge](https://www.chirpstack.io/gateway-bridge/) is updated to v3.9.2.

## v3.3.0

This marks the first non-testing release of the ChirpStack Gateway OS!

### Updates

* [ChirpStack Concentratord](https://www.chirpstack.io/concentratord/) is updated to v3.0.0.

## v3.3.0-test.9

### Updates

* [ChirpStack Concentratord](https://github.com/brocaar/chirpstack-concentratord/) is updated to v3.0.0-test.11.

### Improvements

* `gateway-config` has been updated for the [Pi Supply LoRa Gateway HAT](https://uk.pi-supply.com/products/iot-lora-gateway-hat-for-raspberry-pi).
* New `gateway-config` option has been added to reload the Gateway ID.

## v3.3.0-test.8

## Bugfixes

* Fix ChirpStack Application Server Makefile execution to include web-interface statics in binary.

## v3.3.0-test.7

### Updates

* [ChirpStack Gateway Bridge](https://www.chirpstack.io/gateway-bridge/) is updated to v3.9.1.
* [ChirpStack Network Server](https://www.chirpstack.io/network-server/) is updated to v3.10.0.
* [ChirpStack Application Server](https://www.chirpstack.io/application-server/) is updated to v3.11.0.
* [ChirpStack Concentratord](https://github.com/brocaar/chirpstack-concentratord/) is updated to v3.0.0-test.10.

### Features

* Add `gateway-config` wizard for MQTT configuration.
* Update to Yocto Dunfell + build Go apps from source. ([#55](https://github.com/brocaar/chirpstack-gateway-os/pull/55))

### Bugfixes

* Fix AU915 selection bugs for RAK concentrators. ([#56](https://github.com/brocaar/chirpstack-gateway-os/pull/56))

## v3.3.0-test.6

### Features

* Support has been added for the Raspberry Pi 4.
* Support has been added for the Raspberry Pi Zero W.
* Support has been added for the RAK2246 and RAK2246G shields.
* Class-B beacon configuration has been added to the band configuration.

### Updates

* [ChirpStack Application Server](https://www.chirpstack.io/application-server/) is updated to v3.10.0.
* [ChirpStack Concentratord](https://github.com/brocaar/chirpstack-concentratord) is updated to v3.0.0-test.9.
* [ChirpStack Network Server](https://www.chirpstack.io/network-server/) is updated to v3.9.0.

### Improvements

* `gateway-config` shows ChirpStack Gateway OS version.
* `gateway-config` shows Gateway ID.
* Change ISM band names to their common name. ([#47](https://github.com/brocaar/chirpstack-gateway-os/pull/47))
* `sx1301-reset` script has been modified to leave the reset pin as output.

## v3.3.0-test.5

### Updates

* [ChirpStack Application Server](https://www.chirpstack.io/application-server/) is updated to v3.9.0.
* [ChirpStack Concentratord](https://github.com/brocaar/chirpstack-concentratord) is updated to v3.0.0-test.8.
* [ChirpStack Network Server](https://www.chirpstack.io/network-server/) is updated to v3.8.1.

### Features

#### Wifi Access Point mode

On initial installation on a Raspberry Pi 3, the Raspberry Pi will start Wifi
in Access Point mode, so that it is possible to connect directly to the
Raspberry Pi over WIFI for configuration of the concentrator shield and to
re-configure the WIFI.

### Improvements

* RAK2245 configuration has been improved (using defined Concentratord model name).
* RAK832 configuration has been improved.
* RAK2245 / RAK831 AS923 channel-plan has been added. ([#43](https://github.com/brocaar/chirpstack-gateway-os/pull/43))

### Bugfixes

* Fix passing incorrect model flags in `gateway-config` for some gateways.

## v3.3.0-test.4

When updating from a previous v3.3.0 version, it is recommended to re-run the
`gateway-config` utility to update the concentrator configuration.

### Updates

* [ChirpStack Concentratord](https://github.com/brocaar/chirpstack-concentratord) is updated to v3.0.0-test.6.

## v3.3.0-test.3

### Updates

* [ChirpStack Gateway Bridge](https://www.chirpstack.io/gateway-bridge/) is updated to v3.7.1.

## v3.3.0-test.2

### Updates

* [ChirpStack Gateway Bridge](https://www.chirpstack.io/gateway-bridge/) is updated to v3.7.0.
* [ChirpStack Network Server](https://www.chirpstack.io/network-server/) is updated to v3.7.0.
* [ChirpStack Application Server](https://www.chirpstack.io/application-server/) is updated to v3.8.0.
* [ChirpStack Concentratord](https://github.com/brocaar/chirpstack-concentratord) is updated to v3.0.0-test.5.

### Supported hardware

* Raspberry Pi 1 B+ support has been added (for IMST Lite Gateway)
* [IMST Lite Gateway](https://wireless-solutions.de/products/long-range-radio/lora-lite-gateway.html) has been added to gateway configuration script.

## v3.3.0-test.1

**This is a rewrite of the ChirpStack Gateway OS, you must re-flash your SD Card
to update!** Currently this version only targets the Raspberry Pi 3.

### Features

* Yocto has been updated to version 3.0.
* Software updates are now handled by [SWUpdate](https://github.com/sbabic/swupdate).
* The Semtech UDP Packet Forwarder has been replaced by [ChirpStack Concentratord](https://github.com/brocaar/chirpstack-concentratord).

### Updates

* [ChirpStack Gateway Bridge](https://www.chirpstack.io/gateway-bridge/) is updated to v3.7.0-test.2.
* [ChirpStack Network Server](https://www.chirpstack.io/network-server/) is updated to v3.7.0-test.1.
* [ChirpStack Application Server](https://www.chirpstack.io/application-server/) is updated to v3.8.0-test.1.

### Fixes

* Redis database does not start on boot after power failure that corrupts append only file. ([#32](https://github.com/brocaar/chirpstack-gateway-os/issues/32))

## v3.2.0test1

### General

* Update ChirpStack Gateway Bridge to v3.5.0.
* Update ChirpStack Network Server to v3.5.0.
* Update ChirpStack Application Server to v3.6.1.

### Features

* Add support for [Semtech SX1302 CoreCell](https://www.semtech.com/products/wireless-rf/lora-gateways/sx1302cxxxgw1) evaluation kit.

### Bugfixes

* Fix boot issue due to storage device not yet initialized. ([#9](https://github.com/brocaar/chirpstack-gateway-os/issues/9))
* Fix ChirpStack Network Server `enabled_uplink_channels` configuration. ([#26](https://github.com/brocaar/chirpstack-gateway-os/issues/26))

## v3.1.0test1

This release renames LoRa Gateway OS to ChirpStack Gateway OS.
See the [Rename Announcement](https://www.chirpstack.io/r/rename-announcement) for more information.

## v3.0.0test3

### LORIX One

* Fix Wiregard kernel module dependencies.

## v3.0.0test2

### General

* Update LoRa App Server to v3.2.0.
* Update LoRa Gateway Bridge to v3.1.0.
* Update LoRa Server to v3.1.0.
* Update Monit to 5.26.0 and set check interval to 10 seconds.
* Add `PersistentKeepalive = 25` to Wiregard example config.
* Update openembedded layers to latest versions.

### Raspberry Pi

* Fix concentrator ordering.

## v3.0.0test1

### General

* LoRa App Server v3.1.0.
* LoRa Server v3.0.2.
* LoRa Gateway Bridge v3.0.1.

### Raspberry Pi

* Add support for the [Pi Supply LoRa Gateway Hat](https://uk.pi-supply.com/products/iot-lora-gateway-hat-for-raspberry-pi).
* Fix HDMI related boot issue. ([#9](https://github.com/brocaar/lora-gateway-os/issues/9))

## v2.0.0test4

### General

* Add Wiregard VPN client
* Bump LoRa Server package versions

### Raspberry Pi

* Change SPI speed to 2MHz (required by RAK2245)
* Add IMST iC980A configuration
* Add RAK2245 configuration

### LORIX One 512MB

* Fix u-boot command

## v2.0.0test3

### LORIX One

* Fix setting the MAC address from EEPROM.

## v2.0.0test2

### General

* Implement Mender for (OTA) system updates.
* Implement OverlayFS over read-only root filesystem.
* Update LoRa Gateway Bridge to v2.6.2.
* [lora-gateway-os-full] Update LoRa Server to v2.4.1.

### Raspberry Pi

* Add support for Sandbox Electronics LoRaGo PORT concentrator.
* Implement all US915 and AU915 channel-blocks. ([#2](https://github.com/brocaar/lora-gateway-os/pull/2))
* [lora-gateway-os-full] Automatic (re)configure LoRa Server on setting the concentrator channel-plan.

## v2.0.0test1

* Initial test release.
