# Inhalt

* [Installation, Update, Deinstallation](Installation)
* [Passwort Schutz für Node-RED einrichten](Passwort)
* [Log-Level erhöhen für Fehleranalyse](Loglevel)





Bei einem Update des Addons wird die `settings.js` Datei überschrieben, die vorherige Version wird unter `settings.js.old` gesichert. Der Passwortschutz muss dann manuell wieder hergestellt werden.


### Node-RED Log-Level anpassen

Zur Fehleranalyse ist es hilfreich den Loglevel zu erhöhen:

* Per SSH auf der CCU einloggen
* `/usr/local/addons/node-red/settings.js` Zeile 230 bearbeiten (level auf `debug` statt `info` setzen)
* Node-RED neustarten mit `/etc/config/rc.d/node-red restart`
* Das Log von Node-RED ist im CCU Syslog (`/var/log/messages`) zu finden.
