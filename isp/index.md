# ISP

The chips have two i2c slaves behind the uart pins that seems to work even when the uart is on.

For example on a mercury5 device with the uart pins connected to the i2c controller of a board
running linux we can see two slaves on the bus:

```
$ i2cdetect -y 0
     0  1  2  3  4  5  6  7  8  9  a  b  c  d  e  f
00:          -- -- -- -- -- -- -- -- -- -- -- -- -- 
10: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
20: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
30: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
40: -- -- -- -- -- -- -- -- -- 49 -- -- -- -- -- -- 
50: -- -- -- -- -- -- -- -- -- 59 -- -- -- -- -- -- 
60: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
70: -- -- -- -- -- -- -- -- 
```

These i2c slaves are present on infinity, infinity3, infinity2m, pioneer3.. and probably everything else.

## ISP protocol

The ISP (In System Programmer) slave exposes the SPI bus where the SPI flash is connected.

- on MSB123xC it is at address 0x51
- elsewhere it is at 0x49

When the interface is not active, the string "MSTAR" (0x4d 0x53 0x54 0x41 0x52) needs to be sent to activate the interface.
Then you will be able to send these commands:

- 0x10 = Send bytes over SPI, each next byte is sent over
- 0x11 = Receive bytes from SPI
- 0x12 = End SPI transaction (Pull up CS)
- 0x20 = ?, reads 0xC0 **(reads 0x80 when communication is ongoing (cs low / bus busy))**
- 0x21 = ?, **seem to reset crc register to 0xffff and on kronus spi always reads 0xff**
- 0x22 = read crc register high
- 0x23 = read crc register low
- 0x24 = Exit ISP (also resets the system, so maybe the isp deactivation is the cause of it)
- 0x25 = ? **(the ISP slave disappears and the SPI bus seems to be locked and trying to access it locks up the system, maybe it's the real ISP exit cmd? MSB123xC also pulls down its SDA line)**

### CRC register

The CRC shift register uses the polynomial 0x8005 (x16 + x15 + x2 + 1), and its initial state is 0xffff.
Its contents seem to change only when the bytes are transferred out of SPI bus, and the value that gets into CRC
is either an **previously sent byte** or an **prefetched receive byte**.

```py
with MStarISP(vgaddc_bus, 0x49) as isp:
    isp.spi_send(b'\x03\x01\x00\x00')
    hexdump(isp.spi_recv(100))
    isp.spi_stop()

with MStarISP(vgaddc_bus, 0x49) as isp:
    print("%02x:%02x" % (isp.bus_xfer(b'\x22', 1)[0], isp.bus_xfer(b'\x23', 1)[0]))

    isp.spi_send(b'\x03')
    print("%02x:%02x" % (isp.bus_xfer(b'\x22', 1)[0], isp.bus_xfer(b'\x23', 1)[0]))

    isp.spi_send(b'\x01')
    print("%02x:%02x" % (isp.bus_xfer(b'\x22', 1)[0], isp.bus_xfer(b'\x23', 1)[0]))

    isp.spi_send(b'\x00')
    print("%02x:%02x" % (isp.bus_xfer(b'\x22', 1)[0], isp.bus_xfer(b'\x23', 1)[0]))

    isp.spi_send(b'\x00')
    print("%02x:%02x" % (isp.bus_xfer(b'\x22', 1)[0], isp.bus_xfer(b'\x23', 1)[0]))

    hexdump(isp.spi_recv(99))
    print("%02x:%02x" % (isp.bus_xfer(b'\x22', 1)[0], isp.bus_xfer(b'\x23', 1)[0]))

    isp.spi_stop()

    isp.spi_send(b'\x03')
    print("%02x:%02x" % (isp.bus_xfer(b'\x22', 1)[0], isp.bus_xfer(b'\x23', 1)[0]))

    isp.spi_send(b'\x01')
    print("%02x:%02x" % (isp.bus_xfer(b'\x22', 1)[0], isp.bus_xfer(b'\x23', 1)[0]))

    isp.spi_send(b'\x00')
    print("%02x:%02x" % (isp.bus_xfer(b'\x22', 1)[0], isp.bus_xfer(b'\x23', 1)[0]))

    isp.spi_send(b'\x01')
    print("%02x:%02x" % (isp.bus_xfer(b'\x22', 1)[0], isp.bus_xfer(b'\x23', 1)[0]))

    #hexdump(isp.spi_recv(100))
    print("%02x:%02x" % (isp.bus_xfer(b'\x22', 1)[0], isp.bus_xfer(b'\x23', 1)[0]))

    isp.spi_stop()

    print("=======")

    isp.bus_xfer(b'\x21')

    print("%02x:%02x" % (isp.bus_xfer(b'\x22', 1)[0], isp.bus_xfer(b'\x23', 1)[0]))

    isp.spi_send(b'\x03')
    print("%02x:%02x" % (isp.bus_xfer(b'\x22', 1)[0], isp.bus_xfer(b'\x23', 1)[0]))

    isp.spi_send(b'\x01')
    print("%02x:%02x" % (isp.bus_xfer(b'\x22', 1)[0], isp.bus_xfer(b'\x23', 1)[0]))

    isp.spi_send(b'\x00')
    print("%02x:%02x" % (isp.bus_xfer(b'\x22', 1)[0], isp.bus_xfer(b'\x23', 1)[0]))

    isp.spi_send(b'\x00')
    print("%02x:%02x" % (isp.bus_xfer(b'\x22', 1)[0], isp.bus_xfer(b'\x23', 1)[0]))

    hexdump(isp.spi_recv(100))
    print("%02x:%02x" % (isp.bus_xfer(b'\x22', 1)[0], isp.bus_xfer(b'\x23', 1)[0]))

    isp.spi_stop()
```

```
00000000: 27 05 19 56 8e 8c c5 81 61 b9 fe 38 00 04 f7 22  |'..V....a..8..."|
00000010: 87 5f 01 80 87 5f 06 00 7b 13 27 d5 11 05 02 03  |._..._..{.'.....|
00000020: 4d 53 74 61 72 20 4d 53 44 37 38 31 36 20 55 2d  |MStar MSD7816 U-|
00000030: 42 6f 6f 74 00 00 00 00 00 00 00 00 00 00 00 00  |Boot............|
00000040: 5d 00 00 80 00 ff ff ff ff ff ff ff ff 00 00 1b  |]...............|
00000050: 04 55 3f d3 d1 56 64 2c 9c 6d 7b 38 a6 21 71 4a  |.U?..Vd,.m{8.!qJ|
00000060: 6e 20 ea 3a -- -- -- -- -- -- -- -- -- -- -- --  |n .:            |
                   ^^
              the last byte there is 0x3a
(system resets there, previous read has no effect there)
ff:ff <- rst
fd:02 <- sent 0x03 but it did 0x00
80:07 <- sent 0x01 but it did 0x03
04:06 <- sent 0x00 but it did 0x01
86:1b <- sent 0x00 and it did 0x00
00000000: 27 05 19 56 8e 8c c5 81 61 b9 fe 38 00 04 f7 22  |'..V....a..8..."|
00000010: 87 5f 01 80 87 5f 06 00 7b 13 27 d5 11 05 02 03  |._..._..{.'.....|
00000020: 4d 53 74 61 72 20 4d 53 44 37 38 31 36 20 55 2d  |MStar MSD7816 U-|
00000030: 42 6f 6f 74 00 00 00 00 00 00 00 00 00 00 00 00  |Boot............|
00000040: 5d 00 00 80 00 ff ff ff ff ff ff ff ff 00 00 1b  |]...............|
00000050: 04 55 3f d3 d1 56 64 2c 9c 6d 7b 38 a6 21 71 4a  |.U?..Vd,.m{8.!qJ|
00000060: 6e 20 ea -- -- -- -- -- -- -- -- -- -- -- -- --  |n .             |
                ^^ ^^
           there we read one byte less, the following byte is 0x3a
86:1b <- read does not affect
98:8b <- sent 0x03 but it did 0x3a (the byte that we didnt read but it is present in flash!)
08:59 <- same as before
59:36
37:d6 <- sent 0x01 but it did 0x00
37:d6 <- we didnt read there
======= <- there is the cmd 0x21
ff:ff <- crc reset
7d:07 <- sent 0x03 but it did 0x01 (the last byte i sent previously!)
06:04
84:11
12:18
00000000: ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff  |................|
00000010: ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff  |................|
00000020: ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff  |................|
00000030: ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff  |................|
00000040: ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff  |................|
00000050: ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff  |................|
00000060: ff ff ff ff -- -- -- -- -- -- -- -- -- -- -- --  |....            |
           ^^^^^^^
         cmd 0x21 made all data read from spi be all 0xff
12:18

```

## SERDB protocol

The SERDB (SERial DeBug) slave exposes the HK51/PM51's XDATA and the RIU bus, as well as ability to stop/start MCU for doing some kind of debugging.
(but it is also used to bring up chips like MSB123xC or MSG2138)

- on MSB123xC it is at address 0x69
- on MSG2138 it is at 0x62
- on Kronus it is at 0x5A
- elsewhere it is at 0x59

Same as ISP, it needs to be activated by sending string "SERDB" (0x53 0x45 0x52 0x44 0x42).
Then you will be able to send these commands:

- 0x10 = Read/write bus, next 2/4 bytes is the address (big endian), then goes data
- 0x34 = Disable bus access
- 0x35 = Enable bus access
- 0x36 = Resume MCU
- 0x37 = Stop MCU
- 0x45 = Exit SERDB **(note: this cmd is NAKed)**
- 0x51 = ? (sent when its about to stop mcu, the next cmd is 0x35)
- 0x53 = ? (sent when its not about to stop mcu, the next cmd is 0x7F)
- 0x61 = ?
- 0x70 = ?
- 0x71 = ? "i2c reshape"
- 0x7F = ? (used in place of the stop mcu cmd when its not about to stop mcu)
- 0x80 = clear bus channel no. bit 0
- 0x81 = set bus channel no. bit 0
- 0x82 = clear bus channel no. bit 1
- 0x83 = set bus channel no. bit 1
- 0x84 = clear bus channel no. bit 2
- 0x85 = set bus channel no. bit 2

### Protocol variations

#### The "older" one

This variant uses 2 bytes for bus addressing and does not have channel switching,
thus it only can access 8051 XDATA. (because MStar was making 8051-based chips at the time)

In SoCs where the RIU was split into PM and Non-PM parts (after Saturn?)
the Non-PM part is accessed by writing the bits 16-23 of the RIU address (0x10/0x11/etc) into address 0x0000 and then access with address bits 0-15.

(i.e. to access 0x101ecc write 0x10 into 0x0000 then access 0x1ecc, and to access 0x110c32 write 0x11 into 0x0000 then access 0x0c32)

#### The "newer" one

This variant now uses 4 bytes for bus addressing, and also introduced bus channel switching.

| channel | accessed bus |
|---------|--------------|
|   0     |  8051 XDATA  |
|   3     |  PM RIU      |
|   4     |  Non-PM RIU  |

----

# Debug tool

![isp tool front](debugtool_front_thumb.jpg)

- FTDI FT2232D
- NXP 74HC08D (Quad 2-input AND gate)
- Atmel 93C56A (2Kb EEPROM)

# Homebrew

- Adafruit 5v trinket.
- [i2c-tiny-usb](https://github.com/harbaum/I2C-Tiny-USB/tree/master/digispark)
- [flashrom](https://github.com/flashrom/flashrom) - If you have SPI NOR flash
  - If configured correctly flashrom has a driver that can talk via i2c to the flash very slowly.
  - ```make CONFIG_MSTARDDC_SPI=yes CONFIG_ENABLE_LIBPCI_PROGRAMMERS=no```
- [SNANDer fork with mstarddc support](https://github.com/fifteenhex/SNANDer/tree/mstar) for SPI NOR or NAND.
  - Same deal as flashrom, very slow!
  - Good enough to write the required blobs and u-boot.
  - `sudo ./SNANDer -p mstarddc -c /dev/i2c-4:49 -i`

# ISP SPI protocol

Some details on the SPI over i2c protocol are [here](http://boeglin.org/blog/index.php?entry=Flashing-a-BenQ-Z-series-for-free). The same windows tool is used for all MStar chips it seems so this is probably valid across the board.

The 0x49 i2c slave is the SPI bridge to the flash.

# ISP DEBUG protocol

- Lives on the 0x59 slave
- synchronization string is "SERDB".

Reading a bank of registers looks like this:

```
Writing "SERDB"

i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 53
i2c-1: Data write: 45
i2c-1: Data write: 52
i2c-1: Data write: 44
i2c-1: Data write: 42
---
Setting up something? Memory dump also has this sequence

i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 81
i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 83
i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 84
i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 53
i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 7F
i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 35
i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 71
i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 34
i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 45
---
"SERDB" again

i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 53
i2c-1: Data write: 45
i2c-1: Data write: 52
i2c-1: Data write: 44
i2c-1: Data write: 42

---
Another common senquence between register dump and mem dump

i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 81
i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 83
i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 84
i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 53
i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 7F
i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 35
i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 71
i2c-1: Write
---
Common between reg dump and memdump

i2c-1: Address write: B2
i2c-1: Data write: 10
i2c-1: Data write: 00
i2c-1: Data write: 00
i2c-1: Data write: 1E
i2c-1: Data write: CF
i2c-1: Read
---
Common

i2c-1: Address read: B3
i2c-1: Data read: 00
i2c-1: Write
---
Common
i2c-1: Address write: B2
i2c-1: Data write: 10
i2c-1: Data write: 00
i2c-1: Data write: 00
i2c-1: Data write: 1E
i2c-1: Data write: CC
i2c-1: Read
---
common
i2c-1: Address read: B3
i2c-1: Data read: F5
i2c-1: Write
---
common
i2c-1: Address write: B2
i2c-1: Data write: 10
i2c-1: Data write: 00
i2c-1: Data write: 00
i2c-1: Data write: 1E
i2c-1: Data write: CD
i2c-1: Read
---
common
i2c-1: Address read: B3
i2c-1: Data read: 00
i2c-1: Write
---
common
i2c-1: Address write: B2
i2c-1: Data write: 34
i2c-1: Write
---
common
i2c-1: Address write: B2
i2c-1: Data write: 45
i2c-1: Write
---
common
i2c-1: Address write: B2
i2c-1: Data write: 53
i2c-1: Data write: 45
i2c-1: Data write: 52
i2c-1: Data write: 44
i2c-1: Data write: 42
i2c-1: Write
---
common
i2c-1: Address write: B2
i2c-1: Data write: 81
i2c-1: Write
---
common
i2c-1: Address write: B2
i2c-1: Data write: 83
i2c-1: Write
---
common
i2c-1: Address write: B2
i2c-1: Data write: 84
i2c-1: Write
---
common
i2c-1: Address write: B2
i2c-1: Data write: 53
i2c-1: Write
---
common
i2c-1: Address write: B2
i2c-1: Data write: 7F
i2c-1: Write
---
common
i2c-1: Address write: B2
i2c-1: Data write: 35
i2c-1: Write
---
common
i2c-1: Address write: B2
i2c-1: Data write: 71
i2c-1: Write
---
*** reg dump and mem dump diverge here ***
---
"SERDB"
i2c-1: Address write: B2
i2c-1: Data write: 53
i2c-1: Data write: 45
i2c-1: Data write: 52
i2c-1: Data write: 44
i2c-1: Data write: 42
i2c-1: Write
---
i2c-1: Address write: B2
i2c-1: Data write: 81
i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 83
i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 84
i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 53
i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 7F
i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 35
i2c-1: Write
i2c-1: Address write: B2
i2c-1: Data write: 71
i2c-1: Write
---

This looks like a command and then bank 0x30?

i2c-1: Address write: B2
i2c-1: Data write: 10
i2c-1: Data write: 00
i2c-1: Data write: 00
i2c-1: Data write: 30
i2c-1: Data write: 00
i2c-1: Read
---

Register values?

i2c-1: Address read: B3
i2c-1: Data read: 00
i2c-1: Data read: 00
i2c-1: Data read: 00
i2c-1: Data read: 00
i2c-1: Data read: 00
i2c-1: Data read: 09
i2c-1: Data read: FF
i2c-1: Data read: FF
```

### Channel select

A lot of the above seems to be the sequence to select the desired channel

- Channel select sequence:
  - https://github.com/jockyw2001/utopia/blob/53ee8cc121a030b8d368113ac3e966b4705770ef/UTPA2-700.0.x/modules/demodulator/hal/maldives/demod/halDMD_INTERN_common.c#L319

## Booting from SDRAM

https://github.com/fifteenhex/SDK_pulbic/blob/c1436fa7446457e8d6547874d27ee4e34be150cf/Mercury5/proj/sc/driver/hal/mercury/kernel/inc/kernel_chiptop.h#L1897

## ISP tool scripts

- swch - Switch channel?
  - 0 - DRAM?
  - 3 - PM registers
  - 4 - Normal registers
- wsdr - Write a file?
- wriu - Write a register
  - `-b` write a byte?
  - `-w` write a word?
- wait - Wait for N seconds?

## Command bytes

- 0x10 - Seems to be set address
- 0x34 - Seems to be exit from something
- 0x80 - Clear channel bit 0
- 0x81 - Set channel bit 0
- 0x82 - Clear channel bit 1
- 0x83 - Set channel bit 1
- 0x84 - Clear channel bit 2
- 0x85 - Set channel bit 2

0x51 0x53 
0x37 0x7F
0x35
0x71

----
## Appendix

Python classes to interface ISP/SERDB protocols.

```py
from periphery import I2C, I2CError

class MStarISP():
    def __init__(self, bus, addr):
        self.bus = bus
        self.addr = addr

    def __enter__(self):
        self.enter()
        return self

    def __exit__(self, etype, evalue, trace):
        self.exit()

    ## bus related ##
    def bus_xfer(self, send, recv=0):
        msgs = [I2C.Message(send)]
        if recv > 0: msgs.append(I2C.Message(bytes(recv),read=True))
        self.bus.transfer(self.addr, msgs)
        if recv > 0: return msgs[1].data

    ## protocol related ##
    def enter(self):
        try:
            self.bus_xfer(b'MSTAR')
        except I2CError:
            # try again, maybe the interface is still active?
            self.exit()
            self.bus_xfer(b'MSTAR')

    def exit(self):
        self.bus_xfer(b'\x24')

    def spi_send(self, data):
        self.bus_xfer(b'\x10' + data)

    def spi_recv(self, size):
        return self.bus_xfer(b'\x11', size)

    def spi_stop(self):
        self.bus_xfer(b'\x12')

    def get_isp_status(self):
        return self.bus_xfer(b'\x20', 1)[0]

    def do_cmd21(self): # resets CRC and may also break SPI
        self.bus_xfer(b'\x21')

    def get_isp_crc16(self):
        val = self.bus_xfer(b'\x22', 1) + self.bus_xfer(b'\x23', 1)
        return int.from_bytes(val, 'big')

    def do_cmd25(self): # this kills ISP
        self.bus_xfer(b'\x25')

class MStarSERDB():
    def __init__(self, bus, addr, new_proto=True):
        self.bus = bus
        self.addr = addr
        self.new_proto = new_proto

    def __enter__(self):
        self.enter()
        return self

    def __exit__(self, etype, evalue, trace):
        self.exit()

    ## bus related ##
    def bus_xfer(self, send, recv=0):
        #print("BUS XFER: ", send, recv)
        msgs = [I2C.Message(send)]
        if recv > 0: msgs.append(I2C.Message(bytes(recv),read=True))
        self.bus.transfer(self.addr, msgs)
        if recv > 0: return msgs[1].data

    ## protocol related ##
    def enter(self):
        self.curr_ch = -1
        self.curr_bank = -1

        try:
            self.bus_xfer(b'SERDB')
        except I2CError:
            # try again, maybe the interface is still active?
            self.exit()
            self.bus_xfer(b'SERDB')

    def exit(self):
        try:
            self.bus_xfer(b'\x45')
        except I2CError:
            # it always NAKs
            pass

    def set_channel(self, ch):
        self.bus_xfer(b'\x81' if (ch & 1) else b'\x80')
        self.bus_xfer(b'\x83' if (ch & 2) else b'\x82')
        self.bus_xfer(b'\x85' if (ch & 4) else b'\x84')

    def i2c_reshape(self):
        self.bus_xfer(b'\x71')

    def cmd_53(self):
        self.bus_xfer(b'\x53')

    def cmd_7F(self):
        self.bus_xfer(b'\x7f')

    def stop_mcu(self, stop):
        self.bus_xfer(b'\x37' if stop else b'\x36')

    def bus_enable(self, en):
        self.bus_xfer(b'\x35' if en else b'\x34')

    def bus_write(self, addr, data):
        self.bus_xfer(b'\x10' + int.to_bytes(addr, 4 if self.new_proto else 2, 'big') + data)

    def bus_read(self, addr, size):
        return self.bus_xfer(b'\x10' + int.to_bytes(addr, 4 if self.new_proto else 2, 'big'), size)

    ## higher level protocol ##
    def swch(self, ch):
        if (ch < 0) or (ch > 7): return
        if self.curr_ch == ch: return
        self.curr_ch = ch

        # only new proto can do that
        if not self.new_proto: return

        self.i2c_reshape()
        self.set_channel(ch)
        self.cmd_53()
        self.cmd_7F()

    # read
    def read(self, addr, size):
        self.bus_enable(True)

        if not self.new_proto:
            bank = addr >> 16
            if self.curr_bank != bank:
                self.curr_bank = bank
                self.bus_write(0x0000, bytes([bank]))
            addr &= 0xffff

        data = self.bus_read(addr, size)
        self.bus_enable(False)
        return data

    def read8(self, addr):
        return int.from_bytes(self.read(addr, 1), 'little')

    def read16(self, addr):
        return int.from_bytes(self.read(addr, 2), 'little')

    def read32(self, addr):
        return int.from_bytes(self.read(addr, 4), 'little')

    # write
    def write(self, addr, data):
        self.bus_enable(True)

        if not self.new_proto:
            bank = addr >> 16
            if self.curr_bank != bank:
                self.curr_bank = bank
                self.bus_write(0x0000, bytes([bank]))
            addr &= 0xffff

        self.bus_write(addr, data)
        self.bus_enable(False)

    def write8(self, addr, val):
        self.write(addr, int.to_bytes(val & 0xff, 1, 'little'))

    def write16(self, addr, val):
        self.write(addr, int.to_bytes(val & 0xffff, 2, 'little'))

    def write32(self, addr, val):
        self.write(addr, int.to_bytes(val & 0xffffffff, 4, 'little'))

    def wmask8(self, addr, mask, val):
        self.write8(addr, (self.read8(addr) & ~mask) | (val & mask))

    def wmask16(self, addr, mask, val):
        self.write16(addr, (self.read16(addr) & ~mask) | (val & mask))

    def wmask32(self, addr, mask, val):
        self.write32(addr, (self.read32(addr) & ~mask) | (val & mask))

```
