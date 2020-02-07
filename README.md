# ctf-usb-keyboard-parser

This is the updated script from https://teamrocketist.github.io/2017/08/29/Forensics-Hackit-2017-USB-ducker/

### Usage
```bash
$ python usbkeyboard.py <file>
```

### Extract file from pcap (might not work for every pcap)
```bash
$ tshark -r ./usb.pcap -Y 'usb.capdata && usb.data_len == 8' -T fields -e usb.capdata > usbPcapData
```

Some versions of tshark don't add ":" between each byte like this:

```bash
$ tshark -r ./usb.pcap -Y 'usb.capdata && usb.data_len == 8' -T fields -e usb.capdata
0000240000000000
0000000000000000
...
```

If this happens you can use sed to add them like this:

```bash
$ tshark -r ./usb.pcap -Y 'usb.capdata && usb.data_len == 8' -T fields -e usb.capdata | sed 's/../:&/g' | sed 's/^://'
00:00:24:00:00:00:00:00
00:00:00:00:00:00:00:00
...
```
