Shelly Relais sind kostengünstige Relais (10 Euro), die in Unterputzdosen verbaut werden. 
Sie können über WLAN (REST API, MQTT) in die Hausautomation (ioBroker, FHEM, Node-RED, Alexa, ...) eingebunden werden.

Voraussetzungen: Freien Platz und Strom (Phase, Nulleiter) in der Lichtschalter-Unterputzdose 

Welche Modelle gibt es: [Shelly homepage](https://shelly.cloud/)

## Meine Einsatzbereiche

### 1. Standard Lichtschalter mit standard LED Leuchte: Shelly 1
Die LED Leuchte wird über RedMatic und Alexa geschaltet. Der vorhandene Lichtschalter ist weiterhin funktionsfähig.

Vorteil: Automation zu geringen Kosten.

### 2. Homematic IP 2-fach Lichtschalter mit Standard LED Leuchte: Shelly 2.5
Da nicht genügend Platz in der Lichtschalter-Unterputzdose vorhanden war, wurde der Lichtschalter ausgebaut und durch einen Homematic IP 2-fach Schalter ersetzt. Dieser steuert das Deckenlicht und die Spiegelampe. Das Deckenlicht wird zusätzlich über einen Präsenzmelder und Alexa Kommandos aktiviert.

Vorteil: Automation mit Präsenzmelder und Alexa.

### 3. Homematic IP 6-fach Lichtschalter mit 3 Philips HUE Leuchten: Shelly 1 
Es ist eine Leuchtenleiste mit drei Leuchten installiert. Je nach Nutzung wird nur eine oder mehrere Leuchten eingeschaltet - auch gedimmt (Hue Szenen)
Über den 6-fach Schalter können die einzelnen Leuchten geschaltet plus Szenen aktiviert werden. 

Vorteil: Beste Nutzung der drei Leuchten. Außerdem wird vermieden, dass versehentlich der Schalter betätigt wird und die HUE Lampe keinen Strom hat - somit nicht mehr schaltbar ist (das typische Philips Hue Problem).

## Physische Installation der Shelly durch Elektriker.
Das Shelly1 Relais wird in die Lichtschalter-Unterputzdose verbaut. [Anleitung](https://www.youtube.com/watch?v=N25PJ8uLceg)

Das Shelly2.5 Relais wird analog verbaut. [Anleitung](https://www.youtube.com/watch?v=_DEqoUHP0IM)
Die beiden L Anschlusse werden intern überbrückt. 

## Software Installation für RedMatic (Node-RED) und MQTT
Die Shelly App bzw. die Shelly Cloud wird nicht genutzt. 

MQTT wird in diesem Video gut erläutert: [Shelly MQTT](https://www.youtube.com/watch?v=KQA70lZCccI)

1. Installation RedMatic
2. Als MQTT Broker/Server: node-red-contrib-aedes oder Mosquito, Homematic MQTT Add on, ... 
3. Homematic IP Scripte um die Kanäle für die Homematic IP Schalter zu aktivieren

### Settings und flows
Beispiel 1

Settings:  
* POWER ON DEFAULT MODE: Restore last mode
* BUTTON TYPE: Edge Switch

Internet & Security
* WIFI MODE - CLIENT: yes, mein WLAN, IP statisch: 192.168.178.204
* ADVANCED - DEVELOPER SETTINGS: Enable MQTT, 192.168.178.25:1883
* CLOUD: Disabled

Flow: `[{"id":"e2f04485.a54c48","type":"mqtt in","z":"4a59ce31.c7bf3","name":"","topic":"shellies/shelly1-A4CF12F4221F/relay/0","qos":"2","datatype":"auto","broker":"608a29e6.968158","x":191,"y":2002,"wires":[["22099828.e20a88"]]},{"id":"22099828.e20a88","type":"rbe","z":"4a59ce31.c7bf3","name":"","func":"rbe","gap":"","start":"","inout":"out","property":"payload","x":415,"y":2002,"wires":[["39352df4.5fed22","ecd480eb.1ccd3"]]},{"id":"39352df4.5fed22","type":"ui_switch","z":"4a59ce31.c7bf3","name":"","label":"Büro","tooltip":"","group":"4cbff0bc.b38a3","order":5,"width":3,"height":1,"passthru":false,"decouple":"true","topic":"","style":"","onvalue":"on","onvalueType":"str","onicon":"wb_incandescent","oncolor":"var(--nr-dashboard-widgetBackgroundColor)","offvalue":"off","offvalueType":"str","officon":"wb_incandescent","offcolor":"var(--nr-dashboard-widgetTextColor)","x":551,"y":2002,"wires":[["34143ad0.ff9336"]]},{"id":"34143ad0.ff9336","type":"mqtt out","z":"4a59ce31.c7bf3","name":"","topic":"shellies/shelly1-A4CF12F4221F/relay/0/command","qos":"2","retain":"","broker":"608a29e6.968158","x":817,"y":2002,"wires":[]},{"id":"608a29e6.968158","type":"mqtt-broker","z":"","name":"ccuBroker","broker":"localhost","port":"1883","clientid":"","usetls":false,"compatmode":false,"keepalive":"60","cleansession":true,"birthTopic":"","birthQos":"0","birthPayload":"","closeTopic":"","closeQos":"0","closePayload":"","willTopic":"","willQos":"0","willPayload":""},{"id":"4cbff0bc.b38a3","type":"ui_group","z":"","name":"Lichter","tab":"7effafe8.b39eb","order":1,"disp":true,"width":"9","collapse":false},{"id":"7effafe8.b39eb","type":"ui_tab","z":"","name":"Leuchten Schalter","icon":"fa-lightbulb-o","order":4,"disabled":false,"hidden":false}]`
