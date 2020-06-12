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

## Update(13/06):
1) SMBios to MacbookPro16,3. i7-8557U is the closed to 8550U architecturally.
2) OC 0.5.9 update.
3) Audio fix using CC.
4) Fixed FN keys using AsusSMCDaemon.
5) Intel wifi works but slow.
6) Fixed Battery indicator.
7) Fixed Thunderbolt 3.0 partially.

## BROKEN:
Nothing actually. Airdrop and Continuty don't work due to unsupported hardware.

## PM981:
1) You can not install macOS directly. You will need to create a VM and install macOS to a disk. Backup and restore the disk to PM981.
2) Sleep does not work. Kernel Panic on wake.
3) Just replace the NVMe with a compatible drive.

## Silicon Power 34A80 1TB:
The drive reviews that you will find online are for Phison’s E12 NVMe controller, paired with Toshiba’s BiCS3 64L TLC NAND flash. Sometime in early 2020, Silicon Power changed the controller to SMI SM2262EN with Intel TLC NAND flash(presumably 96L) manufactured by Unic or KYEC marked as 06T1TA9D010. This drive performs better than PM981 and has lower power consumption. The drive also works OOB with macOS.

## Thunderbolt 3.0:
1) The thunderbolt port works when any USB 3.0 plugged into it or by plugging in the Asus Type-C dock for boot.
2) Hotplugging works as long as the the laptop doesn't go to sleep/hibernation.
3) Post sleep thunderbolt and USB 3.0 breaks but the port still works for HDMI out and USB 2.0.
4) Due to lack of Thunderbolt devices I haven't completely able to test it. Can cause KP at times.

## Intel Wi-Fi AC 8265:
1) Works but slow(approx 40 Mbps up/down).
2) Need to edit the `itlwm.kext/Contents/Info.plist`
```
<key>WiFi_1</key>
<dict>
  <key>password</key>
  <string>Wifi passowrd</string>
  <key>ssid</key>
  <string>Wifi SSID</string>
</dict>
```
3) Once edited place it in `EFI/OC/Kexts`

More info at: [itlwm](https://github.com/zxystd/itlwm)

## FN Keys:
Using AsusSMC we are able to get all the FN keys working. Due to lack of 2 buttons to control Keyboard brightness, we sacrifice the F6 for lowering KB backlight. F7 remains to increase the backlight.

## ALCPlugFix:
Needed for 3.5mm Aux to work post sleep. Install by running `./install.sh`

## VoltageShift(Advanced users):
Undervolting CPU and GPU allows to achieve better battery life and run the CPU cooler.
I have been able to achieve a -87 mV on CPU and CPU cache and -50 mV on GPU. Your values  will be different please test different values before enabling it on boot.

More info on how to use: [VoltageShift](https://github.com/sicreative/VoltageShift)

Please feel free to test stuff.
