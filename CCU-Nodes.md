# Nodes

![](images/nodes.png)

## ccu connection node
 
Im Connection Node wird die Verbindung zu den CCU Schnittstellenprozessen und zur Logikschicht verwaltet. Der Connection Node ist ein sogenannter _Configuration Node_, ist nicht in der Palette sichtbar und kann nicht in einem Flow platziert werden. Seine Konfiguration ist im Menü unter _Configuration Nodes_ erreichbar: ![](images/ccu-config.mov.gif)


## ccu value node

Geräte steuern und/oder Events von einem Gerät empfangen.

## ccu rpc event node

Events von einem oder mehreren Geräten empfangen. Filter...

## ccu rpc node

Beliebige RPC Methoden auf Schnittstellenprozess aufrufen und deren Rückgabe ausgeben.

## ccu signal node

Ansteuerung von Funk-Gongs (HM-OU-CFM-*, HM-OU-CM-PCB).

## ccu display node

Ansteuerung von Displays (HM-PB-4Dis-WM, HM-Dis-EP-WM55).


## ccu sysvar node

Rega-Systemvariablen setzen und Wertänderungen empfangen.

![](images/node-sysvar.png)


## ccu program node

Rega-Programme starten, aktivieren oder deaktivieren. Gibt den Zeitpunkt der letzten Programmausführung aus.

## ccu script node

Beliebige Rega-Scripte starten und deren Rückgabe ausgeben.

## ccu poll node

Sofortige Abfrage von Rega-Systemvariablen und -Programmen auslösen.


# Attribute

## topic

Einige der CCU Nodes erlauben es in ihrer Topic-Konfiguration Platzhalter wie z.B. `${channelName}` zu verwenden. Dadurch ist es möglich das Topic dynamisch aus einem eingehenden Event zu erzeugen. Im den Nodes _RPC_ und _Value_ stehen dafür alle Attribute zur Verfügung die auch zum Filtern von Events konfiguriert werden können.
