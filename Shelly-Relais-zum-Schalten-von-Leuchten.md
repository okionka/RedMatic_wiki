Shelly Relais sind kostengünstige Relais (10 Euro), die in Unterputzdosen verbaut werden. 
Sie können über WLAN (REST API, MQTT) in die Hausautomation (ioBroker, FHEM, Node-RED, Alexa, ...) eingebunden werden.

Voraussetzungen: Freien Platz und Strom (Phase, Nulleiter) in der Lichtschalter-Unterputzdose 

Welche Modelle gibt es: [Shelly homepage](https://shelly.cloud/)

## Meine Einsatzbereiche

### 1. Standard Lichtschalter mit standard LED Leuchte: Shelly 1
Die LED Leuchte wird über RedMatic geschaltet. Der vorhandene Lichtschalter ist weiterhin funktionsfähig.

Vorteil: Automation zu geringen Kosten.

### 2. Homematic IP 2-fach Lichtschalter mit Standard LED Leuchte: Shelly 2.5
Da nicht genügend Platz in der Lichtschalter-Unterputzdose vorhanden war, wurde der Lichtschalter ausgebaut und durch einen Homematic IP 2-fach Schalter ersetzt. Dieser steuert das Deckenlicht und die Spiegelampe. Das Deckenlicht wird zusätzlich über einen Präsenzmelder und Alexa Kommandos aktiviert.

Vorteil: Automation mit Präsenzmelder und Alexa.

### 3. Homematic IP 6-fach Lichtschalter mit 3 Philips HUE Leuchten: Shelly 1 
Es ist eine Leuchtenleiste mit drei Leuchten installiert. Je nach Nutzung wird nur eine oder mehrere Leuchten eingeschaltet - auch gedimmt (Hue Szenen)
Über den 6-fach Schalter können die einzelnen Leuchten geschaltet werden plus Szenen aktiviert werden. 

Vorteil: Beste Nutzung der drei Leuchten. Außerdem wird vermieden, dass versehentlich der Schalter betätigt wird und die HUE Lampe keinen Strom hat - somit nicht mehr schaltbar ist (das typische Philips Hue Problem).

## Physische Installation der Shelly durch Elektriker.
Das Shelly1 Relais wird in die Lichtschalter-Unterputzdose verbaut. [Anleitung](https://www.youtube.com/watch?v=N25PJ8uLceg)

Das Shelly2.5 Relais wird analog verbaut. [Anleitung](https://www.youtube.com/watch?v=_DEqoUHP0IM)
Die beiden L Anschlusse werden intern überbrückt. 

## Software Installation für Node-RED
RedMatic (Node-RED) auf der CCU und MQTT für die Shelly's Integration. Die Shelly App bzw. die Shelly Cloud wird nicht genutzt. 

MQTT wird in diesem Video gut erläutert: [Shelly MQTT](https://www.youtube.com/watch?v=KQA70lZCccI)

1. Installation RedMatic
2. Als MQTT Broker/Server: node-red-contrib-aedes oder Mosquito, Homematic MQTT Add on, ... 
3. Homematic IP Scripte um die Kanäle für die Homematic IP Schalter zu aktivieren

Hier sind die Flows und Settings für die 3 Beispiele.
