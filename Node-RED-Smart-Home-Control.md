Nutzung des kostenlosen/spendenfinanzierten Service [Node-RED Smart Home Control](https://red.cb-net.co.uk/) zur Anbindung an Alexa (und Google Assistant bzw. Google Home).

# Einrichtung

1) Account Anlegen auf https://red.cb-net.co.uk/new-user und Email Verifizierung durchführen.
2) In Alexa App den Skill `Node-RED Smart Home Control` von cb-net hinzufügen und mit den in Schritt 1 verwendeten Zugangsdaten verbinden.
3) Über den Node-RED Palette Manager die Nodes `node-red-contrib-alexa-smart-home` installieren (siehe [Zusätzliche Nodes installieren](https://github.com/rdmtc/RedMatic/wiki/Node-Installation))

# Geräte Anlegen

Jedes Gerät das man verwenden möchte muss unter https://red.cb-net.co.uk/devices angelegt werden. Danach muss man Alexa mit der Aufforderung "Suche Geräte" (oder über die App) diese neuen Geräte einbinden lassen.

# Beispielflows

* [Fensterkontakt](#Fensterkontakt)
* [Schaltaktor](#Schaltaktor)
* [Rollladen](#Rollladen)
* [Dimmer](#Dimmer)
* [Thermostat](#Thermostat)
* [Keymatic](#Keymatic)
* [Szenen](#Szenen)

## Fensterkontakt

Als Alexa Gerät wird ein "Contact Sensor" verwendet:

![](images/alexa/tfk0.png)



Ein _CCU Value_ Node wird auf den Datenpunkt `STATE` des Kanals 1 des Fensterkontakts konfiguriert:

![](images/alexa/tfk1.png)

Dieser Node gibt je nach Zustand des Fensterkontakts bool `true` oder `false` als `msg.payload` aus. Der Alexa Service erwartet jedoch folgende `msg`: `{"acknowledge": true, "payload": {"state": {"contact": "DETECTED"}}}` bzw. `{"acknowledge": true, "payload": {"state": {"contact": "NOT_DETECTED"}}}`, es ist also eine Transformation der Nachricht notwendig damit diese vom Alexa Node genutzt werden kann. Dies kann mit einem Switch und 2 Change Nodes durchgeführt werden:


![](images/alexa/tfk3.png)


![](images/alexa/tfk4.png)


![](images/alexa/tfk5.png)



Am Ende des Flows kommt der Node _alexa smart home v3 state_ zum Einsatz:

![](images/alexa/tfk2.png)

#### Flow JSON
```
[{"id":"bb53c7a1.97ef48","type":"ccu-value","z":"6946acad.eb0ca4","name":"","iface":"BidCos-RF","channel":"JEQ0001234:1 Fenster Hobbyraum","datapoint":"STATE","mode":"","start":true,"change":true,"cache":true,"queue":false,"on":0,"onType":"undefined","ramp":0,"rampType":"undefined","working":true,"ccuConfig":"","topic":"${CCU}/${Interface}/${channel}/${datapoint}","x":140,"y":100,"wires":[["9ca4689c.4bce18"]]},{"id":"59e1c4a.2fe113c","type":"alexa-smart-home-v3-state","z":"6946acad.eb0ca4","conf":"","device":"10277","name":"Fenster Hobbyraum","x":800,"y":100,"wires":[]},{"id":"9ca4689c.4bce18","type":"switch","z":"6946acad.eb0ca4","name":"true / false","property":"payload","propertyType":"msg","rules":[{"t":"true"},{"t":"else"}],"checkall":"true","repair":false,"outputs":2,"x":350,"y":100,"wires":[["57e1e99e.5fc1f8"],["7bb89d62.7f3b04"]]},{"id":"57e1e99e.5fc1f8","type":"change","z":"6946acad.eb0ca4","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"{\"state\":{\"contact\":\"DETECTED\"}}","tot":"json"},{"t":"set","p":"acknowledge","pt":"msg","to":"true","tot":"bool"}],"action":"","property":"","from":"","to":"","reg":false,"x":540,"y":80,"wires":[["59e1c4a.2fe113c"]]},{"id":"7bb89d62.7f3b04","type":"change","z":"6946acad.eb0ca4","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"{\"state\":{\"contact\":\"NOT_DETECTED\"}}","tot":"json"},{"t":"set","p":"acknowledge","pt":"msg","to":"true","tot":"bool"}],"action":"","property":"","from":"","to":"","reg":false,"x":540,"y":120,"wires":[["59e1c4a.2fe113c"]]}]
```

## Schaltaktor

... todo

#### Flow JSON

```
[{"id":"819a38a8.d26cd8","type":"alexa-smart-home-v3","z":"6946acad.eb0ca4","conf":"e904a268.f4155","device":"10274","acknowledge":true,"name":"Licht Werkstatt","topic":"","x":120,"y":140,"wires":[["7622c428.dad7ac"]]},{"id":"7622c428.dad7ac","type":"switch","z":"6946acad.eb0ca4","name":"\"ON\"/\"OFF\"","property":"payload","propertyType":"msg","rules":[{"t":"eq","v":"ON","vt":"str"},{"t":"else"}],"checkall":"true","repair":false,"outputs":2,"x":310,"y":140,"wires":[["af3ee014.ef269"],["fe2b057b.2cd088"]]},{"id":"af3ee014.ef269","type":"change","z":"6946acad.eb0ca4","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"true","tot":"bool"}],"action":"","property":"","from":"","to":"","reg":false,"x":510,"y":120,"wires":[["25df98dd.64fad8"]]},{"id":"fe2b057b.2cd088","type":"change","z":"6946acad.eb0ca4","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"false","tot":"bool"}],"action":"","property":"","from":"","to":"","reg":false,"x":510,"y":160,"wires":[["25df98dd.64fad8"]]},{"id":"25df98dd.64fad8","type":"ccu-value","z":"6946acad.eb0ca4","name":"","iface":"HmIP-RF","channel":"000D1709A5915B:10 Licht Werkstatt","datapoint":"STATE","mode":"","start":true,"change":true,"cache":true,"queue":false,"on":0,"onType":"undefined","ramp":0,"rampType":"undefined","working":true,"ccuConfig":"38263145.35ea0e","topic":"${CCU}/${Interface}/${channel}/${datapoint}","x":730,"y":140,"wires":[["b6884af3.03f4d8"]]},{"id":"e503e79e.7e0df8","type":"alexa-smart-home-v3-state","z":"6946acad.eb0ca4","conf":"e904a268.f4155","device":"10274","name":"Licht Werkstatt","x":760,"y":240,"wires":[]},{"id":"b6884af3.03f4d8","type":"switch","z":"6946acad.eb0ca4","name":"true / false","property":"payload","propertyType":"msg","rules":[{"t":"true"},{"t":"else"}],"checkall":"true","repair":false,"outputs":2,"x":330,"y":240,"wires":[["4ce3d9ad.cecb08"],["ac028995.e9e1a8"]]},{"id":"4ce3d9ad.cecb08","type":"change","z":"6946acad.eb0ca4","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"{\"state\":{\"power\":\"ON\"}}","tot":"json"},{"t":"set","p":"acknowledge","pt":"msg","to":"true","tot":"bool"}],"action":"","property":"","from":"","to":"","reg":false,"x":520,"y":220,"wires":[["e503e79e.7e0df8"]]},{"id":"ac028995.e9e1a8","type":"change","z":"6946acad.eb0ca4","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"{\"state\":{\"power\":\"OFF\"}}","tot":"json"},{"t":"set","p":"acknowledge","pt":"msg","to":"true","tot":"bool"}],"action":"","property":"","from":"","to":"","reg":false,"x":520,"y":260,"wires":[["e503e79e.7e0df8"]]}]
```

## Rollladen

... todo


## Dimmer

... todo


## Thermostat

... todo


## Keymatic

... todo


## Szenen

... todo