# MFZ Ovitor RS-485 communication logs

I used to repair az MFZ Ovitor door opener with [CS110 PCB](https://www.mfz-antriebe.de/fileadmin/mfz/php/file.php?filePath=020--Betriebsanleitungen/101--Steuerungen/05--CS110/02--CS110--GB/&fileName=103730_BA_CS110_MFZ_EN_RevA05_1700012038.pdf) connected to a CSI 3 button keypad.
It had Error RS-485 (2x flash of the RED LED).
I made and uploaded traces from the communication with Saleae Logic 1.x.

## files

* init_w_led_changes.logicdata 

This file includes all communication between the CS110 and the CSI keypad after power up. 
It looks that the CS110 supports other devices because there is a quite long traffic after the init before the CSI-3 start answering.

* rest of the files: corresponding to the actions performed on the keypad (idle/open/close)

## Communication

19200 baud, 9n1

Master sends periodically:
0x0C3 0x14F 0x5F

The LED state of the keypad also sent in down, the init_w_led_changes contains it, but I have not noted how it works.

Keypad responds:

0xC3 0x000 0x1F7 - Idle

0xC3 0x102 0x1CD - Open button pressed

0xC3 0x104 0x183 - Close button pressed

0xC3 0x101 0x1EA - Halt button pressed


Just in case if your dog would chew the keypad and you want build a keypad from an Arduino or you want to integrate to [openHAB](https://github.com/openhab) or whatever...
