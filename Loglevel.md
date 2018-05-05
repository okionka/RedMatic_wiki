### Node-RED Log-Level anpassen

Zur Fehleranalyse ist es hilfreich den Loglevel zu erhöhen:

* `/usr/local/addons/node-red/settings.js` Zeile 230 bearbeiten (level auf `debug` statt `info` setzen)
* Node-RED neustarten mit `/etc/config/rc.d/node-red restart`
* Das Log von Node-RED ist im CCU Syslog (`/var/log/messages`) zu finden.
