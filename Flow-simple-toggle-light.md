# Einfacher Flow zum Schalten einer Lampe mittels Taster

Möchte man einfach mittels eines Tastendrucks ein List ein und mit dem nächsten Ausschalten, ist das einfach möglich:
![image](https://user-images.githubusercontent.com/12692680/44587420-2ebe2d00-a7b3-11e8-8f43-9019480b0600.png)

## Inhalt
  - [Vergleich mit einem CCU Programm](#vergleich-mit-einem-ccu-programm)
  - [Node Red Flow](#node-red-flow)
    - [Start](#start)
    - [Trigger des Flow](#trigger-des-flow)
      - [Konfiguration des Trigger](#konfiguration-des-trigger)
    - [Ablauf steuern](#ablauf-steuern)
    - [Ablauf verändern](#ablauf-verandern)
    - [Aktion ausführen](#aktion-ausfuhren)
    - [Abschluss](#abschluss)

## Vergleich mit einem CCU Programm

Wenn man das Problem mittels CCU Programm lösen möchte, hat man vermutlich ein Programm in dieser Art erstellt:
![image](https://user-images.githubusercontent.com/12692680/45623821-de23b200-ba88-11e8-94ee-053888e7bac5.png)

Hier wird das Programm durch einen kurzen Tastendruck getriggert und abhängig vom aktuellen Zustand der Lampe (nur prüfen) diese entweder ein oder ausgeschaltet.

In Node Red ist der Flow ähnlich:
![image](https://user-images.githubusercontent.com/12692680/44587420-2ebe2d00-a7b3-11e8-8f43-9019480b0600.png)


## RedMatic Flow
### Start
Als erstes sollte man sich die [Node-RED Grundlagen](Node-RED) durchlesen. Danach kann es auch schon losgehen.


### Trigger des Flow
Als erstes benötigt man den Trigger für den Flow. Dieser gibt das Event, welches ein Ereignis auslösen soll.

Wenn dieses Event durch eine Taste eines Homematic Gerätes ausgelöst werden soll, nimmt man dafür in der Palette den value node:
![image](https://user-images.githubusercontent.com/12692680/44587497-67f69d00-a7b3-11e8-9284-9b5b022cec19.png)

Diesen platziert man einfach in den Arbeitsbereitch und klickt ihn doppelt:
![image](https://user-images.githubusercontent.com/12692680/44587735-1dc1eb80-a7b4-11e8-860f-d5058af7432c.png)

#### Konfiguration des Trigger
zum konfigurieren sind die Felder wie folgt auszufüllen:
1. Als erstes muss man die Homematic Zentrale auswählen. Hat man noch keine Konfiguriert, so ist mittles Stift Button danaben die EInstellungen zur Zentrale zu tätigen. (siehe auch [CCU Nodes](CCU-Nodes) )
2. Danach das Interface des Homematic Gerätes. ![image](https://user-images.githubusercontent.com/12692680/44587957-b3f61180-a7b4-11e8-886d-9aa9c8d3b5cf.png) Sollte die Drop Down Box leer sein (weil beispielsweise die CCU erst konfiguriert wurde), so muss man die Einstellungen des Node mit dem Done Button einmal schließen und neu öffnen.
3. Hier wählt man den Kanal aus. Dabei kann man sehr einfach den Namen eintippen. Es öffnet sich eine Liste mit den möglichen Kanälen in der man den gewünschten auswählt. ![image](https://user-images.githubusercontent.com/12692680/44588257-8198e400-a7b5-11e8-943d-fd55bdae5bca.png)
4. Der Datenpunkt des Kanals. Die folgenden Datenpunkte sind dabei die gebräuchlichsten:
    * Taster - kurzer Tastendruck: "PRESS_SHORT"
    * Taster - langer Tastendruck: "PRESS_LONG"
    * Status eines Aktors "STATE"
    Für eine Taste als Trigger benötigen wir damit "PRESS_SHORT"
5. Mit dieser Einstellung kann man noch beeinflussen, wann die Node etwas ausgeben soll.
![image](https://user-images.githubusercontent.com/12692680/44588712-c2452d00-a7b6-11e8-9fbf-db21c17b9fdd.png)
    * Die Eigenschaft "Nur geänderte Werte ausgeben" kann man mit dem "bei Änderung", bzw. "bei Aktualisierung" in den Homematic Programmen vergleichen. Ist der Haken bei "Nur geänderte Werte ausgeben" gesetzt, wird der Flow nur gestartet, wenn sich der Datenpunkt auf einen anderen Wert (Bsp. true auf False) ändern ("bei Änderung"). Ist der Haken nicht gesetzt, wird der Flow immer dann gestartet, wenn der Datenpunkt aktualisiert wird ("bei Aktualisierung"). Damit auch wenn sich der Wert selbst nicht ändert (Bsp. true auf true).
      * Wenn man sich unsicher ist, sollte der Haken gesetzt sein.
    * Manche Datenpunkte können während der Änderung auch fortlaufend ihren Status übermitteln. So kann beispielsweise gesteuert werden ob ein Rollladen während der Bewegung ständig seine Position übermittelt oder nur wenn er an seinem Endpukt angekommen ist.
      * Wenn man sich unsicher ist, sollte der Haken gesetzt sein.
    * Mit der EIgenschaft "Beim Start letzten bekannten Wert ausgeben" kann gesteuert werden ob beim Neu/Start von RedMatic der Flow mit dem letzten bekannten Wert getriggert werden soll.

### Ablauf steuern
Als nächstes ziehen wir aus der Palette den Node, der den Ablauf steuern soll. In diesem Beispiel wollen wir abhängig vom Schaltzustand eines Lichtes dieses aus oder einschalten. Also muss sich in Abhängigkeit wvom Zustand des Lichtes (aus oder ein) etwas anderes passieren.
 - Wenn Lampe aus ist, soll sie eingeschaltet werden
 - Wenn Lampe ein ist, soll sie ausgeschaltet werden

Dafür benutzt man aus der Palette de switch Node.
Möchten wir den Flow in abhängigkeit eines Datenpunktes eines Homematic Gerätes steuern nehmen wir den aus der ccu Palette:

![image](https://user-images.githubusercontent.com/12692680/44588995-970f0d80-a7b7-11e8-9bff-2d1da501345a.png)


Es gibt daneben noch den Standard switch node, den wir in diesem Beispiel nicht verwenden:

![image](https://user-images.githubusercontent.com/12692680/44588964-7ba40280-a7b7-11e8-8c02-6816a98a2122.png)


Hat man diesen auf den Arbeitsbereich gezogen, verbindet man den Ausgang des Trigger Nodes mit dem Eingang dieses switch Nodes.

Als nächstes öffnet man die Einstellungen dieses switch Nodes.
Der obere Teil der Konfiguration ähnelt jetzt dem des value Nodes.

![image](https://user-images.githubusercontent.com/12692680/44589104-e5bca780-a7b7-11e8-9609-57bc04de5f42.png)
Hier wählt man jetzt den Datenpunkt der Lampe aus, welche man schalten möchte.
Bei Property ist die "value" auszuwählen.

Im unteren Teil kann man die Bedingungen einstellen:

![image](https://user-images.githubusercontent.com/12692680/44589627-4f898100-a7b9-11e8-878d-316b88b4e3e0.png)

1. Über den Add Button kann man die verschiedenen Bedingungen hinzufügen. Da wir 2 verschiedene Wege gehen möchten, müssen wir 2 Wege hinzufügen.
2. Für jeden dieser Wege kann man einstellen, unter welcher Bedingung er betreten werden soll. Die Bedingung "otherwise" trifft immer zu und sollte als letztes gewählt werden.
3. Diese EInstellung ist sehr wichtig. In der Standard EInstellung steht diese auf "checking all rules". Das bedeutet es wird jede Bedingung geprüft und der Flow an ihr weitergeführt. Für den "otherwise" zweig beispielsweise bedeutet das dieser immer weitergeführt wird, unabhängig von den anderen Bedingungen. Ist in dem Beispiel die Lampe eingeschaltet, geht es mit "checking all rules" sowohl bei "is true" als auch bei "otherwise" weiter. Will amn eher eine Wenn-dann bedingung ist diese Einstellugn auf "stopping after first match" umzustellen.

Die Komplette Konfiguration kann wie folgt aussehen:

![image](https://user-images.githubusercontent.com/12692680/44590081-8a3fe900-a7ba-11e8-921f-e0ba6d4214c2.png)

### Ablauf verändern
Als nächstes möchten wir bestimmen was an den beiden ausgängen passieren soll:

![image](https://user-images.githubusercontent.com/12692680/44590167-c4a98600-a7ba-11e8-84fa-8c6c3b93f114.png)

Der obere wird ja betreten, wenn die Lampe an ist. Hier soll die Lampe ausgeschaltet werden.

Dafür nehmen wir aus der Palette die change Node:

![image](https://user-images.githubusercontent.com/12692680/44590222-eefb4380-a7ba-11e8-8157-0387bdae5f8c.png)

Die steuernde Eigenschaft der weitergegebenen Nachricht ist die `msg.payload`. Um die Lampe auszuschalten muss diese auf "false" gesetzt werden. Der Node ist dafür bereits vorkonfiguriert:

![image](https://user-images.githubusercontent.com/12692680/44590285-12be8980-a7bb-11e8-89cf-0e96f34f5170.png)

Man wählt in der Liste einfach den Typ "boolean" aus und daneben false:

![image](https://user-images.githubusercontent.com/12692680/44590418-692bc800-a7bb-11e8-9773-824e69721a0f.png)

Diesen Node verbindet man mit dem oberen Ausgang des switch Nodes. Den Schritt wiederholt man mit dem underen Ausgang. Hierbei setzt man den payload jedoch auf true:

![image](https://user-images.githubusercontent.com/12692680/44590514-a3956500-a7bb-11e8-835e-76600cd1f17d.png)

### Aktion ausführen
Als Aktion soll ein Homematic Aktor geschaltet werden.
Dafür ist aus der Palette der value Node in den Arbeitsbereich zu ziehen.
Dieser ist genauso wie der Tasten Kanal für den Trigger zu konfigurieren, mit dem unterschied anstelle des Tasterkanals hier den Kanal des Aktors zu wählen.

Als vorletzten Schritt verbindet man die beiden Change Nodes mit dem value Node:
![image](https://user-images.githubusercontent.com/12692680/44587420-2ebe2d00-a7b3-11e8-8f43-9019480b0600.png)

### Abschluss
Ist dies erledigt, wird diese Änderung aktiviert mittels des Deploy Buttons:
![image](https://user-images.githubusercontent.com/12692680/44590937-962caa80-a7bc-11e8-9df3-592da55d8098.png)

