# VE

VE (Video Encoder) encodes an PAL/NTSC/SECAM (the latter seems to be not always present, e.g. in Titania4).

It can also put VBIs like CC (Closed Caption), WSS (Wide Screen Signalling), VPS (Video Programme System) and Teletext.

Apart of the CVBS and S-Video signals it can output YPbPr and RGB as well.

For the input part it can downscale it (but can't upscale!), and it seems to have multiple input sources?

## Registers

-  0x1f207600 [0x103b00]: [VE0 (VE Source)](#ve-source)
-  0x1f207c00 [0x103e00]: [VE1 (VE Encoder)](#ve-encoder)
-  0x1f207e00 [0x103f00]: [VE2 (VE Encoder Ex)](#ve-encoder-ex)

### VE Source
```
reg00:
    b0 = enable ve
    b1 = enable ccir656 (1)
    b2 = enable tv encoder
    b3 = enable vbi?
    b4 = soft reset
    b5 = reg load
    b6 = enable ccir656 (2)
    b7 = ..?
    b8 = disable h scaling
    b9 = disable v scaling
    b10 = set test pattern <?>

reg02:
    b0~b23 = capture buffer read MIU address [3..26]

reg06:
    b0~b23 = Teletext buffer miu address [3..26]

reg0A:
    b0~b23 = Teletext buffer size [3..26]

reg0C:
    b0~b15 = ?

reg10:
    b2 = Teletext read done status
    b8~b15 = ?

reg12:
    b10 = Teletext read done status clear (set then cleared)

reg16:
    b3 = ?

reg20:
    b0 = interlaced source?
    b1 = swap fields

reg22:
    b0~b11 = ?

reg24:
    b0~b11 = capture window HStart

reg26:
    b0~b11 = capture window HEnd

reg28:
    b0~b11 = capture window VStart

reg2A:
    b0~b11 = capture window HEnd

reg2C:
    b0~b10 = horizontal scaling ratio (bias 0x400)
       [ val = dstw * 0x400 / srcw ]

reg2E:
    b0~b10 = vertical scaling ratio (bias 0x400)
       [ val = dsth * 0x400 / srch ]

reg40:
    b0 = FRC enable

reg42:
    b0~b23 = FRC full count

reg4E:
    b0~b7 = ?

reg60:
    b0~b23 = FRC empty count

reg52:
    b0~b15 = ?

reg64:
    b0~b7 = ?

reg6E:
    b0~b15 = ?

reg70:
    b6 = enable solid color
    b7~b14 = solid color Y

reg72:
    b0~b7 = solid color U? Pb?
    b8~b15 = solid color V? Pr?

reg80:
    b0 = ccir656 output standard (0: NTSC, 1: PAL)

reg84:
    b0~b9 = frame line count

reg86:
    b0 = <disables teletext datas?>
    b1 = <toggled when teletext is enabled> %trigger transition%
    b2~b7 = ?

reg88:
    b0~b15 = ?

reg8A:
    b0~b15 = field size [3..18?]

reg8C:
    b2 = <set when the CC or Teletext is enabled>
    b4~b7 = ?
    b0~b15 = ?

reg8E:
    b0~b10 = ccir656 frame line count
    b11~b15 = ?

reg90:
    b0~b10 = ccir656 field 0 blank start

reg92:
    b0~b10 = ccir656 field 0 blank end

reg94:
    b0~b10 = ccir656 field 1 blank start

reg96:
    b0~b10 = ccir656 field 1 blank end

reg98:
    b0~b10 = ccir656 field start

reg9A:
    b0~b10 = ccir656 field end

reg9C:
    b0~b10 = ccir656 field 0 start line

reg9E:
    b0~b10 = ccir656 field 0 end line

regA0:
    b0~b10 = ccir656 field 1 start line

regA2:
    b0~b10 = ccir656 field 1 end line

regAA:
    b0~b7 = <osd enable thing, enable sets 0x15, disable clears 0x13>

regB4:
    b0 = ? enable scaler in?

regF6:
    b0~b23 = capture buffer write miu address [3..26]

regFC:
    b1 = ?
    b4 = SOG enable?
    b8 = ?
```

### VE Encoder
```
reg00:
    b0~b7 = hsync start
    b8~b15 = hsync end

reg02:
    b0~b7 = color burst start
    b8~b15 = color burst end

reg04:
    b8 = disable C mix into X
    b9 = disable Y mix into X

reg06:
    b1 = <set for PAL-M/PAL-N/PAL-NC>
    b3 = total line count (0: 525, 1: 625)
    b4 = display color bars

reg08:
    b0~b15 = contrast (bias 0x8000)

reg0C:
    b0 = <set for PAL-M/PAL-N/PAL-NC/PAL> "pal switch"
    b1 = <set for PAL-M/PAL-N/PAL-NC/PAL/SECAM>

reg0E:
    b0 = output disable?

reg12:
    b0~b10 = line period
       [Fh = Fve<27MHz> / val]

reg14:
    b0~b15 = brightness (bias 0x8000)

reg16:
    b0~b31 = color subcarrier frequency (phase accumulator step)
       [Fsc = val * 2^32 / Fve<27MHz>]

reg1A:
    b0~b15 = ? "lower stage fraction"

reg1C:
    b0~b9 = ? "625 stage fraction"

reg4A:
    b0~b10 = active period start

reg4C:
    b0~b10 = active period end

reg4E:
    b0~b7 = sync tip level?
    b8~b15 = sync pad level?

reg50:
    b0~b7 = sync step?
    b8~b15 = blank level?

reg52:
    b0~b7 = burst amp?
    b8~b15 = burst step?

reg54:
    b0~b15 = chroma gain?

reg56:
    b0~b15 = CC data (odd field)

reg58:
    b0~b15 = CC data (even field)

reg5A:
    b0~b15 = Y clamp?

reg5C:
    b0 = enable CC
    b1 = enable VPS
    b2 = enable WSS
    b3 = enable Teletext
    b7 = VBI stuff master enable? enable VBI?

reg68:
    b0~b31 = VPS data [0..31]

reg6C:
    b0~b31 = VPS data [32..63]

reg70:
    b0~b31 = VPS data [64..95]

reg74:
    b0~b7 = VPS data [96..103]

reg76:
    b0~b13 = WSS data

reg78:
    b0~b31 = Teletext active lines bitmap

reg7A:
    b8~b15 = ?

reg7C:
    b0~b13 = WSS data <?>

reg7E:
    b0~b15 = ?

reg80:
    b0~b1 = VE YPbPr output / VE output select:
      0 => CVBS and S-Video
      1 => YPbPr
      2 => RGB
      3 => same as 2?

reg9C:
    b0~b10 = CC line start (odd field)

reg9E:
    b0~b10 = CC line end (odd field)

regA0:
    b0~b10 = CC line start (even field)

regA2:
    b0~b10 = CC line end (even field)

regA4:
    b0~b10 = VPS line start (odd field)

regA6:
    b0~b10 = VPS line end (odd field)

regA8:
    b0~b10 = VPS line start (even vield)

regAA:
    b0~b10 = VPS line end (even field)

regAC:
    b0~b10 = WSS line start (odd field)

regAE:
    b0~b10 = WSS line end (odd field)

regB0:
    b0~b10 = Teletext line start (odd field)

regB2:
    b0~b10 = Teletext line end (odd field)

regB4:
    b0~b10 = Teletext line start (even field)

regB6:
    b0~b10 = Teletext line end (even field)

regB8:
    b0~b31 = CC frequency (phase accumulator step)
       [Fcc = val * 2^32 / Fve<27MHz>]

regBC:
    b0~b31 = VPS frequency (phase accumulator step)
       [Fvps = val * 2^32 / Fve<27MHz>]

regC0:
    b0~b31 = WSS frequency (phase accumulator step)
       [Fwss = val * 2^32 / Fve<27MHz>]

regC4:
    b0~b31 = Teletext frequency (phase accumulator step)
       [Fttx = val * 2^32 / Fve<27MHz>]

regC8:
    b0~b10 = CC start

regCA:
    b0~b10 = VPS start

regCC:
    b0~b10 = WSS start

regCE:
    b0~b10 = Teletext start

regD0:
    b0~b9 = CC level

regD2:
    b0~b9 = VPS level

regD4:
    b0~b9 = WSS level

regD6:
    b0~b9 = Teletext level

regD8:
    b0~b10 = WSS line start (even field)

regDA:
    b0~b10 = WSS line end (even field)

regF0:
    b0~b15 = Macrovision control?
```

### VE Encoder Ex
```
reg20:
    b0 = enable SECAM
    b0~b3 = ?
    b4~b5 = <changes something in SECAM...>

reg24:
    b0~b31 = SECAM B-Y subcarrier frequency (phase accumulator step)
       [Fby = val * 2^32 / Fve<27MHz>]

reg28:
    b0~b31 = SECAM R-Y subcarrier frequency (phase accumulator step)
       [Fry = val * 2^32 / Fve<27MHz>]

reg38:
    b0~b8 = SECAM B-Y component deviation factor?

reg3A:
    b0~b8 = SECAM R-Y component deviation factor?

reg44:
    b0~b31 = some 350khz clock? for SECAM? (phase accumulator step)
       [Fxxx = val * 2^32 / Fve<27MHz>]

regEE:
    b0~b15 = ?

regF0:
    b0~b15 = ?
```

