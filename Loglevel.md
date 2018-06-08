### Node-RED Log-Level anpassen

Zur Fehleranalyse ist es hilfreich den Loglevel zu erhöhen:

* `/usr/local/addons/redmatic/etc/settings.json` Zeile 9 bearbeiten (level auf `debug` oder `trace` statt `info` setzen)
* Node-RED neu starten über Systemsteuerung Zusatzsoftware oder auf der Konsole mit `/etc/config/rc.d/redmatic restart`
* Das Log von Node-RED ist im CCU Syslog (`/var/log/messages`) zu finden.
