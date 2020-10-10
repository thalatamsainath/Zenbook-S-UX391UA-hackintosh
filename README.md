# Zenbook-S-UX391UA-hackintosh
Asus Zenbook S UX391UA Hackintosh using OpenCore


## Configuration

| Specifications      | Details                                          |
| :--- | :---|
| Computer model      | ASUS ZenBook S UX391UA Deep Dive Blue            |
| Processor           | Intel Core i7-8550U Processor @ 1.8 GHz(2.0GHz)  |
| Memory              | 16 GB LPDDR3 2133 MHz                            |
| Hard Disk           | Silicon Power 34A80(SM2262EN) PCIe NVMe 1TB      |
|                     | (Replaced) Samsung PM981 PCIe NVMe 512 GB        |
| Integrated Graphics | Intel(R) UHD Graphics 620                        |
| Screen              | BOE 1920x1080 (13.3 inch)                        |
| Sound Card          | Realtek ALC294                                   |
| Wireless Card       | Intel Dual Band Wireless-AC 8265                 |
| Bluetooth Card      | Intel Bluetooth 8265                             |


## Update(26/08):
1) Update kext to latest beta.
2) OC 0.6.2
3) Fix Colour banding.
4) Broke Keyboard backlight(will be fixed).
5) Intel wifi now supported through settings(like native).
6) Hand-off and other continuity features should work. Note: Airdrop still doesn't work. 

## Update(26/08):
Big Sur branch(Tested Beta 5)
1) Update kext to latest beta.
2) OC 0.6.1
3) Removed CPU friend(No benefit honestly).
4) Removed VoltageShift as undervolting can be done using modGRUBShell.efi
5) Removed all Thunderbolt related kexts and drivers as this too can be handled at BIOS level.

## BROKEN:
1) Airdrop
2) Keyboard backlight

## Unlock CFG Lock(BIOS 304):
Note: This works only on Asus Zenbook UX391 Bios version 304. If you have any other model use this [Guide](https://dortania.github.io/OpenCore-Install-Guide/extras/msr-lock.html)
1) Open modGRUBShell.efi
2) Type `setup_var 0x562 0x00`

## PM981:
1) You can not install macOS directly. You will need to create a VM and install macOS to a disk. Backup and restore the disk to PM981.
2) Sleep does not work. Kernel Panic on wake.
3) Just replace the NVMe with a compatible drive.

## Silicon Power 34A80 1TB:
The drive reviews that you will find online are for Phison’s E12 NVMe controller, paired with Toshiba’s BiCS3 64L TLC NAND flash. Sometime in early 2020, Silicon Power changed the controller to SMI SM2262EN with Intel TLC NAND flash(presumably 96L) manufactured by Unic or KYEC marked as 06T1TA9D010. This drive performs better than PM981 and has lower power consumption. The drive also works OOB with macOS.

## Thunderbolt 3.0:
1) The thunderbolt port works when any USB 3.0 plugged into it or by plugging in the Asus Type-C dock at the boot time.
2) Due to lack of Thunderbolt devices I haven't completely able to test it.

## Intel Wi-Fi AC 8265:
1) Works but slow(approx 40 Mbps up/down).

More info at: [OpenIntelWireless](https://github.com/OpenIntelWireless)

## FN Keys:
Using AsusSMC we are able to get all the FN keys working. Due to lack of 2 buttons to control Keyboard brightness, we sacrifice the F6 for lowering KB backlight. F7 remains to increase the backlight.

## ALCPlugFix:
Needed for 3.5mm Aux to work post sleep. Install by running `./install.sh`

## Advanced Users only(If you brick your device please do not ask me, do only if you know what you are doing):
BIOS 304 offsets for setup_var

|Detail	             |Var location|Value|Default|
| :--- | :---|:---|:---|
|CFG Lock	            |0x562|0x00|0x01|
|Overclock Lock	      |0x611|0x00|0x00|
|BIOS Lock	          |0x95F|0x00|0x01|
|Overclock feature	  |0x6D1|0x01|0x00|
|Core(VO)	            |0x6D7|0x4B (-75mv)|0x00|
|Core(OP)(-ve)	      |0x6D1|0x01|0x00|
|unCore(VO)	          |0x90A|0x4B (-75mv)|0x00|
|unCore(OP)(-ve)	    |0x90C|0x01|0x00|
|GT(VO)	              |0x912|0x32 (-50mv)|0x00|
|GT(OP)(-ve)	        |0x914|0x01|0x00|
|GPIO3 ForcePwr	      |0x456|0x01|0x00|
|TB Security Level	  |0x459|0x00|0x01|


Please feel free to test stuff.
