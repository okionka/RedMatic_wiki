Falls Probleme beim Update/Installation auftreten, bitte folgendes prüfen/beachten

- Geduld: Update/Installation kann durchaus 60 Minuten dauern

- Prüfen, ob die richtige Datei für die vorhandene Hardware installiert wurde

- Prüfen, ob eine neue Node über die Palette installiert wurde, die spezielle Binärdateien benötigt. Das funktioniert nicht. 

- Erreichbarkeit prüfen: `http://<ccu-address>:80/addons/red/#flow` bzw das dashboard `http://<ccu-address>:80/addons/red/ui/` (falls genutzt)

- Gegebenenfalls die CCU im Safe Mode starten - geht das? Hier können Nodes/Pakete deinstalliert werden

- Logfile untersuchen

  - Konnten die Versionen der einzelnen Komponenten ermittelt werden (Node.JS, npm, node-RED) und stimmen diese mit den Versionen im Change Log überein?

  - Welche Fehlermeldungen kommen beim Starten von Node-RED?

- Nochmal installieren - schadet üblicherweise nicht

- Gegebenenfalls - nach einer Sicherung - Redmatic de-installieren (siehe Anleitung hierzu im Wiki) und nochmal installieren. 




