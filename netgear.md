# Netgear R7000

## Lede Project

To enable wifi install these packages:

    kmod-b43


### 3G/4G Modem

The following has been tested with the Huawei E398 modem. Other modems with different capabilities will likely need
a different setup.

#### Package dependencies

To add support for modem serial interface (ttyUSB0), install these packages:

    kmod-usb-serial                               Kernel support for USB-to-Serial converters
    kmod-usb-serial-option                        Kernel support for Option HSDPA modems
    kmod-usb-serial-wwan                          Kernel support for USB GSM and CDMA modems


To enable the 3G/4G modem, install these packages:

    kmod-usb-net                                  Kernel modules for USB-to-Ethernet convertors
    kmod-usb-wdm                                  USB Wireless Device Management support
    kmod-usb-net-qmi-wwan                         QMI WWAN driver for Qualcomm MSM based 3G and LTE modems
    wwan                                          Generic OpenWrt 3G/4G proto handler
    uqmi                                          Command line tool for controlling mobile broadband modems using the QMI-protocol

#### Modem setup

Check which modes are available for the modem:

    screen /dev/ttyUSB0 115200
    AT^SETPORT=?

The output should be a list of supported modes:

    1:MODEM
    2:PCUI
    3:DIAG
    4:PCSC
    5:GPS
    6:GPS CONTROL
    7:NDIS
    A:BLUE TOOTH
    B:FINGER PRINT
    D:MMS
    E:PC VOICE
    A1:CDROM
    A2:SD

The `SETPORT` example commands below use the numbering from this list so adjust them accordingly. Before
changing the mode, write down the initial setting in case we need to restore it:

    AT^SETPORT?
    A1,A2;1,2,3,7,A1,A2

If the modem only has support for AT commands we need to set it to `modem` mode. The following disables the
CD-ROM and SD modes and enables `modem` mode:

    AT^SETPORT="FF;1,2,3,7"

If the modem has support for `NDIS` mode, then the following disables CD-ROM and SD modes and enabled `NDIS`:

    AT^SETPORT="FF;7,1,2,3"

The initial `FF` disables the mount-mode. *Never* disable `PCUI` mode or you won't be able to connect to the modem
serial interface.

#### UQMI Setup

    uqmi -d /dev/cdc-wdm0 --get-data-status
    uqmi -d /dev/cdc-wdm0 --get-signal-info
    uqmi -d /dev/cdc-wdm0 --start-network <provider APN> --autoconnect

    uqmi -d /dev/cdc-wdm0 --start-network mobileinternet.tele2.se --autoconnect

Provider APN is `mobileinternet.tele2.se`.

If starting the network does not work, try stopping it first:

    uqmi -d /dev/cdc-wdm0 --stop-network 0xFFFFFFFF --autoconnect

Create the network interface for the modem by adding the following to `/etc/config/network`:

    config interface 'wwan'
        option proto 'dhcp'
        option ifname 'wwan0'


    config interface 'modem'
        option proto 'qmi'
        option device '/dev/cdc-wdm0'
        option apn 'mobileinternet.tele2.se'
        option auth 'none'


Other useful commands:

    uqmi -d /dev/cdc-wdm0 --get-current-settings                Current connection settings
    uqmi -d /dev/cdc-wdm0 --get-capabilities                    List device capabilities


### General configuration

#### SSH

Add the desired options to the `config dropbear` section in `/etc/config/dropbear`.

Allow ssh access from local network only:

    option Interface 'lan'

Increase the idle timeout:

    option IdleTimeout 3600


## Commands

    iw list                               List all wireless devices and their capabilities
    iw dev                                List all netwirk interfaces for wireless hardware

    logread -l <n> -f                     Tail dmesg log, n previous lines

    cat /sys/kernel/debug/usb/devices     Get info on connected USB devices

    ubus

    ubus call network.interface.wwan status

    iwinfo

    gcom


    {qmi.sh} /bin/sh ./qmi.sh qmi setup modem {"proto":"qmi","device":"\/dev\/cdc-wdm0","apn":"mobileinternet.tele2.se","auth":"none"}


## Additional packages

    vim
    curl
    luci-app-adblock


## Other notes

3G start scripts:

    /lib/netifd/proto/3g.sh
    /overlay/upper/lib/netifd/proto/3g.sh

