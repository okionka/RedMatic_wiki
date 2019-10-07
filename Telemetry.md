# Anonyme Nutzungsstatistiken

## Warum?

* Neugier. Ich möchte wissen wieviele Nutzer RedMatic hat und im zeitlichen Verlauf dazugewinnt.
* Bessere Priorisierung der Weiterentwicklung durch Kenntnis welche CCU/RaspberryMatic Versionen und welche Nodes von wie vielen Usern eingesetzt werden und wie lange es nach einem Release dauert bis Updates von den Nutzern installiert werden.

## Welche Daten werden übertragen und gespeichert?

* Eine zufällig erzeugte Kennung die auf der CCU gespeichert ist aber nicht zurückverfolgt werden kann
* Zeitpunkt der Installation
* Zeitpunkt des letzten Updates
* RedMatic Version
* CCU bzw. RaspberryMatic Version
* CCU Plattform (ein Bezeichner der genutzten Hardware, z.B. `rpi3`, `tinkerboard`, ...)
* Eine Liste der installierte Nodes
* Das Land

## Welche Daten werden _nicht_ übertragen und/oder gespeichert?

* IP-Adressen
* Flows, Nodes
* Konfigurationsdaten
* Betriebsdaten
* Informationen über angebundene Geräte

## Transparenz

Um diesen Vorgang so transparent wie möglich zu gestalten hat Jedermann die Möglichkeit jederzeit Einsicht in die Daten, die Auswertung sowie die Software auf dem Server zu nehmen:

* Auswertung: https://telemetry.redmatic.de
* Rohdaten: https://telemetry.redmatic.de/database (SQLite Datenbank, zu öffnen z.B. mit [SQLiteStudio](https://sqlitestudio.pl/index.rvt))
* Server Software: https://github.com/rdmtc/redmatic-telemetry-server

## Opt-Out

Ich bitte darum das nicht zu tun. Bei RedMatic handelt es sich um ein Projekt in das viel Arbeit gesteckt wird, für das viel Freizeit geopfert wird und für dessen Nutzung außer dem Übertragen dieser (meiner Meinung nach nicht Privacy-relevanten) Daten (und dem Vergeben eines Github Sternchens 😉) keinerlei Gegenleistung erwartet wird. 

Wer dennoch unbedingt das Übertragen der Nutzungsstatistiken deaktivieren möchte kann eine der folgenden Möglichkeiten nutzen:

* Eine Firewall einsetzen und den Server an den die Daten gesendet werden blockieren.
* Über die hosts Datei den Servernamen auf 127.0.0.1 umlenken.
* Den Curl Aufruf im Startscript auskommentieren oder entfernen.
* Die CCU vom Internet trennen.
* RedMatic deinstallieren - niemand wird gezwungen RedMatic zu nutzen!
