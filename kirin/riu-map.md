# Kirin RIU map

## PM

| riu addr |  phy addr  |             name              |
|----------|------------|-------------------------------|
| 0x000800 | 0x1f001000 | SERFLASH                      |
| 0x000e00 | 0x1f001c00 |                               |
| 0x001600 | 0x1f002c00 | FSP                           |
| 0x001e00 | 0x1f003c00 | PM_TOP                        |
| 0x003100 | 0x1f006200 | EPHY (MDIO)                   |
| 0x003200 | 0x1f006400 | ethernet related?             |
| 0x003300 | 0x1f006600 | ethernet related?             |
| 0x003c00 | 0x1f007800 | SERFLASH DMA                  |

## Non-PM

| riu addr |  phy addr  |             name              |
|----------|------------|-------------------------------|
| 0x100900 | 0x1f201200 | BDMA                          |
| 0x100980 | 0x1f201300 | UART0                         |
| 0x101900 | 0x1f203200 | INTR_CTRL                     |
| 0x101e00 | 0x1f203c00 | pad mux                       |
| 0x102500 | 0x1f204a00 | GPIO                          |
| 0x103300 | 0x1f206600 | ethernet related?             |
| 0x111500 | 0x1f222a00 | AUDSP                         |
| 0x111600 | 0x1f222c00 | AUDSP                         |
| 0x121b00 | 0x1f243600 | EMAC                          |
| 0x121f00 | 0x1f243e00 | ethernet related?             |
| 0x160300 | 0x1f2c0600 | AUDSP top                     |
