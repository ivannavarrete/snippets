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
