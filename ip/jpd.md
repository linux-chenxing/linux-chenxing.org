# JPD

JPD (JPeg Decoder) is an hardware JPEG decoder...

- ROI (Region Of Interest)
- RCSM -- the data after the SOS (FF-DA) marker
- MRC -- input jpeg file data
- MWC -- output framebuffer
- TID -- internal data stuff with huffman tables/idct quantize tables/etc

## Registers

**Note, except for lines, the coordinates and sizes are specified in 8-pixel blocks!**

```
reg00: s config
    b0~b1 = [Comp_H_sampling]
    b2 = [Comp_V_sampling - 1]
    b3 = Color format
      0 => Y (grayscale)
      1 => YCbCr
    b4~b5 = Downscale ratio
      0 => 1/1
      1 => 1/2
      2 => 1/4
      3 => 1/8
    b6 = Enable restart interval
    b7 = Start decoding
    b10 = Progressive mode
    b11 = Enable ROI
    b13 = ?? when set, accessing reg80/reg82 does not lock up RIU

    b0~b6
    b8~b15

    b8 = ?? always set to 1...
    b9 = ?? jpd_suvq -> set when there is more than two IDCT quant tables
    b10 = enable downscale? progressive mode?
    b14 = ??

reg02: m config
    b3 = Reset

    b0~b1
    b2~b15

    b0 = ?? should be set otherwise decoding won't go
    b1 = ??
    b7 = ??
    b8 = write protect

reg04: rst intv
    b0~b15 = Restart interval (-1)

reg06: pic h
    b0~b10 = Picture width

reg08: pic v
    b0~b10 = Picture height

reg0A: roi h
    b0~b10 = ROI start column

reg0C: roi v
    b0~b10 = ROI start row

reg0E: roi width
    b0~b10 = ROI width

reg10: roi height
    b0~b10 = ROI height

reg12: int en
    b0~b6 = interrupt enable bits

reg14: event flag
    b0~b6 = interrupt pending bits

reg16-19: rcsm addr
    b0~b27 = RCSM "MRC start" MIU address [0..27]

reg1A-1D: mrc buff floor
    b0~b24 = MRC "Read buffer" buffer MIU start address [3..27]

reg1E-21: mrc buff ceil
    b0~b24 = MRC "Read buffer" buffer MIU end address [3..27]

reg22-25: mwc buff start addr
    b0~b24 = MWC "Output frame buffer" buffer MIU address [3..27]

reg26: mw buff line num
    b0~b13 = MWC "Output frame buffer" buffer line count

reg28: cur mrc addr
    b0~b27 = Current MRC buffer MIU address [0..27]

reg2C: cur row
    b0~b10 = Current row

reg2E: cur col
    b0~b10 = Current column

reg30: cur vidx
    b0~b10 = Current line

reg38: spare
    b0~b15

... ? ...

reg80: tid addr
    b0~b11 = TID address
    * Address is auto incremented by 1 after read-accessing the top 8 bits
    * The RIU bus will lock up if the bit13 in reg00 is not set

reg82: tid dat
    b0~b15 = TID data
    * Address is auto incremented by 2 or 1 (depending on access width)
    * The RIU bus will lock up if the bit13 in reg00 is not set

... alias of 04~7F ...

```
