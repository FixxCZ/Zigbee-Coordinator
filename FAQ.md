## Jak si nastavit Zigbee2MQTT na nový koordinátor
K vaší už existující konfiguraci je nutné přidat několik parametrů.<br>
Nastavení portu - bud prímo na RPi můžete spustit príkaz **ls -l /dev/serial/by-id/** nebo v Home Assistant v menu Supervisor > System > v okýnku Host jsou tři tečky a tam je Hardware.<br>
Výsledek by měl vypadat nějak takhle:
```
pi@raspberrypi:~ $ ls -l /dev/serial/by-id/
lrwxrwxrwx 1 root root 13 Feb  7 18:45 usb-1a86_USB_Serial-if00-port0 -> ../../ttyUSB0
```
Do configurace tedy napíšeme tohle:
```
serial:
  port: /dev/serial/by-id/usb-1a86_USB_Serial-if00-port0

advanced:
  baudrate: 115200  #tahle položka je nutná protože používáme UART převodník viz. níže
  rtscts: false  #tahle funkce je vypnutá protože řízení toku vyžaduje jiný FW a nefunguje dobře na RPi

experimental:
  transmit_power: 20  #toto funguje jen pro CC2652P kde je možné výkon řídit. 20 je maximum, dostupné hodnoty jsou -20, -18, -15, -12, -10, -9, -6, -5, -3, 0, 1..5, 14..20
```
Na desce je přítomný UART převodník CH340, aby bylo možné nahrávat nový FW bez nutnosti dalšího HW (J-Link), z toho důvodu se koordinátor nehlásí jako třeba usb-Texas_Instruments_TI_CC2538_USB, ale jako usb-1a86_USB_Serial-if00-port0.<br>
Doporučuju si zapnout i nový Zigbee2MQTT frontend:
```
frontend:
  port: 8485
experimental:
  new_api: true  #tahle hodnota je aktuálně nutná jen pokud bežíte na Home Assitant. Stand alone instalace Zigbee2MQTT ji nevyžaduje.
``` 
Port 8485 potřebujete pokud máte Home Assitant v Dockeru, jinak můžete použí výchozí port 8080. Samozřejmě za předpokladu že nepoužíváte SOCAT. Rozhraní pak poběží na stejné adrese jako Home Assistant jen na portu 8485 a ne 8123. Přídání do sidebaru mě nefunguje, ale třeba se vám zadaří.
#### CC2652P




**Je lepší CC2538+CC2592 nebo CC2652P?**<br>
CC2652P vede na poli výpočetního výkonu, CPU má 48MHz a disponuje 80KB+8KB SRAM, CC2538 má 32MHz a 32KB SRAM. Pro porovnání CC2531 ma takt CPU 12MHz a 8KB SRAM.<br>
Co se týče vysílacího a přijímacího výkonu, tak příjem je stejný, ale vysílací výkon má CC2538 díky zesilovači CC2592 o pár decibel lepší.

proc ma deska tak malo soucastek

co se starym cc2531
