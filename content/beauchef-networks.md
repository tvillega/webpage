+++
title = "Beauchef Networks"
date = "2023-03-06"
[taxonomies]
tags = ["linux","network"]
+++

There are several networks available with their respective guides, but some programs require setting the configurations by hand on a text file.

This is a small documentation of my findings, in the event I need them again.

---

## iwd - iNet Wireless Daemon

From the [Arch Wiki](https://wiki.archlinux.org/title/Iwd): *The core goal of the project is to optimize resource utilization by not depending on any external libraries and instead utilizing features provided by the Linux Kernel to the maximum extent possible.*

To change between networks while inside a Window Manager or Desktop Environment, the program [iwgtk](https://github.com/J-Lentz/iwgtk) is a good companion. However, this program **does not allow to configure** network connections, it only reads the content of `/var/lib/iwd`

### Configuration file template for `DCCAIR`

Following the instructions from the <a href="https://sistemas.dcc.uchile.cl/wifi#Lin">official guide.</a>
      </p>

```ini
/var/lib/iwd/DCCAIR.8021x
-------------------------
[Security]
EAP-Method=PEAP
EAP-Identity=your_user
EAP-Password=your_passwd
EAP-PEAP-Phase2-Method=MSCHAPV2

[Settings]
Autoconnect=true
```

### Configuration file template for `fcfm`

Following the instructions from the [official guide](https://www.cec.uchile.cl/red-fcfm-como-conectar-en-linux).

```ini
/var/lib/iwd/fcfm.8021x
-----------------------
[Security]
EAP-Method=TTLS
EAP-Identity=your_user   
EAP-Password=your_pass
EAP-TTLS-Phase2-Method=MSCHAPV2
EAP-TTLS-Phase2-Identity=your_user
EAP-TTLS-Phase2-Password=your_pass

[Settings]
Autoconnect=true
```

### Configuration file template for `eduroam`

Following the instructions from the [official guide](https://vti.uchile.cl/ayudatecnologica/articulo/manual-de-conexion-a-eduroam/).

```ini
/var/lib/iwd/eduroam.8021x
--------------------------
[Security]
EAP-Method=PEAP
EAP-Identity=your_user
EAP-Password=your_pass
EAP-PEAP-Phase2-Method=GTC
EAP-PEAP-Phase2-Identity=your_user
EAP-PEAP-Phase2-Password=your_pass

[Settings]
Autoconnect=true
```
