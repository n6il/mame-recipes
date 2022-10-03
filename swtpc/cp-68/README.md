# MAME Recipe for running CP/68 1.0 on SWTPC 6800

## Required MAME Patch and Settings

In order to boot CP/68 there are two requirements:

1. MAME must be patched to detect the CP/68 Disk Image Format. Patch is here [mame-cp68.patch](mame-cp68.patch).
2. MAME must be properly configured in order to boot the disk image.  Please follow quick start instructions or consult [swtpc.cfg](swtpc.cfg) for the required settings:
    1. `SWTBUG disk boot patch, load at 0xa100` must be set to `No`
    2. `Expected density` must be set to `single density`
    3. `FLEX expected sectors per side` must be set to `18`
    4. `FLEX track zero expected sectors per side` must be set to `18`

## Quick Start
1. Copy the `swtpc.cfg` file into your MAME `cfgpath` directory
2. Copy `swtpc.zip` into your MAME `rompath` directory
3. Run the emulator:
    1. Using MAME GUI:
        1. Copy the `swtpc.ini` file into your MAME `inipath` directory
        2. Ensure that `CP68.DSK` is in the current directory
        3. Select `SWTPC 6800 Computer System (with SWTBUG)`
    2. Command Line:

            mame -window swtpc -flop1 CP68.DSK

4. At the SWTBUG Prompt type `D` to boot the disk

## MAME Settings and Options
1.  The `swtpc` machine has a default setting for `SWTBUG_LOAD_AT_A100` which will not work for regular FLEX images.  Regular FLEX loads at `$2600`.  The fix is to disable this setting by setting it to `0`.  The config below has already been set in `swtpc.cfg`:
  
 ```
<mameconfig version="10">
    <system name="swtpc">
        <input>
            <port tag=":SWTBUG_LOAD_AT_A100" type="CONFIG" mask="1" defvalue="1" value="0" />
        </input>
    </system>
</mameconfig>
```
 
2. `Expected density` must be set to `single density`
3. `FLEX expected sectors per side` must be set to `18`
4. `FLEX track zero expected sectors per side` must be set to `18`

## Disk Images

|Size|Sides|Density|FormFactor|Tracks|MAME|
|----|-----|-------|----------|------|----|
|89600|Single|Single|5.25"|35|`sssd35`|

# Sources & References

Source: [https://deramp.com/downloads/swtpc/software/CP68/](https://deramp.com/downloads/swtpc/software/CP68/)

Reference: [Readme.txt](https://deramp.com/downloads/swtpc/software/CP68/-ReadMe.txt)


