# Pioneer3 IPL RE

```
MstarEmu.java> Running...
New check point 0x0000a001
New check point 0x0000a002
New check point 0x0000b001
RIU Register unhandled write:	0x00223624 -> 0x00000000, write size 1
```
```
RIU Register write - mpll:	0x00206005: 0x00000000 -> 0x00000000, write size 1
```

Turn on MPLL, this is used for the UART clock and everything else so I guess they do it first.

```
New check point 0x0000b002
New check point 0x00000b12
```

```
RIU Register write - clkgen:	0x00207080: 0x00000000 -> 0x00000004, write size 1
RIU Register write - clkgen:	0x00207004: 0x00000000 -> 0x00000030, write size 1
RIU Register write - clkgen:	0x00207180: 0x00000000 -> 0x00000010, write size 1
RIU Register write - clkgen:	0x002070c8: 0x00000000 -> 0x00000004, write size 1
RIU Register read - clkgen:	0x002070c8 = 0x00000000, size 1
RIU Register write - clkgen:	0x002070c8: 0x00000000 -> 0x00000020, write size 1
New check point 0x00000b13
```

Configuring clocks

- 0x20 MIU boot clock
- 0x4 is riubrdg
- 0x180 is BDMA
- 0xc8 is SPI

```
RIU Register read - pmsleep:	0x00001c7c = 0x00000000, size 2
RIU Register write - pmsleep:	0x00001c81: 0x00000000 -> 0x00000400, write size 1
RIU Register read - pmsleep:	0x00001c81 = 0x00000000, size 1
RIU Register write - pmsleep:	0x00001c81: 0x00000000 -> 0x00004000, write size 1
New check point 0x0000b012
RIU Register read - chiptop_ssd210:	0x00203d20 = 0x00000006, size 1
RIU Register unhandled read:	0x0020025c, size 2
RIU Register unhandled write:	0x0020025c -> 0x00000001, write size 2
```

```
RIU Register write - clkgen:	0x002070c4: 0x00000000 -> 0x00000000, write size 1
RIU Register write - clkgen:	0x002070c4: 0x00000000 -> 0x00000000, write size 1
```

- UART0 clock

```
RIU Register read - pmsleep:	0x00001c24 = 0x00000000, size 2
RIU Register write - pmsleep:	0x00001c24: 0x00000000 -> 0x00000000, write size 2
RIU Register write - chiptop_ssd210:	0x00203d4c: 0x00000000 -> 0x00003210, write size 2
RIU Register write - chiptop_ssd210:	0x00203d4c: 0x00000000 -> 0x00003012, write size 2
RIU Register read - pmsleep:	0x00001c24 = 0x00000000, size 2
RIU Register write - pmsleep:	0x00001c24: 0x00000000 -> 0x00000800, write size 2
RIU Register write - cpupll:	0x00206448: 0x0000ffff -> 0x0000ff88, write size 1
RIU Register write - cpupll:	0x00206449: 0x0000ffff -> 0x000000ff, write size 1
RIU Register write - cpupll:	0x00206445: 0x0000ffff -> 0x000001ff, write size 1
RIU Register write - cpupll:	0x00206584: 0x0000ffff -> 0x0000ff45, write size 1
RIU Register write - cpupll:	0x00206581: 0x0000ffff -> 0x00001eff, write size 1
RIU Register write - cpupll:	0x00206580: 0x0000ffff -> 0x0000ffb8, write size 1
RIU Register write - cpupll:	0x00206588: 0x0000ffff -> 0x0000ff01, write size 1
RIU Register write - cpupll:	0x00206445: 0x0000ffff -> 0x000000ff, write size 1
RIU Register write - cpupll:	0x00206540: 0x0000ffff -> 0x00001eb8, write size 2
RIU Register write - cpupll:	0x00206544: 0x0000ffff -> 0x00000045, write size 2
RIU Register write - cpupll:	0x00206548: 0x0000ffff -> 0x00001eb9, write size 2
RIU Register write - cpupll:	0x0020654c: 0x0000ffff -> 0x00000045, write size 2
RIU Register write - cpupll:	0x00206560: 0x0000ffff -> 0x00000001, write size 2
RIU Register write - cpupll:	0x00206554: 0x0000ffff -> 0x00000006, write size 2
RIU Register write - cpupll:	0x0020655c: 0x0000ffff -> 0x00000008, write size 2
RIU Register read - cpupll:	0x00206564 = 0x0000ffff, size 2
RIU Register write - cpupll:	0x00206564: 0x0000ffff -> 0x0000ffff, write size 2
RIU Register write - cpupll:	0x00206550: 0x0000ffff -> 0x00000000, write size 2
RIU Register write - cpupll:	0x00206550: 0x0000ffff -> 0x00000001, write size 2
RIU Register read - cpupll:	0x00206574 = 0x0000ffff, size 2
RIU Register write - cpupll:	0x00206550: 0x0000ffff -> 0x00000000, write size 2
RIU Register write - cpupll:	0x00206540: 0x0000ffff -> 0x00001eb9, write size 2
RIU Register write - cpupll:	0x00206544: 0x0000ffff -> 0x00000045, write size 2
RIU Register read - pmsleep:	0x00001cc0 = 0x00000000, size 1
RIU Register write - pmsleep:	0x00001cc0: 0x00000000 -> 0x00000010, write size 1
UART TX: 
UART TX: IPL g6b146fc
UART TX: D-06
```

```
RIU Register read - wdt:	0x00006008 = 0x00000000, size 2
RIU Register read - pmpor:	0x00000c04 = 0x00000000, size 2
UART TX: 
HW Reset
```

- Reset cause

```
RIU Register write - lpll:	0x00206720: 0x0000ffff -> 0x0000ffa3, write size 1
RIU Register write - lpll:	0x00206721: 0x0000ffff -> 0x00008bff, write size 1
RIU Register write - lpll:	0x00206724: 0x0000ffff -> 0x0000ff2e, write size 1
RIU Register write - lpll:	0x00206725: 0x0000ffff -> 0x000000ff, write size 1
RIU Register write - lpll:	0x00206700: 0x0000ffff -> 0x0000ff01, write size 1
RIU Register write - lpll:	0x00206701: 0x0000ffff -> 0x000022ff, write size 1
RIU Register write - lpll:	0x00206704: 0x0000ffff -> 0x0000ff20, write size 1
RIU Register write - lpll:	0x00206705: 0x0000ffff -> 0x000004ff, write size 1
RIU Register write - lpll:	0x00206708: 0x0000ffff -> 0x0000ff43, write size 1
RIU Register write - lpll:	0x00206709: 0x0000ffff -> 0x000000ff, write size 1
RIU Register write - lpll:	0x0020670c: 0x0000ffff -> 0x0000ff02, write size 1
RIU Register write - lpll:	0x0020670d: 0x0000ffff -> 0x000000ff, write size 1
RIU Register write - lpll:	0x00206710: 0x0000ffff -> 0x0000ff00, write size 1
RIU Register write - lpll:	0x00206711: 0x0000ffff -> 0x000005ff, write size 1
RIU Register write - lpll:	0x00206728: 0x0000ffff -> 0x0000ff01, write size 1
RIU Register write - lpll:	0x00206729: 0x0000ffff -> 0x000000ff, write size 1
RIU Register write - lpll:	0x0020672c: 0x0000ffff -> 0x0000ff00, write size 1
RIU Register write - lpll:	0x0020672d: 0x0000ffff -> 0x000000ff, write size 1
```

LPLL setup

```
RIU Register read - upll0:	0x00284000 = 0x00000000, size 1
```

Turn on UPLL

--- Up to here we might resume so DDR could be alive already ---

```
UART TX: 00000000 00000000
UART TX: Resume? N, addr 00000000
RIU Register write - miudig:	0x0020243c: 0x00000000 -> 0x00000c00, write size 2
RIU Register write - miudig:	0x0020243c: 0x00000000 -> 0x00000c00, write size 2
RIU Register write - miudig:	0x0020243c: 0x00000000 -> 0x00000c00, write size 2
RIU Register write - miudig:	0x0020243c: 0x00000000 -> 0x00000c01, write size 2
```

MIU digital software reset. 0xc00 is the default value. bit 0 is the reset bit.

```
RIU Register write - miudig:	0x0020248c: 0x00000000 -> 0x0000fffe, write size 2 - req 0 mask
RIU Register write - miudig:	0x002024cc: 0x00000000 -> 0x0000ffff, write size 2 - req 1 mask
RIU Register write - miudig:	0x0020250c: 0x00000000 -> 0x0000ffff, write size 2 - req 2 mask
RIU Register write - miudig:	0x0020254c: 0x00000000 -> 0x0000ffff, write size 2 - req 3 mask
RIU Register write - miudig:	0x0020220c: 0x00000000 -> 0x0000ffff, write size 2 - ??
RIU Register write - miudig:	0x0020224c: 0x00000000 -> 0x0000ffff, write size 2 - ??
RIU Register write - miudig:	0x002023cc: 0x00000000 -> 0x0000fffe, write size 2 - ??
```

-- Disable access from other clients?

```
RIU Register write - miuana:	0x002020f0: 0x00000000 -> 0x00000001, write size 2 - 0x3c
RIU Register write - miuana:	0x00202048: 0x00000000 -> 0x00001000, write size 2 - 0x12 - ddrat
RIU Register write - miuana:	0x00202048: 0x00000000 -> 0x00000000, write size 2 -
RIU Register write - miuana:	0x0020206c: 0x00000000 -> 0x00000400, write size 2 - 0x1b ddrpll
RIU Register write - miuana:	0x00202068: 0x00000000 -> 0x00002004, write size 2 - 0x1a ddrpll
RIU Register write - miuana:	0x00202114: 0x00000000 -> 0x00000001, write size 2 - 0x45 - ??
RIU Register write - miuana:	0x00202060: 0x00000000 -> 0x00008000, write size 2 - 0x18 - ddfset
RIU Register write - miuana:	0x00202064: 0x00000000 -> 0x00000029, write size 2 - 0x1c - ddfset
RIU Register write - miuana:	0x00202044: 0x00000000 -> 0x00000004, write size 2 - 0x11 - ddrat
RIU Register write - miuana:	0x00202058: 0x00000000 -> 0x00000114, write size 2 - 0x16
```

DDRPLL config?

```
RIU Register write - miudig:	0x00202404: 0x00000000 -> 0x00000292, write size 2 - 0x1 - DDR config
RIU Register write - miudig:	0x00202408: 0x00000000 -> 0x00000051, write size 2 - 0x2
RIU Register write - miudig:	0x0020240c: 0x00000000 -> 0x00001b50, write size 2
RIU Register write - miudig:	0x00202410: 0x00000000 -> 0x00001e99, write size 2
RIU Register write - miudig:	0x00202414: 0x00000000 -> 0x00002777, write size 2
RIU Register write - miudig:	0x00202418: 0x00000000 -> 0x000095a8, write size 2
RIU Register write - miudig:	0x0020241c: 0x00000000 -> 0x0000404c, write size 2
RIU Register write - miudig:	0x00202420: 0x00000000 -> 0x00000003, write size 2
RIU Register write - miudig:	0x00202424: 0x00000000 -> 0x00004004, write size 2
RIU Register write - miudig:	0x00202428: 0x00000000 -> 0x00008000, write size 2
RIU Register write - miudig:	0x0020242c: 0x00000000 -> 0x0000c000, write size 2
RIU Register write - miudig:	0x00202450: 0x00000000 -> 0x00000070, write size 2
RIU Register write - miudig:	0x002025a4: 0x00000000 -> 0x00006000, write size 2
RIU Register unhandled write:	0x00202644 -> 0x00000003, write size 2
RIU Register unhandled write:	0x0020267c -> 0x00000000, write size 2
RIU Register unhandled write:	0x00202680 -> 0x00000909, write size 2
RIU Register unhandled write:	0x00202684 -> 0x0000071e, write size 2
RIU Register unhandled write:	0x00202688 -> 0x00002707, write size 2
RIU Register unhandled write:	0x0020268c -> 0x00000908, write size 2
RIU Register unhandled write:	0x00202690 -> 0x00000905, write size 2
RIU Register unhandled write:	0x00202694 -> 0x00000304, write size 2
RIU Register unhandled write:	0x00202698 -> 0x00000528, write size 2
RIU Register unhandled write:	0x0020269c -> 0x00000046, write size 2
RIU Register unhandled write:	0x002026a0 -> 0x0000e000, write size 2
RIU Register unhandled write:	0x002026a4 -> 0x00000000, write size 2
RIU Register unhandled write:	0x002026a8 -> 0x00000900, write size 2
RIU Register unhandled write:	0x00202700 -> 0x00000000, write size 2
RIU Register unhandled write:	0x0020270c -> 0x00000000, write size 2
RIU Register unhandled write:	0x002027fc -> 0x00000000, write size 2
RIU Register write - miudig:	0x002022c0: 0x00000000 -> 0x00000000, write size 2
RIU Register write - miudig:	0x002022c4: 0x00000000 -> 0x00000000, write size 2
RIU Register write - miudig:	0x002022c8: 0x00000000 -> 0x00000000, write size 2
RIU Register write - miudig:	0x002022cc: 0x00000000 -> 0x00000030, write size 2
RIU Register write - miudig:	0x002022d0: 0x00000000 -> 0x00005000, write size 2
```

```
RIU Register write - miuana:	0x00202004: 0x00000000 -> 0x0000aaaa, write size 2
RIU Register write - miuana:	0x00202008: 0x00000000 -> 0x00000000, write size 2
RIU Register write - miuana:	0x00202014: 0x00000000 -> 0x00000000, write size 2
RIU Register write - miuana:	0x0020201c: 0x00000000 -> 0x0000008f, write size 2
RIU Register write - miuana:	0x0020205c: 0x00000000 -> 0x00001122, write size 2
RIU Register write - miuana:	0x00202070: 0x00000000 -> 0x00000077, write size 2
RIU Register write - miuana:	0x00202074: 0x00000000 -> 0x00007070, write size 2
RIU Register write - miuana:	0x00202078: 0x00000000 -> 0x00009111, write size 2
RIU Register write - miuana:	0x0020207c: 0x00000000 -> 0x00001111, write size 2
RIU Register write - miuana:	0x00202090: 0x00000000 -> 0x00000077, write size 2
RIU Register write - miuana:	0x00202094: 0x00000000 -> 0x00007070, write size 2
RIU Register write - miuana:	0x00202098: 0x00000000 -> 0x00000011, write size 2
RIU Register write - miuana:	0x0020209c: 0x00000000 -> 0x00000011, write size 2
RIU Register write - miuana:	0x002020a0: 0x00000000 -> 0x00001111, write size 2
RIU Register write - miuana:	0x002020a4: 0x00000000 -> 0x00000000, write size 2
RIU Register write - miuana:	0x002020d8: 0x00000000 -> 0x00000808, write size 2
RIU Register write - miuana:	0x002020dc: 0x00000000 -> 0x00000808, write size 2
RIU Register write - miuana:	0x002020e8: 0x00000000 -> 0x00000404, write size 2
RIU Register write - miuana:	0x002020ec: 0x00000000 -> 0x00000404, write size 2
RIU Register write - miuana:	0x00202128: 0x00000000 -> 0x00001516, write size 2
RIU Register write - miuana:	0x00202140: 0x00000000 -> 0x0000bcdc, write size 2
RIU Register write - miuana:	0x00202144: 0x00000000 -> 0x0000cddc, write size 2
RIU Register write - miuana:	0x00202148: 0x00000000 -> 0x00003232, write size 2
RIU Register write - miuana:	0x0020214c: 0x00000000 -> 0x00004311, write size 2
RIU Register write - miuana:	0x00202150: 0x00000000 -> 0x00001111, write size 2
RIU Register write - miuana:	0x00202154: 0x00000000 -> 0x00001111, write size 2
RIU Register write - miuana:	0x00202158: 0x00000000 -> 0x00001111, write size 2
RIU Register write - miuana:	0x0020215c: 0x00000000 -> 0x00001111, write size 2
RIU Register write - miuana:	0x0020216c: 0x00000000 -> 0x00000000, write size 2
RIU Register write - miuana:	0x00202170: 0x00000000 -> 0x00001111, write size 2
RIU Register write - miuana:	0x00202174: 0x00000000 -> 0x00000111, write size 2
RIU Register write - miuana:	0x00202178: 0x00000000 -> 0x00000111, write size 2
RIU Register write - miuana:	0x0020217c: 0x00000000 -> 0x00000111, write size 2
RIU Register write - miuana:	0x002021a0: 0x00000000 -> 0x00004444, write size 2
RIU Register write - miuana:	0x002021a4: 0x00000000 -> 0x00004444, write size 2
RIU Register write - miuana:	0x002021a8: 0x00000000 -> 0x00004444, write size 2
RIU Register write - miuana:	0x002021ac: 0x00000000 -> 0x00004444, write size 2
RIU Register write - miuana:	0x002021b0: 0x00000000 -> 0x00000044, write size 2
RIU Register write - miuana:	0x002021c0: 0x00000000 -> 0x00005555, write size 2
RIU Register write - miuana:	0x002021c4: 0x00000000 -> 0x00005555, write size 2
RIU Register write - miuana:	0x002021c8: 0x00000000 -> 0x00005555, write size 2
RIU Register write - miuana:	0x002021cc: 0x00000000 -> 0x00005555, write size 2
RIU Register write - miuana:	0x002021d0: 0x00000000 -> 0x00000055, write size 2
RIU Register write - miuana:	0x002020c4: 0x00000000 -> 0x0000007f, write size 2
RIU Register write - miuana:	0x002020c8: 0x00000000 -> 0x0000f000, write size 2
RIU Register write - miuana:	0x002020c0: 0x00000000 -> 0x000000cb, write size 2
RIU Register write - miuana:	0x002020c0: 0x00000000 -> 0x000000cf, write size 2
RIU Register write - miuana:	0x002020c0: 0x00000000 -> 0x000000cb, write size 2
RIU Register write - miuana:	0x002020c0: 0x00000000 -> 0x000000c3, write size 2
RIU Register write - miuana:	0x002020c0: 0x00000000 -> 0x000000cb, write size 2
RIU Register write - miuana:	0x002020c0: 0x00000000 -> 0x000000c3, write size 2
RIU Register write - miuana:	0x002020c0: 0x00000000 -> 0x000000cb, write size 2
RIU Register write - miuana:	0x002020c0: 0x00000000 -> 0x000000c2, write size 2
RIU Register write - miuana:	0x002020c0: 0x00000000 -> 0x000000c0, write size 2
RIU Register write - miuana:	0x002020c0: 0x00000000 -> 0x000033c8, write size 2
RIU Register write - miuana:	0x002020e0: 0x00000000 -> 0x00000000, write size 2
RIU Register write - miuana:	0x00202130: 0x00000000 -> 0x00000000, write size 2
RIU Register write - miuana:	0x00202134: 0x00000000 -> 0x00000000, write size 2
RIU Register write - miuana:	0x00202120: 0x00000000 -> 0x0000f0f1, write size 2
RIU Register write - miuana:	0x002020e0: 0x00000000 -> 0x00000800, write size 2
```

```
RIU Register write - miudig:	0x00202458: 0x00000000 -> 0x00008021, write size 2
RIU Register write - miudig:	0x002025f8: 0x00000000 -> 0x0000951a, write size 2
RIU Register write - miudig:	0x002024a4: 0x00000000 -> 0x0000ffff, write size 2
RIU Register write - miudig:	0x002024e4: 0x00000000 -> 0x0000ffff, write size 2
RIU Register write - miudig:	0x00202524: 0x00000000 -> 0x0000ffff, write size 2
RIU Register write - miudig:	0x00202564: 0x00000000 -> 0x00000000, write size 2
RIU Register write - miudig:	0x00202224: 0x00000000 -> 0x0000ffff, write size 2
RIU Register write - miudig:	0x00202264: 0x00000000 -> 0x0000ffff, write size 2
RIU Register write - miudig:	0x00202480: 0x00000000 -> 0x00008015, write size 2
RIU Register write - miudig:	0x002024c0: 0x00000000 -> 0x00008015, write size 2
RIU Register write - miudig:	0x00202500: 0x00000000 -> 0x00008015, write size 2
RIU Register write - miudig:	0x00202540: 0x00000000 -> 0x00008015, write size 2
RIU Register write - miudig:	0x00202200: 0x00000000 -> 0x00008015, write size 2
RIU Register write - miudig:	0x00202240: 0x00000000 -> 0x00008015, write size 2
```

```
RIU Register write - miuana:	0x00202114: 0x00000000 -> 0x00000001, write size 2
RIU Register write - miuana:	0x002020e0: 0x00000000 -> 0x00000800, write size 2
RIU Register write - miuana:	0x002020b0: 0x00000000 -> 0x00000a0a, write size 2
RIU Register write - miuana:	0x002020b4: 0x00000000 -> 0x0000aaaa, write size 2
RIU Register write - miuana:	0x002020b8: 0x00000000 -> 0x0000aaaa, write size 2
RIU Register write - miuana:	0x002020bc: 0x00000000 -> 0x0000aaaa, write size 2
RIU Register write - miuana:	0x00202034: 0x00000000 -> 0x00008000, write size 2
RIU Register write - miuana:	0x00202038: 0x00000000 -> 0x00000020, write size 2
RIU Register write - miuana:	0x00202010: 0x00000000 -> 0x0000003f, write size 2
RIU Register write - miuana:	0x0020203c: 0x00000000 -> 0x00000005, write size 2
RIU Register write - miuana:	0x0020203c: 0x00000000 -> 0x0000000f, write size 2
RIU Register write - miuana:	0x0020203c: 0x00000000 -> 0x00000005, write size 2
```

```
RIU Register write - miudig:	0x0020243c: 0x00000000 -> 0x00008c01, write size 2
RIU Register write - miudig:	0x0020243c: 0x00000000 -> 0x00008c00, write size 2
```

Release MIU dig reset

```
RIU Register write - miuana:	0x00202000: 0x00000000 -> 0x00002010, write size 2
RIU Register write - miuana:	0x00202000: 0x00000000 -> 0x00000000, write size 2
RIU Register write - miuana:	0x00202030: 0x00000000 -> 0x00000000, write size 2
RIU Register write - miuana:	0x002020f8: 0x00000000 -> 0x00000000, write size 2
RIU Register write - miuana:	0x002020a8: 0x00000000 -> 0x00004000, write size 2
RIU Register write - miuana:	0x0020203c: 0x00000000 -> 0x00000005, write size 2
RIU Register write - miuana:	0x0020203c: 0x00000000 -> 0x0000000f, write size 2
RIU Register write - miuana:	0x0020203c: 0x00000000 -> 0x00000005, write size 2
RIU Register write - miuana:	0x00202000: 0x00000000 -> 0x00000001, write size 2
```

```
RIU Register write - miudig:	0x00202400: 0x00000000 -> 0x00000000, write size 2
RIU Register write - miudig:	0x00202400: 0x00000000 -> 0x00000008, write size 2
RIU Register write - miudig:	0x00202400: 0x00000000 -> 0x0000000c, write size 2
RIU Register write - miudig:	0x00202400: 0x00000000 -> 0x0000000e, write size 2
RIU Register write - miudig:	0x00202400: 0x00000000 -> 0x0000000f, write size 2
```

```
RIU Register write - miuana:	0x0020203c: 0x00000000 -> 0x00000005, write size 2
RIU Register write - miuana:	0x0020203c: 0x00000000 -> 0x0000000f, write size 2
RIU Register write - miuana:	0x0020203c: 0x00000000 -> 0x00000005, write size 2
```

```
RIU Register write - miudig:	0x0020248c: 0x00000000 -> 0x00007ffe, write size 2
RIU Register write - miudig:	0x002023cc: 0x00000000 -> 0x0000fffa, write size 2
RIU Register write - miudig:	0x002025fc: 0x00000000 -> 0x0000a0e1, write size 2
RIU Register write - miudig:	0x002025fc: 0x00000000 -> 0x000080e1, write size 2
RIU Register write - miudig:	0x002025e0: 0x00000000 -> 0x00000000, write size 2
RIU Register read - efuse:	0x0000400c = 0x00000000, size 2
RIU Register write - efuse:	0x0000400c: 0x00000000 -> 0x00000000, write size 2
RIU Register read - efuse:	0x0000402c = 0x00000000, size 2
RIU Register read - efuse:	0x00004024 = 0x00000000, size 2
RIU Register read - efuse:	0x0000402c = 0x00000000, size 2
RIU Register read - miuana:	0x00202064 = 0x00000029, size 2 - 0x19 - ddfset
RIU Register read - miuana:	0x00202060 = 0x00008000, size 2 - 0x18 - ddfset
RIU Register read - miudig:	0x00202404 = 0x00000000, size 2 
```

```
UART TX: miupll_200MHz
RIU Register write - miupll:	0x00206208: 0x00000000 -> 0x00000000, write size 1
RIU Register write - miupll:	0x00206209: 0x00000000 -> 0x00000000, write size 1
RIU Register write - miupll:	0x0020620c: 0x00000000 -> 0x00000019, write size 1
RIU Register write - miupll:	0x0020620d: 0x00000000 -> 0x00000100, write size 1
RIU Register write - miupll:	0x00206210: 0x00000000 -> 0x00000010, write size 1
RIU Register write - miupll:	0x00206211: 0x00000000 -> 0x00000000, write size 1
RIU Register write - miupll:	0x00206205: 0x00000000 -> 0x00000000, write size 1
```

```
RIU Register write - miudig:	0x00202480: 0x00000000 -> 0x00000015, write size 1
RIU Register write - miudig:	0x00202481: 0x00000000 -> 0x00008000, write size 1
RIU Register write - miudig:	0x00202484: 0x00000000 -> 0x00000008, write size 1
RIU Register write - miudig:	0x00202485: 0x00000000 -> 0x00002000, write size 1
RIU Register write - miudig:	0x00202488: 0x00000000 -> 0x00000000, write size 1
RIU Register write - miudig:	0x00202489: 0x00000000 -> 0x00000400, write size 1
RIU Register write - miudig:	0x00202490: 0x00000000 -> 0x000000ff, write size 1
RIU Register write - miudig:	0x00202491: 0x00000000 -> 0x0000ff00, write size 1
RIU Register write - miudig:	0x00202494: 0x00000000 -> 0x00000010, write size 1
RIU Register write - miudig:	0x00202495: 0x00000000 -> 0x00003200, write size 1
RIU Register write - miudig:	0x00202498: 0x00000000 -> 0x00000054, write size 1
RIU Register write - miudig:	0x00202499: 0x00000000 -> 0x00007600, write size 1
RIU Register write - miudig:	0x0020249c: 0x00000000 -> 0x00000098, write size 1
RIU Register write - miudig:	0x0020249d: 0x00000000 -> 0x0000ba00, write size 1
RIU Register write - miudig:	0x002024a0: 0x00000000 -> 0x000000dc, write size 1
RIU Register write - miudig:	0x002024a1: 0x00000000 -> 0x0000fe00, write size 1
RIU Register write - miudig:	0x002024b8: 0x00000000 -> 0x00000000, write size 1
RIU Register write - miudig:	0x002024b9: 0x00000000 -> 0x00000000, write size 1
RIU Register write - miudig:	0x002024c0: 0x00000000 -> 0x00000015, write size 1
RIU Register write - miudig:	0x002024c1: 0x00000000 -> 0x00008000, write size 1
RIU Register write - miudig:	0x002024c4: 0x00000000 -> 0x00000008, write size 1
RIU Register write - miudig:	0x002024c5: 0x00000000 -> 0x00002000, write size 1
RIU Register write - miudig:	0x002024c8: 0x00000000 -> 0x00000000, write size 1
RIU Register write - miudig:	0x002024c9: 0x00000000 -> 0x00000400, write size 1
RIU Register write - miudig:	0x002024d0: 0x00000000 -> 0x000000ff, write size 1
RIU Register write - miudig:	0x002024d1: 0x00000000 -> 0x0000ff00, write size 1
RIU Register write - miudig:	0x002024d4: 0x00000000 -> 0x00000010, write size 1
RIU Register write - miudig:	0x002024d5: 0x00000000 -> 0x00003200, write size 1
RIU Register write - miudig:	0x002024d8: 0x00000000 -> 0x00000054, write size 1
RIU Register write - miudig:	0x002024d9: 0x00000000 -> 0x00007600, write size 1
RIU Register write - miudig:	0x002024dc: 0x00000000 -> 0x00000098, write size 1
RIU Register write - miudig:	0x002024dd: 0x00000000 -> 0x0000ba00, write size 1
RIU Register write - miudig:	0x002024e0: 0x00000000 -> 0x000000dc, write size 1
RIU Register write - miudig:	0x002024e1: 0x00000000 -> 0x0000fe00, write size 1
RIU Register write - miudig:	0x00202500: 0x00000000 -> 0x00000015, write size 1
RIU Register write - miudig:	0x00202501: 0x00000000 -> 0x00008000, write size 1
RIU Register write - miudig:	0x00202504: 0x00000000 -> 0x00000008, write size 1
RIU Register write - miudig:	0x00202505: 0x00000000 -> 0x00002000, write size 1
RIU Register write - miudig:	0x00202508: 0x00000000 -> 0x00000000, write size 1
RIU Register write - miudig:	0x00202509: 0x00000000 -> 0x00000400, write size 1
RIU Register write - miudig:	0x00202510: 0x00000000 -> 0x000000ff, write size 1
RIU Register write - miudig:	0x00202511: 0x00000000 -> 0x0000ff00, write size 1
RIU Register write - miudig:	0x00202514: 0x00000000 -> 0x00000010, write size 1
RIU Register write - miudig:	0x00202515: 0x00000000 -> 0x00003200, write size 1
RIU Register write - miudig:	0x00202518: 0x00000000 -> 0x00000054, write size 1
RIU Register write - miudig:	0x00202519: 0x00000000 -> 0x00007600, write size 1
RIU Register write - miudig:	0x0020251c: 0x00000000 -> 0x00000098, write size 1
RIU Register write - miudig:	0x0020251d: 0x00000000 -> 0x0000ba00, write size 1
RIU Register write - miudig:	0x00202520: 0x00000000 -> 0x000000dc, write size 1
RIU Register write - miudig:	0x00202521: 0x00000000 -> 0x0000fe00, write size 1
RIU Register write - miudig:	0x00202540: 0x00000000 -> 0x00000015, write size 1
RIU Register write - miudig:	0x00202541: 0x00000000 -> 0x00008000, write size 1
RIU Register write - miudig:	0x00202544: 0x00000000 -> 0x00000008, write size 1
RIU Register write - miudig:	0x00202545: 0x00000000 -> 0x00002000, write size 1
RIU Register write - miudig:	0x00202548: 0x00000000 -> 0x00000000, write size 1
RIU Register write - miudig:	0x00202549: 0x00000000 -> 0x00000400, write size 1
RIU Register write - miudig:	0x00202550: 0x00000000 -> 0x000000ff, write size 1
RIU Register write - miudig:	0x00202551: 0x00000000 -> 0x0000ff00, write size 1
RIU Register write - miudig:	0x00202554: 0x00000000 -> 0x00000010, write size 1
RIU Register write - miudig:	0x00202555: 0x00000000 -> 0x00003200, write size 1
RIU Register write - miudig:	0x00202558: 0x00000000 -> 0x00000054, write size 1
RIU Register write - miudig:	0x00202559: 0x00000000 -> 0x00007600, write size 1
RIU Register write - miudig:	0x0020255c: 0x00000000 -> 0x00000098, write size 1
RIU Register write - miudig:	0x0020255d: 0x00000000 -> 0x0000ba00, write size 1
RIU Register write - miudig:	0x00202560: 0x00000000 -> 0x000000dc, write size 1
RIU Register write - miudig:	0x00202561: 0x00000000 -> 0x0000fe00, write size 1
RIU Register write - miudig:	0x002025fc: 0x00000000 -> 0x000000e1, write size 1
RIU Register write - miudig:	0x002025fd: 0x00000000 -> 0x00008000, write size 1
RIU Register write - miudig:	0x002023c0: 0x00000000 -> 0x00000002, write size 1
RIU Register write - miudig:	0x002023c1: 0x00000000 -> 0x00000000, write size 1
RIU Register write - miudig:	0x002023c4: 0x00000000 -> 0x0000001e, write size 1
RIU Register write - miudig:	0x002023c5: 0x00000000 -> 0x00000000, write size 1
RIU Register write - miudig:	0x002023d0: 0x00000000 -> 0x00000018, write size 1
RIU Register write - miudig:	0x002023d1: 0x00000000 -> 0x00000000, write size 1
RIU Register write - miudig:	0x002023d4: 0x00000000 -> 0x00000008, write size 1
RIU Register write - miudig:	0x002023d5: 0x00000000 -> 0x00004000, write size 1
RIU Register write - miudig:	0x002023d8: 0x00000000 -> 0x00000002, write size 1
RIU Register write - miudig:	0x002023d9: 0x00000000 -> 0x00000200, write size 1
RIU Register write - miudig:	0x002023f0: 0x00000000 -> 0x000000e1, write size 1
RIU Register write - miudig:	0x002023f1: 0x00000000 -> 0x0000ff00, write size 1
```

```
RIU Register read - clkgen:	0x0020705c = 0x00000000, size 1
RIU Register write - clkgen:	0x0020705c: 0x00000000 -> 0x00000000, write size 1
RIU Register write - clkgen:	0x0020705c: 0x00000000 -> 0x00000008, write size 1
RIU Register read - clkgen:	0x0020705c = 0x00000000, size 1
RIU Register write - clkgen:	0x0020705c: 0x00000000 -> 0x00000010, write size 1
RIU Register write - clkgen:	0x00207080: 0x00000000 -> 0x00000004, write size 1
```

- MIU clock
- MIU boot clock

```
RIU Register unhandled write:	0x002041f0 -> 0x00000001, write size 1
RIU Register write - l3bridge:	0x00204404: 0x00000000 -> 0x00000084, write size 1
mcu_req_max_miu0: 84
```

```
RIU Register write - clkgen:	0x002070c4: 0x00000000 -> 0x00000000, write size 1
RIU Register write - clkgen:	0x00207180: 0x00000000 -> 0x00000010, write size 1
```

- 0xc4 - UART0 clock
- 0x180 - BDMA

```
RIU Register write - pmsleep:	0x00001c81: 0x00000000 -> 0x00001000, write size 1
RIU Register read - pmsleep:	0x00001c81 = 0x00000000, size 1
RIU Register write - pmsleep:	0x00001c81: 0x00000000 -> 0x00004000, write size 1
UART TX: SPI 54M
```

```
RIU Register write - clkgen:	0x002070c8: 0x00000000 -> 0x00000010, write size 1
RIU Register read - clkgen:	0x002070c8 = 0x00000000, size 1
RIU Register write - clkgen:	0x002070c8: 0x00000000 -> 0x00000020, write size 1
RIU Register unhandled write:	0x00002fc8 -> 0x00000001, write size 1
RIU Register write - clkgen:	0x002071c4: 0x00000000 -> 0x00000003, write size 1
RIU Register write - clkgen:	0x002071c5: 0x00000000 -> 0x00000000, write size 1
RIU Register write - clkgen:	0x00207184: 0x00000000 -> 0x00000004, write size 1
RIU Register write - clkgen:	0x00207184: 0x00000000 -> 0x00000014, write size 1
```

- 0xc8 - SPI
- 0x1c4/1c5 - pll gates
- 0x184 - ISP

```
RIU Register write - miudig:	0x0020248c: 0x00000000 -> 0x00000000, write size 2
RIU Register write - miudig:	0x002024cc: 0x00000000 -> 0x00000000, write size 2
RIU Register write - miudig:	0x0020250c: 0x00000000 -> 0x00000000, write size 2
RIU Register write - miudig:	0x0020254c: 0x00000000 -> 0x00000000, write size 2
RIU Register write - miudig:	0x0020224c: 0x00000000 -> 0x00000000, write size 2
RIU Register write - miudig:	0x002023cc: 0x00000000 -> 0x00000000, write size 2
RIU Register write - miudig:	0x0020243c: 0x00000000 -> 0x00008c08, write size 2
RIU Register read - efuse:	0x0000400c = 0x00000000, size 2
RIU Register write - efuse:	0x0000400c: 0x00000000 -> 0x00000000, write size 2
RIU Register read - efuse:	0x00004010 = 0x00000000, size 2
RIU Register read - efuse:	0x00004014 = 0x00000000, size 2
RIU Register read - efuse:	0x0000400c = 0x00000000, size 2
RIU Register write - efuse:	0x0000400c: 0x00000000 -> 0x00000000, write size 2
RIU Register read - efuse:	0x00004020 = 0x00000000, size 2
RIU Register read - efuse:	0x00004024 = 0x00000000, size 2
RIU Register read - efuse:	0x0000400c = 0x00000000, size 2
RIU Register write - efuse:	0x0000400c: 0x00000000 -> 0x00000000, write size 2
RIU Register read - efuse:	0x00004028 = 0x00000000, size 2
RIU Register read - efuse:	0x0000402c = 0x00000000, size 2
RIU Register read - efuse:	0x0000400c = 0x00000000, size 2
RIU Register write - efuse:	0x0000400c: 0x00000000 -> 0x00000100, write size 2
RIU Register read - efuse:	0x00004060 = 0x00000000, size 2
RIU Register read - efuse:	0x00004064 = 0x00000000, size 2
RIU Register read - efuse:	0x0000400c = 0x00000000, size 2
RIU Register write - efuse:	0x0000400c: 0x00000000 -> 0x00000100, write size 2
RIU Register read - efuse:	0x00004068 = 0x00000000, size 2
RIU Register read - efuse:	0x0000406c = 0x00000000, size 2
RIU Register read - efuse:	0x0000400c = 0x00000000, size 2
RIU Register write - efuse:	0x0000400c: 0x00000000 -> 0x00000100, write size 2
RIU Register read - efuse:	0x00004070 = 0x00000000, size 2
RIU Register read - efuse:	0x00004074 = 0x00000000, size 2
Memory read: 0x00000000 = 0x00000000
Memory write: 0x00000000 -> 0x11111111
MstarEmu.java> Finished!
```
