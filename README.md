[Aktuální novinky zde](https://github.com/FixxCZ/Zigbee-Coordinator/blob/main/novinky.md)

## Jak si vybrat
#### RPi Shield vs. USB verze
Wifi a Bluetooth(BT) vysílají na stejné frekvenci jako Zigbee, takže pokud používáte na vaší Raspberry Pie(RPi) jedno z toho a potřebujete Zigbee signálem pokrýt co nejvetší oblast tak volte variantu USB a připojte ji 0.5m USB prodlužovacím kabelem k RPi.<br>
Pokud máte RPi připojenou LAN kabelem a BT ani Wifi nepoužíváte, vypněte je v nastavení a s klidem zvolte variantu RPi shieldu, budete mít vše v jedné krabičce. <br>
Uživatelé RPi 4 si musí dát pozor na to jestli nepoužívají USB 3.0 zařízení (typicky disk) pripojený do USB 3.0 portu (modré porty)<br>
![USB3](/img/usb3-blue.jpg)
![USB3](/img/USB3.png)


## Rozdělení koordinátorů
#### Starší generace:
- **CC2530**: 2.4GHz Zigbee a IEEE 802.15.4 wireless MCU. Intel 8051 core, 256kB Flash, má jenom 8kB RAM. Vyžaduje externí programátor pro nahrání firmware.
- **CC2531**: Stejný jako CC2530 ale má vestavěné USB. Používá se v rozšířených levných Zigbee koordinátorech. Intel 8051 core, 256 Flash, má jen 8kB RAM. Vyžaduje externí programátor pro nahrání firmware.

#### Současná generace:
- **CC2538**: 2.4GHz Zigbee, 6LoWPAN, a IEEE 802.15.4 wireless MCU. ARM Cortex-M3 core s 512kB Flash a 32kB RAM.
- **CC2538 + CC2592**: Stejný jako CC2538, ale doplněný o zesilovač CC2592. Zesílení vysílání na 22dBm a zlepšení příjmu o 3dB. [Viz. data sheet.](https://www.ti.com/lit/ds/symlink/cc2592.pdf?ts=1610831220971 "Viz. data sheet.")

#### Nejnovější generace:
- **CC2652R**: Podporuje vícero protokolů na 2.4GHz jako třeba (Zigbee, Bluetooth, Thread, ...). Cortex-M0 pro rádiovou část a Cortex-M4F pro aplikační část a 80kB RAM. Vysílací výkon 5 dBm. Tento chip je použitý v coordinatoru Electrolama zzh!.
- **CC2652RB**: Identický jako CC2652R, ale nevyžaduje externí krystal. Používá ho slaesh's CC2652RB stick.
- **CC2652P**: Chipset CC2652R s vestavěným zesilovačem. Vysílací výkon 20 dBm. Bude v budoucnu použitý v Electrolama zzh-p.<br>
*Zdroj informací [https://electrolama.com/projects/zig-a-zig-ah/](https://electrolama.com/projects/zig-a-zig-ah/ "Zdroj") + TI data sheets*
## Podporovaný firmware:
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
    <td>Z-Stack_Home_1.2 (default)</td>
    <td>CC2531</td>
    <td>1.2 HA</td>
    <td>20</td>
    <td>30/0</td>
    <td></td>
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

###### Vysvětlivky:
**Direct children:** Počet zařízení, které se mohou připojit přímo na koordinátora. Není to maximální počet zařízení v síti, ale po dosažení tohoto počtu zařízení musíte do sítě přidat aspoň jeden router, aby mohla sít růst dál. Router je většinou každý prvek, který je trvale zapojený do elektřiny, jako je třeba zásuvka, žárovka, ale záleží na konkrétním výrobci.<br>
**Routes:** Počet cest "routes" které může koordinátor držet v paměti. Například 100/200 znamená, že koordinátor zvládne 100 normálních a 200 source routes. Source routes zlepšují celkovou odezvu a výkon větších sítí s 40+ zařízeními.<br>
*Zdroj: [https://github.com/Koenkk/Z-Stack-firmware/tree/master/coordinator](https://github.com/Koenkk/Z-Stack-firmware/tree/master/coordinator "https://github.com/Koenkk/Z-Stack-firmware/tree/master/coordinator")*

