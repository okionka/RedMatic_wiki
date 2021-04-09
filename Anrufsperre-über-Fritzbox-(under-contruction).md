Dieser flow definiert eine Anrufsperre für ankommende Anrufe über die Fritzbox.

* Kann über das dashboard aktiviert / deaktiviert werden
* Die Anrufsperre wird per default am nächsten Morgen um 08:00 automatisch wieder deaktiviert
* Vorbereitung für Telegram-Benachrichtigung
* Es wird eine globale Variable in Redmatic definiert die den Status der Anrufsperre per boolean true/false global zur Verfügung stellt

## Voraussetzungen: 
* Konfigurierter Zugriff mit Benutzername / Passwort via node-red-contrib-fritz auf die Fritzbox

## Installation:
1.  Den Anrufbeantworter der Fritzbox aktivieren, falls dieser nicht verwendet wird

![grafik](https://user-images.githubusercontent.com/75842297/114156002-66595380-9922-11eb-8384-9e96cb26c4eb.png)

2.  Rufumleitung unter Telefonie -> Rufumleitung anlegen

a) Alle ankommenden Anrufe auf den AB umleiten

![grafik](https://user-images.githubusercontent.com/75842297/114156219-9f91c380-9922-11eb-87e0-16373f1a0350.png)

b) Sollte so aussehen:

![grafik](https://user-images.githubusercontent.com/75842297/114156381-cea83500-9922-11eb-9f99-f4774e8137fa.png)

c) Anrufbeantworter wieder deaktivieren (sic)

## Screenshot des flows:
![flow](https://user-images.githubusercontent.com/75842297/114154568-d5ce4380-9920-11eb-922c-5c0076f5ac72.png)

## Flow:
```

```

## Getestete Firmware und Hardware
| Hardware/Router  | Versionsstand |
| ------------- | ------------- |
| Fritzbox 7590  | 7.21 |


## Version: 
| Version | Bemerkung | Datum |
| ------------- | ------------- |  ------------- | 
| 1.0  | Funktionierend | 09. April 2021 |