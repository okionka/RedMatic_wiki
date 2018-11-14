# Ausführen von Funktion in definierten Zeitfenstern

Dieser Flow stellt exemplarisch dar, wie Funktionen an Zeitfenster geknüpft werden können. Dafür werden beispielhaft zwei Szenarien dargestellt.


## Inhalt
  - [Steuerung der Außenbeleuchtung - AstroFunktion](#Gartenbeleuchtung)
  - [Bewegungsmelder für Beleuchtung im Hof (Nachts)](#Hofbeleuchtung)

## Gartenbeleuchtung

In RedMatic ist der Node [time-range](https://flows.nodered.org/node/node-red-contrib-time-range-switch) integriert. Dieser Node ermöglicht es sowohl Zeitfenster selbst festzulegen als auch Zeitfenster an Hand des Sonnenstandes zu ermitteln. Dafür stehen die unterschiedlichen definierten Sonnenauf- und untergänge als Start- bzw. End-Time zur Verfügung, zum besseren Verständnis empfehle ich folgenden Link: [Dämmerung – die drei Dämmerungsphasen](https://www.timeanddate.de/astronomie/daemmerung-phasen).

Ein verbesserter Node ist in dem Paket [node-red-contrib-sun-position](https://flows.nodered.org/node/node-red-contrib-sun-position) enthalten, welches zusätzlich installiert werden kann. Hier kann man zusätzlich auch der Mond aufgang oder untergang genutzt werden oder verschiedene Zeiten für Feiertage oder Wochenende.

### Flow mit der [time-range](https://flows.nodered.org/node/node-red-contrib-time-range-switch) node

Im folgenden Flow wird jeden Tag nach zivilem Sonnenuntergang die Beleuchtung im Garten eingeschaltet und nach zivilem Sonnenaufgang die Beleuchtung im Garten deaktiviert.
![image](https://user-images.githubusercontent.com/12249109/47701541-71b8d880-dc1a-11e8-88b1-ce446543640d.png)

Das Programm wird minütlich per InjectNode aufgerufen, Konfiguration des Nodes siehe hier:

![image](https://user-images.githubusercontent.com/12249109/47701596-9dd45980-dc1a-11e8-8018-563df4836266.png)

Minütlich wird somit der time-range Node angestoßen, dieser muss wie im folgenden Bild eingestellt werden.

![image](https://user-images.githubusercontent.com/12249109/47701604-a62c9480-dc1a-11e8-83c7-0403ac0dc9f9.png)

Zur Erklärung.
Zum einen muss man definieren welcher Ort zur Bestimmung der AstroDaten verwendet werden soll. Wollt Ihr Zeitfenster selbst definieren könnt ihr die Einstellung an dieser Stelle überspringen.

Ich habe für meinen Anwendungsfall **start-time** als **sunset** definiert, laut info des Nodes ist dies die **zivile Abenddämmerung.**
**End-Time **ist** dawn**, dies entspricht dem **zivilen Sonnenaufgang**. Somit wird jeden Abend wenn die Dämmerung einsetzt und die Dunkelheit beginnt die Beleuchtung im Garten eingeschaltet, sollte die Morgendämmerung eingesetzt haben werden die Lampen deaktiviert.

Je nach zutreffender Bedingung hat der Node zwei Ausgänge. An diese Ausgänge setze ich den Aktor welchen ich schalten mag. 

Per change-node wird nun der zu treffende Schaltstatus definiert, im Beispielbild wird **msg.payload** auf **true** gesetzt. **Das Licht soll angeschaltet werden**. _Sollte das Licht ausgeschaltet werden sollen muss msg.payload auf false gesetzt werden._

![image](https://user-images.githubusercontent.com/12249109/47701946-cc9eff80-dc1b-11e8-90e6-03ee3c488ded.png)

Abschließend noch die Konfiguration des ccu-value nodes

![image](https://user-images.githubusercontent.com/12249109/47701955-d294e080-dc1b-11e8-9705-1e2eda6f7ea4.png)

### Flow mit der [node-red-contrib-sun-position](https://flows.nodered.org/node/node-red-contrib-sun-position) nodes

mit Hilfe des time-inject nodes lässt sich das stark vereinfachen:

![image](https://user-images.githubusercontent.com/12692680/48482183-4c2df080-e810-11e8-8983-a9cade14dd6c.png)

Die time-inject Nodes senden eine Nachricht beim erreichen der eingestellten zeit gleich mit dem richtigen payload:

![image](https://user-images.githubusercontent.com/12692680/48482268-87302400-e810-11e8-995b-b09c18bd6a8a.png)

Die Einstellung für die Position wird hier zentral über eine extra Konfiguration gehandelt und muss nicht in jeder Node einzeln konfiguriert werden.

#### verschiedene Zeiten für Wochenende

Dies lässt sich mit Hilfe der Auswahl der Tage und entsprechend mehr time-inject nodes realisieren:

![image](https://user-images.githubusercontent.com/12692680/48483980-33740980-e815-11e8-850a-71538a9cd038.png)

![image](https://user-images.githubusercontent.com/12692680/48484053-64543e80-e815-11e8-889f-644fd8703d7b.png)

![image](https://user-images.githubusercontent.com/12692680/48484087-7f26b300-e815-11e8-82d0-069a97ea146c.png)


#### verschiedene Zeiten für Feiertage

_**noch offen**_

## Gartenbeleuchtung

_**ausstehend.**_
