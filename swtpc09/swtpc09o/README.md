# SWTPC S/09 OS9 Level 1
## Info
* SWTPC 6809 Computer
* io0 -- mps2 MP-S2 Dual Serial Interface
    * io0:mps2:rs232_upper
    * io0:mps2:rs232_lower
* io1 -- dc5 DC5 Floppy Disk Controller
    * io1:dc5:fdc:0
    * io1:dc5:fdc:1
    * io1:dc5:fdc:2
    * io1:dc5:fdc:3

## Running
    mame swtpc09o -io1:dc5:fdc:0 qd -flop1 OS9BTBK3.DSK

