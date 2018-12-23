---
Title: Installation
Category: RedMatic
---

* Zur Sicherheit __ein Backup der CCU anfertigen__.
* Neueste Version von https://github.com/HM-RedMatic/RedMatic/releases/latest herunterladen. Es wird die Datei 
`redmatic-<version>.tar.gz` benötigt: ![](images/install-1.png)
* Im Homematic WebUI Systemsteuerung Zusatzsoftware aufrufen: ![](images/install-2.png) ![](images/install-3.png)
* Heruntergeladene Datei auswählen: ![](images/install-4.png) ![](images/install-5.png)
* Datei auf die CCU hochladen: ![](images/install-6.png)
* Installation Starten: ![](images/install-7.png)
* Im Anschluss abwarten bis sich die CCU neu gestartet hat - hier ist Geduld erforderlich. Die Installation von RedMatic benötigt einige Zeit.
* Node-RED ist unter `http://<ccu-adresse>/addons/red` erreichbar.
* Node-RED Dashboard ist unter `http://<ccu-adresse>/addons/red/ui` erreichbar.

### CUxD und Homematic-Wired

Per Default werden die Schnittstellenprozesse CUxD und hs485d (wired) nicht aktiviert. Für eine Zukünftige Version ist dies geplant (https://github.com/hobbyquaker/RedMatic/issues/34), Stand heute muss das noch manuell im _ccu configuration_ Node gemacht werden.

### rmupdate

RedMatic lässt sich auch über das [Addon rmupdate](https://github.com/j-a-n/raspberrymatic-addon-rmupdate) installieren und updaten. Dies bietet den Vorteil dass kein überflüssiger Zwangs-Reboot im Anschluss an die Installation durchgeführt wird.