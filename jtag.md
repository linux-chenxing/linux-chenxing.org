# jtag

## MSC313

```
(gdb) monitor cortex_a cache_info
L1 I-Cache: linelen 32, associativity 2, nsets 256, cachesize 16 KBytes
L1 D-Cache: linelen 64, associativity 4, nsets 64, cachesize 16 KBytes
L2 D-Cache: linelen 64, associativity 8, nsets 256, cachesize 128 KBytes
```

### ROM table 

```
(gdb) monitor dap info
AP ID register 0x24770002
        Type is MEM-AP APB
MEM-AP BASE 0x80000000
        ROM table in legacy format
                Component base address 0x80000000
                Peripheral ID 0x0801020304
                Designer ASCII code 0x20, <unknown>
                Part is 0x304, Unrecognized 
                Component class is 0x1, ROM table
                MEMTYPE system memory not present: dedicated debug bus
        ROMTABLE[0x0] = 0x100003
                Component base address 0x80100000
                Peripheral ID 0x04000bb4a7
                Designer is 0x4bb, ARM Ltd
                Part is 0x4a7, Unrecognized 
                Component class is 0x1, ROM table
                MEMTYPE system memory not present: dedicated debug bus
        [L01] ROMTABLE[0x0] = 0x10003
                Component base address 0x80110000
                Peripheral ID 0x04005bbc07
                Designer is 0x4bb, ARM Ltd
                Part is 0xc07, Cortex-A7 Debug (Debug Unit)
                Component class is 0x9, CoreSight component
                Type is 0x15, Debug Logic, Processor
        [L01] ROMTABLE[0x4] = 0x11003
                Component base address 0x80111000
                Peripheral ID 0x04005bb9a7
                Designer is 0x4bb, ARM Ltd
                Part is 0x9a7, Cortex-A7 PMU (Performance Monitor Unit)
                Component class is 0x9, CoreSight component
                Type is 0x16, Performance Monitor, Processor
        [L01] ROMTABLE[0x8] = 0x12002
                Component not present
        [L01] ROMTABLE[0xc] = 0x13002
                Component not present
        [L01] ROMTABLE[0x10] = 0x14002
                Component not present
        [L01] ROMTABLE[0x14] = 0x15002
                Component not present
        [L01] ROMTABLE[0x18] = 0x16002
                Component not present
        [L01] ROMTABLE[0x1c] = 0x17002
                Component not present
        [L01] ROMTABLE[0x20] = 0x18002
                Component not present
        [L01] ROMTABLE[0x24] = 0x19002
                Component not present
        [L01] ROMTABLE[0x28] = 0x1a002
                Component not present
        [L01] ROMTABLE[0x2c] = 0x1b002
                Component not present
        [L01] ROMTABLE[0x30] = 0x1c002
                Component not present
        [L01] ROMTABLE[0x34] = 0x1d002
                Component not present
        [L01] ROMTABLE[0x38] = 0x1e002
                Component not present
        [L01] ROMTABLE[0x3c] = 0x1f002
                Component not present
        [L01] ROMTABLE[0x40] = 0x0
        [L01]   End of ROM table
        ROMTABLE[0x4] = 0x0
                End of ROM table

(gdb) 
```

## MSC313E

### Cache info

```
(gdb) monitor cortex_a cache_info
L1 I-Cache: linelen 32, associativity 2, nsets 256, cachesize 16 KBytes
L1 D-Cache: linelen 64, associativity 4, nsets 64, cachesize 16 KBytes
L2 D-Cache: linelen 64, associativity 8, nsets 256, cachesize 128 KBytes
```

### ROM table

```
> dap info
AP ID register 0x24770002
        Type is MEM-AP APB
MEM-AP BASE 0x80000000
        ROM table in legacy format
                Component base address 0x80000000
                Peripheral ID 0x0801020304
                Designer ASCII code 0x20, <unknown>
                Part is 0x304, Unrecognized 
                Component class is 0x1, ROM table
                MEMTYPE system memory not present: dedicated debug bus
        ROMTABLE[0x0] = 0x100003
                Component base address 0x80100000
                Peripheral ID 0x04000bb4a7
                Designer is 0x4bb, ARM Ltd
                Part is 0x4a7, Unrecognized 
                Component class is 0x1, ROM table
                MEMTYPE system memory not present: dedicated debug bus
        [L01] ROMTABLE[0x0] = 0x10003
                Component base address 0x80110000
                Peripheral ID 0x04005bbc07
                Designer is 0x4bb, ARM Ltd
                Part is 0xc07, Cortex-A7 Debug (Debug Unit)
                Component class is 0x9, CoreSight component
                Type is 0x15, Debug Logic, Processor
        [L01] ROMTABLE[0x4] = 0x11003
                Component base address 0x80111000
                Peripheral ID 0x04005bb9a7
                Designer is 0x4bb, ARM Ltd
                Part is 0x9a7, Cortex-A7 PMU (Performance Monitor Unit)
                Component class is 0x9, CoreSight component
                Type is 0x16, Performance Monitor, Processor
        [L01] ROMTABLE[0x8] = 0x12002
                Component not present
        [L01] ROMTABLE[0xc] = 0x13002
                Component not present
        [L01] ROMTABLE[0x10] = 0x14002
                Component not present
        [L01] ROMTABLE[0x14] = 0x15002
                Component not present
        [L01] ROMTABLE[0x18] = 0x16002
                Component not present
        [L01] ROMTABLE[0x1c] = 0x17002
                Component not present
        [L01] ROMTABLE[0x20] = 0x18002
                Component not present
        [L01] ROMTABLE[0x24] = 0x19002
                Component not present
        [L01] ROMTABLE[0x28] = 0x1a002
                Component not present
        [L01] ROMTABLE[0x2c] = 0x1b002
                Component not present
        [L01] ROMTABLE[0x30] = 0x1c002
                Component not present
        [L01] ROMTABLE[0x34] = 0x1d002
                Component not present
        [L01] ROMTABLE[0x38] = 0x1e002
                Component not present
        [L01] ROMTABLE[0x3c] = 0x1f002
                Component not present
        [L01] ROMTABLE[0x40] = 0x0
        [L01]   End of ROM table
        ROMTABLE[0x4] = 0x0
                End of ROM table
```

## SSD20xD

### FUART (mode 1)

#### Enable in kernel:

```
devmem 0x1f203c3c 16 1
```

#### Enable in u-boot:

```
mw.w 0x1f203c3c 1
```


### Cache info

```
(gdb) monitor cortex_a cache_info
L1 I-Cache: linelen 32, associativity 2, nsets 512, cachesize 32 KBytes
L1 D-Cache: linelen 64, associativity 4, nsets 128, cachesize 32 KBytes
L2 D-Cache: linelen 64, associativity 8, nsets 512, cachesize 256 KBytes
```

### ROM table

```
AP ID register 0x24770002
        Type is MEM-AP APB
MEM-AP BASE 0x80000000
        ROM table in legacy format
                Component base address 0x80000000
                Peripheral ID 0x0801020304
                Designer ASCII code 0x20, <unknown>
                Part is 0x304, Unrecognized 
                Component class is 0x1, ROM table
                MEMTYPE system memory not present: dedicated debug bus
        ROMTABLE[0x0] = 0x100003
                Component base address 0x80100000
                Peripheral ID 0x04000bb4a7
                Designer is 0x4bb, ARM Ltd
                Part is 0x4a7, Unrecognized 
                Component class is 0x1, ROM table
                MEMTYPE system memory not present: dedicated debug bus
        [L01] ROMTABLE[0x0] = 0x10003
                Component base address 0x80110000
                Peripheral ID 0x04005bbc07
                Designer is 0x4bb, ARM Ltd
                Part is 0xc07, Cortex-A7 Debug (Debug Unit)
                Component class is 0x9, CoreSight component
                Type is 0x15, Debug Logic, Processor
        [L01] ROMTABLE[0x4] = 0x11003
                Component base address 0x80111000
                Peripheral ID 0x04005bb9a7
                Designer is 0x4bb, ARM Ltd
                Part is 0x9a7, Cortex-A7 PMU (Performance Monitor Unit)
                Component class is 0x9, CoreSight component
                Type is 0x16, Performance Monitor, Processor
        [L01] ROMTABLE[0x8] = 0x12003
                Component base address 0x80112000
                Peripheral ID 0x04005bbc07
                Designer is 0x4bb, ARM Ltd
                Part is 0xc07, Cortex-A7 Debug (Debug Unit)
                Component class is 0x9, CoreSight component
                Type is 0x15, Debug Logic, Processor
        [L01] ROMTABLE[0xc] = 0x13003
                Component base address 0x80113000
                Peripheral ID 0x04005bb9a7
                Designer is 0x4bb, ARM Ltd
                Part is 0x9a7, Cortex-A7 PMU (Performance Monitor Unit)
                Component class is 0x9, CoreSight component
                Type is 0x16, Performance Monitor, Processor
        [L01] ROMTABLE[0x10] = 0x14002
                Component not present
        [L01] ROMTABLE[0x14] = 0x15002
                Component not present
        [L01] ROMTABLE[0x18] = 0x16002
                Component not present
        [L01] ROMTABLE[0x1c] = 0x17002
                Component not present
        [L01] ROMTABLE[0x20] = 0x18002
                Component not present
        [L01] ROMTABLE[0x24] = 0x19002
                Component not present
        [L01] ROMTABLE[0x28] = 0x1a002
                Component not present
        [L01] ROMTABLE[0x2c] = 0x1b002
                Component not present
        [L01] ROMTABLE[0x30] = 0x1c002
                Component not present
        [L01] ROMTABLE[0x34] = 0x1d002
                Component not present
        [L01] ROMTABLE[0x38] = 0x1e002
                Component not present
        [L01] ROMTABLE[0x3c] = 0x1f002
                Component not present
        [L01] ROMTABLE[0x40] = 0x0
        [L01]   End of ROM table
        ROMTABLE[0x4] = 0x0
                End of ROM table

(gdb) 
```

## SSD210

```
> dap info                    
AP ID register 0x24770002
        Type is MEM-AP APB2 or APB3
MEM-AP BASE 0x80000000
        ROM table in legacy format
                Component base address 0x80000000
                Peripheral ID 0x0801020304
                Designer ASCII code 0x20, <unknown>
                Part is 0x304, Unrecognized 
                Component class is 0x1, ROM table
                MEMTYPE system memory not present: dedicated debug bus
        ROMTABLE[0x0] = 0x100003
                Component base address 0x80100000
                Peripheral ID 0x04000bb4a7
                Designer is 0x23b, ARM Ltd
                Part is 0x4a7, Unrecognized 
                Component class is 0x1, ROM table
                MEMTYPE system memory not present: dedicated debug bus
        [L01] ROMTABLE[0x0] = 0x10003
                Component base address 0x80110000
                Peripheral ID 0x04005bbc07
                Designer is 0x23b, ARM Ltd
                Part is 0xc07, Cortex-A7 Debug (Debug Unit)
                Component class is 0x9, CoreSight component
                Type is 0x15, Debug Logic, Processor
        [L01] ROMTABLE[0x4] = 0x11003
                Component base address 0x80111000
                Peripheral ID 0x04005bb9a7
                Designer is 0x23b, ARM Ltd
                Part is 0x9a7, Cortex-A7 PMU (Performance Monitor Unit)
                Component class is 0x9, CoreSight component
                Type is 0x16, Performance Monitor, Processor
        [L01] ROMTABLE[0x8] = 0x12003
                Component base address 0x80112000
                Peripheral ID 0x04005bbc07
                Designer is 0x23b, ARM Ltd
                Part is 0xc07, Cortex-A7 Debug (Debug Unit)
                Component class is 0x9, CoreSight component
                Type is 0x15, Debug Logic, Processor
        [L01] ROMTABLE[0xc] = 0x13003
                Component base address 0x80113000
                Peripheral ID 0x04005bb9a7
                Designer is 0x23b, ARM Ltd
                Part is 0x9a7, Cortex-A7 PMU (Performance Monitor Unit)
                Component class is 0x9, CoreSight component
                Type is 0x16, Performance Monitor, Processor
        [L01] ROMTABLE[0x10] = 0x14002
                Component not present
        [L01] ROMTABLE[0x14] = 0x15002
                Component not present
        [L01] ROMTABLE[0x18] = 0x16002
                Component not present
        [L01] ROMTABLE[0x1c] = 0x17002
                Component not present
        [L01] ROMTABLE[0x20] = 0x18002
                Component not present
        [L01] ROMTABLE[0x24] = 0x19002
                Component not present
        [L01] ROMTABLE[0x28] = 0x1a002
                Component not present
        [L01] ROMTABLE[0x2c] = 0x1b002
                Component not present
        [L01] ROMTABLE[0x30] = 0x1c002
                Component not present
        [L01] ROMTABLE[0x34] = 0x1d002
                Component not present
        [L01] ROMTABLE[0x38] = 0x1e002
                Component not present
        [L01] ROMTABLE[0x3c] = 0x1f002
                Component not present
        [L01] ROMTABLE[0x40] = 0x0
        [L01]   End of ROM table
        ROMTABLE[0x4] = 0x0
                End of ROM table

> 
```
