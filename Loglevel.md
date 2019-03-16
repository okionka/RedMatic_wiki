---
Title: Log-Level erhöhen zur Fehleranalyse
Category: Administration
---

### Node-RED Log-Level anpassen

Zur Fehleranalyse ist es hilfreich den Loglevel zu erhöhen:

* Im CCU WebUI unter Einstellungen-Systemsteuerung-RedMatic auf den Reiter Debug klicken
* Log Level auf `debug` setzen
* Node-RED neu starten

![](images/loglevel.mov.gif)


### Log herunterladen

RedMatic loggt in das CCU Syslog (`/var/log/messages`), im UI kann das Log (gefiltert auf Meldungen von RedMatic/Node-RED) heruntergeladen werden:

![](images/log-download.png)