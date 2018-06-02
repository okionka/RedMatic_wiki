![](images/nodes.png)

## connection
 
Im Connection Node wird die Verbindung zu den CCU Schnittstellenprozessen und zur Logikschicht verwaltet. Der Connection Node ist ein sogenannter _Configuration Node_, ist nicht in der Palette sichtbar und kann nicht in einem Flow platziert werden. Seine Konfiguration im Menü unter _Configuration Nodes_ erreichbar: ![](images/ccu-config.mov.gif)


## value

Geräte steuern und Events von Geräten empfangen.

## rpc event

Gibt RPC events aus.

## rpc

Beliebige RPC Methoden aufrufen und deren Rückgabe ausgeben.

## signal

Ansteuerung von Funk-Gongs (HM-OU-CFM-*, HM-OU-CM-PCB).

## display

Ansteuerung von Displays (HM-PB-4Dis-WM, HM-Dis-EP-WM55).


## sysvar

Systemvariablen setzen und Wertänderungen empfangen.

![](images/node-sysvar.png)


## program

Programme starten, aktivieren oder deaktivieren. Gibt den Zeitpunkt der letzten Programmausführung aus.

## script

Beliebige Scripte starten und deren Rückgabe ausgeben.

## poll

Abfrage von Variablen und Programmen auslösen.