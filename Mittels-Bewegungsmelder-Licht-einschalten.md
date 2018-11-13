# Mittels Bewegungsmelder Licht einschalten

Möchte man mittels eines Bewegungsmelser ein Licht abhängig von der Helligkeit und der Tageszeit ein Licht mittels Dimmer einschalten, löst:

![image](https://user-images.githubusercontent.com/12692680/44587420-2ebe2d00-a7b3-11e8-8f43-9019480b0600.png)

## Inhalt
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

## Vorwort

Das Problem ließe sich sicherlich auf den ersten Blick einfacher mit einem Function Node und etwas JavaScript lösen. Die Empfehlung von IBM (der Firma hinter Node-Red) ist es möglichst auf die Function Nodes zu verzichten.

Die Gründe dafür sind:
 - Die Funktion eines Flows erschließt sich viel einfacher mit der Verwendung der Standard Nodes
    - Auch wenn die Flows damit vielleicht nicht so aufgeräumt wirken, kann man die Funktion später viel einfacher nachvollziehen.
 - Die *Function Nodes* haben gegenüber den Standard Nodes eine schlechtere Performance, da der Javascript Code in einer Sandbox ausgeführt wird.

## Vorbereitung

als Vorbereitung installiert man sich das zusätzliche Paket 

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

