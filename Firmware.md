# Flashovani firmware CC2652P a CC2538
Pro nahrani nejnovejiho FW doprucuju oficialni TI nastroj SmartRF Flash Programmer 2, po registraci zdarma na stazeni zde https://www.ti.com/tool/FLASH-PROGRAMMER <br><br>
Koordinator FW pro CC2652P je zde:<br>
https://github.com/egony/cc2652p_E72-2G4M20S1E/tree/master/firmware/coordinator <br>

Router FW pro CC2652P neni custom a pouziva se standardni od Koenkk, tim padem neni zesilovac aktivni. Na router je lepsi pouzit CC2538.<br>
https://github.com/Koenkk/Z-Stack-firmware/tree/master/router/Z-Stack_3.x.0/bin<br>

Koordinator FW pro CC2538 zde<br>
https://github.com/jethome-ru/zigbee-firmware/tree/master/ti/coordinator/cc2538_cc2592 <br>

Router firmware pro CC2538<br>
https://github.com/jethome-ru/zigbee-firmware/tree/master/ti/router/cc2538_cc2592 <br>



### Postup
1. Stahnete si FW a otevrte SmartRF Flash Programmer 2.
2. Pripojte dongle, v Programmeru vam musi pribyt nova polozka<br>
![image](https://user-images.githubusercontent.com/46757804/116809294-88b74900-ab3d-11eb-9db1-26fa0fc103ad.png)<br>
V pripade, ze se neobjevi, doprucuju nainstalovat CH340 driver https://sparks.gogo.co.nz/ch340.html
3. Kliknete na Unknown radek u polozky USB-SERIAL CH340 a dole vyberte CC2652P a nebo CC2538xF53 podle toho jaky stick flashujete.<br>
![image](https://user-images.githubusercontent.com/46757804/116809382-08ddae80-ab3e-11eb-852a-e2017a036182.png)
4. Nastavte si Programmer podle tohoto obrazku<br>![image](https://user-images.githubusercontent.com/46757804/116809418-3a567a00-ab3e-11eb-962c-49d037e7d5fb.png)





Pokud se vam muj dongle nezobrazuje ve spravci zarizeni (Device manager), budete muset doinstalovat driver https://learn.sparkfun.com/tutorials/how-to-install-ch340-drivers/all#windows-710 <br><br>
Po pripojeni by se mel jmenovat takhle<br>
![image](https://user-images.githubusercontent.com/46757804/115614716-4f393f00-a2ee-11eb-81b0-cf51ebec7d00.png)<br>
*Cislo COM portu si poznamenejte.*


Pokud jeste nepouzivate [Windows Terminal](https://www.microsoft.com/en-us/p/windows-terminal/9n0dx20hk701?activetab=pivot:overviewtab) tak muzete pouzit PowerShell nebo prikazovou radku (cmd.exe).

### Vytvoreni virtualniho prostredi
Vytvorte a aktivujte virtualni prostredi.
```console
py -3 -m venv venv
venv\Scripts\activate.ps1  # for PowerShell
venv\Scripts\activate.bat  # for cmd.exe
```
### Instalace zigpy-znp
Je potreba nainstalovat DEV branch projektu, protoze network backup je porad v BETA verzi.
```
pip install https://github.com/zigpy/zigpy-znp/archive/dev.tar.gz
```
Pokud narazite jako ja na chybu **Command "python setup.py egg_info" failed with error code 1 in ...** tak si aktualizujte PIP a zkuste to znovu.<br>
*python -m pip install --upgrade pip*

## Backup and restore
Prvni do PC pripojte puvodni stick treba CC2531, v device manageru si zjistete cislo COM portu. Pokud si nejste jisty ktery to je, tak ho odpojte a znovu pripojte, pritom sledujte ktera polozka zmizi a zase se objevi.<br>
V mem pripade to je COM21, takze zadam prikaz:
```console
python -m zigpy_znp.tools.network_backup COM21 -o network_backup.json
```
Vytvori se soubor network_backup.json kde je zaloha cele site v plain textu.<br>
<br>
Pak pripojime novy stick treba CC2652 a zjistime si COM port, v mem pripade trea COM8. Takze spustim:
```console
python -m zigpy_znp.tools.network_restore COM8 -i network_backup.json
```
Mame hotovo.<br>
Tento postup lze pouzit i na backup pred upgradem Firmware zgbee sticku.

