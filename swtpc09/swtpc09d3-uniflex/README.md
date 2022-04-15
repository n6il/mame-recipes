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
*** BEWARE *** This will eat your disk images.  It is highly recomended to make backups.

1. Using MAME GUI
        1. Copy the `swtpc09d3-fd0.ini` file into your MAME `inipath` directory
        2. Ensure that `UNIFLEXFLOPPYBOOT.DSK` is in the current directory
        3. Select `swtpc S/09 UNIBug + DMAF3`

2. Command Line

        mame -window swtpc09d3 -flop1 UNIFLEXFLOPPYBOOT.DSK


# Notes
## MAME Settings and Options
* The `swtpc09d3` machine has a MP-S2 card in slot `io0`.  This card has two serial ports, named `rs232_upper` and `rs232_lower`.  The default setting for this machine is to show two terminal windows: The left window is the main console on `rs232_upper` and the right window is the `rs232_lower`.  Why the driver is confured this way is a bit mysterious.  The fix is to disable the second `rs232_lower` terminal by simply redirecting it to `null_modem` instead of the default `serial_terminal`.  The config below has already been set in `swtpc09d3.ini` but you can also add this setting as a command line option:

        io0:mps2:rs232_lower null_modem


## Disk Images

|Size|Sides|Density|FormFactor|Tracks|MAME|
|----|-----|-------|----------|------|----|
|315392|Single|Single|8"|77|`8sssd`|
|630784|Double|Single|8"|77|`8dssd`|
|1261568|Double|Double|8"|77|`8dsdd`|

# Sources & References
 
1. [Evenson Consulting's SWTPC 6800/6809 Emulator](http://www.evenson-consulting.com/swtpc/Downloads.htm)
2. [http://swtpcemu.com/swtpc/Manuals/UniFLEX/](http://swtpcemu.com/swtpc/Manuals/UniFLEX/)
3. [http://swtpcemu.com/swtpc/Manuals/SWTPC_Hardware/](http://swtpcemu.com/swtpc/Manuals/SWTPC_Hardware/)
4. [Soren Roug's UniFLEX/6809 Retro Computing Page](https://www.roug.org/retrocomputing/os/UniFLEX) 
5. [kees1948/UniFLEX](https://github.com/kees1948/UniFLEX)


