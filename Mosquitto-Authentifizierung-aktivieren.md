# Mosquitto Authentifizierung aktivieren
<br>
als erstens das Addon HM-Tools auf der CCU installieren und per SSH auf die CCU verbinden
<br>
<br>
<br>

1. in das Config-Verzeichnis wechseln `cd /usr/local/addons/mosquitto/etc/conf.d`

2. Passwortdatei anlegen 
   `touch passwd.txt`

3. User anlegen
   `/usr/local/addons/mosquitto/bin/mosquitto_passwd -b passwd.txt USERNAME PASSWORD`
<br>
<br>

## Authentifizierung aktivieren

<br>

* Datei anlegen `nano login.conf`

* nun folgenden Inhalt in die Datei login.conf kopieren

  `allow_anonymous false`

  `password_file /usr/local/addons/mosquitto/etc/conf.d/passwd.txt`
<br>
<br>

* Mosquitto neustart
`/etc/config/rc.d/mosquitto restart`
<br>
<br>

## Logindaten auf den Geräten verteilen

Der Benutzername und Passwort muss natürlich auf den MQTT Geräten eingegeben werden und in RedNote im MQTT-Server.

In RedNode auf eine MQTT-Node klicken und den kleinen Stift auswählen:

![MQTT-Server](https://homematic-forum.de/forum/download/file.php?id=64776&mode=view)

<br>
<br>

Hier nun das Passwort eintragen
<br>
<br>

![MQTT-Passwort](https://homematic-forum.de/forum/download/file.php?id=64777&mode=view)