* [Change Node](#change-node)
* [Delay Node](#delay-node)
* [Switch Node](#switch-node)
* [If Node](#if-node)
* [Statistic Node](#statistic-node)
* [List Node](#list-node)
* [Links](#links)
* [Subflows](#subflows)
* [MQTT](#mqtt)

## Change Node

Mit diesem Node kann der Payload eine _Message_ manipuliert werden, um z.B. die `payload` _Property_ auf einen bestimmten Wert zu setzen.

## Delay Node

Verzögert die Weiterleitung einer _Message_ für eine bestimmte Zeit.

Beispiel: Lampe bei Bewegungserkennung anschalten und 5 Minuten verzögert wieder ausschalten ![](images/delay-1.png)

## Switch Node


## If Node

## Statistic Node

## List Node

## Links

Link Nodes ermöglichen es Flow-übergreifende Verbindungen einzurichten. Sie eignen sich z.B. auch gut um eine strukturierte Szenen-Steuerung zu realisieren:
![](images/link-1.png)
![](images/link-2.png)

## Subflows

## MQTT

Node-RED eignet sich hervorragend zur Ansteuerung von Geräten oder Empfang von (Sensor-)Daten via MQTT.

* [Mosquitto MQTT Broker als CCU3/RaspberryMatic Addon](https://github.com/hobbyquaker/ccu-addon-mosquitto)
* [MQTT Link Liste](https://github.com/hobbyquaker/awesome-mqtt)