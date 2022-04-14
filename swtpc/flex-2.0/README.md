# MAME Recipe for running FLEX 2.0 on SWTPC 6800

## Quick Start
1. Copy the `swtpc.cfg` file into your MAME `cfgpath` directory
2. Copy `swtpc.zip` into your MAME `rompath` directory
3. Run the emulator:
    1. Using MAME GUI:
        1. Copy the `swtpc.ini` file into your MAME `inipath` directory
        2. Ensure that `FLEX2-35.DSK` is in the current directory
        3. Select `SWTPC 6800 Computer System (with SWTBUG)`
    2. Command Line:

            mame -window swtpc -flop1 FLEX2-35.DSK

4. At the SWTBUG Prompt type `D` to boot the disk

## Variations
### Single-Sided Single-Density 5.25" 35-Track
1. Using MAME GUI
    1. Copy the `swtpc.ini` or `swtpc-flex2-35.ini` file into your MAME `inipath` directory named as `swtpc.ini`
    2. Ensure that `FLEX2-35.DSK` is in the current directory
    3. Select `SWTPC 6800 Computer System (with SWTBUG)`

2. Command Line

        mame -window swtpc -flop1 FLEX2-35.DSK

    or

        mame -window swtpc -io5:dc5:fdc:0 sssd35 -flop1 FLEX2-35.DSK


### Double-Sided Single-Density 5.25" 40-Track
1. Using MAME GUI
    1. Copy the `swtpc-flex2-ds.ini` file into your MAME `inipath` directory named as `swtpc.ini`
    2. Ensure that `FLEX2-DS.DSK` is in the current directory
    3. Select `SWTPC 6800 Computer System (with SWTBUG)`

2. Command Line

        mame -window swtpc -io5:dc5:fdc:0 dssd -flop1 FLEX2-DS.DSK

# Notes
## Disk Images

|Size|Sides|Density|FormFactor|Tracks|MAME|
|----|-----|-------|----------|------|----|
|89600|Single|Single|5.25"|35|`sssd35`|
|102400|Single|Single|5.25"|40|`sssd`|
|204800|Double|Single|5.25"|40|`dssd`|

# Sources & References

Source: [https://deramp.com/downloads/swtpc/software/FLEX/FLEX%202.0%20and%203.0%20Disk%20Images/](https://deramp.com/downloads/swtpc/software/FLEX/FLEX%202.0%20and%203.0%20Disk%20Images/)

Reference: [Readme.pdf](https://deramp.com/downloads/swtpc/software/FLEX/FLEX%202.0%20and%203.0%20Disk%20Images/-ReadMe.pdf)


