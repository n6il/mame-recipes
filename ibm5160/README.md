The IBM HDC Card supports 4 drives:

http://minuszerodegrees.net/ibm_xebec/ibm_xebec.htm

MAME does have dip switch settings for these, but
no matter which position you have the jumpers set in
the machines assumes a type 2 drive:

CHS
echo $((615*4*17))
41820 sectors

SIZE

echo $((615*4*17*512))
21411840 bytes

    chdman createhd -o pcmfm2t20mb-pcdos210.chd -chs 615,4,17
    ~/src/mame/mame -resolution 640x480 -switchres -window ibm5160 -hard1 pcmfm2t20mb-pcdos210.chd
    ~/src/mame/mame -resolution 640x480 -switchres -window ibm5170 -isa4 hdc -hard1 pcmfm2t20mb-pcdos210.chd
    ~/src/mame/mame -resolution 640x480 -switchres -window at386 -hard1 pcmfm2t20mb-pcdos210.chd
