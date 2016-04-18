### List system hardware and software configuration

In OSX the `system_profiler` command reports system hardware and software configuration.

List USB devices:

    system_profiler SPUSBDataType



### Record or capture live USB traffic

In windows use USBPcapCMD to record or capture live USB traffic.

List the Root Hubs and their connected devices, and do a non-live capture:

    USBPcapCMD.exe

To do a live capture, start a command shell with administrator privileges and run:

    USBPcapCMD.exe -d <root_hub> -o - | "C:\Program Files\Wireshark\Wireshark.exe" -k -i -

It may be necessary to stop and start the capture in Wireshark to get it to start the capture.



### pmset - manipulate power management settings

Display the current power management settings:

    pmset -g

Modify a power management setting:

    sudo pmset -a <setting> <value>

`hibernatemode` supports values of 0, 3, or 25. Whether or not a hibernation image gets written is also dependent on the values of
`standby` and `autopoweroff`.

`hibernatemode = 0` - The system will not back memory up to persistent storage.

`hibernatemode = 3` - The system will store a copy of memory to persistent storage, and will power memory during sleep. The system will wake from memory unless a power loss forces it to restore from hibernate image.

`hibernatemode = 25` - The system will store a copy of memory to persistent storage, and will remove power from memory. The system will restore from disk image.

`standby`, if enabled, hibernates a machine after it has slept for a specified time period.

`standbydelay` specifies the delay in seconds before writing the hibernation image to disk and powering off memory.

Example: enable hibernation mode:

    sudo pmset -a hibernatemode 25
    sudo pmset -a standby 1
    sudo pmset -a standbydelay 30

Then select `Sleep` in the apple menu and wait for 30 seconds, and some additional time to save the memory state to disk image.
After this delay it is safe to unplug the power source.

