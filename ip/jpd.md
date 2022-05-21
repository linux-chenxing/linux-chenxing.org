# JPD

JPD (JPeg Decoder) is an hardware JPEG decoder...

-  ROI (Region Of Interest)
-  RCSM -- set to the data after the FF-DA (SOS) marker
-  MRC -- input jpeg file data
-  MWC -- output framebuffer

## Registers

```
reg00: s config
    b0~b6
    b8~b15
    
    b7 = ?? <set at the last moment when decoding>
    b10 = enable downscale?
    b11 = enable ROI?
    b13 = ?? <clr then set after reset>
    b14 = ?? <set on decode>

reg02: m config
    b0~b1
    b2~b15
    
    b3 = reset?
    b8 = write protect

reg04: rst intv
    b0~b15

reg06: pic h
    b0~b10 = pic h [3..13]

reg08: pic v
    b0~b10 = pic v [3..13]

reg0A: roi h
    b0~b10 = ROI h

reg0C: roi v
    b0~b10 = ROI v

reg0E: roi width
    b0~b10 = ROI width

reg10: roi height
    b0~b10 = ROI height

reg12: int en
    b0~b6

reg14: event flag
    b0~b6

reg16: rcsm addr
    b0~b27 = RCSM "MRC start" MIU address [0..27]

reg1A: mrc buff floor
    b0~b24 = MRC "Read buffer" buffer MIU start address [3..27]

reg1E: mrc buff ceil
    b0~b24 = MRC "Read buffer" buffer MIU end address [3..27]

reg22: mwc buff start addr
    b0~b24 = MWC "Output frame buffer" buffer MIU address [3..27]

reg26: mw buff line num
    b0~b13 = MWC "Output frame buffer" buffer line count

reg28: cur mrc addr
    b0~b27 = Current MRC buffer MIU address [0..27]

reg2C: cur row
    b0~b10 = Current row [3..13?]

reg2E: cur col
    b0~b10 = Current column [3..13?]

reg30: cur vidx
    b0~b10 = Current line

reg38: spare
    b0~b15

... ? ...

reg80: tid addr
    **Note: Accessing locks up RIU bus**
    b0~b15

reg82: tid dat
    **Note: Accessing locks up RIU bus**
    b0~b15

... alias of 04~7F ...

```

```
<< MStar >># md bf202e00
BF202E00: 00002109 00000000 00000000 0000005A    .!..........Z...
BF202E10: 00000048 00000000 00000000 00000000    H...............
BF202E20: 00000000 0000007F 00000001 000001EF    ................
BF202E30: 00000000 00000000 00000000 0000FFFF    ................
BF202E40: 00000001 00006000 0000000E 00000000    .....`..........
BF202E50: 00005AB2 00000001 00000000 00000000    .Z..............
BF202E60: 00000240 0000017F 00000000 00000000    @...............
BF202E70: 0000007B 00000000 00000000 00000000    {...............
BF202E80: 00000000 00000000 00000000 00000000    ................
BF202E90: 00000000 00000000 00000000 00000000    ................
BF202EA0: 00000001 00000000 00000000 00000000    ................
BF202EB0: 00000000 00000000 00000000 00000000    ................
BF202EC0: 00000000 00000000 00000000 00000000    ................
BF202ED0: 00000000 00000000 00000000 00000000    ................
BF202EE0: 00000000 00000000 00000000 00000000    ................
BF202EF0: 00000000 00000000 00000000 00000000    ................
<< MStar >># md bf202f08
BF202F08: 00000000 0000005A 00000048 00000000    ....Z...H.......
BF202F18: 00000000 00000000 00000000 0000007F    ................
BF202F28: 00000001 000001EF 00000000 00000000    ................
BF202F38: 00000000 0000FFFF 00000001 00006000    .............`..
BF202F48: 0000000E 00000000 00005AB2 00000001    .........Z......
BF202F58: 00000000 00000000 00000240 0000017F    ........@.......
BF202F68: 00000000 00000000 0000007B 00000000    ........{.......
BF202F78: 00000000 00000000 00000000 00000000    ................
BF202F88: 00000000 00000000 00000000 00000000    ................
BF202F98: 00000000 00000000 00000001 00000000    ................
BF202FA8: 00000000 00000000 00000000 00000000    ................
BF202FB8: 00000000 00000000 00000000 00000000    ................
BF202FC8: 00000000 00000000 00000000 00000000    ................
BF202FD8: 00000000 00000000 00000000 00000000    ................
BF202FE8: 00000000 00000000 00000000 00000000    ................
BF202FF8: 00000000 00000000 00000000 00000000    ................
<< MStar >># md bf202f00
BF202F00:
```
