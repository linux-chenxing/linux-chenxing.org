# GE

GE (Graphics Engine) is an 2D graphics accelerator that can do many things:
- Draw rectangles
  - with gradients in two dimensions
- Draw lines
  - with gradients
  - and pattern
- Bitblit
   - Stretching with nearest neightbor or with some smoothing
   - Offset within source image (Tiled copy)
   - "Patch" mode (repeat last row/column when going off set image size)
   - Color space conversion (YUV->RGB and RGB->YUV)
   - Rotate (in fixed 0/90/180/270 angles?)
- Do source and dest color keying
- Various raster operations
- Various alpha blending stuff
- Dithering
- Italic font thing (slant/shear/wtw)
- maybe many more...

## Registers
-  0x1f205000 [0x102800]: GE
-  0x1f220e00 [0x110700]: Another GE
-  0x1f281200 [0x140900]: on Infinity2m?

**NOTE: The registers should be written in 16-bit words only! i.e. you can't read out a byte then modify and write it back,
if you do so then some nonsense will happen! If you are accessing it bytewise then the write order should be little endian (lower reg first)**

```
reg00: en0
    b0 = Enable GE
    b1 = Enable dithering
    b2 = Enable ABL (alpha blending)
    b5 = Enable ROP (raster opeation)
    b6 = Enable SCK (source color keying)
    b7 = Enable DCK (dest color keying)
    b8 = Enable LPT (line pattern)

reg02: en1
    b0 = Enable CMQ (command queue)
    b1 = Enable VCMQ (virtual? command queue)
    b2 = rpriority (miu read priority?)
    b3 = wpriority (miu write priority?)
    b4 = Enable STBB (stretch bitblt)
    b6 = Enable ITC ("italic" i.e. shear/slant/wtw)

reg04: dbg
    ??

reg06: stbb
    ??

reg0E: status
    b0 = GE is busy
    b1 = BLT is busy
    b7 = CMQ fifo is empty
    b11~b15 = CMQ fifo remaining count

reg20: rop2
    b0~b3 = ROP operation
      0 => 0
      1 => ~(src | dst)
      2 => (~src) & dst
      3 => ~src
      4 => src & (~dst)
      5 => ~dst
      6 => src ^ dst
      7 => ~(src & dst)
      8 => src & dst
      9 => ~(src ^ dst)
      A => dst
      B => (~src) | dst
      C => src
      D => src | (~dst)
      E => src | dst
      F => ~0

reg22: abl_coef
    b0~b3 = ABL coefficient:
      0 => One      [Csrc]
      1 => Const    [Csrc * Aconst + Cdst * (1 - Aconst)]
      2 => Asrc     [Csrc * Asrc + Cdst * (1 - Asrc)] 
      3 => Adst     [Csrc * Adst + Cdst * (1 - Adst)]
      4 => Zero     [Cdst]
      5 => 1-Const  [Csrc * (1 - Aconst) + Cdst * Aconst]
      6 => 1-Asrc   [Csrc * (1 - Asrc) + Cdst * Asrc]
      7 => 1-Adst   [Csrc * (1 - Adst) + Cdst * Adst]
      ... ??? ...
      8 => ROP8 Alpha   [((Asrc * Aconst) * Csrc + (1 - (Asrc * Aconst)) * Cdst) / 2]
      9 => ROP8 SrcOver [((Asrc * Aconst) * Csrc + Adst * Cdst * (1 - (Asrc * Aconst))) / ((Asrc * Aconst) + Adst * (1 - Asrc * Aconst))]
      A => ROP8 DstOver [((Asrc * Aconst) * Csrc * (1 - Adst) + Adst * Cdst) / (Asrc * Aconst) * (1 - Adst) + Adst]
      ... These are not supported? ...
      B => Const src   [Csrc * Aconst]
      C => 1-Const src [Csrc * (1 - Aconst)]
      D => src atop dst [Cdst * Adst * Asrc * Aconst + Cdst * Adst * (1 - Asrc * Aconst)]
      E => dst atop src [Cdst * Asrc * Aconst * Adst + Csrc * Asrc * Aconst * (1 - Adst)]
      F => src xor dst  [(1 - Adst) * Csrc * Asrc * Aconst + Adst * Cdst * (1 - Asrc * Aconst)]

reg24: db_abl
    b8~b11 = Destination alpha value:
      0 => Aconst
      1 => Asrc
      2 => Adst
      3 => Asrc * Aconst
      4 => Asrc * Aconst * Adst
      5 => Adst * (1 - Asrc * Aconst)
      6 => Asrc * Aconst * (1 - Adst)
      7 => Asrc * Aconst * (1 - Adst) + Adst
      8 => 1 - Aconst
      9 => 1 - Asrc
      A => 1 - Adst
      B => Adst * Asrc * Aconst + Adst * (1 - Asrc * Aconst)
      C => Asrc * Aconst * Adst + Asrc * Aconst * (1 - Adst)
      D => (1 - Adst) * Asrc * Aconst + Adst * (1 - Asrc * Aconst)
      E => Asrc * Asrc * Aconst + Adst * (1 - Asrc * Aconst) ???
      F => Asrc * (1 - Asrc * Aconst) + Adst * Asrc * Aconst

reg26: abl_const
    b0~b7 = ABL Aconst
    b8~b15 = ABL Aconst (for ARGB1555 with A=0)

reg28: sck_hth[0|1]
    b0~b31 = SCK color higher bound

reg2C: sck_lth[0|1]
    b0~b31 = SCK color lower bound

reg30: dck_hth[0|1]
    b0~b31 = DCK color higher bound

reg34: dck_lth[0|1]
    b0~b31 = DCK color lower bound

reg38: blt_ck_op_ode
    b0 = SCK mode:
    b1 = DCK mode:
      0 => Perform color keying when the color is within bounds
      1 => Perform color keying when the color is out of bounds

reg3C: irq?
    ?? an infinity2m+ thing ??
    b6~b7 = mask
    b8~b9 = force
    b10~b11 = clear
    b12~b13 = final status
    b14~b15 = raw status

reg3E: dc_csc_fm
    b0 = RGB to YUV range:
      0 => Y=16~235, UV=0~240
      1 => YUV=0~255
    
    b2 = Y output range
      0 => Y=0~255
      1 => Y=16~235
    
    b3 = UV input range
      0 => UV = 0~255
      1 => UV = -128~127
    
    b4~b5 = YUV source format:
    b6~b7 = YUV dest format:
      0 => YVYU
      1 => YUYV
      2 => VYUY
      3 => UYVY

reg40: sb_base_[l|h]
    b0~b31 = Source bitmap base address

reg4C: db_base_[l|h]
    b0~b31 = Dest bitmap base address

reg50: vcmq_base_[l|h]
    b0~b31 = VCMQ base address

reg54: vcmq_size
    b0~b2 = VCMQ size
      0 => 4k
      1 => 8k
      2 => 16k
      3 => 32k
      4 => 64k
      5 => 128k
      6 => 256k
      7 => 512k
      8 => 1024k

reg5A: p256_[0|1]
    b0~b31 = 256-color palette value (see pri_[gb|ar]_st)

reg5E: p256_idx
    b0~b7 = 256-color palette index
    b8 = 256-color palette write

reg60: sb_pit
    b0~b15 = Source bitmap stride

reg66: db_pit
    b0~b15 = Destination bitmap stride

reg68: b_fm
    b0~b3 = Source bitmap format:
    b8~b11 = Destination bitmap format:
      0 => I1 (1 bpp, 2-color palette)
      1 => I2 (2 bpp, 4-color palette)
      2 => I4 (4 bpp, 16-color palette)
      3 => I8 (8 bpp, 256-color palette)
      8 => RGB565
      9 => ARGB1555
      A => ARGB4444
      B => 1BAAFgBg123433 (some GOP blinking format)
      C => ARGB1555_DST (for dest, the A bit sets when the alpha is nonzero)
      D => ARGB6666
      E => YUV422
      F => ARGB8888

reg6A: i0_c[0|1]
    b0~b31 = 16-color palette value 0 (see pri_[gb|ar]_st)

reg6E: i1_c[0|1]
    b0~b31 = 16-color palette value 1

reg72: i2_c[0|1]
    b0~b31 = 16-color palette value 2

reg76: i3_c[0|1]
    b0~b31 = 16-color palette value 3

reg7A: i4_c[0|1]
    b0~b31 = 16-color palette value 4

reg7E: i5_c[0|1]
    b0~b31 = 16-color palette value 5

reg82: i6_c[0|1]
    b0~b31 = 16-color palette value 6

reg86: i7_c[0|1]
    b0~b31 = 16-color palette value 7

reg8A: i8_c[0|1]
    b0~b31 = 16-color palette value 8

reg8E: i9_c[0|1]
    b0~b31 = 16-color palette value 9

reg92: i10_c[0|1]
    b0~b31 = 16-color palette value 10

reg96: i11_c[0|1]
    b0~b31 = 16-color palette value 11

reg9A: i12_c[0|1]
    b0~b31 = 16-color palette value 12

reg9E: i13_c[0|1]
    b0~b31 = 16-color palette value 13

regA2: i14_c[0|1]
    b0~b31 = 16-color palette value 14

regA6: i15_c[0|1]
    b0~b31 = 16-color palette value 15

regAA: clip left
    b0~b15 = clip window left

regAC: clip right
    b0~b15 = clip window right

regAE: clip top
    b0~b15 = clip window top

regB0: clip bottom
    b0~b15 = clip window bottom

regB2: rot
    b0~b1 = rotation angle:
      0 => 0
      1 => 90
      2 => 180
      3 => 270
    b2~b15 = ?

regB6: stbb_sck_type
    b0~b1 = What STBB will do when source color key will be matched
      0 => "ignore" / "do nothing"
      1 => stretch with nearest-neightbor?
      2 => replace with set color

regB8: stbb_sck_[bg|ar]
    b0~b31 = color that will be put on stbb_sck_type==2 (see pri_[gb|ar]_st)

regBC: stbb_ini_dx
    b0~b12 = STBB stretch delta x init
        [ val = (srcw - dstw) * 0x1000 / (dstw * 2) ]

regBE: stbb_ini_dy
    b0~b12 = STBB stretch delta y init
        [ val = (srch - dsth) * 0x1000 / (dsth * 2) ]

regC0: cmd
    b4~b6 = command:
      1 => Draw line
      3 => Draw rectangle
      4 => Bitblt
    b7 = Invert source X
    b8 = Invert source Y
    b9 = Invert dest X
    b10 = Invert dest Y
    b11 = Draw line with gradient
    b12 = Draw rect with horizontal gradient
    b13 = Draw rect with vertical gradient
    b14 = STBB nearest-neighbor mode
    b15 = STBB patch mode (Repeat the last row/column when going out off image size)

regC2: line
    b1~b14 = Line delta Y/X (bias 0x1000, twos complement)    
    b15 = Swap X/Y coordinates

regC4: lpt
    b0~b5 = line pattern bits
    b6~b7 = line pattern period:
      0 => 1 pixel
      1 => 2 pixels
      2 => 4 pixels
      3 => 8 pixels
    b8 = reset line pattern

regC6: line_len
    b0~b11 = line length

regC8: stbb_dx
    b0~b12 = STBB stretch delta x
        [ val = srcw * 0x1000 / dstw ]

regCA: stbb_dy
    b0~b12 = STBB stretch delta y
        [ val = srch * 0x1000 / dsth ]

regCC: itc0
    b0~b7 = ??ini_line
    b8~b15 = ??ini_dis

regCE: itc1
    b0~b4 = itc delta

regD0: pri_v0_x
    b0~b15 = X0 coordinate (left)

regD2: pri_v0_y
    b0~b15 = Y0 coordinate (top)

regD4: pri_v1_x
    b0~b15 = X1 coordinate (right)

regD6: pri_v1_y
    b0~b15 = Y1 coordinate (bottom)

regD8: pri_v2_x
    b0~b15 = X2 coordinate (tile x)

regDA: pri_v2_y
    b0~b15 = Y2 coordinate (tile y)

regDC: stbb_s_w
    b0~b15 = Source image width

regDE: stbb_s_h
    b0~b15 = Source image height

regE0: pri_[gb|ar]_st
    b0~b31 = Color
    For RGB:
      b0~b7 = Blue
      b8~b15 = Green
      b16~b23 = Red
      b24~b31 = Alpha
    For YUV:
      b0~b7 = Y
      b8~b15 = U?
      b16~b23 = V?
      b24~b31 = Alpha

regE4: pri_r_dx[0|1]
    b0~b19 = Red gradient delta X
      [ val = (Rend - Rbegin) * 0x1000 / width ]

regE8: pri_r_dy[0|1]
    b0~b19 = Red gradient delta Y
      [ val = (Rend - Rbegin) * 0x1000 / height ]

regEC: pri_g_dx[0|1]
    b0~b19 = Green gradient delta X
      [ val = (Gend - Gbegin) * 0x1000 / width ]

regF0: pri_g_dy[0|1]
    b0~b19 = Green gradient delta Y
      [ val = (Gend - Gbegin) * 0x1000 / height ]
    
regF4: pri_b_dx[0|1]
    b0~b19 = Blue gradient delta X
      [ val = (Bend - Bbegin) * 0x1000 / width ]

regF8: pri_b_dy[0|1]
    b0~b19 = Blue gradient delta Y
      [ val = (Bend - Bbegin) * 0x1000 / height ]

regFC: pri_a_dx0
    b0~b15 = Alpha gradient delta X
      [ val = (Aend - Abegin) * 0x800 / width ]

regFE: pri_a_dy0
    b0~b15 = Alpha gradient delta Y
      [ val = (Aend - Abegin) * 0x800 / height ]
```

----

- Seems to be at 0x1f281200 on i2m
- i2m version seems to be the same or similar to the mst786 one.

| offset | name                  | 15         | 14         | 13           | 12           | 11  | 10  | 9         | 8         | 7     | 6       | 5     | 4     | 3     | 2            | 1     | 0        | notes                          |
|--------|-----------------------|------------|------------|--------------|--------------|-----|-----|-----------|-----------|-------|---------|-------|-------|-------|--------------|-------|----------|--------------------------------|
| 0x0    |                       |            | ?          |              |              |     | ?   |           |           |       |         |       |       |       | alpha blend? |       | enable   |                                |
| 0x4    |                       | ?          | ?          |              |              |     |     |           |           |       |         |       |       |       |              | ?     | ?        |                                |
| 0xc    |                       |            |            |              |              |     |     |           |           |       |         |       |       | ?     | ?            |       | ?        |                                |
| 0x10   | vcmd queue status?    |            |            |              |              |     |     |           |           |       |         |       |       |       |              |       |          |                                |
| 0x14   |                       |            |            |              |              |     |     |           |           | ?     |         | ?     | ?     |       | ?            | ?     |          |                                |
| 0x1c   | cmd queue status?     | ?          | ?          | ?            | ?            | ?   |     |           |           | ?     | ?       | ?     | ?     | ?     |              |       | GE busy? |                                |
| 0x40   | rop2                  |            |            |              |              |     |     |           |           |       |         |       |       |       |              |       |          |                                |
| 0x4c   |                       | ?          | ?          | ?            | ?            | ?   | ?   | ?         | ?         | ?     | ?       | ?     | ?     | ?     | ?            | ?     | ?        |                                |
| 0x50   | src colour key?       |            |            |              |              |     |     |           |           |       |         |       |       |       |              |       |          |                                |
| 0x54   | src colour key?       |            |            |              |              |     |     |           |           |       |         |       |       |       |              |       |          |                                |
| 0x58   | src colour key?       |            |            |              |              |     |     |           |           |       |         |       |       |       |              |       |          |                                |
| 0x5c   | src colour key?       |            |            |              |              |     |     |           |           |       |         |       |       |       |              |       |          |                                |
| 0x60   | dst colour key?       |            |            |              |              |     |     |           |           |       |         |       |       |       |              |       |          |                                |
| 0x64   | dst colour key?       |            |            |              |              |     |     |           |           |       |         |       |       |       |              |       |          |                                |
| 0x68   | dst colour key?       |            |            |              |              |     |     |           |           |       |         |       |       |       |              |       |          |                                |
| 0x6c   | dst colour key?       |            |            |              |              |     |     |           |           |       |         |       |       |       |              |       |          |                                |
| 0x78   | irq                   | raw status | raw status | final status | final status | clr | clr | force irq | force irq | mask  | mask    |       |       |       |              |       |          |                                |
| 0x7c   | src/dst yuv format    |            |            |              |              |     |     |           |           |       |         |       |       |       |              |       |          |                                |
| 0x80   | srcl                  |            |            |              |              |     |     |           |           |       |         |       |       |       |              |       |          |                                |
| 0x84   | srch                  |            |            |              |              |     |     |           |           |       |         |       |       |       |              |       |          |                                |
| 0x90   | ?                     |            |            |              |              |     |     |           |           |       |         |       |       |       |              |       |          | written when waiting for a tag |
| 0x94   | ?                     |            |            |              |              |     |     |           |           |       |         |       |       |       |              |       |          | written when waiting for a tag |
| 0x98   | dstl                  |            |            |              |              |     |     |           |           |       |         |       |       |       |              |       |          |                                |
| 0x9c   | dsth                  |            |            |              |              |     |     |           |           |       |         |       |       |       |              |       |          |                                |
| 0xb4   | p256                  | g          | g          | g            | g            | g   | g   | g         | g         | b     | b       | b     | b     | b     | b            | b     | b        |                                |
| 0xb8   | p256                  | a          | a          | a            | a            | a   | a   | a         | a         | r     | r       | r     | r     | r     | r            | r     | r        |                                |
| 0xbc   | p256                  |            |            |              |              |     |     |           | rw        | index | index   | index | index | index | index        | index | index    |                                |
| 0xc0   | src pitch             |            |            |              |              |     |     |           |           |       |         |       |       |       |              |       |          |                                |
| 0xc4   | tag l                 |            |            |              |              |     |     |           |           |       |         |       |       |       |              |       |          |                                |
| 0xc8   | tag h                 |            |            |              |              |     |     |           |           |       |         |       |       |       |              |       |          |                                |
| 0xcc   | dst pitch             |            |            |              |              |     |     |           |           |       |         |       |       |       |              |       |          |                                |
| 0xd0   | color format          |            |            |              | dst          | dst | dst | dst       | dst       |       |         |       |       | src   | src          | src   | src      |                                |
| 0xd4   | intensity?            |            |            |              |              |     |     |           |           |       |         |       |       |       |              |       |          |                                |
| 0xd8   | intensity?            |            |            |              |              |     |     |           |           |       |         |       |       |       |              |       |          |                                |
| 0x154  | clip left             |            |            |              |              | x   | x   | x         | x         | x     | x       | x     | x     | x     | x            | x     | x        |                                |
| 0x158  | clip right            |            |            |              |              | x   | x   | x         | x         | x     | x       | x     | x     | x     | x            | x     | x        |                                |
| 0x15c  | clip top              |            |            |              |              | x   | x   | x         | x         | x     | x       | x     | x     | x     | x            | x     | x        |                                |
| 0x160  | clip bottom           |            |            |              |              |     |     |           |           |       |         |       |       |       |              |       |          |                                |
| 0x164  |                       |            |            |              |              |     |     |           |           |       |         |       |       |       |              | rot   | rot      | GE_SetRotate                   |
| 0x180  | cmd                   |            |            |              |              |     |     |           |           |       | bit blt |       |       |       |              |       |          |                                |
| 0x188  | line ctrl?            |            |            |              |              |     |     |           |           |       |         |       |       |       |              |       |          |                                |
| 0x198  | italic?               |            |            |              |              |     |     |           |           |       |         |       |       |       |              |       |          |                                |
| 0x19c  | italic?               |            |            |              |              |     |     |           |           |       |         |       |       |       |              |       |          |                                |
| 0x1a0  | x0                    |            |            |              |              |     |     |           |           |       |         |       |       |       |              |       |          |                                |
| 0x1a4  | y0                    |            |            |              |              |     |     |           |           |       |         |       |       |       |              |       |          |                                |
| 0x1a8  | x1                    |            |            |              |              |     |     |           |           |       |         |       |       |       |              |       |          |                                |
| 0x1ac  | y1                    |            |            |              |              |     |     |           |           |       |         |       |       |       |              |       |          |                                |
| 0x1b0  | x2                    |            |            |              |              |     |     |           |           |       |         |       |       |       |              |       |          |                                |
| 0x1b4  | y2                    |            |            |              |              |     |     |           |           |       |         |       |       |       |              |       |          |                                |
| 0x1b8  | bit blt source width  |            |            |              |              | x   | x   | x         | x         | x     | x       | x     | x     | x     | x            | x     | x        |                                |
| 0x1bc  | bit blt source height |            |            |              |              | x   | x   | x         | x         | x     | x       | x     | x     | x     | x            | x     | x        |                                |
| 0x1c0  | start colour?         | g          | g          | g            | g            | g   | g   | g         | g         | b     | b       | b     | b     | b     | b            | b     | b        |                                |
| 0x1c4  | start colour?         | a          | a          | a            | a            | a   | a   | a         | a         | r     | r       | r     | r     | r     | r            | r     | r        |                                |
| 0x1c8  | delta r?              |            |            |              |              |     |     |           |           |       |         |       |       |       |              |       |          |                                |
| 0x1cc  | delta r?              |            |            |              |              |     |     |           |           |       |         |       |       |       |              |       |          |                                |
| 0x1d8  | delta g?              |            |            |              |              |     |     |           |           |       |         |       |       |       |              |       |          |                                |
| 0x1dc  | delta g?              |            |            |              |              |     |     |           |           |       |         |       |       |       |              |       |          |                                |
| 0x1e8  | delta b?              |            |            |              |              |     |     |           |           |       |         |       |       |       |              |       |          |                                |
| 0x1ec  | delta b?              |            |            |              |              |     |     |           |           |       |         |       |       |       |              |       |          |                                |
| 0x1f8  | delta a?              |            |            |              |              |     |     |           |           |       |         |       |       |       |              |       |          |                                |
