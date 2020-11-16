---
Title: Deinstallation
Category: Administration
---
Im Homematic WebUI unter _Systemsteuerung_ - _Zusatzsoftware_ auf _Deinstallieren_ klicken:
![](images/uninstall.png)

Das Addon sollte nach einigen Sekunden - selbst ohne Reboot - vollständig entfernt worden sein. 

__Achtung__: Hierbei werden auch die Node-RED Flows gelöscht. Wenn man diese vor der Deinstallation sichern möchte sind folgende Dateien relevant: 
* `/usr/local/addons/redmatic/var/flows.json`
* `/usr/local/addons/redmatic/var/flows_cred.json`
* `/usr/local/addons/redmatic/etc/credentials.key`

Es ist auch möglich das Addon über die Kommandozeile zu entfernen: `/usr/local/etc/config/rc.d/redmatic uninstall`. Bitte vorher die richtige Umgebung mit dem Source Befehl aktivieren: `source /usr/local/addons/redmatic/home/.profile`.

Folgende Dateien und Ordner werden vom Addon auf der CCU Installiert, sollte eine Deinstallation nicht fehlerfrei ablaufen, können diese auch manuell gelöscht werden:

* `/usr/local/addons/redmatic`
* `/usr/local/etc/config/addons/www/redmatic`
* `/usr/local/etc/config/lighttpd/redmatic.conf`
* `/usr/local/etc/config/rc.d/redmatic`
* Abschnitt `RedMatic` in `/usr/local/etc/config/hm_addons.cfg`