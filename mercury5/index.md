# Mercury 5

The mercury 5 family seems to be targetted at dash recorders. So far all of the devices that have been obtained have been running something that seems to be based on uC/OSII and not Linux.

The mercury 5 seems to be very close to the [infinity3](/infinity3).

# Specs

- Probably a 800MHz Cortex A7 (Main ID register is 0x410fc075, confirms cortex A7)
- 32KB Boot ROM
- 128KB SRAM (based on where the boot rom sets the stack pointer)

## Chips

### SSC8336N

#### Boot ROM Tag

This is slighly interesting. Presumably I3 is infinity3 so maybe this chip's ROM is a hacked up. 

```
MVX1##I3gb83f2cbCMN_ROM######XVM
```

#### Known Devices 

- 70mai Smart dash cam [vendor page](https://www.70mai.com/en/70mai-dash-cam-lite/?gclid=EAIaIQobChMIzsLkl6y_5QIVEz5gCh1UOg9eEAAYASAAEgLvffD_BwE) [fcc.io internal photos](https://fccid.io/2AOK9-MIDRIVED08/Internal-Photos/internal-photos-4351132)

### SSC8339D
