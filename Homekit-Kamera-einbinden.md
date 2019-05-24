Man nehme einen Homekit Kamera Node:

![](https://up.picr.de/35828323ed.jpg)

Diesen benennt man und fügt die URL zum Bewegtbild und Standbild der Kamera hinzu.
Bei meiner Foscam ist das z.B.:
`http://IP_ADRESSE/videostream.cgi?user=USERNAME&pwd=PASSWORT`
und
`http://IP_ADRESSE/snapshot.jpg?user=USERNAME&pwd=PASSWORT`

![](https://up.picr.de/35828324aa.jpg)

Eine Liste der Links nahezu aller Kameras gibt es hier, es funktionieren MJPEG und RTSP Streams:
[iSpyConnect](https://www.ispyconnect.com/sources.aspx)

Dann implementieren und Redmatic einmal neu starten.

In der HomeApp ein neues Gerät hinzufügen und den QR-Code des Camera Node scannen.
Und schon sollte die Kamera in der Home App angezeigt werden, auf der Übersichtsseite als Standbild, das alle 10 Sekunden aktualisiert wird, wenn man drauf klickt als Bewegtbild.

![](https://up.picr.de/35828325mo.jpg)

![](https://up.picr.de/35828326ny.jpg)

Auf einem RPi3B ist die CPU Auslastung mit dem sich aktualisierenden Standbild kaum höher, bei Livebild liegt sie bei ca. 16-20% mehr als üblich.

**Achtung:**
**Bei mehreren Kameras unbedingt im Camera Node unterschiedliche Ports vergeben. Sonst bleibt RedMatic hängen und man kommt auch nicht mehr ohne weiteres rein.**