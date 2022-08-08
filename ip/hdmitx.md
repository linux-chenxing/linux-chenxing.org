# HDMI TX

# Kronus variant

HDMI TX variant in [Kronus](/kronus) family (e.g. **MSD7816**)

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
    b0 = SDA pin
    b4 = SCL pin
    b15 = ?? i2c driver clears it together with chiptop.regA0 (set all pad in)

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
    b0 = Hotplug

reg20:
    b0~b31 = TXPLL out divider (bias 0x10000000)

reg3C:
    b0~b15 = clkgen

reg54:
    b0~b3 = tm atop power down <0x0 on power on, 0xf on power down>
    set to 000f on init

reg56:
    b0 = ?? set to 1 on init
    b1 = ?? set to 1 on init, changed in video mode setting

reg58:
    set to 0000 on init

reg5A:
    b5 = ?

reg5C:
    b0~b3 = tm atop enable <0xf on power on, 0x0 on power down>
    b4~b7 = ?
    b8~b11 = ?
    set to 0000 on video init

reg5E:
    b0~b3 = ?
    b4~b7 = ?

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
      3 => ?? picture jitters a little bit, set for modes with pclk=148.5 MHz

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
    b0 = ? interlaced
    b1~b3 = ?
    b6 = ?
    b10 = swap R/B channels

reg02:
    b0 = enable sync polarity control (when disabled, syncs are positive)
    b1 = hsync polarity [0: negative, 1: positive]
    b2 = vsync polarity [0: negative, 1: positive]
    b4~b5 = ?? set to 3 on video init
    b8 = Convert YUV to RGB
    b9 = ?

reg04:
    b0~b7 = vsync width

reg06:
    b0~b8 = vdelay (amount of pclks before the active period starts after vsync)

reg08:
    b0~b11 = vactive

reg0A:
    b0~b7 = ?? vertical delay (input delay? syncs delay?)

reg0C:
    b0~b9 = ??

reg0E:
    b0~b9 = hsync width

reg10:
    b0~b9 = hdelay (amount of lines before the active period starts after hsync)

reg12:
    b0~b11 = hactive

reg14:
    b0~b9 = ?? horizontal delay (input delay? syncs delay?)

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
    b0~b2 = color depth:
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

### Init code

This code inits the HDMITX and the display subsystem at 1280x1024@60Hz mode.

```py
vm_hactive = 1280
vm_hbporch = 48
vm_hsync   = 112
vm_hfporch = 248
vm_vactive = 1024
vm_vbporch = 1
vm_vsync   = 3
vm_vfporch = 38
vm_pclk    = 108000000
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
print('hfreq: %.3f kHz' % (vm_pclk / 1000 / vm_htotal))
print('vfreq: %.3f Hz' % (vm_pclk / vm_htotal / vm_vtotal))

dispw = vm_hactive
disph = vm_vactive
dispaddr = 0x1000000

#==================================================#

#--- disable ints
riu.write16(0x113018, 0xffff)
riu.write16(0x11301a, 0xffff)
#--- clear ints
riu.write16(0x11301c, 0x0000)
riu.write16(0x11301e, 0x0005)

riu.write16(0x113054, 0x000f)

riu.write16(0x103350, 0x0000)

riu.write16(0x11303c, 0xffff) # clkgen
riu.write16(0x11308a, 0x0000)
riu.write16(0x113066, 0x0000)
riu.write16(0x113056, 0x0003)
riu.write16(0x113058, 0x0000)

#--- synth soft reset
riu.wmask16(0x113000, 1<<7, 1<<7)
riu.wmask16(0x113000, 1<<7, 0<<7)

riu.write16(0x1131a6, 0x0300)
riu.write16(0x1130b0, 0x0003)
riu.write16(0x113082, 0x1010)
riu.write16(0x113068, 0x1010)

#--- enable ints
riu.write16(0x113018, 0xffff)
riu.write16(0x11301a, 0xfffa)

#--- video init
riu.write16(0x113066, 0x0000)
riu.write16(0x11305c, 0x0000)
riu.wmask16(0x113202, 0x30, 0x30)
riu.wmask16(0x113224, 0xf, 0x8)

#--- audio init
riu.wmask16(0x11300a, 0x1087, 0x1003)

#---------- Video On/OFF
riu.wmask16(0x113216, 1<<6, 1<<0)

#-------- set hdmitx mode

#--- color depth
riu.wmask16(0x11322E, 7<<0, 0<<0)
riu.wmask16(0x113100, 0xff, 0x04)

'''
#--- packet 5
#riu.read16(0x113106) #=> 0x0021
riu.write16(0x113106, 0x0020)

#--- packet 0
#riu.read16(0x113104) #=> 0x000d
riu.write16(0x113104, 0x0005)
'''

'''
# ======= 0x81 Infoframe ======= #
#riu.read16(0x11314e) #=> 0x0c03
riu.write16(0x11314e, 0x0c03)
#riu.read16(0x11314e) #=> 0x0c03
#riu.read16(0x113150) #=> 0x0000
#riu.read16(0x113152) #=> 0x0000
#riu.read16(0x113154) #=> 0x0000
#riu.read16(0x113156) #=> 0x0000
#riu.read16(0x113158) #=> 0x0000
#riu.read16(0x11315a) #=> 0x0000
#riu.read16(0x11315c) #=> 0x0000
#riu.read16(0x11315e) #=> 0x0000
#riu.read16(0x113160) #=> 0x0000
#riu.read16(0x113162) #=> 0x0000
#riu.read16(0x113164) #=> 0x0000
#riu.read16(0x113166) #=> 0x0000
#riu.read16(0x113168) #=> 0x0000
riu.write16(0x11316a, 0x547d)
'''

'''
# ======= 0x83 Infoframe ======= #
#riu.read16(0x11312a) #=> 0x0000
riu.write16(0x11312a, 0x534d)
#riu.read16(0x11312c) #=> 0x0000
riu.write16(0x11312c, 0x6174)
#riu.read16(0x11312e) #=> 0x0000
riu.write16(0x11312e, 0x2072)
#riu.read16(0x113130) #=> 0x0000
riu.write16(0x113130, 0x2020)
#riu.read16(0x113132) #=> 0x0000
riu.write16(0x113132, 0x4448)
#riu.read16(0x113134) #=> 0x0000
riu.write16(0x113134, 0x494d)
#riu.read16(0x113136) #=> 0x0000
riu.write16(0x113136, 0x5420)
#riu.read16(0x113138) #=> 0x0000
riu.write16(0x113138, 0x2078)
#riu.read16(0x11313a) #=> 0x0000
riu.write16(0x11313a, 0x6544)
#riu.read16(0x11313c) #=> 0x0000
riu.write16(0x11313c, 0x6f6d)
#riu.read16(0x11313e) #=> 0x0000
riu.write16(0x11313e, 0x0000)
#riu.read16(0x113140) #=> 0x0000
riu.write16(0x113140, 0x0000)
#riu.read16(0x113142) #=> 0x0000
riu.write16(0x113142, 0x0001)
#riu.read16(0x11312a) #=> 0x534d
#riu.read16(0x11312c) #=> 0x6174
#riu.read16(0x11312e) #=> 0x2072
#riu.read16(0x113130) #=> 0x2020
#riu.read16(0x113132) #=> 0x4448
#riu.read16(0x113134) #=> 0x494d
#riu.read16(0x113136) #=> 0x5420
#riu.read16(0x113138) #=> 0x2078
#riu.read16(0x11313a) #=> 0x6544
#riu.read16(0x11313c) #=> 0x6f6d
#riu.read16(0x11313e) #=> 0x0000
#riu.read16(0x113140) #=> 0x0000
#riu.read16(0x113142) #=> 0x0001
riu.write16(0x113144, 0x687d)
'''

#-------- set color format (YUV -> YUV444)
riu.wmask16(0x113202, 1<<8, 0<<8) # convert yuv to rgb
riu.wmask16(0x113230, 1<<0, 0<<0) # out chroma subsampling

'''
# ======= AVI InfoFrame ======= #
#riu.read16(0x113112) #=> 0x0000
riu.write16(0x113112, 0x58d0) # b5~b6 => color format: 10 = YUV444, 00 = RGB
#riu.read16(0x113114) #=> 0x0000
riu.write16(0x113114, 0x0200)
#riu.read16(0x113116) #=> 0x0000
riu.write16(0x113116, 0x0000)
#riu.read16(0x113112) #=> 0x58d0
#riu.read16(0x113112) #=> 0x58d0
#riu.read16(0x113114) #=> 0x0200
#riu.read16(0x113116) #=> 0x0000
#riu.read16(0x113118) #=> 0x0000
#riu.read16(0x11311a) #=> 0x0000
#riu.read16(0x11311c) #=> 0x0000
#riu.read16(0x11311e) #=> 0x0000
riu.write16(0x113120, 0xc505)
'''

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
riu.write16(0x100ba6, (0<<5)|(2<<2)|0)

#
# 576 MHz * 3/4 / 4 => 108 MHz / <div>
# >>> No jitter
#
# 576 MHz * 1/2 / 2 => 144 MHz / <div>
# >>> Jitter
#

riu.write16(0x11300a, 0x0430 | (1<<0))
riu.write32(0x113020, int((108000000 / vm_pclk) * 0x10000000))

#------- HDMI video mode & syncs -------

riu.wmask16(0x113200, 0x4f, 0x4e) # ?

riu.wmask16(0x113202, 1<<2, vm_vspos<<2) # vsync polarity
riu.wmask16(0x113202, 1<<1, vm_hspos<<1) # hsync polarity
riu.wmask16(0x113202, 1<<0, 1<<0) # enable sync polarity control

riu.wmask16(0x113070, 3<<6, 1<<6)
riu.wmask16(0x113066, 7<<4, 5<<4)
riu.wmask16(0x11305A, 1<<5, 0<<5)
riu.wmask16(0x113056, 1<<1, 1<<1)
riu.wmask16(0x11305C, 0xf<<4, 0x0<<4)
riu.wmask16(0x11305C, 0xf<<8, 0x0<<8)
riu.wmask16(0x11305E, 0xf<<0, 0x0<<0)
riu.wmask16(0x11305E, 0xf<<4, 0x0<<4)

riu.write16(0x113204, vm_vsync)   # vsync
riu.write16(0x113206, vm_vfporch) # vdelay
riu.write16(0x113208, vm_vactive) # vactive
riu.write16(0x11320a, 0x0000) # vertical offset thing
riu.write16(0x11320c, 0x0000)
riu.write16(0x11320e, vm_hsync)   # hsync
riu.write16(0x113210, vm_hfporch) # hdelay
riu.write16(0x113212, vm_hactive) # hactive
riu.write16(0x113214, 0x0000) # horizontal offset thing
riu.write16(0x113226, vm_vtotal) # vtotal
riu.write16(0x113228, vm_htotal) # htotal

#-------- set overscan afd

'''
# ======= AVI InfoFrame ======= #
#riu.read16(0x113112) #=> 0x58d0
riu.write16(0x113112, 0xaad0)
#riu.read16(0x113114) #=> 0x0200
riu.write16(0x113114, 0x0400)
#riu.read16(0x113116) #=> 0x0000
riu.write16(0x113116, 0x0000)
#riu.read16(0x113112) #=> 0xaad0
#riu.read16(0x113112) #=> 0xaad0
#riu.read16(0x113114) #=> 0x0400
#riu.read16(0x113116) #=> 0x0000
#riu.read16(0x113118) #=> 0x0000
#riu.read16(0x11311a) #=> 0x0000
#riu.read16(0x11311c) #=> 0x0000
#riu.read16(0x11311e) #=> 0x0000
riu.write16(0x113120, 0x7105)
'''

#----- Turn on TMDS -----
riu.wmask16(0x113200, 1<<10, 0<<10) # no swap
riu.wmask16(0x113054, 0xf, 0x0) # power up
riu.wmask16(0x11305c, 0xf, 0xf) # enable

#----------------------------------------------------

riu.write16(0x103000, 0x0001)
riu.write16(0x103002, 0x000f) # ...fix hdmi... b1 matters

#============================================================================#

riu.write8(0x102F00, 0x0F) # xc bank 0x0F
riu.wmask16(0x102FAE, 1<<11, 1<<11) # ---> ve is receiving image!! MST786:"capture image to ip enable"

riu.write8(0x102F00, 0x10) # xc bank 0x10
riu.wmask16(0x102F46, 1<<5, 1<<5) # sets b5?

riu.write8(0x102F00, 0x2F) # xc bank 0x2F
riu.wmask16(0x102F4E, 1<<0, 1<<0) # ---> gop is displayed!!

##########################
# EASY PART              #
#========================#===================================================#
# I KNOW THIS WORKS WELL #
##########################

riu.write8(0x102F00, 0x10) # xc bank 0x10
riu.write16(0x102F02, vm_hsend)    # vop_hsend_width
riu.write16(0x102F04, vm_vsst)     # vop_vsst
riu.write16(0x102F06, vm_vsend)    # vop_vsend
riu.write16(0x102F08, vm_hstart)   # vop_de_hstart
riu.write16(0x102F0A, vm_hend)     # vop_de_hend
riu.write16(0x102F0C, vm_vstart)   # vop_de_vstart
riu.write16(0x102F0E, vm_vend)     # vop_de_vend
riu.write16(0x102F18, vm_htotal-1) # vop_hdtot
riu.write16(0x102F1A, vm_vtotal-1) # vop_vdtot

riu.write8(0x102F00, 0x00) # xc bank 0x00
riu.write16(0x102F0C, 0x8000) # enable GOP MUX0

riu.write16(0x101FFC, (0<<0)|(1<<3)|(2<<6)|(3<<9))

riu.write8(0x101FFE, 0x0) # gop bank 0x0
riu.write16(0x101F00, 0x400C)       # ctrl0
riu.write16(0x101F02, 0x4102)       # ctrl1
riu.write16(0x101F1C, (dispw + 3) // 2)   # rdma_ht
riu.write16(0x101F1E, vm_hstart-13) # hs_pipe
riu.write16(0x101F32, 0x4760)       # bw
riu.write16(0x101F60, dispw // 2)   # strch_hsz
riu.write16(0x101F62, disph)        # strch_vsz
riu.write16(0x101F64, 0)            # strch_hstr
riu.write16(0x101F68, 0)            # strch_vstr
riu.write16(0x101F6A, int(dispw * 0x1000 / vm_hactive) & 0x1fff) # strch_hstrch
riu.write16(0x101F6C, int(disph * 0x1000 / vm_vactive) & 0x1fff) # strch_vstrch
riu.write16(0x101F70, 0)            # strch_hstrch_ini
riu.write16(0x101F72, 0)            # strch_vstrch_ini
riu.write8(0x101FFF, 1) # write_force
riu.write8(0x101FFF, 0)

riu.write8(0x101FFE, 0x1) # gop bank 0x1
riu.write16(0x101F00, 0x3F51)           # gwin_ctrl
riu.write32(0x101F02, dispaddr >> 3)    # dram_rblk_[l|h]
riu.write16(0x101F08, 0)                # hstr
riu.write16(0x101F0A, (dispw * 4) >> 3) # hend
riu.write16(0x101F0C, 0)                # vstr
riu.write16(0x101F10, disph)            # vend
riu.write16(0x101F12, (dispw * 4) >> 3) # dram_rblk_hsize
riu.write16(0x101F14, 0x3)              # gwin_alpha_01
riu.write32(0x101F18, 0)                # dram_vstr
riu.write16(0x101F1C, 0)                # dram_hstr
riu.write8(0x101FFF, 1) # write_force
riu.write8(0x101FFF, 0)

#================================================#
# second part, just to show something "sensible" #
#================================================#

riu.wmask16(0x102800, 1, 0) # disable GE
riu.write16(0x102800, 0x0007) # abl, dither, ge
riu.write16(0x102802, 0x0011) # stbb, cmq

riu.write16(0x102822, 0x2) # asrc

riu.write16(0x102824, 0x0<<8)
riu.write16(0x102826, 0xff00) # aconst

riu.write32(0x10284C, dispaddr)
riu.write16(0x102866, dispw * 4)
riu.wmask16(0x102868, 0xf<<8, 0xf<<8)

riu.write16(0x1028AA, 0)
riu.write16(0x1028AC, dispw - 1)
riu.write16(0x1028AE, 0)
riu.write16(0x1028B0, disph - 1)

# base color
riu.write32(0x1028E0, 0xff008000)
# horizontal gradient
riu.write32(0x1028E4, int((0x00 - 0x00) * 0x1000 / dispw) & 0xfffff)
riu.write32(0x1028EC, int((0x00 - 0x00) * 0x1000 / dispw) & 0xfffff)
riu.write32(0x1028F4, int((0xff - 0x00) * 0x1000 / dispw) & 0xfffff)
riu.write16(0x1028FC, 0)
# vertical gradient
riu.write32(0x1028E8, int((0xff - 0x00) * 0x1000 / disph) & 0xfffff)
riu.write32(0x1028F0, int((0x00 - 0x00) * 0x1000 / disph) & 0xfffff)
riu.write32(0x1028F8, int((0x00 - 0x00) * 0x1000 / disph) & 0xfffff)
riu.write16(0x1028FE, 0)
# draw
riu.write16(0x1028D0, 0)
riu.write16(0x1028D2, 0)
riu.write16(0x1028D4, dispw-1)
riu.write16(0x1028D6, disph-1)
riu.write16(0x1028C0, 0x3030)
while riu.read16(0x10280E) & 1: pass

def xrect(x, y, w, h, char):
    if char == ' ': return

    color = 0x0000aa
    if   char == '#': color = 0x555555
    elif char == '@': color = 0xff5555
    elif char == '.': color = 0xffffff

    riu.write32(0x1028E0, 0xff000000)
    riu.write16(0x1028D0, 5+x)
    riu.write16(0x1028D2, 5+y)
    riu.write16(0x1028D4, 5+x+w-1)
    riu.write16(0x1028D6, 5+y+h-1)
    riu.write16(0x1028C0, 0x0030)
    while riu.read16(0x10280E) & 1: pass

    riu.write32(0x1028E0, 0xff000000 | color)
    riu.write16(0x1028D0, x)
    riu.write16(0x1028D2, y)
    riu.write16(0x1028D4, x+w-1)
    riu.write16(0x1028D6, y+h-1)
    riu.write16(0x1028C0, 0x0030)
    while riu.read16(0x10280E) & 1: pass

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
