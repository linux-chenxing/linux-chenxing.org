# AEON R2

The AEON R2 is a modified version of [OpenRISC](or1k.md),
which basically has a different instruction format (using variable 16/24/32-bit instruction width),
as well as some custom additions to the ISA (like the cache management instructions).

## Some tools

- [Reko](https://github.com/uxmal/reko), which has some support for AEON R2
- Ghidra [processor module](https://github.com/shinyquagsire23/ghidra-aeon), allegedly based off the Reko findings.

## Instructions

Note: the listing below is dated and partially incorrect. Right now it's kept there only for historical reasons.

```
000000000000000000000000                l.nop
000010DddddAaaaa00000001                l.lhz                 rD, 0(rA)
000011BbbbbAaaaa00000000                l.sw                  0(rA), rB
000111DddddAaaaaKkkkkkkk                l.addi                rD, rA, K
00100000Nnnnnnnnnnnnnnnn                l.bf                  N
001101100000000000000001                l.movhi               r1, ???
010001DddddAaaaaBbbbb100                l.and                 rD, rA, rB
010100AaaaaBbbbbKkkkkkkk                l.ori                 rA, rB, K
010111AaaaaIiiii00000001                l.sfeqi               rA, I
010111AaaaaBbbbb00001101                l.sfne                rA, rB
010111BbbbbAaaaa00010111                l.sfgeu               rA, rB
100100Nnnnnnnnnnnnnnnnnn                l.j                   N

... TODO ...

110000DddddKkkkkkkkkkkkkkkkk0001        l.movhi               rD, K
110000BbbbbAaaaaKkkkkkkkkkkk1101        l.mtspr               rA, rB, K
110000DddddAaaaaKkkkkkkkkkkk1111        l.mfspr               rD, rA, K
110001DddddAaaaaKkkkkkkkkkkkkkkk        l.andi                rD, rA, K
110010DddddAaaaaKkkkkkkkkkkkkkkk        l.ori                 rD, rA, K
111010Nnnnnnnnnnnnnnnnnnnnnnnnnn        l.j                   N
111011BbbbbAaaaaIiiiiiiiiiiiiiii        l.sw                  I(rA), rB
11110100000Aaaaa00000000000J0001        l.invalidate_line     0(rA), J    ***1
111111DddddAaaaaKkkkkkkkkkkkkkkk        l.addi                rA, rB, K
```
