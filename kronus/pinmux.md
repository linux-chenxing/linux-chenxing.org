# Kronus Pinmux

## Registers

### PM_SLEEP

```
reg12:
    b11 = uart0 rx enable
    b12 = reg_uart_sel0

reg24:
    b0~b15 = 0xBABE to unlock gpio_pm4

reg38:
    b4 = irin is gpio
    b6 = cec is gpio

reg50:
    b0 = irin is gpio_pm5?

reg6A:
    b0 = spi bus is gpio
    b1 = spi cz is gpio
    b2 = gpio_pm6 is gpio
```

### CHIPTOP

```
reg04:
    b0~b2 = ts0:
      0 => none
      1 => ts0_[clk/...]
      2 => ts0_d7 [?!]
      3 => ts0_d0 [?!]
      4 => ci_d3 [?!]
      5 => ci_d2 [?!]
      6 => ci_a14 [?!]
    
    b4~b7 = ts1:
      0 => none
      1 => ts1_[clk/...]
      2 => ts1_d7 [?!]
      3 => ts1_d0 [?!]
      4 => ci_a6 [?!]
      5 => ci_a7 [?!]
      6 => ci_a12 [?!]
      7 => ci_a4 [?!]
    
    b8~b9 = ts2: [??]
      0 => none
      1 => ts2_[clk/...]
      2 => i2s_out_sd0 [?!]

reg06:
    b0~b2 = uart1_[rx/tx]:
      0 => none
      1 => hsync_out/vsync_out [?] || hdmi_hpd/spdif_out
      2 => i2cm0_[sda/scl]
      3 => i2cm1_[sda/scl] || s_gpio3/s_gpio4
      4 => ts1_[clk/sync] [?]
    
    b4~b5 = uart2_[rx/tx]:
      0 => none
      1 => ts1_[d6/d7]
      2 => pf_[a4/a3] [??]
      3 => i2s_out_[sd2/sd3] [??]
    
    b8~b9 = uart3_[rx/tx]:
      0 => none
      1 => et_rxd2/et_rxd3 [?]
      2 => ts0_d1/ts0_d0 [?]
      3 => hsync_out/vsync_out [?]

reg08:
    b4~b6 = [tms/tdo/tdi/tck]_mcu:
      0 => none
      1 => ts1_[clk/d7/vld/sync]

reg0A:
    b0~b2 = spdif_in: [..?]
      0 => none
      1 => ci_a12
      2 => ts0_clk
      3 => spdif_out
      4 => ts1_d6
      5 => sm0_cd
    
    b4~b6 = spdif_out:
      0 => none
      1 => ci_a12
      2 => ts0_clk
      3 => spdif_out
      4 => ts1_d6 || spdif_out?
      5 => sm0_cd
    
    b8~b9 = i2s_in_[bck/ws/d0]:
      0 => none
      1 => sm1_rst [??] || ts1_[clk/d7/d6]
      3 => ts1_clk [?!] || <same as 1>
    
    b12~b13 = i2s_out_[mute/bck/d0/ws/d1/d2/mck]:
      0 => none
      1 => ts1_[d4/d3/d2/d1/d0/vld/sync]
      3 => ts1_clk [?!] || <same as 1>

reg0C:
    b0~b3 = nand: [..?]
      0 => none
      1 => ts1_vld
      2 => ts0_d7
      3 => s_gpio4
      4 => pf_a21 [??]
      5 => ci_a5
    
    b4~b6 = sdio: [..?]
      0 => none
      1 => ts1_clk [?!]
      2 => et_txd1 [?!]
      4 => pf_a5 [?!]
      5 => pf_a14 [?!]
    
    b8~b9 = 

reg0E:
    b0 = ci:
      0 => none
      1 => ci_[a14/...]
    
    b4~b6 = mpif_[clk/cs0z/d0/busy]:
      0 => none
      1 => ts1_clk [?!] || ts1_[d2/d0/vld/sync]?
      2 => et_txd1 [?!]
      4 => pf_a5 [?!]
      5 => pf_a14 [?!]
    
    b8~b10 = et:
      0 => none
      1 => et_crs [?!]
      2 => et_txd1 [?!]
      3 => pf_a14 [??]
      4 => pf_a3 [??]
    
    b12~b13 = modem: [..?]
      0 => none
      1 => ts0_d3 [?!]
      2 => ts1_clk [?!]
      3 => ci_a14 [?!]

reg10:
    b0~b1 = ccir_in: [..?]
      0 => none
      1 => ts0_clk [?!]
    
    b4~b5 = ccir_out: [..?]
      0 => none
      1 => ts0_clk [?!]
    
    b8 = panel_if: [..?]
      0 => none
      1 => ci_a12 [?!]
    
    b12 = i2s_out_[sd3/...]: [??]
      0 => none
      1 => i2s_out_[sd3/...]

reg12:
    b0~b1 = i2cm0_[sda/scl]:
      0 => none
      1 => i2cm0_[sda/scl]
      2 => sm0_[io/clk] [?]
      3 => ci_[cez/irqaz] [?]
    
    b4~b6 = i2cm1_[sda/scl]:
      0 => none
      1 => i2cm1_[sda/scl]
      2 => et_[txd1/txd0] [?]
      3 => ts0_[d5/d4] [?]
      4 => ts1_[d5/d4] [?] || ts1_[d6/d5]
    
    b8~b10 = 
    
    b12~b14 = 

reg16:
    b0 = hsync:
      0 => none
      1 => hsync
    
    b4 = vsync:
      0 => none
      1 => vsync

reg18:
    b0 = sm0_[clk/rst]:
      0 => none
      1 => sm0_[clk/rst]
    
    b4 = sm0_[c4/c8]:
      0 => none
      1 => sm0_[gpio0/gpio1]
    
    b8 = sm0_[io/clk/rst/cd/vcc]:
      0 => none
      1 => sm0_[io/clk/rst/cd/vcc]

reg1A:
    b0~b1 = sm1_[clk/rst]: [??]
      0 => none
      1 => sm1_[clk/rst]
      2 => ts1_[clk/d6] [?]
    
    b4~b5 = sm1_[c4/c8]: [??]
      0 => none
      1 => sm1_[gpio0/gpio1]
      2 => ts1_[d7/d6] [?]
    
    b8~b9 = sm1: [??]
      0 => none
      1 => sm1_[rst/cd/vcc] [?!]
      2 => sm1_[gpio0/gpio1] [?!]
      3 => ts1_[clk/sync/vld/d7/d6] [?]

reg1C:
    b0 =
    
    b4 = 

reg1E:
    b0 = pf_cs1:
      0 => none
      1 => pf_a25

reg20:
    b4~b7 = 

reg22:
    b0~b3 = 
    
    b4~b5 = 
    
    b8~b9 = 
    
    b12~b13 = 

reg24:
    b0~b2 = 
    
    b4~b6 = 

reg28:
    b0 = 
    
    b4 = 

reg2C:
    b0~b3 = 
    
    b4 = 
    
    b8 = 

reg2E:
    b0 = 
    
    b4~b5 = 

reg38:
    b0 =
    
    b1 = <when set to 1, system hangs up... what...>

    b2 = 
    
    b8~b9 = 

reg3A:
    b0 = if_agc:
      0 => none
      1 => if_agc
    
    b1 = rf_agc:
      0 => none
      1 => rf_agc

reg3E:
    b0~b1 = 
    
    b3 = 
    
    b4~b6 = 

reg44:
    b10 = reg_156_mode??

regA0:
    b15 = set all pads to input

regA6:
    b0~b3 = uart0 sel:
    b4~b7 = uart1 sel:
    b8~b11 = uart2 sel:
    b12~b15 = uart3 sel:
      ===below===

regA8:
    b0~b3 = uart4 sel:
      0 => none
      1 => mheg5 (aeon)
      2 => vd_mheg5
      3 => tsp
      4 => piu_uart0
      5 => piu_uart1
      6 => piu_uart2
      7 => piu_fast_uart
      A => mcu51_txd0
      B => mcu51_txd1

regAA:
    b8 = uart0 invert
    b9 = uart1 invert
    b10 = uart2 invert
    b11 = uart3 invert
    b12 = uart4 invert

```
