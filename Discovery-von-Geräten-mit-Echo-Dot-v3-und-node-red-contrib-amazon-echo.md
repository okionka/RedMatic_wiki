* Die Nodes node-red-contrib-amazon-echo installieren (siehe https://github.com/rdmtc/RedMatic/wiki/Node-Installation)
* Die Node `Amazon Echo Hub` in den Flow ziehen und dessen Konfiguration öffnen.
* Port auf 6502 setzen. `Set port to 80 if you have latest generation Amazon Echo devices.` bitte ignorieren. Die Gerätesuche wird durch eine [Proxy-Regel](https://github.com/rdmtc/RedMatic/commit/19b09bc93b4625d7a3990ff898f441509eca4740#diff-acb0ade2165e8f269b930fb087cc4cf6) auf Port 6502 weitergeleitet.
* Flows entsprechend der Anleitung von [node-red-contrib-amazon-echo] erstellen.

Sollten keine Geräte gefunden werden, so sind `/var/log/lighttpd-access.log` and `/var/log/lighttpd-error.log` auf Fehler zu prüfen.


