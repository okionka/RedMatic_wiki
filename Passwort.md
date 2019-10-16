---
Title: Passwort-Schutz für Node-RED einrichten
Category: Administration
---

In Standardeinstellung wird für Node-RED der gleiche Username und das gleiche Passwort verwendet das auch zur Authentifizierung am CCU WebUI genutzt werden muss. Hierbei Groß-/Kleinschreibung beachten, der Standardbenutzer der CCU ist `Admin` mit großem A.

Bitte die [Hinweise zum Thema Sicherheit](Sicherheit) beachten!

### Passwort-Schutz für Node-RED einrichten, falls noch nicht geschehen.

* Unter Systemsteuerung Zusatzsoftware RedMatic die Konfigurationsseite aufrufen (Button "Einstellen")
* Unter Authentifizierung Admin ist die Einstellung "ReGaHSS" nach einer Neuinstallation der Default. Dann muss ein gültiger CCU WebUI User einloggen genommen werden.
* über Button "Set" bestätigen
* Node-RED neu starten

Es ist zu beachten dass die Authentifizierung für das Node-RED Admin UI ("Admin Auth") und für Node-RED Dashboard getrennt vorgenommen werden muss ([siehe Node-RED Dokumentation](https://nodered.org/docs/security#http-node-security), "Node Auth" gilt für das Dashboard).

