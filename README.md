## Rozdeleni coordinatoru
#### Podle chipsetu
#### Starsi generace:
**CC2530**: 2.4GHz Zigbee a IEEE 802.15.4 wireless MCU. Intel 8051 core, 256kB Flash, ma jenom 8kB RAM. Vyzaduje externi programator pro nahrani firmware.
**CC2531**: Stejny jako CC2530 ale ma vestavene USB. Pouziva se v rozsirenych levnych Zigbee coordinatorech. Intel 8051 core, 256 Flash, ma jen 8kB RAM. Vyzaduje externi programator pro nahrani firmware.

#### Soucasna generace:
**CC2538**: 2.4GHz Zigbee, 6LoWPAN, a IEEE 802.15.4 wireless MCU. ARM Cortex-M3 core s 512kB Flash a 32kB RAM.
**CC2538 + CC2592**: Stejny jako CC2538, ale doplneny o zesilovac CC2592. Zesileni vysilani na 22dBm a zlepseni prijimani o 3dB. [Viz. datasheet.](https://www.ti.com/lit/ds/symlink/cc2592.pdf?ts=1610831220971 "Viz. data sheet.")

#### Nejnovejsi generace:
**CC2652R**: Podporuje vicero protokolu na 2.4GHz jako treba (Zigbee, Bluetooth, Thread, ...). Cortex-M0 pro radiovou cast a Cortex-M4F pro aplikacni cast a 80kB RAM. Vysilaci vykon 5 dBm.  Tento chip je pouzity v coordinatoru Electrolama zzh!.
**CC2652P**: Chipset CC2652R s vestavenym zesilovacem. Neni zpetne kompatibilni s CC2652R/CC2652RB. Vysilaci vykon 20 dBm
Zdroj informaci [https://electrolama.com/projects/zig-a-zig-ah/](https://electrolama.com/projects/zig-a-zig-ah/ "Zdroj") + TI data sheets
