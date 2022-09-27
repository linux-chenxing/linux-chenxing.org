# IR

Seems to be located at 0x1f007a00 on i3, i2m

https://github.com/linux-chenxing/linux-ssc325/blob/takoyaki_dls00v050/drivers/sstar/ir/reg_ir.h

----

## Registers

### NEC part

```
reg00: ir_ctrl
    b0 = en
    b1 = ldcchk en
    b2 = ccode chk en
    b3 = dcode pchk en
    b4 = lg01h chk en
    b5 = rpcode en
    b6 = int mask
    b7 = inv
    b8 = timeout chk en
    b9 = sepr en

reg02: hdc_upb
    header code upper bound

reg04: hdc_lob
    header code lower bound

reg06: ofc_upb
    offset code upper bound

reg08: ofc_lob
    offset code lower bound

reg0A: ofc_rp_upb
    offset code (repeat) upper bound

reg0C: ofc_rp_lob
    offset code (repeat) lower bound

reg0E: lg01h_upb
    logic 0/1 header upper bound

reg10: lg01h_lob
    logic 0/1 header lower bound

reg12: lg0_upb
    logic 0 upper bound

reg14: lg0_lob
    logic 0 lower bound

reg16: lg1_upb
    logic 1 upper bound

reg18: lg1_lob
    logic 1 lower bound

reg1A: sepr_upb
    separator upper bound

reg1C: sepr_lob
    separator lower bound

reg1E: timeout_cyc_l
    b0~b19 = timeout cycle count [0..15]

reg20: timeout_cyc_h / code byte
    b0~b3 = timeout cycle count [16..19]
    b4~b7 = ? -- set to 3
    b8~b15 = ? -- set to 9F "ir_ccode_byte:1 + ir_code_bit_num:32"

reg22: sepr_bit
    b6 = ? set for swdecode

reg23: fifo_ctrl
    b0~b2 = FIFO depth (n-1 ?)
    b3 = enable FIFO full (if cleared, then if FIFO becomes full, it clears itself)
    b4~b5 = ?
      0 => raw data / full decode
      1 => sw decode rcmm type
      2 => sw decode 
      3 => sw decode - int np edge trig
    b6 = ? set for swdecode
    b7 = clear FIFO

reg24: ccode
    b0~b15 = customer code (e.g. NEC address bytes)

reg26: glhrm_num
    b0~b11 = ? set to 804
    b12~b13 = ? mode?
      1 => for swdecode
      2 => for raw data
      3 => for full decode

reg28: ckdiv_num
    b0~b7 = clock divider (n-1)

reg29: key_data
    b0~b7 = FIFO read data

reg2A: shot_cnt_[l|h]
    b0~b23 = shot count

reg2D: fifo_status
    b0 = repeat flag
    b1 = fifo empty
    b2 = fifo ready ?? briefly cleared when a key is received
    b3 = fifo full
    b4 = ?

reg30: fifo_rd_pulse
    b0 = fifo read
    b5 = "wakeup key sel"

```

### RC5/RC6 part

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
    b2 = fifo full
    b1 = timeout flag
    b0 = fifo empty

reg12: fifo_rd_pulse

reg14: cmp_rckey

```

