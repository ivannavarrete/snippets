### Record or capture live USB traffic

In windows use USBPcapCMD to record or capture live USB traffic.

List the Root Hubs and their connected devices, and do a non-live capture:

    USBPcapCMD.exe

To do a live capture, start a command shell with administrator privileges and run:

    USBPcapCMD.exe -d <root_hub> -o - | "C:\Program Files\Wireshark\Wireshark.exe" -k -i -

It may be necessary to stop and start the capture in Wireshark to get it to start the capture.
