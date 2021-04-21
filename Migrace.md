# Migrace z CC2531 na cc2652P / CC2538 a jiny Texas Instruments chip
Navod sem prevzal z https://github.com/zigpy/zigpy-znp/blob/dev/TOOLS.md a tim jak jde vyvoj rychle dopredu, tak muze byt rychle neaktualni, takze pokud narazite na problem, tak kouknete na puvodni stranku v anglictine.

### Windows 10
Stahnete si posledni verzi Python 3 https://www.python.org/downloads/

Pokud se vam muj dongle nezobrazuje ve spravci zarizeni (Device manager), budete muset doinstalovat driver https://learn.sparkfun.com/tutorials/how-to-install-ch340-drivers/all#windows-710 <br><br>
Po pripojeni by se mel jmenovat takhle<br>
![image](https://user-images.githubusercontent.com/46757804/115614716-4f393f00-a2ee-11eb-81b0-cf51ebec7d00.png)<br>
*Cislo COM portu si poznamenejte.*


Pokud jeste nepouzivate [Windows Terminal](https://www.microsoft.com/en-us/p/windows-terminal/9n0dx20hk701?activetab=pivot:overviewtab) tak muzete pouzit PowerShell nebo prikazovou radku (cmd.exe).

### Vytvoreni virtualniho prostredi
Vytvorte a aktivujte virtualni prostredi.
```console
> py -3 -m venv venv
> venv\Scripts\activate.ps1  # for PowerShell
> venv\Scripts\activate.bat  # for cmd.exe
```
### Instalace zigpy-znp
Je potreba nainstalovat DEV branch projektu, protoze network backup je porad v BETA verzi.
```
pip install https://github.com/zigpy/zigpy-znp/archive/dev.tar.gz
```
Pokud narazite jako ja na chybu **Command "python setup.py egg_info" failed with error code 1 in ...** tak si aktualizujte PIP<br>
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
