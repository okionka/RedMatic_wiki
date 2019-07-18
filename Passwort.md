---
Title: Passwort-Schutz für Node-RED einrichten
Category: Administration
---

In Standardeinstellung wird für Node-RED der gleiche Username und das gleiche Passwort verwendet das auch zur Authentifizierung am CCU WebUI genutzt werden muss. Hierbei Groß-/Kleinschreibung beachten, der Standardbenutzer der CCU ist `Admin` mit großem A.

Sollte kein Passwortschutz eingestellt sein, so kann jeder im LAN oder falls Portforwarding des Port 80 vorhanden ist, jeder aus dem Internet die CCU relativ einfach mit einer Remote Code Execution übernehmen!<br>
In jedem Fall muss das Passwort stark genug sein!<br>
Node-Red ist sicher? Der Exploit [Gaining RCE by abusing Node-RED](https://quentinkaiser.be/pentesting/2018/09/07/node-red-rce/) funktioniert ohne Authentifizierung sofort, und mit Authentifizierung müssen die Logindaten angegeben werden.<br>
Stand Heute Juli 2019: An die verschlüsselten Logindaten einer CCU zu kommen, ist aktuell realtiv einfach.

### Passwort-Schutz für Node-RED einrichten, falls noch nicht geschehen.

* Unter Systemsteuerung Zusatzsoftware Redmatic die Konfigurationsseite aufrufen (Button "Einstellen")
* Unter Authentifizierung Admin ist die Einstellung "ReGaHSS" nach einer Neuinstallation der Default. Dann muss der CCU User "Admin" zum einloggen genommen werden.<br>
Es kann auch "Credentials" eingestellt werden, um getrennte Username/Passwort Kombinationen nutzen zu können.
<br>Schaltet man die Authentifizierung ab mit "Keine Authentifizierung", so ist der Zugang völlig ungeschützt!
* über Button "Set" bestätigen
* Node-RED neustarten

Es ist zu beachten dass die Authentifzierung für das Node-RED Admin UI ("Admin Auth") und für Node-RED Dashboard getrennt vorgenommen werden muss ([siehe Node-RED Dokumentation](https://nodered.org/docs/security#http-node-security), "Node Auth" gilt für das Dashboard).

Wichtig! 

Das Eingabefeld unter der Admin Authentifzierung ist der Session Timeout in Sekunden. Nach dem Session Timeout wird der Login-Dialog neu angezeigt.

Hier kann eine große Zahl (z.B. 3600 = 1 Stunde) eingetragen werden oder man lässt das Feld auf 0 (dies ist der Default der auf einem Tag stehen sollte).
