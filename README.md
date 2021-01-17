## Rozdeleni koordinatoru
#### Starsi generace:
- **CC2530**: 2.4GHz Zigbee a IEEE 802.15.4 wireless MCU. Intel 8051 core, 256kB Flash, ma jenom 8kB RAM. Vyzaduje externi programator pro nahrani firmware.<br>
- **CC2531**: Stejny jako CC2530 ale ma vestavene USB. Pouziva se v rozsirenych levnych Zigbee koordinatorech. Intel 8051 core, 256 Flash, ma jen 8kB RAM. Vyzaduje externi programator pro nahrani firmware.

#### Soucasna generace:
- **CC2538**: 2.4GHz Zigbee, 6LoWPAN, a IEEE 802.15.4 wireless MCU. ARM Cortex-M3 core s 512kB Flash a 32kB RAM.<br>
- **CC2538 + CC2592**: Stejny jako CC2538, ale doplneny o zesilovac CC2592. Zesileni vysilani na 22dBm a zlepseni prijimani o 3dB. [Viz. datasheet.](https://www.ti.com/lit/ds/symlink/cc2592.pdf?ts=1610831220971 "Viz. data sheet.")

#### Nejnovejsi generace:
- **CC2652R**: Podporuje vicero protokolu na 2.4GHz jako treba (Zigbee, Bluetooth, Thread, ...). Cortex-M0 pro radiovou cast a Cortex-M4F pro aplikacni cast a 80kB RAM. Vysilaci vykon 5 dBm.  Tento chip je pouzity v koordinatoru Electrolama zzh!.<br>
- **CC2652P**: Chipset CC2652R s vestavenym zesilovacem. Neni zpetne kompatibilni s CC2652R/CC2652RB. Vysilaci vykon 20 dBm<br>

*Zdroj informaci [https://electrolama.com/projects/zig-a-zig-ah/](https://electrolama.com/projects/zig-a-zig-ah/ "Zdroj") + TI data sheets*
## Podporovany firmware:
<table>
  <tr>
    <td><b>Z-Stack</b></td>
    <td><b>Device</b></td>
    <td><b>Zigbee</b></td>
    <td><b>Direct children</b></td>
    <td><b>Routes</b></td>
    <td><b>Notes</b></td>
  </tr>
  <tr>
    <td rowspan="2">Z-Stack_Home_1.2 (default)</td>
    <td>CC2531</td>
    <td>1.2 HA</td>
    <td>20</td>
    <td>30/0</td>
    <td></td>
  </tr>
  <tr>
  </tr>
  <tr>
    <td>Z-Stack_Home_1.2 (source_routing)</td>
    <td>CC2531</td>
    <td>1.2 HA</td>
    <td>5</td>
    <td>40/40</td>
    <td></td>
  </tr>
  <tr>
    <td rowspan="3">Z-Stack_3.0.x</td>
    <td>CC2531</td>
    <td>3.0</td>
    <td>15</td>
    <td>40/0</td>
    <td>
      - <a href="https://github.com/Koenkk/zigbee2mqtt/issues/1445">Discussion #1445</a>
      - Max 40 Zigbee 3.0 devices
    </td>
  </tr>
  <tr>
  </tr>
    <tr>
    <td>CC2538 + CC2592</td>
    <td>3.0</td>
    <td>100</td>
    <td>200/400</td>
    <td>
      - <a href="https://github.com/Koenkk/zigbee2mqtt/issues/1568">Discussion #1568</a>
      - Max 200 Zigbee 3.0 devices
    </td>
  </tr>
  <tr>
    <td rowspan="2">Z-Stack_3.x.0</td>
    <td>CC2652R,CC2652RB, CC2652P</td>
    <td>3.0</td>
    <td>50</td>
    <td>100/200</td>
    <td>
      - <a href="https://github.com/Koenkk/zigbee2mqtt/issues/1429">Discussion #1429</a>
      - Max 200 Zigbee 3.0 devices
    </td>
  </tr>
</table>

###### Vysvetlivky:
**Direct children:** Pocet zarizeni, ktere se mohou pripojit primo na koordinatora. Neni to maximalni pocet zarizeni v siti, ale po dosazeni tohoto poctu zarizeni musite do site pridat aspon jeden router, aby mohla sit rust dal. Router je vetsinou kazdy prvek, ktery je trvale zapojeny do elektriny, jako je treba zasuvka, zarovka, ale zaleri na konkretnim vyrobci.<br>
**Routes:** Pocet cest "routes" ktere muze koordinator drzet v pameti. Napriklad 100/200 znamena, ze koordinator zvladne 100 normalnich a 200 source routes.  Source routes zlepsuji celkovou odezvu a vykon vetsich siti se 40+ zarizenimi.<br>
*Zdroj: [https://github.com/Koenkk/Z-Stack-firmware/tree/master/coordinator](https://github.com/Koenkk/Z-Stack-firmware/tree/master/coordinator "https://github.com/Koenkk/Z-Stack-firmware/tree/master/coordinator")*
