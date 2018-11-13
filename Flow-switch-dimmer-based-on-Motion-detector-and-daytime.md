# Mittels Bewegungsmelder Licht einschalten

Möchte man mittels eines Bewegungsmelder ein Licht abhängig von der Helligkeit und der Tageszeit ein Licht mittels Dimmer einschalten, sind einige Flows nötig.

## Inhalt
  - [Überblick](#Überblick)
  - [Vorwort](#Vorwort)
  - [Vorbereitung](#Vorbereitung)
  - [Node Red Flow](#node-red-flow)
    - [Start](#start)
    - [Trigger des Flow](#trigger-des-flow)
      - [Konfiguration des Trigger](#konfiguration-des-trigger)
    - [Ablauf steuern](#ablauf-steuern)
    - [Ablauf verändern](#ablauf-verandern)
    - [Aktion ausführen](#aktion-ausfuhren)
    - [Abschluss](#abschluss)
    - [Flows als Download](#flows-als-download)

## Überblick

Klassifizierung der Tageszeit:

![image](https://user-images.githubusercontent.com/12692680/48412589-66e76300-e745-11e8-9844-e8ee0e183d14.png)

Klassifizierung der Helligkeit:

![image](https://user-images.githubusercontent.com/12692680/48420297-5d1c2a80-e75a-11e8-91ad-cb8a1096b751.png)

Eigentlicher Flow:

![image](https://user-images.githubusercontent.com/12692680/48420338-77ee9f00-e75a-11e8-89ee-c6417cfa5d26.png)


## Vorwort

Das Problem ließe sich sicherlich auf den ersten Blick einfacher mit einem Function Node und etwas JavaScript lösen. Die Empfehlung von IBM (der Firma hinter Node-Red) ist es möglichst auf die Function Nodes zu verzichten.

Die Gründe dafür sind:
 - Die Funktion eines Flows erschließt sich viel einfacher mit der Verwendung der Standard Nodes
    - Auch wenn die Flows damit vielleicht nicht so aufgeräumt wirken, kann man die Funktion später viel einfacher nachvollziehen.
 - Die *Function Nodes* haben gegenüber den Standard Nodes eine schlechtere Performance, da der Javascript Code in einer Sandbox ausgeführt wird.

## Vorbereitung

als Vorbereitung installiert man sich das zusätzliche Paket [node-red-contrib-sun-position](https://flows.nodered.org/node/node-red-contrib-sun-position) und [node-red-node-smooth](https://flows.nodered.org/node/node-red-node-smooth).

Die Installation erfolgt wie im im wiki auch unter [Node-Installation](https://github.com/hobbyquaker/RedMatic/wiki/Node-Installation) erklärt ist.

**1.**

  ![image](https://user-images.githubusercontent.com/12692680/48411467-e2dfac00-e741-11e8-946f-b1ba41162746.png)

**2.**

  ![image](https://user-images.githubusercontent.com/12692680/48411498-f68b1280-e741-11e8-8378-dee025c590bd.png)

**3.**

  ![image](https://user-images.githubusercontent.com/12692680/48411538-14f10e00-e742-11e8-9809-adb46df1247f.png)

**4.**

  ![image](https://user-images.githubusercontent.com/12692680/48411571-2d612880-e742-11e8-92b2-01065c2fee87.png)

**5.**

  ![image](https://user-images.githubusercontent.com/12692680/48411607-4c5fba80-e742-11e8-8f29-07af8708aeb4.png)

**6.**

  warten bis fertig

  ![image](https://user-images.githubusercontent.com/12692680/48411664-79ac6880-e742-11e8-9f83-9f74eca08148.png)

**6.**

neue nodes verwenden


## RedMatic Flow
### Start
Als erstes sollte man sich die [Node-RED Grundlagen](Node-RED) durchlesen. Danach kann es auch schon losgehen.

### Trigger des Flow

#### Konfiguration des Trigger

### Ablauf steuern

### Ablauf verändern

### Aktion ausführen

### Abschluss
Ist dies erledigt, wird diese Änderung aktiviert mittels des Deploy Buttons:    
![image](https://user-images.githubusercontent.com/12692680/44590937-962caa80-a7bc-11e8-9df3-592da55d8098.png)

### Flows als Download
