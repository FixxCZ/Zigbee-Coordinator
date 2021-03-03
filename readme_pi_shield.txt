

====================================
Raspberry Pi, Raspbian:
====================================

https://www.raspberrypi.org/documentation/configuration/uart.md

Zapnuti UART:
pomocí
nano /boot/config.txt

přidat řádek
enable_uart=1

Pak pustit raspi-config
sudo raspi-config

V nabidce vybrat polozku cislo 3
3 Interfacing Options Configure connections to peripherals, 

pak polozku 
P6 - Serial Port

na otazku:
Would you like a login shell to be accessible over serial?
Odpovedet "No"

nasledujici otazku:
Would you like the serial port hardware to be enabled?
odpovedet "Yes"

Restartovat Raspberry

Shield se bude hlasit bud na 
/dev/ttyAMA0
nebo 
/dev/ttyS0

Je vhodne vypnout Bluetooth a pokud to jde i WIFI kvuli ruseni.

================================
Orange Pi, Armbian:
================================

Na Armbianu je mozne jeste nainstalovat: 
sudo apt-get install python2.7


Orange Pi PC:
~~~~~~~~~~~~~
sudo nano /boot/armbianEnv.txt

pridat radek
overlays=uart3

restartovat 

ls -l /dev/ttyS3

v konfiguraci zigbee2mqtt upravte port na
/dev/ttyS3


Orange Pi Zero:
~~~~~~~~~~~~~~~
sudo nano /boot/armbianEnv.txt

pridat radek
overlays=uart1

restartovat 

ls -l /dev/ttyS1

v konfiguraci zigbee2mqtt upravte port na
/dev/ttyS1



==============================
Flashovani
==============================
Pro CC2538:
Stahnete si UART firmware zde https://github.com/jethome-ru/zigbee-firmware/tree/master/ti/coordinator/cc2538_cc2592
JH_2538_2592_ZNP_UART_20201010.hex

Pro CC2652
Stahente FW tady https://66cdjufjndqt42tyvuaih7tihi--github-com.translate.goog/egony/cc2652p_E72-2G4M20S1E/tree/master/firmware/coordinator
znp_CC2652P_E72_sdk_4_40_00_44_20210211.hex

Instalace flashovaciho nastroje:

cd /opt
sudo wget https://github.com/1248/cc2538-prog/archive/master.zip
rozbalit
cd /opt/cc2538-prog-master
sudo make
nakopirujte do slozky stazeny firmware JH_2538_2592_ZNP_UART_20201010.hex nebo znp_CC2652P_E72_sdk_4_40_00_44_20210211.hex

Flashovani:

Zastavte zigbee2mqtt pokud bezi.

Zmacknete a drzte tlacitko FLASH, kratce zmacknete tlacitko RESET, pustte tlacitko FLASH.

cd /opt/cc2538-prog-master
Pro CC2538:
./cc2538-prog -d /dev/ttyS0 -f JH_2538_2592_ZNP_UART_20201010.hex
Pro CC2652
./cc2538-prog -d /dev/ttyS0 -f znp_CC2652P_E72_sdk_4_40_00_44_20210211.hex

kde /dev/ttyS0 je port na kterem vam stit bezi (nejpis /dev/ttyS0 nebo /dev/ttyAMA0)