# DC256 BLE CTF Files

Manual installation tips:

Download the three required files:
* [bootloader.bin](bootloader.bin)
* [partition-table.bin](partition-table.bin)
* [firmware.bin](firmware.bin)

Install `esptool` as appropriate for your platform:
* Easiest, if you have working Python: `pip install esptool` or `pipx install esptool`.
* Or download binary from [https://github.com/espressif/esptool/releases/tag/v5.1.0](espressif/esptool).

Figure out what serial port your device is on:
* On Windows, look in Device Manager under Ports (COM & LPT) and see what shows up when you plug in your device.  Generally something like COM6.
* On Mac/Linux, look in /dev for a new /dev/ttyUSBx or /dev/ttyACMx or /dev/tty.usbmodemx or /dev/tty.usbserialx or something.

Flash the device:
* `esptool -p <PORT> -b 921600 write-flash 0x1000 bootloader.bin 0x8000 partition-table.bin 0x10000 firmware.bin` and substitute in the port name from above.
* You may have to preface the command with `python3 -m` depending on your environment and how you installed it.
* If you have trouble where it starts flashing but errors, or if it completes but doesn't run properly, reduce the -b setting to 115200 and try again.

The device should auto reset and start broadcasting the BLE signal immediately. However, your computer could hold the port in a weird state, so try plugging it into a standalone charger before suspecting anything else.
Open LightBlue and hopefully you see "CTF:SOLIDUS"!

Good luck!
