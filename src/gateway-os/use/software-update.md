# Software updates

ChirpStack Gateway OS uses [SWUpdate](https://github.com/sbabic/swupdate) for handling updates.
SWUpdate is open-source and can be used either as a CLI utility on the gateway
or it can be integrated with [Eclipse hawkBit](https://www.eclipse.org/hawkbit/).

## Partition layout

ChirpStack Gateway OS uses 4 partitions:

* Boot partition
* RootFS partition A
* RootFS partition B
* Data partition (used for OverlayFS)

One RootFS partition is used for booting, the other for the next update.
The bootloader will automatically revert to the last functioning RootFS
partition on a failed update.

## CLI update

After downloading the update file (`.swu`) on the gateway, execute the `software-update`
utility:

```bash
sudo software-update path/to/update.swu
```

Please refer to the install section to find the correct `.swu` artifact for
your gateway.

After `software-update` has completed, reboot the gateway.
