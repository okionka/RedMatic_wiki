### Passwort-Schutz für Node-RED einrichten

_(Workaround bis in einer späteren Addon Version die Authentifizierung an der Rega implementiert ist)_

* Per SSH auf der CCU einloggen
* Node.js zum Pfad hinzufügen: `export PATH=$PATH:/usr/local/addons/node-red/bin`
* Einen Passwort-Hash erzeugen `/usr/local/addons/node-red/lib/node_modules/.bin/node-red-admin hash-pw`
* Datei `/usr/local/addons/node-red/settings.js` bearbeiten (siehe https://nodered.org/docs/security#usernamepassword-based-authentication)
* Node-RED neustarten `/etc/config/rc.d/node-red restart`

__Hinweis__: Bei einem Update des Addons wird die `settings.js` Datei überschrieben, die vorherige Version wird unter `settings.js.old` gesichert. Die Konfiguration der Authentifizierung muss dann manuell wieder hergestellt werden.