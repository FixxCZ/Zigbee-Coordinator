# Migrace z CC2531 na cc2652P / CC2538 a jiny Texas Instruments chip
Navod sem prevzal z https://github.com/zigpy/zigpy-znp/blob/dev/TOOLS.md a tim jak jde vyvoj rychle dopredu, tak muze byt rychle neaktualni, takze pokud narazite na problem, tak kouknete na puvodni stranku v anglictine.

### Windows 10
Stahnete si posledni verzi Python 3 https://www.python.org/downloads/

Budete mozna potrebovat If you are using a zzh! or any other device with a CH340 USB-serial adapter, you may have
to install a driver before the COM port is recognized. SparkFun Electronics has a detailed
guide on how to do this here: https://learn.sparkfun.com/tutorials/how-to-install-ch340-drivers/all#windows-710 .

Device Manager will tell you the radio's assigned `COM` port.

If you are not already using the [Windows Terminal](https://www.microsoft.com/en-us/p/windows-terminal/9n0dx20hk701?activetab=pivot:overviewtab) by Microsoft, I suggest you try it. Otherwise, open a PowerShell or Command Prompt window.

The Windows `py` launcher will be used in place of `python` in all subsequent commands
so instead of running this:

```console
> python -m zigpy_znp.tools.foo
```

Run this:

```console
> py -3 -m zigpy_znp.tools.foo
```
