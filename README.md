[Aktuální novinky zde](https://github.com/FixxCZ/Zigbee-Coordinator/blob/main/novinky.md)

#### Update: 21.5.2021 - Aktualne neni zadny kus skladem, pocitam tak 2 tydny nez prijde dalsi varka dilu. 
### Co nabízím
Na základě kladných ohlasů na [FB](https://www.facebook.com/groups/2232679967058877/permalink/2843937365933131) vyrábím Zigbee koordinátory podle designu popsaného Jagerem na [modkam.ru](https://modkam.ru/) a jejich clonech od Egony. Aktuálně je na výběr mezi CC2538 se zesilovacem CC2592 a mezi CC2652P, obojí jak USB tak RPi, za cenu 700Kč včetně dopravy po ČR Českou Poštou v bublinkové obálce. Na Slovensko zasílám pomocí www.zasielkovna.sk tam celková cena vychází na 30€. Můžu přidat i vytištěnou krabičku za 20Kč.<br>
Všechny modely mají externí anténu a jsou flashnuté pro práci se Zigbee2MQTT, na přání můžu flashnout i router firmware.<br>
**Pro objednání mi napište na zigbee(zavináč)seznam.cz**<br>
![Varianty](/img/varianty.png)<br>
*Všechny varianty, pořadí tak jak na fotce: CC2652P USB, CC2652P RPI shield, CC2538 RPI shield, CC2538 USB*
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
- **CC2652R**: Nová generace čipu od Texas Instruments pro pásmo 2,4GHz. Cortex-M0 pro rádiovou část a Cortex-M4F pro aplikační část a 80kB RAM. Vysílací výkon 5 dBm. Tento chip je použitý v coordinatoru Electrolama zzh!.
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

**Je lepší CC2538+CC2592 nebo CC2652P?**<br>
CC2652P vede na poli výpočetního výkonu, CPU má 48MHz a disponuje 80KB+8KB SRAM, CC2538 má 32MHz a 32KB SRAM. Pro porovnání CC2531 ma takt CPU 12MHz a 8KB SRAM.<br>
Co se týče vysílacího a přijímacího výkonu, tak příjem je stejný, ale vysílací výkon má CC2538 díky zesilovači CC2592 o pár decibel lepší, CC2652P má zase plíškem odstíněný čip už těsne za anténou a i konektor antény je pájená napřímo.<br>


## Jak si nastavit nový koordinátor v Zigbee2MQTT
Pokud přecházíte z jiného koordinátoru s čipem Texas Instruments, jako je třeba CC2531, tak je nově možné zmigrovat celé nastaceni sítě a vyhnout se nutnosti párování všech zařízení, více na https://github.com/FixxCZ/Zigbee-Coordinator/blob/main/Migrace.md <br><br>
Pro nastavení RPI verze [začněte tady](https://github.com/FixxCZ/Zigbee-Coordinator/blob/main/readme_pi_shield.txt) s USB verzí můžete číst dál.<br>
K vaší už existující konfiguraci je nutné přidat několik parametrů.<br>
Změna nastavení portu - buď přímo na RPi můžete spustit příkaz **ls -l /dev/serial/by-id/** nebo v Home Assistant v menu Supervisor > System > v okýnku Host jsou tři tečky a tam je Hardware.<br>
Výsledek by měl vypadat nějak takhle:
```
pi@raspberrypi:~ $ ls -l /dev/serial/by-id/
lrwxrwxrwx 1 root root 13 Feb  7 18:45 usb-1a86_USB_Serial-if00-port0 -> ../../ttyUSB0
```
Do configurace doplňku Zigbee2MQTT tedy napíšeme tohle:
```
serial:
  port: /dev/serial/by-id/usb-1a86_USB_Serial-if00-port0

advanced:
  baudrate: 115200  #tahle položka je nutná protože používáme UART převodník viz. níže
  rtscts: false  #tahle funkce je vypnutá protože řízení toku vyžaduje jiný FW a nefunguje dobře na RPi
  pan_id: 6752 #Pokud používáte pan_id musíte nastavit hodnotu i jedna vyšší než máte nyní. Takže pokud máte pan_id: 6752 tak dáte pan_id: 6753

experimental:
  transmit_power: 20  #toto funguje jen pro CC2652P kde je možné výkon řídit. 20 je maximum, dostupné hodnoty jsou -20, -18, -15, -12, -10, -9, -6, -5, -3, 0, 1..5, 14..20
```
Na desce je přítomný UART převodník CH340, aby bylo možné nahrávat nový FW bez nutnosti dalšího HW (J-Link), z toho důvodu se koordinátor nehlásí jako třeba usb-Texas_Instruments_TI_CC2538_USB, ale jako usb-1a86_USB_Serial-if00-port0.<br><br>
**Nově není nutné přepárovat všechna zařízení při přechodu třeba z CC2531, objevil se nový nástroj od zigpy na migraci mezi Texas instruments čipy. Zkoušel sem ho a můžu potvrdit že funguje. Stačí pomocí Network backup (beta) stáhnout data z CC2531 a nahrát je do CC2538/CC2652. Postup je zde https://github.com/zigpy/zigpy-znp/blob/dev/TOOLS.md#network-backup-beta**<br><br>
Doporučuju si zapnout i nový Zigbee2MQTT frontend:
```
frontend:
  port: 8485
experimental:
  new_api: true  #tahle hodnota je aktuálně nutná jen pokud bežíte na Home Assitant. Stand alone instalace Zigbee2MQTT ji nevyžaduje.
``` 
Port 8485 potřebujete pokud máte Home Assitant v Dockeru, jinak můžete použí výchozí port 8080. Samozřejmě za předpokladu, že nepoužíváte SOCAT. Rozhraní pak poběží na stejné adrese jako Home Assistant jen na portu 8485 a ne 8123. Přídání do sidebaru mě nefunguje, ale třeba se vám zadaří.<br>
<br>
Pokud máte problém napárovat zařízení co vám předtím fungovalo, přesunte se co nejblíže koordinátoru a přesvedčte se, že baterie nemá méně než 20%. Zařízení se slabou baterií se odmítají párovat.<br>


### LED diody
Funce LED diod je daná firmware nahraným v koordinatoru, takže pokud si tam nahrajete jiný, můžou ukazovat něco jiného.<br>
**CC2538** <br>
LED1 (zelená) Power LED.<br>
LED2 (žlutá) Zatím nevyužitá.<br>
LED3 (modrá) Bliká když je povoleno párování nových zařízení (permit_join: true).<br>
LED4 (červená) Problikává když probíha datový přenos.<br>
<br>
**CC2652P** <br>
LED1 (zelená) svítí pokud se nepoužívá vestavěný zesilovač (vysílací výkon je mezi -20 až 5 dBm)<br>
LED2 (červená) svítí pokud se využívá vestavěný zesilovač (vysílací výkon je mezi 15 až 20 dBm)<br>

### Krabičky - 3D Tisk
![3D](/img/3D_pouzdra.png)<br>
CC2538 - https://www.thingiverse.com/thing:4437685 Soubory **bottom_usb_ant.STL** a **top_ant.STL**. Vyzkoušeno a pasuje pěkně.<br>
CC2652P - https://www.thingiverse.com/thing:4695634 Vrchní díl je někdy trošku volnějsí, osvedčilo se mi ho zvetšit na délku ve sliceru na 100.64% takže na rovných 47 mm.<br>

### Flashovani firmware CC2652P a CC2538
Dongly jsou vybaveny UART prevodnikem, takze na jejich flashovani neni potreba zadny dalsi hardware. Postup je popsan zde: https://github.com/FixxCZ/Zigbee-Coordinator/blob/main/Firmware.md

### Co s původním nevyužitým CC2531? Přece router!

Pokud vám po upgradu zůstal nevyužitý koordinátor CC2531 a máte CC debuger, můžete do nej flashnout router firmware [CC2531-router.hex (ptvo.info)](https://ptvo.info/cc2531-based-router-firmware-136/) a pokrýt třeba oblast se slabším signálem. Pokud CC debuger nevlastníte, je několik [alternativních metod](https://www.zigbee2mqtt.io/information/alternative_flashing_methods.html) jak do něj nahrát FW.
