- [Pre-requirement Setup how to boot from usb](#pre-requirement-setup-how-to-boot-from-usb)
- [Windows 10 Dell XPS Clean Installation](#dell-xps---windows-10-recovery---clean-install)
- [Ubuntu dual Dell XPS boot installation](##ubuntu-dual-dell-xps-boot-installation)
   - [Setup Ubuntu as a working space](#)

## Pre-requirement Setup how to boot from usb

1. Start the system while tapping F2 key to enter the BIOS
2. Change Boot List option to Legacy from UEFI
3. Then Change boot priority - Keep Internal Hard Drive as primary Boot Device/First boot device
4. Then change the Boot List Option from Legacy to UEFI, navigate to Advanced Boot Options, confirm the Secure Boot Option Disabled
5. Navigate to Exit and "Exit Saving Changes"


## DELL XPS - Windows 10 Recovery - Clean Install

1. Use Dell Windows 10 DVD/USB Media
2. Reboot and use the F12 boot menu option
3. Choose UEFI DVD/USB boot option then press the Enter key
4. Dell Screen will show for a few moments
   - When prompted, choose your language (English is default)
   - Choose your region (US Default)
5. Choose Troubleshoot
6. Choose Recover from a drive
7. Choose "Fully clean drive"
8. A pop up will appear, click the Recovery button
9. Dell screen – will show **recovering this PC XX%**
10. The system will Reboot to Windows 10 when the installation is finished

## Ubuntu dual Dell XPS boot installation

1. Reboot and use the F12 boot menu option
2. In installation option choose **something else**
3. Set partition
   - `/swap` : `32000` MB, `ext 4`, type `logical`
   - `/root` : `100000` MB,`ext 4`, type `logical`
   - `/home` : the remaining, `ext 4`, type `primary`
4. Finish the installation

## Setup Ubuntu as a working space



### Links

- https://www.dell.com/support/article/id/en/iddhs1/sln300635/how-to-install-windows-10-from-a-dell-windows-10-recovery-dvd?lang=en
- https://www.dell.com/support/article/id/en/iddhs1/sln301754/how-to-install-ubuntu-and-windows-8-or-10-as-a-dual-boot-on-your-dell-pc?lang=en#Installing
- https://www.dell.com/support/article/id/en/iddhs1/sln151841/how-to-install-ubuntu-with-multiple-custom-partitions-on-your-dell-pc?lang=en
