#### Boot options

    Command + V                   Verbose Mode

    Command + R                   Recovery mode

    Command + S                   Single User Mode

    Shift                         Safe Boot

    Alt/Option                    Startup Manager

    Command + Option + P + R      Reset NVRAM

    T                             Target Disk Mode

    C                             Boot from CD, DVD, or USB

    N                             Netboot to a compatible network server


#### System Management Controller

Reset the SMC on Mac desktop computers:

1. Shut down your Mac.
2. Unplug the power cord.
3. Wait 15 seconds.
4. Plug the power cord back in.
5. Wait five seconds, then press the power button to turn on your Mac.


#### System Integrity Protection

System Integrity Protection limits what can be done on the system. It is present on OSX 10.11 (El Capitan)
and later. Boot into recovery mode and open a terminal (Utilities > Terminal). The command `csrutil`
is used to disable or enable SIP.

    csrutil

It is also possible to enable SIP protection and selectively disable aspects of it by adding one or more flags
to the `csrutil enable` command.

SIP changes will take effect on next restart.

To verify whether a file or folder is restricted use the `-lO` option with ls. Look for the `restricted`
text to indicate where SIP is enforced.

    ls -lO /path


#### Kernel Extensions

List all kernel extensions:

    kextstat

Install kernel extension:

    cd /System/Library/Extensions
    sudo cp /path/file.kext .
    sudo chmod -R 755 file.kext
    sudo chown -R root:wheel file.kext

    sudo rm -R Exteneions.kextcache
    sudo rm -R Extensions.mkext

On El Capitan or newer, the 'file system protection' of System Integrity Protection must be disabled.


### List system hardware and software configuration

`system_profiler` is a cli tool that reports hardware and software configuration. Some examples:

    system_profiler                         generate full text report with standard detail level

    system_profiler -listDataTypes          list available data types

    system_profiler SPUSBDataType           list USB devices


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


#### Manual software uninstall

If the application does not have an uninstall feature either in the installed app or the original dmg file,
use the following procedure:

0. Quit the application.

1. Remove the application at `/Applications/<app_name>.app`.

2. Find and remove application specific directories:

    ```
    find ~/Library -type d | grep -i <app>
    find /Library -type d | grep -i <app>
    ```

3. The most common directories are:

    * ~/Library/Preferences
    * ~/Library/Caches
    * ~/Library/Application Support
    * ~/Library/Logs
    * ~/Library/Saved Application State

4. Unload any plist files from `/Library/LaunchAgents`, `/Library/LaunchDaemons`, `~/Library/LaunchAgents`, and `~/Library/LaunchDaemons`.

    ```
    launchctl unload <path_to_plist_file>
    ```

5. Remove the above plist files.

6. If there is no plist file for a service, remove it directly without unloading

    ```
    launchctl list | grep <app>
    launchctl remove <service_name>
    ```

7. Restart the computer.
