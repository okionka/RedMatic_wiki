### Passwort-Schutz für Node-RED einrichten

_(Workaround bis in einer späteren Addon Version die Authentifizierung an der Rega implementiert ist)_

* Per SSH auf der CCU einloggen
* Einen Passwort-Hash erzeugen `node-red-admin hash-pw`
* Datei `/usr/local/addons/node-red/settings.js` bearbeiten (siehe https://nodered.org/docs/security#usernamepassword-based-authentication)
* Node-RED neustarten `/etc/config/rc.d/node-red restart`

Bei einem Update des Addons wird die `settings.js` Datei überschrieben, die vorherige Version wird unter `settings.js.old` gesichert. Der Passwortschutz muss dann manuell wieder hergestellt werden.


### Node-RED Log-Level anpassen

* Per SSH auf der CCU einloggen
* `/usr/local/addons/node-red/settings.js` Zeile 230 bearbeiten (level auf `debug` statt `info` setzen)
* Node-RED neustarten mit `/etc/config/rc.d/node-red restart`
* Das Log von Node-RED ist im CCU Syslog (`/var/log/messages`) zu finden.
