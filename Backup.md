## CCU Backup

Da das RedMatic Addon sehr groß ist und die Backup-Routine der CCU3 die Backupdatei im RAM anlegt ist es in der Vergangenheit bei einigen Nutzern zu Problemen mit der Speicherauslastung gekommen, die im schlimmsten Fall dazu geführt haben dass Node-RED oder der hmipserver beim Backup beendet wurden. Um dieses Problem zu lösen musste der Platzbedarf von RedMatic im Backup reduziert werden, daher werden in der Default-Einstellung nur noch die wirklich relevanten Dateien von RedMatic mit ins CCU Backup gepackt. Wahlweise kann aber auch der komplette RedMatic Ordner im Backup inkludiert werden - auf eigene Gefahr! Dabei beachten: Eine Änderung der Backup-Konfiguration erfordert einen Node-RED Neustart um wirksam zu werden.

Leider bringt das Reduzieren der Backup-Größe folgenden Nachteil mit:

**Nach dem Zurückspielen eines CCU-Backups muss RedMatic (und eventuell genutzte Zusatzpakete) wieder manuell nachinstalliert werden.** 

## Manuelles Backup

Wer die Flows und Einstellungen von RedMatic unabhängig vom CCU Backup sichern möchte benötigt mindestens folgende Dateien:

* `/usr/local/addons/redmatic/var/flows.json`
* `/usr/local/addons/redmatic/var/flows_cred.json`
* `/usr/local/addons/redmatic/etc/credentials.key`
* `/usr/local/addons/redmatic/etc/settings.json`
* `/usr/local/addons/redmatic/var/package.json`

Falls das Node-RED Projects-Feature aktiviert ist das Verzeichnis
* `/usr/local/addons/redmatic/var/projects`

Falls RedMatic-HomeKit genutzt wird das Verzeichnis
* `/usr/local/addons/redmatic/var/homekit`

Falls node-red-contrib-zigbee genutzt wird das Verzeichnis
* `/usr/local/addons/redmatic/var/zigbee`

Wenn man ein manuelles Backup zurückspielt sollte zuerst Node-RED gestoppt werden, dann erst die Dateien zurück kopieren. 