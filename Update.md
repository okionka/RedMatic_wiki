### Update

Das Addon sollte vor einem Update **nicht** deinstalliert werden, man installiert die neue Version einfach "darüber". Die Vorgehensweise ist genau die gleiche wie bei einer ersten [Installation](Installation) auch.

Bei einem Update des Addons wird die Datei `/usr/local/addons/node-red/settings.js` überschrieben, die vorherige Version wird unter `settings.js.old` gesichert. Falls manuelle Änderungen an der Datei vorgenommen wurden, z.B. ein Passwortschutz konfiguriert war, muss die Datei nach dem Update manuell wieder hergestellt werden.

### Deinstallation

Ist ebenfalls über Systemsteuerung -> Zusatzsoftware möglich und sollte das Addon restlos entfernen. __Achtung__: Hierbei werden auch die Node-RED Flows gelöscht. Wenn man diese sichern möchte findet sich die Flows Datei hier: `/usr/local/addons/node-red/var/flows.json`


