### Addon Update

Einfach über Systemsteuerung -> Zusatzsoftware die neue Version "drüberinstallieren"

### Addon Deinstallation

Ist ebenfalls über Systemsteuerung -> Zusatzsoftware möglich und sollte das Addon restlos entfernen. __Achtung__: Hierbei werden auch die Node-RED Flows gelöscht. Wenn mann diese sichern möchte findet sich die Flows Datei hier: `/usr/local/addons/node-red/var/flows.json`

### Passwort-Schutz für Node-RED einrichten

_(Workaround bis in einer späteren Addon Version die Authentifizierung an der Rega implementiert ist)_

* Per SSH auf der CCU einloggen
* Node.js zum Pfad hinzufügen: `export PATH=$PATH:/usr/local/addons/node-red/bin`
* Einen Passwort-Hash erzeugen `/usr/local/addons/node-red/lib/node_modules/.bin/node-red-admin hash-pw`
* Datei `/usr/local/addons/node-red/settings.js` bearbeiten (siehe https://nodered.org/docs/security#usernamepassword-based-authentication)
* Node-RED neustarten `/etc/config/rc.d/node-red restart`

Bei einem Update des Addons wird die `settings.js` Datei überschrieben, die vorherige Version wird unter `settings.js.old` gesichert. Der Passwortschutz muss dann manuell wieder hergestellt werden.


### Node-RED Log-Level anpassen

* Per SSH auf der CCU einloggen
* `/usr/local/addons/node-red/settings.js` Zeile 230 bearbeiten (level auf `debug` statt `info` setzen)
* Node-RED neustarten mit `/etc/config/rc.d/node-red restart`
* Das Log von Node-RED ist im CCU Syslog (`/var/log/messages`) zu finden.
