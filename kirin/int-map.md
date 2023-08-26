# Kirin Interrupt map

## MIPS CPU intc

Eight interrupt lines are directly attached to the CPU, mediated by the IM0..7 bits in the `Status` register.[^1]

| line | description                                                    |
|------|----------------------------------------------------------------|
|  0   | software interrupt                                             |
|  1   | software interrupt                                             |
|  2   | non-PM interrupt controller 0 ([0xbf203340]), no EOI           |
|  3   | non-PM interrupt controller 1 (0xbf203300)                     |
|  4   |                                                                |
|  5   |                                                                |
|  6   |                                                                |
|  7   | timer interrupt                                                |

[^1]: MIPS® Architecture For Programmers Vol. III: MIPS32®/microMIPS32™ Privileged Resource Architecture, chapter 9.32 Status Register

[0xbf203340]: ../ip/intc.md#mips

## Non-PM intc 0

| line |        name        |    notes                                  |
|------|--------------------|-------------------------------------------|
|   0  | UART0              |                                           |
|   3  | MVD                |                                           |
|   9  | EMAC               |                                           |
|  10  | XC                 |                                           |
|  22  | HDMITX             |                                           |
|  25  | GPD                |                                           |
|  39  | SC                 |                                           |
|  45  | JPD                |                                           |

## Non-PM intc 1

| line |        name        |    notes                                  |
|------|--------------------|-------------------------------------------|
|   4  | MAILBOX            |                                           |
|  13  | MAILBOX            |                                           |
|  14  | AUDIO              |                                           |
|  24  | CIPHER             |                                           |
|  26  | XC                 |                                           |
|  27  | IR                 |                                           |
|  29  | AUDIO              |                                           |
|  37  | MAILBOX            |                                           |
|  38  | MAILBOX            |                                           |
