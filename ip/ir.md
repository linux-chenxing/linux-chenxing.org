# IR

Seems to be located at 0x1f007a00 on i3, i2m & every MIPS chip & etc

https://github.com/linux-chenxing/linux-ssc325/blob/takoyaki_dls00v050/drivers/sstar/ir/reg_ir.h

------------------------------------------------

# NEC part

This part decodes the pulse-distance based protocols such as NEC.

## Registers

```
reg00: ir_ctrl
    b0 = Enable
    b1 = Enable Header "leader?" code check
    b2 = Enable Customer code check (Full decode mode)
    b3 = Enable Data code "polarity?" check (Full decode mode)
    b4 = Enable logic 0/1 header check
    b5 = Enable repeat code
    b6 = Interrupt mask
    b7 = Invert incoming signal
    b8 = Enable timeout check
    b9 = Enable separator
    b14~b15 = ? set to 3 after reset

reg02: hdc_upb
    b0~b13 = Header code upper bound

reg04: hdc_lob
    b0~b13 = Header code lower bound

reg06: ofc_upb
    b0~b13 = Offset code upper bound

reg08: ofc_lob
    b0~b13 = Offset code lower bound

reg0A: ofc_rp_upb
    b0~b13 = Offset code (repeat) upper bound

reg0C: ofc_rp_lob
    b0~b13 = Offset code (repeat) lower bound

reg0E: lg01h_upb
    b0~b13 = Logic 0/1 header upper bound

reg10: lg01h_lob
    b0~b13 = Logic 0/1 header lower bound

reg12: lg0_upb
    b0~b13 = Logic 0 upper bound

reg14: lg0_lob
    b0~b13 = Logic 0 lower bound

reg16: lg1_upb
    b0~b13 = Logic 1 upper bound

reg18: lg1_lob
    b0~b13 = Logic 1 lower bound

reg1A: sepr_upb
    b0~b13 = Separator upper bound

reg1C: sepr_lob
    b0~b13 = Separator lower bound

reg1E: timeout_cyc_l
    b0~b19 = Timeout cycle count [0..15]

reg20: timeout_cyc_h / code byte
    b0~b3 = Timeout cycle count [16..19]
    b4~b7 = ? -- set to 3
    b8~b14 = Code total bit count (n-1)
    b15 = Customer code byte count (n-1)

reg22: sepr_bit
    b6 = ? set for swdecode

reg23: fifo_ctrl
    b0~b2 = FIFO depth (n-8-1)
    b3 = Enable FIFO full
    b4~b5 = ?
      0 => raw data / full decode
      1 => sw decode rcmm type
      2 => sw decode 
      3 => sw decode - int np edge trig
    b6 = ? set for swdecode
    b7 = Clear FIFO

reg24: ccode
    b0~b15 = Customer code (e.g. NEC address bytes)

reg26: glhrm_num
    b0~b11 = ? set to 804
    b12~b13 = Mode?
      1 => SW decode
      2 => Raw data
      3 => Full decode

reg28: ckdiv_num
    b0~b7 = Clock divider (n-1)

reg29: key_data
    b0~b7 = FIFO read data

reg2A: shot_cnt_[l|h]
    b0~b23 = Count of ticks that has been passed in between signal changes.
                  (for SW decode mode)

reg2D: fifo_status
    b0 = Repeat flag
    b1 = FIFO empty
    b2 = ? briefly cleared when the key is received
    b3 = FIFO full
    b4 = ?

reg30: fifo_rd_pulse
    b0 = FIFO read
    b5 = "wakeup key sel"

```

--------------------------------------------------------

# RC5/RC6 part

This part decodes the Philips' RC5/RC6 protocols.

## Registers

```
reg00: ctrl
    b5 = autoconfig
    b6 = fifo clear
    b7 = fifo wfirst
    b8 = en
    b9 = rc6 en
    b10 = rc5ext en
    b11 = wkup en
    b15 = rcin inv

reg02: longpulse_thr

reg04: longpulse_mar

reg06: clk_int_thr

reg08: wd_timeout_cnt

reg0A: comp_key1_key2

reg0C: key_command_add

reg0E: key_misc

reg10: key_fifo_status
    b0 = fifo empty
    b1 = timeout flag
    b2 = fifo full

reg12: fifo_rd_pulse

reg14: cmp_rckey

```

