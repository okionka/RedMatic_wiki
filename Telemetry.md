# Anonyme Nutzungsstatistiken

## Warum?

* Neugier. Ich möchte wissen wieviele Nutzer RedMatic hat.
* Bessere Priorisierung der Weiterentwicklung durch Kenntnis welche Nodes von wie vielen Usern eingesetzt werden und wie lange es nach einem Release dauert bis Updates installiert werden.

## Welche Daten werden übertragen und gespeichert?

* Eine Zufällig erzeugte Kennung die auf der CCU gespeichert ist aber nicht zurückverfolgt werden kann
* Zeitpunkt der Installation
* Zeitpunkt des letzten Updates
* RedMatic Version
* CCU bzw. RaspberryMatic Version
* CCU Plattform (ein Bezeichner der genutzten Hardware, z.B. `rpi2`, `rpi3`, ...)
* Eine Liste der installierte Nodes

## Welche Daten werden _nicht_ übertragen und/oder gespeichert?

* IP-Adressen
* Flows
* Node-Konfigurationen
* Informationen über angebundene Geräte

## Transparenz

Um diesen Vorgang so Transparent wie möglich zu gestalten hat Jedermann die Möglichkeit jederzeit Einsicht in die Daten, die Auswertung sowie die Software auf dem Server zu nehmen:

* Auswertung: https://telemetry.redmatic.de
* Rohdaten (sqlite3 Datenbank): https://telemetry.redmatic.de/database
* Server Sourcen: https://github.com/rdmtc/redmatic-telemetry-server

## Opt-Out

Ich bitte darum das nicht zu tun. Bei RedMatic handelt es sich um ein Projekt das viel (Frei)zeit und Arbeit verursacht und für dessen Nutzung außer dem Übertragen dieser Daten keine Gegenleistung verlangt wird. Wer dennoch unbedingt das Übertragen der Nutzungsstatistiken deaktivieren möchte hat folgende Möglichkeiten:

* RedMatic deinstallieren (niemand es gezwungen RedMatic zu nutzen!).
* Den Curl Aufruf im Startscript auskommentieren oder entfernen.
* Eine Firewall einsetzen und den Server an den die Daten gesendet werden blockieren.
* Die CCU vom Internet trennen.