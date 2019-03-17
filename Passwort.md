---
Title: Passwort-Schutz für Node-RED einrichten
Category: Administration
---

In Standardeinstellung wird für Node-RED der gleiche Username und das gleiche Passwort verwendet das auch zur Authentifizierung am CCU WebUI genutzt werden muss. Hierbei Groß-/Kleinschreibung beachten, der Standardbenutzer der CCU ist `Admin` mit großem A.

### Passwort-Schutz für Node-RED einrichten

* Unter Systemsteuerung Zusatzsoftware Redmatic die Konfigurationsseite aufrufen (Button "Einstellen")
* Authentifizierung aktivieren, Username und Passwort eingeben und über Button "Set" bestätigen
* Node-RED neustarten

Es ist zu beachten dass die Authentifzierung für das Node-RED Admin UI ("Admin Auth") und für Node-RED Dashboard getrennt vorgenommen werden muss ([siehe Node-RED Dokumentation](https://nodered.org/docs/security#http-node-security), "Node Auth" gilt für das Dashboard).

Wichtig! 

Das Eingabefeld unter der Admin Authentifzierung ist der Session Timeout in Sekunden. Nach dem Session Timeout wird der Login-Dialog neu angezeigt.

Hier kann eine große Zahl (z.B. 86400 = 1 Tag) eingetragen werden. 
