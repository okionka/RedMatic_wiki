### Addon Update

Einfach über Systemsteuerung -> Zusatzsoftware die neue Version "drüberinstallieren" - __nicht__ vorher deinstallieren!

### Addon Deinstallation

Ist ebenfalls über Systemsteuerung -> Zusatzsoftware möglich und sollte das Addon restlos entfernen. __Achtung__: Hierbei werden auch die Node-RED Flows gelöscht. Wenn man diese sichern möchte findet sich die Flows Datei hier: `/usr/local/addons/node-red/var/flows.json`

__Hinweis__: Bei einem Update des Addons wird die `settings.js` Datei überschrieben, die vorherige Version wird unter `settings.js.old` gesichert. Falls z.B. ein Passwortschutz konfiguriert war muss dieser manuell wieder hergestellt werden.
