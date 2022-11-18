# HDMI TX

# Kronus variant

HDMI TX variant in [Kronus](../kronus/index.md) family (e.g. **MSD7816**)

## Registers

- 0x1f226000 [0x113000] -- Bank 0 (main)
- 0x1f226200 [0x113100] -- Bank 1 (infoframes)
- 0x1f226400 [0x113200] -- Bank 2 (video)
- 0x1f226600 [0x113300] -- Bank 3 (audio)

### Bank 0

```
reg00:
    b7 = synth soft reset

reg02:
    b0 = HDMI_SCL pin
    b4 = HDMI_SDA pin
    b15 = Connects the HDMI_[SDA/SCL] to I2CM_[SDA/SCL] (overrides the pinmux!)

reg0A:
    b0~b2 = TXPLL out second divider:
      0 => 1/1
      1 => 3/4
      2 => 4/5
      3 => 1/2
      4 => 5/6
      5 => 1/4

    b4~b6 = 
      0 => 
      1 => 
      2 => 
      3 => 
      4 => 
      5 => 
      6 => 
      7 => 

    b8~b11 = 
      0 => 
      1 => 
      2 => 
      3 => 
      4 => 
      5 => 
      6 => 
      7 => 

reg14:
    b5 = Hotplug status [0: plugged, 1: unplugged]

reg18:
    b0~b15 = Interrupt mask

reg1A:
    b0~b15 = Interrupt mask
    b0 = Hotplug

reg1C:
    b0~b15 = Interrupt pending, set to clear

reg1E:
    b0~b15 = Interrupt pending, set to clear

reg20:
    b0~b31 = TXPLL out divider (bias 0x10000000)

reg3C:
    b0~b15 = clkgen

reg54:
    b0~b3 = TMDS atop power down <0x0 on power on, 0xf on power down>
    set to 000f on init

reg56:
    b0 = ?? set to 1 on init
    b1 = ?? set to 1 on init, changed in video mode setting

reg58:
    set to 0000 on init

reg5A:
    b5 = Pre-emphasis mode

reg5C:
    b0~b3 = TMDS atop enable <0xf on power on, 0x0 on power down>
    b4~b7 = TM Precon
    b8~b11 = Pre-emphasis enable
    set to 0000 on video init

reg5E:
    b0~b3 = Double termination pre-emphasis enable
    b4~b7 = Double termination enable

reg66:
    b4~b6 = ?
      2 => ?? set for modes with pclk=148.5 MHz
      5 => ?? set for modes with pclk=74.25 MHz
      7 => ?? set for modes with pclk=27 MHz

    set to 0000 on video init

reg68:
    set to 1010 on init

reg70:
    b2~b3 = ?
      1 => ?? set for modes with pclk=27 MHz
      2 => ?? set for modes with pclk=74.25 MHz
      3 => ?? set for modes with pclk=148.5 MHz

reg82:
    set to 1010 on init

reg8A:
    set to 0000 on init

regB0:
    set to 0003 on init
```

### Bank 1

```
reg00:
    b0~b7 = color depth hint?:
      01 => 8 bits (24 bpp)
      44 => 10 bits (30 bpp)
      84 => 12 bits (36 bpp)

reg12-1F:
    AVI InfoFrame [0x82-0x02] data bytes (14 bytes)

reg20:
    b0~b4 = 
    b5~b7 = 
    b8~b15 =

reg22-27:
    Audio InfoFrame [0x84-0x01] data bytes (6 bytes)

reg28:
    b0~b4 = 
    b5~b7 = 
    b8~b15 =

reg2A-43:
    Some infoframe [0x83] data bytes (26 bytes)

reg44:
    b0~b4 = 
    b5~b7 = 
    b8~b15 =

reg4E-69:
    HDMI Vendor Specific InfoFrame [0x81-0x01] data bytes (28 bytes)

reg6A:
    b0~b4 = 
    b5~b7 = 
    b8~b15 = 

regA6:
    set to 0300 on init

```

### Bank 2

```
reg00:
    b0 = ? set on interlaced modes
    b1~b3 = ?
    b6 = ? 
    b10 = swap R/B channels

    * for everything progressive,             it's set to 0x004E |1.00.111.0|
    * for everything interlaced upto 1080i60, it's set to 0x000D |0.00.110.1|
    *                           for everything else, it's 0x004F |1.00.111.1|

reg02:
    b0 = enable sync polarity control (when disabled, syncs are positive)
    b1 = hsync polarity [0: negative, 1: positive]
    b2 = vsync polarity [0: negative, 1: positive]
    b4~b5 = ?? set to 3 on video init
    b8 = Convert YUV to RGB
    b9 = ?

reg04: vs_width
    b0~b7 = VSync width

reg06: vs_bporch
    b0~b8 = Vertical back porch

reg08: vde_width
    b0~b11 = Active area height

reg0A: vs_delayline
    b0~b7 = VSync delay (line)

reg0C: vs_delaypixel
    b0~b9 = VSync delay (pixel)

reg0E: hs_width
    b0~b9 = HSync width

reg10: hs_bporch
    b0~b9 = Horizontal back porch

reg12: hde_width
    b0~b11 = Active area width

reg14: hs_delay
    b0~b9 = HSync delay

reg16:
    b6 = Disable video output

reg22:
    b0~b5 = ?? set to 3 when disabling video output, not changed when enabling

reg24:
    b0~b3 = ?? set to 8 on video init

reg26:
    b0~b11 = vtotal

reg28:
    b0~b11 = htotal

reg2E:
    b0~b2 = color channel depth:
      0 => 8 bits (24 bpp)
      1 => 10 bits (30 bpp)
      2 => 12 bits (36 bpp)

reg30:
    b0 = Output chroma subsampling [0: 444, 1: 422]

```

### Bank 3

```
reg00:
    b0~b2 = ?? set to 3 on audio init
    b7 = ?? set to 0 on audio init
    b12 = ?? set to 1 on audio init
```

## Random stuff

### TXPLL

The DAC_CLK_OUT is apparently the only high-frequency pixel clock in Kronus (maybe i could get LPLL "VEPLL" working, but not now).
This clock comes from the HDMITX's TXPLL.

#### TXPLL's clock frequency

The TXPLL runs at frequency of 576 MHz (1.33333333 times faster compared to 432 MHz MPLL and 48 times compared to 12 MHz XTAL,
but changing the MPLL frequency seems to make it change too so this is relative to the MPLL)

The 1.3333333 factor is exactly 1.5555555 in HEX, which miltiplied by 0x10000000 gives 0x15555555 -- the Bank0.reg20 reset value,
but this is not the case because if we write a bigger value there then the frequency should go higher rather than lower.

This is also exactly 4/3 factor for divison and 3/4 factor for multiplication.
Maybe this factor is hardwired, but OK, this is not really a problem,
since at least now it could be _derived_ (i.e. Ftxpll = Fmpll * 4 / 3) rather than _assumed_ (i.e. Ftxpll = 576 MHz).

### Video modes

Goes from the stock vendor U-Boot for MSD7816... Just for me to have a quick reference.

#### Panel type table

Panel type table and the corresponding eTiming value for HDMTIX and DAC:

| #  | name                | hdmitx | dac |
|----|---------------------|--------|-----|
| 0  | SEC LE32            | 13     | 9   |
| 1  | SXGA AU17 EN05      | 13     | 9   |
| 2  | WXGA AU20 T200XW02  | 13     | 9   |
| 3  | WXGAP CMO M190A1    | 13     | 9   |
| 4  | WSXGA AU22 M201EW01 | 13     | 9   |
| 5  | FullHD CMO216 H1L01 | 13     | 9   |
| 6  | DACOUT 480i60       | 1      | 0   |
| 7  | DACOUT 480p60       | 3      | 1   |
| 8  | DACOUT 576i50       | 2      | 2   |
| 9  | DACOUT 576p50       | 4      | 3   |
| 10 | DACOUT 720p50       | 5      | 4   |
| 11 | DACOUT 720p60       | 6      | 5   |
| 12 | DACOUT 1080i50      | 7      | 6   |
| 13 | DACOUT 1080i60      | 8      | 7   |
| 14 | DACOUT 1080p24      | 9      | 12  |
| 15 | DACOUT 1080p25      | 10     | 11  |
| 16 | DACOUT 1080p30      | 11     | 10  |
| 17 | DACOUT 1080p50      | 12     | 8   |
| 18 | DACOUT 1080p60      | 13     | 9   |
| 19 | DACOUT 640x480 60Hz | 13     | 9   |
| 20 | CMO260J2 UXGA       | 13     | 9   |

The panel type is passed to the `set_paneltype` command, which is put into the `panel_cmd` envvar
so that the `boot_logo` command can call it (the `osd_create` command seem to always use 1080i60)

#### HDMITX mode table

Table from which the HDMITX parameters are set from:

| #  | Mode    | interlaced | hsync | vsync | vs_width | vs_bporch | vde_width | vs_delayline | vs_delaypixel | hs_width | hs_bporch | hde_width | hs_delay | vtotal | htotal |
|----|---------|------------|-------|-------|----------|-----------|-----------|--------------|---------------|----------|-----------|-----------|----------|--------|--------|
| 0  | VGA     | no         | neg   | neg   | 2        | 33        | 480       | 1            | 0             | 96       | 48        | 640       | 0        | 800    | 525    |
| 1  | 480i    | yes        | neg   | neg   | 3        | 15        | 240       | 1            | 0             | 124      | 57        | 720       | 0        | 262    | 858    |
| 2  | 576i    | yes        | neg   | neg   | 3        | 19        | 288       | 1            | 0             | 126      | 69        | 720       | 0        | 312    | 864    |
| 3  | 480p    | no         | neg   | neg   | 6        | 30        | 240       | 1            | 0             | 62       | 60        | 720       | 0        | 525    | 858    |
| 4  | 576p    | no         | neg   | neg   | 5        | 39        | 576       | 1            | 0             | 64       | 68        | 720       | 0        | 625    | 864    |
| 5  | 720p50  | no         | pos   | pos   | 5        | 20        | 720       | 1            | 0             | 40       | 220       | 1280      | 0        | 750    | 1980   |
| 6  | 720p60  | no         | pos   | pos   | 5        | 20        | 720       | 1            | 0             | 40       | 220       | 1280      | 0        | 750    | 1650   |
| 7  | 1080i50 | yes        | pos   | pos   | 5        | 16        | 540       | 1            | 0             | 44       | 149       | 1920      | 0        | 562    | 2640   |
| 8  | 1080i60 | yes        | pos   | pos   | 5        | 16        | 540       | 1            | 0             | 44       | 149       | 1920      | 0        | 562    | 2200   |
| 9  | 1080p24 | no         | pos   | pos   | 5        | 36        | 1080      | 1            | 0             | 44       | 148       | 1920      | 0        | 1125   | 2750   |
| 10 | 1080p25 | no         | pos   | pos   | 5        | 36        | 1080      | 1            | 0             | 44       | 148       | 1920      | 0        | 1125   | 2640   |
| 11 | 1080p30 | no         | pos   | pos   | 5        | 36        | 1080      | 1            | 0             | 44       | 148       | 1920      | 0        | 1125   | 2200   |
| 12 | 1080p50 | no         | pos   | pos   | 5        | 36        | 1080      | 1            | 0             | 44       | 148       | 1920      | 0        | 1125   | 2640   |
| 13 | 1080p60 | no         | pos   | pos   | 5        | 36        | 1080      | 1            | 0             | 44       | 148       | 1920      | 0        | 1125   | 2200   |

#### DAC mode table

The pclk that's setup by the DAC driver:

| #  | Mode    | HDMITX.20  | HDMITX.0A | TXPLL     | CLKGEN0.A6 | pclk       |
|----|---------|------------|-----------|-----------|------------|------------|
| 0  | 480i    | 0x15555555 | 0x0863    | 216 MHz   | 0x0C       | 27 MHz     |
| 1  | 480p    | 0x15555555 | 0x0863    | 216 MHz   | 0x0C       | 27 MHz     |
| 2  | 576i    | 0x15555555 | 0x0863    | 216 MHz   | 0x0C       | 27 MHz     |
| 3  | 576p    | 0x15555555 | 0x0863    | 216 MHz   | 0x0C       | 27 MHz     |
| 4  | 720p50  | 0x1745D174 | 0x0431    | 297 MHz   | 0x08       | 74.25 MHz  |
| 5  | 720p60  | 0x174BC6A7 | 0x0431    | 296.7 MHz | 0x08       | 74.175 MHz |
| 6  | 1080i50 | 0x1745D174 | 0x0431    | 297 MHz   | 0x04       | 148.5 MHz  |
| 7  | 1080i60 | 0x174BC6A7 | 0x0431    | 296.7 MHz | 0x04       | 148.35 MHz |
| 8  | 1080p50 | 0x1745D174 | 0x0111    | 297 MHz   | 0x04       | 148.5 MHz  |
| 9  | 1080p60 | 0x174BC6A7 | 0x0111    | 296.7 MHz | 0x04       | 148.35 MHz |
| 10 | 1080p30 | 0x1745D174 | 0x0431    | 297 MHz   | 0x08       | 74.25 MHz  |
| 11 | 1080p25 | 0x1745D174 | 0x0431    | 297 MHz   | 0x08       | 74.25 MHz  |
| 12 | 1080p24 | 0x1745D174 | 0x0431    | 297 MHz   | 0x08       | 74.25 MHz  |

### Init code

This code inits the HDMITX and the display subsystem at 1280x720@60Hz mode, the HDMI outputs video in YUV444 format.

```py
vm_hactive = 1280
vm_hbporch = 1650-1280-40-220
vm_hsync   = 40
vm_hfporch = 220
vm_vactive = 720
vm_vbporch = 750-720-5-20
vm_vsync   = 5
vm_vfporch = 20
vm_pclk    = 74.25
vm_hspos   = True
vm_vspos   = True

vm_hsend  = vm_hsync-1
vm_vsst   = vm_vactive+vm_vbporch
vm_vsend  = vm_vactive+vm_vbporch+vm_vsync-1
vm_hstart = vm_hsync+vm_hfporch
vm_hend   = vm_hsync+vm_hfporch+vm_hactive-1
vm_vstart = 0
vm_vend   = vm_vactive-1
vm_htotal = vm_hactive+vm_hbporch+vm_hsync+vm_hfporch
vm_vtotal = vm_vactive+vm_vbporch+vm_vsync+vm_vfporch

print('hsync:    0-%d' % (vm_hsend))
print('vsync: %4d-%4d' % (vm_vsst, vm_vsend))
print('hact:  %4d-%4d' % (vm_hstart, vm_hend))
print('vact:  %4d-%4d' % (vm_vstart, vm_vend))
print('total: %4d, %4d' % (vm_htotal, vm_vtotal))
print('hfreq: %.3f kHz' % (vm_pclk * 1000 / vm_htotal))
print('vfreq: %.3f Hz' % (vm_pclk * 1000000 / vm_htotal / vm_vtotal))

dispw = vm_hactive
disph = vm_vactive
dispaddr = 0x3800000

#==================================================#

CLKGEN0   = 0x100B00
GOP       = 0x101F00
GE0       = 0x102800
SC1_XC    = 0x102F00
SC2_HDGEN = 0x103000
CLKGEN1   = 0x103300
HDMITX0   = 0x113000
HDMITX1   = 0x113100
HDMITX2   = 0x113200
HDMITX3   = 0x113300

#--- disable all ints
riu.write16(HDMITX0+0x18, 0xffff)
riu.write16(HDMITX0+0x1a, 0xffff)
#--- clear all ints
riu.write16(HDMITX0+0x1c, 0xffff)
riu.write16(HDMITX0+0x1e, 0xffff)

riu.write16(HDMITX0+0x54, 0x000f)

riu.write16(CLKGEN1+0x50, 0x0000) # clkgen2

riu.write16(HDMITX0+0x3c, 0xffff) # hdmi clkgen
riu.write16(HDMITX0+0x8a, 0x0000)
riu.write16(HDMITX0+0x66, 0x0000)
riu.write16(HDMITX0+0x56, 0x0003)
riu.write16(HDMITX0+0x58, 0x0000)

#--- synth soft reset
riu.wmask16(HDMITX0+0x00, 1<<7, 1<<7)
riu.wmask16(HDMITX0+0x00, 1<<7, 0<<7)

riu.write16(HDMITX1+0xa6, 0x0300)
riu.write16(HDMITX0+0xb0, 0x0003)
riu.write16(HDMITX0+0x82, 0x1010)
riu.write16(HDMITX0+0x68, 0x1010)

#--- video init
riu.write16(HDMITX0+0x5c, 0x0000)
riu.wmask16(HDMITX2+0x02, 0x30, 0x30)
riu.wmask16(HDMITX2+0x24, 0xf, 0x8)

#--- audio init
riu.wmask16(HDMITX3+0x00, 0x1087, 0x1003)

#---------- Video On/OFF
riu.wmask16(HDMITX2+0x16, 1<<6, 0<<6)

#-------- set hdmitx mode

#--- color depth
riu.wmask16(HDMITX2+0x2E, 7<<0, 0<<0)
riu.wmask16(HDMITX1+0x00, 0xff, 0x04)

#--- packet 5
#riu.read16(HDMITX1+0x06) #=> 0x0021
riu.write16(HDMITX1+0x06, 0x0020)

#--- packet 0
#riu.read16(HDMITX1+0x04) #=> 0x000d
riu.write16(HDMITX1+0x04, 0x0005)

# ======= 0x81 Infoframe ======= #
riu.write16(HDMITX1+0x4e, 0x0c03)
riu.write16(HDMITX1+0x6a, 0x547d) #<- checksum, etc

# ======= 0x83 Infoframe ======= #
riu.write16(HDMITX1+0x2a, 0x534d) # 'MS'
riu.write16(HDMITX1+0x2c, 0x6174) # 'ta'
riu.write16(HDMITX1+0x2e, 0x2072) # 'r '
riu.write16(HDMITX1+0x30, 0x2020) # '  '
riu.write16(HDMITX1+0x32, 0x4448) # 'HD'
riu.write16(HDMITX1+0x34, 0x494d) # 'MI'
riu.write16(HDMITX1+0x36, 0x5420) # ' T'
riu.write16(HDMITX1+0x38, 0x2078) # 'X '
riu.write16(HDMITX1+0x3a, 0x6544) # 'De'
riu.write16(HDMITX1+0x3c, 0x6f6d) # 'mo'
riu.write16(HDMITX1+0x3e, 0x0000)
riu.write16(HDMITX1+0x40, 0x0000)
riu.write16(HDMITX1+0x42, 0x0001)
riu.write16(HDMITX1+0x44, 0x687d) #<- checksum, etc

#-------- set color format (YUV -> YUV444)
riu.wmask16(HDMITX2+0x02, 1<<8, 0<<8) # convert yuv to rgb
riu.wmask16(HDMITX2+0x30, 1<<0, 0<<0) # out chroma subsampling

# ======= AVI InfoFrame ======= #
riu.write16(HDMITX1+0x12, 0x58d0) # b5~b6 => color format: 10 = YUV444, 00 = RGB
riu.write16(HDMITX1+0x14, 0x0200)
riu.write16(HDMITX1+0x16, 0x0000)
riu.write16(HDMITX1+0x20, 0xc505) #<- checksum, etc

#-------- pixel clock

#b2~b4:
#  1 => clk_out_dac/2
#  2 => clk_out_dac/4
#  3 => clk_out_dac/8
#  4 => clk_out_dac
#  6 => 27MHz
#  7 => XTAL [LPLL?]
#b5~b6:
#  0 => 1/1
#  1 => 1/2
#  2 => 1/3
riu.write16(CLKGEN0+0xa6, (0<<5)|(2<<2)|0)

#
# 576 MHz * 3/4 / 4 => 108 MHz / <div>
# >>> No jitter
#
# 576 MHz * 1/2 / 2 => 144 MHz / <div>
# >>> Jitter
#

riu.write16(HDMITX0+0x0a, 0x0430 | (1<<0))
riu.write32(HDMITX0+0x20, int((576 * 3/4 / 4 / vm_pclk) * 0x10000000))

#------- HDMI video mode & syncs -------

riu.wmask16(HDMITX2+0x00, 0x4f, 0x4e)

riu.wmask16(HDMITX2+0x02, 1<<2, vm_vspos<<2) # vsync polarity
riu.wmask16(HDMITX2+0x02, 1<<1, vm_hspos<<1) # hsync polarity
riu.wmask16(HDMITX2+0x02, 1<<0, 1<<0) # enable sync polarity control

riu.wmask16(HDMITX0+0x70, 3<<6, 1<<6)
riu.wmask16(HDMITX0+0x66, 7<<4, 5<<4)
riu.wmask16(HDMITX0+0x5A, 1<<5, 0<<5) # pre-emphasis mode
riu.wmask16(HDMITX0+0x56, 1<<1, 1<<1) # ... double termination == 0
riu.wmask16(HDMITX0+0x5C, 0xf<<4, 0x0<<4) # tm precon 
riu.wmask16(HDMITX0+0x5C, 0xf<<8, 0x0<<8) # pre-emphasis
riu.wmask16(HDMITX0+0x5E, 0xf<<0, 0x0<<0) # double termination pre-emphasis
riu.wmask16(HDMITX0+0x5E, 0xf<<4, 0x0<<4) # double termination

riu.write16(HDMITX2+0x04, vm_vsync)   # vs_width
riu.write16(HDMITX2+0x06, vm_vfporch) # vs_bporch
riu.write16(HDMITX2+0x08, vm_vactive) # vde_width
riu.write16(HDMITX2+0x0a, 1)          # vs_delayline
riu.write16(HDMITX2+0x0c, 0)          # vs_delaypixel
riu.write16(HDMITX2+0x0e, vm_hsync)   # hs_width
riu.write16(HDMITX2+0x10, vm_hfporch) # hs_bporch
riu.write16(HDMITX2+0x12, vm_hactive) # hde_width
riu.write16(HDMITX2+0x14, 0)          # hs_delay
riu.write16(HDMITX2+0x26, vm_vtotal)  # vtotal
riu.write16(HDMITX2+0x28, vm_htotal)  # htotal

#-------- set overscan afd

# ======= AVI InfoFrame ======= #
riu.write16(HDMITX1+0x12, 0xaad0)
riu.write16(HDMITX1+0x14, 0x0400)
riu.write16(HDMITX1+0x16, 0x0000)
riu.write16(HDMITX1+0x20, 0x7105) #<- checksum, etc

#----- Turn on TMDS -----
riu.wmask16(HDMITX2+0x00, 1<<10, 0<<10) # no swap
riu.wmask16(HDMITX0+0x54, 0xf, 0x0) # power up
riu.wmask16(HDMITX0+0x5c, 0xf, 0xf) # enable

#----------------------------------------------------

riu.write16(SC2_HDGEN+0x00, 0x0001) # HDGEN bank 0x1
riu.write16(SC2_HDGEN+0x02, 0x000f) # ...fix hdmi... b1 matters

#============================================================================#

riu.write8(SC1_XC+0x00, 0x0F) # xc bank 0x0F
riu.wmask16(SC1_XC+0xAE, 1<<11, 1<<11) # ---> ve is receiving image!! MST786:"capture image to ip enable"

riu.write8(SC1_XC+0x00, 0x10) # xc bank 0x10
riu.wmask16(SC1_XC+0x46, 1<<5, 1<<5) # sets b5?

riu.write8(SC1_XC+0x00, 0x2F) # xc bank 0x2F
riu.wmask16(SC1_XC+0x4E, 1<<0, 1<<0) # ---> gop is displayed!!

##########################
# EASY PART              #
#========================#===================================================#
# I KNOW THIS WORKS WELL #
##########################

riu.write8(SC1_XC+0x00, 0x10) # xc bank 0x10
riu.write16(SC1_XC+0x02, vm_hsend)    # vop_hsend_width
riu.write16(SC1_XC+0x04, vm_vsst)     # vop_vsst
riu.write16(SC1_XC+0x06, vm_vsend)    # vop_vsend
riu.write16(SC1_XC+0x08, vm_hstart)   # vop_de_hstart
riu.write16(SC1_XC+0x0A, vm_hend)     # vop_de_hend
riu.write16(SC1_XC+0x0C, vm_vstart)   # vop_de_vstart
riu.write16(SC1_XC+0x0E, vm_vend)     # vop_de_vend
riu.write16(SC1_XC+0x18, vm_htotal-1) # vop_hdtot
riu.write16(SC1_XC+0x1A, vm_vtotal-1) # vop_vdtot

riu.write8(SC1_XC+0x00, 0x00) # xc bank 0x00
riu.write16(SC1_XC+0x0C, 0x8000) # enable GOP MUX0

riu.write16(GOP+0xFC, (0<<0)|(1<<3)|(2<<6)|(3<<9))

riu.write8(GOP+0xFE, 0x0) # gop bank 0x0
riu.write16(GOP+0x00, 0x440C)       # ctrl0
riu.write16(GOP+0x02, 0x4102)       # ctrl1
riu.write16(GOP+0x1C, (dispw + 3) // 2)   # rdma_ht
riu.write16(GOP+0x1E, vm_hstart-13) # hs_pipe
riu.write16(GOP+0x32, 0x4760)       # bw
riu.write16(GOP+0x60, dispw // 2)   # strch_hsz
riu.write16(GOP+0x62, disph)        # strch_vsz
riu.write16(GOP+0x64, 0)            # strch_hstr
riu.write16(GOP+0x68, 0)            # strch_vstr
riu.write16(GOP+0x6A, int(dispw * 0x1000 / vm_hactive) & 0x1fff) # strch_hstrch
riu.write16(GOP+0x6C, int(disph * 0x1000 / vm_vactive) & 0x1fff) # strch_vstrch
riu.write16(GOP+0x70, 0)            # strch_hstrch_ini
riu.write16(GOP+0x72, 0)            # strch_vstrch_ini
riu.write8(GOP+0xFF, 1) # write_force
riu.write8(GOP+0xFF, 0)

riu.write8(GOP+0xFE, 0x1) # gop bank 0x1
riu.write16(GOP+0x00, 0x3F11)           # gwin_ctrl
riu.write32(GOP+0x02, dispaddr >> 3)    # dram_rblk_[l|h]
riu.write16(GOP+0x08, 0)                # hstr
riu.write16(GOP+0x0A, (dispw * 2) >> 3) # hend
riu.write16(GOP+0x0C, 0)                # vstr
riu.write16(GOP+0x10, disph)            # vend
riu.write16(GOP+0x12, (dispw * 2) >> 3) # dram_rblk_hsize
riu.write16(GOP+0x14, 0x3)              # gwin_alpha_01
riu.write32(GOP+0x18, 0)                # dram_vstr
riu.write16(GOP+0x1C, 0)                # dram_hstr
riu.write8(GOP+0xFF, 1) # write_force
riu.write8(GOP+0xFF, 0)

#================================================#
# second part, just to show something "sensible" #
#================================================#

riu.wmask16(GE0+0x00, 1, 0) # disable GE
riu.write16(GE0+0x00, 0x0007) # abl, dither, ge
riu.write16(GE0+0x02, 0x0011) # stbb, cmq

riu.write16(GE0+0x22, 0x2) # asrc

riu.write16(GE0+0x24, 0x0<<8)
riu.write16(GE0+0x26, 0xff00) # aconst

riu.write32(GE0+0x4C, dispaddr)
riu.write16(GE0+0x66, dispw * 4)
riu.wmask16(GE0+0x68, 0xf<<8, 0xf<<8)

riu.write16(GE0+0xAA, 0)
riu.write16(GE0+0xAC, dispw - 1)
riu.write16(GE0+0xAE, 0)
riu.write16(GE0+0xB0, disph - 1)

# base color
riu.write32(GE0+0xE0, 0xff008000)
# horizontal gradient
riu.write32(GE0+0xE4, int((0x00 - 0x00) * 0x1000 / dispw) & 0xfffff)
riu.write32(GE0+0xEC, int((0x00 - 0x00) * 0x1000 / dispw) & 0xfffff)
riu.write32(GE0+0xF4, int((0xff - 0x00) * 0x1000 / dispw) & 0xfffff)
riu.write16(GE0+0xFC, 0)
# vertical gradient
riu.write32(GE0+0xE8, int((0xff - 0x00) * 0x1000 / disph) & 0xfffff)
riu.write32(GE0+0xF0, int((0x00 - 0x00) * 0x1000 / disph) & 0xfffff)
riu.write32(GE0+0xF8, int((0x00 - 0x00) * 0x1000 / disph) & 0xfffff)
riu.write16(GE0+0xFE, 0)
# draw
riu.write16(GE0+0xD0, 0)
riu.write16(GE0+0xD2, 0)
riu.write16(GE0+0xD4, dispw-1)
riu.write16(GE0+0xD6, disph-1)
riu.write16(GE0+0xC0, 0x3030)
while riu.read16(GE0+0x0E) & 1: pass

def xrect(x, y, w, h, char):
    if char == ' ': return

    color = 0x0000aa
    if   char == '#': color = 0x555555
    elif char == '@': color = 0xff5555
    elif char == '.': color = 0xffffff

    riu.write32(GE0+0xE0, 0xff000000)
    riu.write16(GE0+0xD0, 5+x)
    riu.write16(GE0+0xD2, 5+y)
    riu.write16(GE0+0xD4, 5+x+w-1)
    riu.write16(GE0+0xD6, 5+y+h-1)
    riu.write16(GE0+0xC0, 0x0030)
    while riu.read16(GE0+0x0E) & 1: pass

    riu.write32(GE0+0xE0, 0xff000000 | color)
    riu.write16(GE0+0xD0, x)
    riu.write16(GE0+0xD2, y)
    riu.write16(GE0+0xD4, x+w-1)
    riu.write16(GE0+0xD6, y+h-1)
    riu.write16(GE0+0xC0, 0x0030)
    while riu.read16(GE0+0x0E) & 1: pass

lines = [
 ' ##     ##         ',
 ' ###   ###@@       ',
 ' #### ####@        ',
 ' ##  @@@##         ',
 ' ## @@@@##  @@@@@@@',
 ' #@@@@@ ##    @ @  ',
 ' ##@@@  ##    @ @  ',
 ' ## @   ##  @ @ @  ',
 '####   ####  @  @@@',
]

width = 0

for line in lines:
    if len(line) > width:
        width = len(line)

x = (dispw // 2) - (width * 50 // 2)
y = (disph // 2) - (len(lines) * 50 // 2)
print(x,y,width,len(lines))

for i, line in enumerate(lines):
    for j, char in enumerate(line):
        xrect(x + j*50, y + i*50, 40, 40, char)
```
