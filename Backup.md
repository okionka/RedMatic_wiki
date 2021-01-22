## CCU Backup

Da das RedMatic Addon sehr groß ist und die Backup-Routine der CCU3 die Backupdatei im RAM anlegt ist es in der Vergangenheit bei einigen Nutzern zu Problemen mit der Speicherauslastung gekommen, die im schlimmsten Fall dazu geführt haben dass Node-RED oder der hmipserver beim Backup beendet wurden oder der Restore des Backups extrem lange dauert. Um dieses Problem zu lösen musste der Platzbedarf von RedMatic im Backup reduziert werden, daher werden in der Default-Einstellung nur noch die wirklich relevanten Dateien von RedMatic mit ins CCU Backup gepackt. 

Wahlweise kann aber auch der komplette RedMatic Ordner im Backup inkludiert werden - **auf eigene Gefahr!** Dabei beachten: Eine Änderung der Backup-Konfiguration erfordert einen Node-RED Neustart um wirksam zu werden.

⚠️ Leider bringt das reduzierte Backup folgenden Nachteil mit: **Nach dem Zurückspielen eines CCU-Backups muss RedMatic (und eventuell genutzte Zusatzpakete) wieder manuell nachinstalliert werden.** 

## Manuelles Backup

Wer die Flows und Einstellungen von RedMatic unabhängig vom CCU Backup sichern möchte, sollte die folgenden Dateien und Verzeichnisse inklusive aller Unterverzeichnisse sichern:
* `/usr/local/addons/redmatic/etc/credentials.key`
* `/usr/local/addons/redmatic/etc/settings.json`
* `/usr/local/addons/redmatic/var` aber ohne Verzeichnis `node_modules`

Das entspricht der Empfehlung von [Node-RED Cookbook](https://github.com/node-red/cookbook.nodered.org/wiki/How-to-backup-flows-and-related-configuration).

**Achtung** - Falls das Node-RED "Projects" Feature genutzt wird: Die Dateien `.config.json` bzw. `.config.*.json` (ab 1.20) sind versteckte Dateien und sollten ebenfalls gesichert werden.

**Achtung**: Der Node-RED Context (falls man ihn im Dateisystem ablegt und den Default Pfad geändert hat) muss ggf. zusätzlich gesichert werden.

Wenn man ein manuelles Backup zurückspielt sollte Node-RED gestoppt werden bevor man die Dateien zurückkopiert.