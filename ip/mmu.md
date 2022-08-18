# MMU

| offset | name              | 15 | 14 | 13 | 12 | 11 | 10 | 9 | 8 | 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 | notes  |
|--------|-------------------|----|----|----|----|----|----|---|---|---|---|---|---|---|---|---|---|--------|
| 0x0    |                   |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   |        |
| 0x44   |                   |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   | p3 ipl |
| 0x7c   |                   |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   | p3 ipl |
| 0x80   |                   |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   | p3 ipl |
| 0x84   |                   |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   | p3 ipl |
| 0x88   |                   |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   | p3 ipl |
| 0x8c   |                   |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   | p3 ipl |
| 0x90   |                   |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   | p3 ipl |
| 0x94   |                   |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   | p3 ipl |
| 0x98   |                   |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   | p3 ipl |
| 0x9c   |                   |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   | p3 ipl |
| 0xa0   |                   |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   | p3 ipl |
| 0xa4   |                   |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   | p3 ipl |
| 0xa8   |                   |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   | p3 ipl |
| 0x100  |                   |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   | p3 ipl |
| 0x10c  |                   |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   |        |
| 0x140  | CTRL              |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   |        |
| 0x144  | RW_ENTRY          |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   |        |
| 0x148  | W_DATA            |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   |        |
| 0x14c  | R_DATA            |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   |        |
| 0x150  | CLIENT_ID_0_1     |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   |        |
| 0x154  | CLIENT_ID_2_3     |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   |        |
| 0x158  | CLIENT_ID_4_5     |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   |        |
| 0x15c  | CLIENT_ID_6_7     |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   |        |
| 0x160  | CLIENT_ID_SEL     |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   |        |
| 0x164  | IRQ_CTRL          |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   |        |
| 0x168  | COLLISION_ENTRY   |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   |        |
| 0x16c  | ACCESS            |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   |        |
| 0x170  | INVALID_ENTRY     |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   |        |
| 0x174  | INVALID_CLIENT_ID |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   |        |
| 0x180  | PROTECT0_START    |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   |        |
| 0x184  | PROTECT0_END      |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   |        |
| 0x188  | PROTECT1_START    |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   |        |
| 0x18c  | PROTECT1_END      |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   |        |
| 0x190  | PROTECT2_START    |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   |        |
| 0x194  | PROTECT2_END      |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   |        |
| 0x198  | PROTECT3_START    |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   |        |
| 0x19c  | PROTECT3_END      |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   |        |
| 0x1BC  | PROTECT_STATUS    |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   |        |
| 0x1D4  | PROTECT_LOADDR    |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   |        |
| 0x1d8  | PROTECT_HIADDR    |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   |        |
| 0x1fc  |                   |    |    |    |    |    |    |   |   |   |   |   |   |   |   |   |   | p3 ipl |

## Dump from P3 before touching the registers

```
mmu dump
mmu dump: 0x1f202600 - 0x0000
mmu dump: 0x1f202604 - 0x0000
mmu dump: 0x1f202608 - 0x0000
mmu dump: 0x1f20260c - 0x0000
mmu dump: 0x1f202610 - 0x0000
mmu dump: 0x1f202614 - 0x0000
mmu dump: 0x1f202618 - 0x0000
mmu dump: 0x1f20261c - 0x0000
mmu dump: 0x1f202620 - 0x0000
mmu dump: 0x1f202624 - 0x0000
mmu dump: 0x1f202628 - 0x0000
mmu dump: 0x1f20262c - 0x0000
mmu dump: 0x1f202630 - 0x0000
mmu dump: 0x1f202634 - 0x0000
mmu dump: 0x1f202638 - 0x0000
mmu dump: 0x1f20263c - 0x0000
mmu dump: 0x1f202640 - 0x0000
mmu dump: 0x1f202644 - 0x0000
mmu dump: 0x1f202648 - 0x0000
mmu dump: 0x1f20264c - 0x0000
mmu dump: 0x1f202650 - 0x0000
mmu dump: 0x1f202654 - 0x0000
mmu dump: 0x1f202658 - 0x0000
mmu dump: 0x1f20265c - 0x0000
mmu dump: 0x1f202660 - 0x0000
mmu dump: 0x1f202664 - 0x0000
mmu dump: 0x1f202668 - 0x0000
mmu dump: 0x1f20266c - 0x0000
mmu dump: 0x1f202670 - 0x0000
mmu dump: 0x1f202674 - 0x0000
mmu dump: 0x1f202678 - 0x0000
mmu dump: 0x1f20267c - 0x0000
mmu dump: 0x1f202680 - 0x0303
mmu dump: 0x1f202684 - 0x0208
mmu dump: 0x1f202688 - 0x0c01
mmu dump: 0x1f20268c - 0x0601
mmu dump: 0x1f202690 - 0x0603
mmu dump: 0x1f202694 - 0x0301
mmu dump: 0x1f202698 - 0x0528
mmu dump: 0x1f20269c - 0x000e
mmu dump: 0x1f2026a0 - 0xe00e
mmu dump: 0x1f2026a4 - 0x0406
mmu dump: 0x1f2026a8 - 0x0302
mmu dump: 0x1f2026ac - 0x0004
mmu dump: 0x1f2026b0 - 0x0000
mmu dump: 0x1f2026b4 - 0x0000
mmu dump: 0x1f2026b8 - 0x0000
mmu dump: 0x1f2026bc - 0x0000
mmu dump: 0x1f2026c0 - 0x2010
mmu dump: 0x1f2026c4 - 0x0040
mmu dump: 0x1f2026c8 - 0x5555
mmu dump: 0x1f2026cc - 0x5555
mmu dump: 0x1f2026d0 - 0x2010
mmu dump: 0x1f2026d4 - 0x0040
mmu dump: 0x1f2026d8 - 0x5555
mmu dump: 0x1f2026dc - 0x5555
mmu dump: 0x1f2026e0 - 0x2010
mmu dump: 0x1f2026e4 - 0x0040
mmu dump: 0x1f2026e8 - 0x5555
mmu dump: 0x1f2026ec - 0x5555
mmu dump: 0x1f2026f0 - 0x0000
mmu dump: 0x1f2026f4 - 0x0000
mmu dump: 0x1f2026f8 - 0x0000
mmu dump: 0x1f2026fc - 0x0000
mmu dump: 0x1f202700 - 0x0010
mmu dump: 0x1f202704 - 0x0000
mmu dump: 0x1f202708 - 0x0000
mmu dump: 0x1f20270c - 0x0000
mmu dump: 0x1f202710 - 0x0000
mmu dump: 0x1f202714 - 0x0300
mmu dump: 0x1f202718 - 0x0000
mmu dump: 0x1f20271c - 0x0000
mmu dump: 0x1f202720 - 0x0000
mmu dump: 0x1f202724 - 0x0000
mmu dump: 0x1f202728 - 0x0000
mmu dump: 0x1f20272c - 0x0000
mmu dump: 0x1f202730 - 0x0000
mmu dump: 0x1f202734 - 0x0000
mmu dump: 0x1f202738 - 0x0000
mmu dump: 0x1f20273c - 0x0000
mmu dump: 0x1f202740 - 0x0020
mmu dump: 0x1f202744 - 0x0000
mmu dump: 0x1f202748 - 0x0000
mmu dump: 0x1f20274c - 0x0000
mmu dump: 0x1f202750 - 0x0000
mmu dump: 0x1f202754 - 0x0000
mmu dump: 0x1f202758 - 0x0000
mmu dump: 0x1f20275c - 0x0000
mmu dump: 0x1f202760 - 0x0000
mmu dump: 0x1f202764 - 0x0000
mmu dump: 0x1f202768 - 0x0000
mmu dump: 0x1f20276c - 0x0000
mmu dump: 0x1f202770 - 0x0000
mmu dump: 0x1f202774 - 0x0000
mmu dump: 0x1f202778 - 0x0000
mmu dump: 0x1f20277c - 0x0000
mmu dump: 0x1f202780 - 0x0000
mmu dump: 0x1f202784 - 0x0000
mmu dump: 0x1f202788 - 0x0000
mmu dump: 0x1f20278c - 0x0000
mmu dump: 0x1f202790 - 0x0000
mmu dump: 0x1f202794 - 0x0000
mmu dump: 0x1f202798 - 0x0000
mmu dump: 0x1f20279c - 0x0000
mmu dump: 0x1f2027a0 - 0x0000
mmu dump: 0x1f2027a4 - 0x0000
mmu dump: 0x1f2027a8 - 0x0000
mmu dump: 0x1f2027ac - 0x0000
mmu dump: 0x1f2027b0 - 0x0000
mmu dump: 0x1f2027b4 - 0x0000
mmu dump: 0x1f2027b8 - 0x0000
mmu dump: 0x1f2027bc - 0x0000
mmu dump: 0x1f2027c0 - 0x0000
mmu dump: 0x1f2027c4 - 0x0000
mmu dump: 0x1f2027c8 - 0x0000
mmu dump: 0x1f2027cc - 0x0000
mmu dump: 0x1f2027d0 - 0x0000
mmu dump: 0x1f2027d4 - 0x0000
mmu dump: 0x1f2027d8 - 0x0000
mmu dump: 0x1f2027dc - 0x0000
mmu dump: 0x1f2027e0 - 0x0000
mmu dump: 0x1f2027e4 - 0x0000
mmu dump: 0x1f2027e8 - 0x0000
mmu dump: 0x1f2027ec - 0x0000
mmu dump: 0x1f2027f0 - 0x0000
mmu dump: 0x1f2027f4 - 0x0000
mmu dump: 0x1f2027f8 - 0x0000
mmu dump: 0x1f2027fc - 0x0000
```
