# MAME Recipe for running UniFLEX on swtpc09d3 6809
UniFLEX can be booted from floppy or winchester Disk.  Quickstart walks you through the Winchester Disk recipe but recipes for both are provided below under Variations.  
## Quick Start
1. Copy `swtpc09.zip` into your MAME `rompath` directory
2. Run the emulator:
    1. Using MAME GUI:
        1. Copy the `swtpc09d3.ini` file into your MAME `inipath` directory
        2. Ensure that `uni-cmi5619-boot.chd` is in the current directory
        3. Select `swtpc S/09 UNIBug + DMAF3`
    2. Command Line:

            mame -window swtpc09d3 -io0:mps2:rs232_lower null_modem -hard1 uni-cmi5619-boot.chd

3. At the UNIBug Prompt type `W` to boot the from the Winchester Disk
4. When you are finished playing with UniFLEX you should shut down the system in a clean manner as follows:
    1. Type: `/etc/stop`
    2. The screen should show `System Stopped!`
    3. Press `F3` to reset the computer back to the UNIBug prompt
    4. Quit MAME

## Variations
### Booting Uniflex from a Floppy Disk
** BEWARE ** MAME has a bug where the disk image will be corrupted when the emulated comptuer writes to the disk.  It is highly recomended to make backups.

1. Using MAME GUI
        1. Copy the `swtpc09d3-fd0.ini` file into your MAME `inipath` directory
        2. Ensure that `UNIFLEXFLOPPYBOOT.DSK` is in the current directory
        3. Select `swtpc S/09 UNIBug + DMAF3`

2. Command Line

        mame -window swtpc09d3 -io0:mps2:rs232_lower null_modem -flop1 UNIFLEXFLOPPYBOOT.DSK


# Notes
## MAME Settings and Options
* The `swtpc09d3` machine has a MP-S2 card in slot `io0`.  This card has two serial ports, named `rs232_upper` and `rs232_lower`.  The default setting for this machine is to show two terminal windows: The left window is the main console on `rs232_upper` and the right window is the `rs232_lower`.  Why the driver is confured this way is a bit mysterious.  The fix is to disable the second `rs232_lower` terminal by simply redirecting it to `null_modem` instead of the default `serial_terminal`.  The config below has already been set in `swtpc09d3.ini` but you can also add this setting as a command line option:

        io0:mps2:rs232_lower null_modem


## Floppy Disk Images

|Size|Sides|Density|FormFactor|Cylenders|Sectors/Cyl|MAME|
|----|-----|-------|----------|------|-------|----|
|315,392|Single|Single|8"|77|8|`8sssd`|
|630,784|Double|Single|8"|77|8|`8dssd`|
|630,784|Single|Single|8"|77|16|`8dssd`|
|1,261,568|Double|Double|8"|77|16|`8dsdd`|

UniFLEX numbers disk sectors on double sided disks differently than most other computers.  This means that some tools may not work properly with them.  For example, a Double Sided Double Density disk has the sectors numbered as follows:

|Cylender|Head|Sectors|
|--------|----|-------|
| 0      | 0  | 1-16  |
| 0      | 1  | 17-32 |
|...|


## Winchester Disk Images

UniFLEX supports a number of different types and sizes of winchester disks.  MAME has support
for the DMAF3+WD1000 Controller setup.   The UniFLEX `/etc/formatwd1000` command formats the
winchester disk drives.  You can get a list of supported devices by running 

    /etc/formatwd1000 +M

and then answering `Y` to list all the available disk formats.  A subset of those drives and their CHS values is listed in the [UniFLEX Utility Commands](https://github.com/kees1948/UniFLEX/blob/master/Documents/Manuals/UniFLEX/Utility%20Commands.pdf) manual page 66.  On page 65 the manual also
says that the default drive is a Computer Memories CMI-5619.  The CHS for this drive is 306, 6, 17.  

### Creating a CHD Image
 
To create a CHD image for the CMI-5619 drive run:

    chdman createhd -o cmi5619-test.chd -c 306,6,17

### Formatting a CHD Image
Once you have the CHD image, you can attach it to MAME and format it.  For example, you can
attach it as a second hard drive either by adding it to your ini file (without the leading `-`)
or adding `-hard2 cmi5619-test.chd` on the command line.  Now you can format the drive:

    /etc/formatwd1000 +d=/dev/wd1  +m=CMI-5619

After the drive is formatted you can mount it:

    /etc/mount /dev/wd1 /usr3

### Using Pre-Made Hard Drive Images

It is possible to create a CHD image from an existing winchester disk image file.  For example, the `uni-cmi5619-boot.chd` hard drive image provided in this repository came from the Evenson Consulting SWTPC Emulator package.

    \ProgramData\EvensonConsultingServices\SWTPCmemulator\DISKS\wd0.DSK

In order to convert this into a CHD image you need to determine the CHS of the image itself.  First, start with the file size:

    -rw-r--r-- 1 pi pi 15980544 Apr 12 18:45 wd0.DSK

Well we don't know the exact CHS for this image, but based on the information above we should probably start with the default Computer Memories CMI-5619 drive.  The CHS for this drive is 306, 6, 17.  Multiplying this out yields:


    306 * 6 * 17 = 15980544

Since this is an exact match it should work out.  Create the CHD image as above which has been initialized with the `wd0.DSK` image:

    chdman createhd -chs 306,6,17 -o /tmp/wd0.chd -i wd0.DSK 


# Sources & References
 
1. [Evenson Consulting's SWTPC 6800/6809 Emulator](http://www.evenson-consulting.com/swtpc/Downloads.htm)
2. [http://swtpcemu.com/swtpc/Manuals/UniFLEX/](http://swtpcemu.com/swtpc/Manuals/UniFLEX/)
3. [http://swtpcemu.com/swtpc/Manuals/SWTPC_Hardware/](http://swtpcemu.com/swtpc/Manuals/SWTPC_Hardware/)
4. [Soren Roug's UniFLEX/6809 Retro Computing Page](https://www.roug.org/retrocomputing/os/UniFLEX) 
5. [kees1948/UniFLEX](https://github.com/kees1948/UniFLEX)


