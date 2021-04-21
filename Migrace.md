# Migrace z CC2531 na cc2652P / CC2538 a jiny Texas Instruments chip
Navod sem prevzal z https://github.com/zigpy/zigpy-znp/blob/dev/TOOLS.md a tim jak jde vyvoj rychle dopredu, tak muze byt rychle neaktualni, takze pokud narazite na problem, tak kouknete na puvodni stranku v anglictine.

### Windows 10
Stahnete si posledni verzi Python 3 https://www.python.org/downloads/

Pokud se vam muj dongle nezobrazuje ve spravci zarizeni (Device manager), budete muset doinstalovat driver https://learn.sparkfun.com/tutorials/how-to-install-ch340-drivers/all#windows-710
Po pripojeni by se mel jmenovat takhle<br>
![image](https://user-images.githubusercontent.com/46757804/115614716-4f393f00-a2ee-11eb-81b0-cf51ebec7d00.png)
Cislo COM portu si poznamenejte.


Pokud jeste nepouzivate [Windows Terminal](https://www.microsoft.com/en-us/p/windows-terminal/9n0dx20hk701?activetab=pivot:overviewtab) tak muzete pouzit PowerShell nebo prikazovou radku (cmd.exe).

The Windows `py` launcher will be used in place of `python` in all subsequent commands
so instead of running this:

```console
> python -m zigpy_znp.tools.foo
```


Run this:

```console
> py -3 -m zigpy_znp.tools.foo
```
