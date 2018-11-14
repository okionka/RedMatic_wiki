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

![image](https://user-images.githubusercontent.com/12692680/48480191-e3437a00-e809-11e8-8a3d-86cca7713c58.png)


## Vorwort

Die hier vorgestellte Lösung ist erstmal nur dazu gedacht das Funktionsprinzip zu erläutern und einen Startpunkt zu erhalten. Daher kann es für den Einzelfall vielleicht "übertrieben" sein die Steuerung sowohl über Zeit als auch Helligkeit zu gestalten. Im in der Praxis muss das damit den gewünschten örtlichen Gegebenheiten angepasst werden.

Beispiel:
  - andere Zeitpunkte, andere Helligkeiten
  - nur Zeit basiert ohne Einbeziehung der Helligkeit 

Weiterhin ließe sich das Problem sicherlich auf den ersten Blick einfacher mit einem Function Node und etwas JavaScript lösen. Die Empfehlung von IBM (der Firma hinter Node-Red) ist es möglichst auf die Function Nodes zu verzichten.

Die Gründe dafür sind:
 - Die Funktion eines Flows erschließt sich viel einfacher mit der Verwendung der Standard Nodes
    - Auch wenn die Flows damit vielleicht nicht so aufgeräumt wirken, kann man die Funktion später viel einfacher nachvollziehen und ändern.
 - Die *Function Nodes* haben gegenüber den Standard Nodes eine schlechtere Performance, da der Javascript Code in einer Sandbox ausgeführt wird.

## Vorbereitung

als Vorbereitung installiert man sich das zusätzliche die Pakete:
 - [node-red-contrib-sun-position](https://flows.nodered.org/node/node-red-contrib-sun-position)
 - [node-red-node-smooth](https://flows.nodered.org/node/node-red-node-smooth).

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

In diesem Beispiel haben wir 3 Flows mit unterschiedlichen Triggern:
  - Klassifizierung der Tageszeit
  - Klassifizierung der Helligkeit
  - Flow zum Schalten

Im folgenden wird die Funktionsweise der 3 Flows erläutert.

### Klassifizierung der Tageszeit

![image](https://user-images.githubusercontent.com/12692680/48412589-66e76300-e745-11e8-9844-e8ee0e183d14.png)

#### Flow zum Import:
```
[{"id":"8de8648b.932458","type":"time-inject","z":"d7bd7fb6.a0c13","name":"","positionConfig":"d9e9ca6a.952218","payload":"Sonnenaufgang","payloadType":"str","topic":"","time":"sunrise","timeType":"pdsTime","timeDays":"*","offset":"-30","offsetMultiplier":60,"property":"","propertyType":"none","timeAlt":"","timeAltType":"entered","timeAltOffset":0,"timeAltOffsetMultiplier":60,"x":1130,"y":260,"wires":[["9d6b34b2.e2ea38"]]},{"id":"9d6b34b2.e2ea38","type":"change","z":"d7bd7fb6.a0c13","name":"Persist as global.dayPeriod","rules":[{"t":"set","p":"dayPeriod","pt":"global","to":"payload","tot":"msg"}],"action":"","property":"","from":"","to":"","reg":false,"x":1540,"y":340,"wires":[["572fa036.14429"]]},{"id":"deb7e8e2.865da8","type":"time-inject","z":"d7bd7fb6.a0c13","name":"","positionConfig":"d9e9ca6a.952218","payload":"Tag","payloadType":"str","topic":"","time":"sunriseEnd","timeType":"pdsTime","timeDays":"*","offset":0,"offsetMultiplier":60,"property":"","propertyType":"none","timeAlt":"","timeAltType":"entered","timeAltOffset":0,"timeAltOffsetMultiplier":60,"x":1100,"y":320,"wires":[["9d6b34b2.e2ea38"]]},{"id":"5a609b8c.6ce964","type":"time-inject","z":"d7bd7fb6.a0c13","name":"","positionConfig":"d9e9ca6a.952218","payload":"Sonnenuntergang","payloadType":"str","topic":"","time":"sunset","timeType":"pdsTime","timeDays":"*","offset":0,"offsetMultiplier":60,"property":"","propertyType":"none","timeAlt":"","timeAltType":"entered","timeAltOffset":0,"timeAltOffsetMultiplier":60,"x":1130,"y":380,"wires":[["9d6b34b2.e2ea38"]]},{"id":"54fdf606.03dd98","type":"time-inject","z":"d7bd7fb6.a0c13","name":"","positionConfig":"d9e9ca6a.952218","payload":"Morgendämmerung","payloadType":"str","topic":"","time":"dawn","timeType":"pdsTime","timeDays":"*","offset":0,"offsetMultiplier":60,"property":"","propertyType":"none","timeAlt":"","timeAltType":"entered","timeAltOffset":0,"timeAltOffsetMultiplier":60,"x":1140,"y":200,"wires":[["9d6b34b2.e2ea38"]]},{"id":"79030ca5.4518b4","type":"time-inject","z":"d7bd7fb6.a0c13","name":"","positionConfig":"d9e9ca6a.952218","payload":"Abenddämmerung","payloadType":"str","topic":"","time":"dusk","timeType":"pdsTime","timeDays":"*","offset":0,"offsetMultiplier":60,"property":"","propertyType":"none","timeAlt":"","timeAltType":"entered","timeAltOffset":0,"timeAltOffsetMultiplier":60,"x":1130,"y":440,"wires":[["9d6b34b2.e2ea38"]]},{"id":"ac053b69.3061d8","type":"time-inject","z":"d7bd7fb6.a0c13","name":"","positionConfig":"d9e9ca6a.952218","payload":"Nacht","payloadType":"str","topic":"","time":"nauticalDusk","timeType":"pdsTime","timeDays":"*","offset":0,"offsetMultiplier":60,"property":"","propertyType":"none","timeAlt":"","timeAltType":"entered","timeAltOffset":0,"timeAltOffsetMultiplier":60,"x":1120,"y":500,"wires":[["9d6b34b2.e2ea38"]]},{"id":"572fa036.14429","type":"link out","z":"d7bd7fb6.a0c13","name":"chg-dayPeriod","links":[],"x":1755,"y":340,"wires":[]},{"id":"d9e9ca6a.952218","type":"position-config","z":"","name":"Entenhausen","longitude":"13.72324","latitude":"51.12381","angleType":"deg"}]
```

#### Erläuterung des Flows

##### time-inject Nodes
Der Flow wird durch die spezielle Inject Nodes getriggert. Diese starten jewels zum angegebenen Zeitpunkt den Flow gleich mit entsprechendem Payload.

Einstellungen der time-inject nodes:

![image](https://user-images.githubusercontent.com/12692680/48479542-ef2e3c80-e807-11e8-882d-2c1d71b429b5.png)


Bei der Position kann einmalig die GPS Koordinaten zu hinterlegen und das gewünschte Format für die Winkelangaben:

![image](https://user-images.githubusercontent.com/12692680/48474045-06662d80-e7fa-11e8-875b-881db9b7482b.png)

Unter Payload stellt man den Payload der Nachricht ein, die gesendet werden soll. In diesem Falle ist das der name der Tageszeit.

![image](https://user-images.githubusercontent.com/12692680/48479628-2a307000-e808-11e8-8dfd-7840a4bd7996.png)

Als Zeit wählt man den gewünschten Start-Zeitpunkt der Tageszeit. Hier kann man mit einem positiven oder negativen Offset arbeiten. Über die Wahl der Tage kann man einstellen für welche Tage die Zeit gilt. Damit ist es möglich getrennte Trigger mit unterschiedlichen Zeiten für Wochenende/Wochentage anzulegen.

![image](https://user-images.githubusercontent.com/12692680/48479641-35839b80-e808-11e8-9bf1-bbfce3bf3d31.png)

Die zusätzlichen Einstellungen (falls vorhanden) lässt man erstmal wie diese sind.

##### Change Node

Der Change Node dient zum persistenten abspeichern des aktuellen Tageszeit. Dazu wird der in der Nachricht enthaltene payload auf einen globalen Parameter abgespeichert.

![image](https://user-images.githubusercontent.com/12692680/48479788-9f9c4080-e808-11e8-9f0e-07df482eabe7.png)

anstelle global (für alle Reiter) kann man Einstellungen der aktuellen Nachricht verändern (msg.) oder nur lokal für den aktuellen Reiter (flow.)

![image](https://user-images.githubusercontent.com/12692680/48479825-b80c5b00-e808-11e8-916f-ba476049b9ab.png)

### Klassifizierung der Helligkeit

![image](https://user-images.githubusercontent.com/12692680/48420297-5d1c2a80-e75a-11e8-91ad-cb8a1096b751.png)

#### Flow zum Import:
```
[{"id":"e15b0c08.ecb44","type":"debug","z":"d7bd7fb6.a0c13","name":"Sonnenintensität","active":true,"tosidebar":false,"console":false,"tostatus":true,"complete":"payload","x":2930,"y":260,"wires":[]},{"id":"ab495667.c3d4e8","type":"link out","z":"d7bd7fb6.a0c13","name":"chg-sunIntensity","links":[],"x":2735,"y":320,"wires":[]},{"id":"dcb5bc25.8fc86","type":"comment","z":"d7bd7fb6.a0c13","name":"chg-SunIntensity.type","info":"","x":2940,"y":320,"wires":[]},{"id":"3ea055c8.b7510a","type":"ccu-value","z":"d7bd7fb6.a0c13","name":"Lichtsensor","iface":"","channel":"JPLIO00001:1 K30_810_Lichtsensor","datapoint":"LUX","mode":"","start":true,"change":true,"cache":true,"on":0,"onType":"undefined","ramp":0,"rampType":"undefined","working":false,"ccuConfig":"78742432.c6d88c","topic":"ccu/system/info/sun/intensity/lightN","x":2030,"y":200,"wires":[["5b3d4e4c.203d8"]]},{"id":"dbc9afc7.f819","type":"change","z":"d7bd7fb6.a0c13","name":"","rules":[{"t":"set","p":"#:(memory)::sunIntensity","pt":"global","to":"payload","tot":"msg"}],"action":"","property":"","from":"","to":"","reg":false,"x":2680,"y":260,"wires":[["e15b0c08.ecb44","e53c6626.f79618"]]},{"id":"5069726a.50143c","type":"switch","z":"d7bd7fb6.a0c13","name":"","property":"payload","propertyType":"msg","rules":[{"t":"lte","v":"0","vt":"num"},{"t":"lte","v":"160","vt":"num"},{"t":"lte","v":"650","vt":"num"},{"t":"lte","v":"3500","vt":"num"},{"t":"lte","v":"10500","vt":"num"},{"t":"else"}],"checkall":"false","repair":false,"outputs":6,"x":2190,"y":260,"wires":[["c131def3.5d9f8"],["76083db9.4514b4"],["c37ef4b9.b759b8"],["c45402d4.a8484"],["86fb0a74.233978"],["55d021b5.21566"]]},{"id":"c131def3.5d9f8","type":"change","z":"d7bd7fb6.a0c13","name":"tiefschwarz","rules":[{"t":"set","p":"payload","pt":"msg","to":"tiefschwarz","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":2390,"y":160,"wires":[["dbc9afc7.f819"]]},{"id":"76083db9.4514b4","type":"change","z":"d7bd7fb6.a0c13","name":"finster","rules":[{"t":"set","p":"payload","pt":"msg","to":"finster","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":2370,"y":200,"wires":[["dbc9afc7.f819"]]},{"id":"c37ef4b9.b759b8","type":"change","z":"d7bd7fb6.a0c13","name":"stockdunkel","rules":[{"t":"set","p":"payload","pt":"msg","to":"stockdunkel","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":2390,"y":240,"wires":[["dbc9afc7.f819"]]},{"id":"c45402d4.a8484","type":"change","z":"d7bd7fb6.a0c13","name":"dunkel","rules":[{"t":"set","p":"payload","pt":"msg","to":"dunkel","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":2370,"y":280,"wires":[["dbc9afc7.f819"]]},{"id":"86fb0a74.233978","type":"change","z":"d7bd7fb6.a0c13","name":"halbdunkel","rules":[{"t":"set","p":"payload","pt":"msg","to":"halbdunkel","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":2390,"y":320,"wires":[["dbc9afc7.f819"]]},{"id":"55d021b5.21566","type":"change","z":"d7bd7fb6.a0c13","name":"hell","rules":[{"t":"set","p":"payload","pt":"msg","to":"hell","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":2370,"y":360,"wires":[["dbc9afc7.f819"]]},{"id":"e53c6626.f79618","type":"rbe","z":"d7bd7fb6.a0c13","name":"","func":"rbe","gap":"","start":"","inout":"out","property":"payload","x":2630,"y":320,"wires":[["ab495667.c3d4e8"]]},{"id":"5b3d4e4c.203d8","type":"smooth","z":"d7bd7fb6.a0c13","name":"","property":"payload","action":"max","count":"6","round":"","mult":"multi","x":2020,"y":260,"wires":[["5069726a.50143c"]]},{"id":"78742432.c6d88c","type":"ccu-connection","z":"","name":"Homematic-Dummy","host":"localhost","regaEnabled":false,"bcrfEnabled":true,"iprfEnabled":false,"virtEnabled":false,"bcwiEnabled":false,"cuxdEnabled":false,"regaPoll":false,"regaInterval":"120","rpcPingTimeout":"60","rpcInitAddress":"127.0.0.51","rpcServerHost":"172.20.51.58","rpcBinPort":"2047","rpcXmlPort":"2048","contextStore":"memory"}]
```

#### Erläuterung des Flows

Für die Bestimmung der Helligkeit wird der der Messwert des Lichtsensors verwendet und ebenfalls in eine Klassifizierung übernommen.

Um zu verhindern das sich das Ergebnis bei kurzfristiger Änderung der Helligkeit verändert (Wolke vor der Sonne) wurde die Smooth Node zur Glättung der Ergebnisse vorgeschaltet. In die Beispiel wird der maximalwert der letzten 6 Messwerte ausgegeben:

![image](https://user-images.githubusercontent.com/12692680/48480567-32d67580-e80b-11e8-94f4-6e211f180cbb.png)

Die switch node dient dazu den Flow anhand verschiedener Messwerte zu "verzweigen". Es ist zu beachten, das im unteren bereich der EInstellungen das Verhalten der switch node auf "stopping after first match" umgestellt wird. Damit wird sichergestellt das eine Nachricht nur an **einen** Ausgang gesendet wird. Ist dies auf **checking all rules** gesetzt wird die nachricht an alle ausgänge für welche die bedingung zutrifft gesendet. Im Beispiel der Einstellung "otherwise" immer an den entsprechenden Ausgang.

Der Link am Ende wird erstmal nicht genutzt. Dieser dient dazu andere Flows bei Änderung der Tageszeit zu "triggern". Damit kann man beispielsweise Rollläden automatisch steuern.

![image](https://user-images.githubusercontent.com/12692680/48480710-95c80c80-e80b-11e8-8545-9aca4e36da33.png)

über die change Nodes wird einfach der Wert des payload verändert und im nachgelagerten change node auf eine globale Variable gespeichert.

![image](https://user-images.githubusercontent.com/12692680/48480874-066f2900-e80c-11e8-82c5-9a089733cedb.png)

Das ließe sich vereinfachen indem man gleich den Wert auf die globalen Variable (context) speichert. Die Implementierung hier ist so gewählt worden um ebenfalls mit einem nachgelagerten link node bei Änderung des Helligkeitsverlaufes andere Flows triggern zu können. Der rbe Node dient dazu die Nachricht nur bei einer wirklichen Änderung weiterzuleiten.

### Flow zum Schalten

![image](https://user-images.githubusercontent.com/12692680/48480191-e3437a00-e809-11e8-8a3d-86cca7713c58.png)


#### Flow zum Import:

```
[{"id":"a2c8adce.7a01e","type":"ccu-value","z":"d7bd7fb6.a0c13","name":"Bewegungsmelder","iface":"","channel":"JPLIO00006:1","datapoint":"MOTION","mode":"","start":true,"change":true,"cache":false,"on":0,"onType":"undefined","ramp":0,"rampType":"undefined","working":false,"ccuConfig":"78742432.c6d88c","topic":"${CCU}/${Interface}/${channel}/${datapoint}","x":1130,"y":660,"wires":[["3594cf09.7eba7"]]},{"id":"3594cf09.7eba7","type":"switch","z":"d7bd7fb6.a0c13","name":"TREPPE_AUTOMATIK","property":"TREPPE_AUTOMATIK","propertyType":"flow","rules":[{"t":"true"},{"t":"else"}],"checkall":"false","repair":false,"outputs":2,"x":1390,"y":660,"wires":[["573d29ad.2b90a8"],[]]},{"id":"cd1161c6.a62e3","type":"inject","z":"d7bd7fb6.a0c13","name":"","topic":"","payload":"true","payloadType":"bool","repeat":"","crontab":"","once":false,"onceDelay":0.1,"x":1090,"y":760,"wires":[["c98e0564.0cef88"]]},{"id":"dd77f2a8.b8904","type":"inject","z":"d7bd7fb6.a0c13","name":"","topic":"","payload":"true","payloadType":"bool","repeat":"","crontab":"","once":false,"onceDelay":0.1,"x":1090,"y":880,"wires":[["6ee57f47.8a331"]]},{"id":"35cbc477.9cfc8c","type":"ccu-value","z":"d7bd7fb6.a0c13","name":"Taster1","iface":"","channel":"JPLIO00006:1","datapoint":"PRESS_SHORT","mode":"","start":true,"change":true,"cache":false,"on":0,"onType":"undefined","ramp":0,"rampType":"undefined","working":false,"ccuConfig":"78742432.c6d88c","topic":"${CCU}/${Interface}/${channel}/${datapoint}","x":1100,"y":800,"wires":[["c98e0564.0cef88"]]},{"id":"4511c81f.547d78","type":"ccu-value","z":"d7bd7fb6.a0c13","name":"Taster2","iface":"","channel":"JPLIO00009:1","datapoint":"PRESS_SHORT","mode":"","start":true,"change":true,"cache":false,"on":0,"onType":"undefined","ramp":0,"rampType":"undefined","working":false,"ccuConfig":"78742432.c6d88c","topic":"${CCU}/${Interface}/${channel}/${datapoint}","x":1100,"y":920,"wires":[["6ee57f47.8a331"]]},{"id":"c98e0564.0cef88","type":"change","z":"d7bd7fb6.a0c13","name":"flow.TREPPE_AUTOMATIK = true","rules":[{"t":"set","p":"TREPPE_AUTOMATIK","pt":"flow","to":"true","tot":"bool"}],"action":"","property":"","from":"","to":"","reg":false,"x":1400,"y":760,"wires":[[]]},{"id":"6ee57f47.8a331","type":"change","z":"d7bd7fb6.a0c13","name":"flow.TREPPE_AUTOMATIK = false","rules":[{"t":"set","p":"TREPPE_AUTOMATIK","pt":"flow","to":"true","tot":"bool"}],"action":"","property":"","from":"","to":"","reg":false,"x":1400,"y":900,"wires":[[]]},{"id":"573d29ad.2b90a8","type":"switch","z":"d7bd7fb6.a0c13","name":"is true","property":"payload","propertyType":"msg","rules":[{"t":"true"},{"t":"else"}],"checkall":"true","repair":false,"outputs":2,"x":1610,"y":660,"wires":[["b5c5e3f5.eb27d"],["7b8d7767.c1f078"]]},{"id":"b5c5e3f5.eb27d","type":"switch","z":"d7bd7fb6.a0c13","name":"dayPeriod","property":"dayPeriod","propertyType":"global","rules":[{"t":"eq","v":"Morgendämmerung","vt":"str"},{"t":"eq","v":"Sonnenaufgang","vt":"str"},{"t":"eq","v":"Tag","vt":"str"},{"t":"eq","v":"Sonnenuntergang","vt":"str"},{"t":"eq","v":"Abenddämmerung","vt":"str"},{"t":"else"}],"checkall":"false","repair":false,"outputs":6,"x":1780,"y":580,"wires":[["1e31fc2e.515da4"],["1e31fc2e.515da4"],["d6334be4.f24768"],["1e31fc2e.515da4"],["1e31fc2e.515da4"],["5154cd32.e0a874"]]},{"id":"d6334be4.f24768","type":"change","z":"d7bd7fb6.a0c13","name":"100%","rules":[{"t":"set","p":"payload","pt":"msg","to":"1","tot":"num"}],"action":"","property":"","from":"","to":"","reg":false,"x":2150,"y":600,"wires":[["6b1dd258.71ebbc"]]},{"id":"1e31fc2e.515da4","type":"change","z":"d7bd7fb6.a0c13","name":"75%","rules":[{"t":"set","p":"payload","pt":"msg","to":"0.75","tot":"num"}],"action":"","property":"","from":"","to":"","reg":false,"x":2150,"y":640,"wires":[["6b1dd258.71ebbc"]]},{"id":"b4465a88.e29268","type":"change","z":"d7bd7fb6.a0c13","name":"50%","rules":[{"t":"set","p":"payload","pt":"msg","to":"0.5","tot":"num"}],"action":"","property":"","from":"","to":"","reg":false,"x":2150,"y":680,"wires":[["6b1dd258.71ebbc"]]},{"id":"6b1dd258.71ebbc","type":"ccu-value","z":"d7bd7fb6.a0c13","name":"Lampe Treppe","iface":"","channel":"JPLIO00005:1","datapoint":"STATE","mode":"","start":true,"change":true,"cache":false,"on":0,"onType":"undefined","ramp":0,"rampType":"undefined","working":false,"ccuConfig":"78742432.c6d88c","topic":"${CCU}/${Interface}/${channel}/${datapoint}","x":2380,"y":720,"wires":[[]]},{"id":"7b8d7767.c1f078","type":"delay","z":"d7bd7fb6.a0c13","name":"","pauseType":"delay","timeout":"10","timeoutUnits":"minutes","rate":"1","nbRateUnits":"1","rateUnits":"second","randomFirst":"1","randomLast":"5","randomUnits":"seconds","drop":false,"x":1790,"y":820,"wires":[["228171e5.567e0e"]]},{"id":"228171e5.567e0e","type":"change","z":"d7bd7fb6.a0c13","name":"aus","rules":[{"t":"set","p":"payload","pt":"msg","to":"0","tot":"num"}],"action":"","property":"","from":"","to":"","reg":false,"x":1970,"y":820,"wires":[["6b1dd258.71ebbc"]]},{"id":"5154cd32.e0a874","type":"switch","z":"d7bd7fb6.a0c13","name":"sunIntensity","property":"sunIntensity","propertyType":"global","rules":[{"t":"eq","v":"tiefschwarz","vt":"str"},{"t":"eq","v":"finster","vt":"str"},{"t":"eq","v":"stockdunkel","vt":"str"},{"t":"eq","v":"dunkel","vt":"str"},{"t":"eq","v":"halbdunkel","vt":"str"},{"t":"else"}],"checkall":"false","repair":false,"outputs":6,"x":1950,"y":700,"wires":[["d6334be4.f24768"],["d6334be4.f24768"],["1e31fc2e.515da4"],["b4465a88.e29268"],["b4465a88.e29268"],[]]},{"id":"78742432.c6d88c","type":"ccu-connection","z":"","name":"Homematic-Dummy","host":"localhost","regaEnabled":false,"bcrfEnabled":true,"iprfEnabled":false,"virtEnabled":false,"bcwiEnabled":false,"cuxdEnabled":false,"regaPoll":false,"regaInterval":"120","rpcPingTimeout":"60","rpcInitAddress":"127.0.0.51","rpcServerHost":"172.20.51.58","rpcBinPort":"2047","rpcXmlPort":"2048","contextStore":"memory"}]
```

#### Erläuterung des Flows

die beiden kleineren Flows zum setzen des Automaic Modus sind recht einfach aufgebaut:

![image](https://user-images.githubusercontent.com/12692680/48487888-c6b23c80-e81f-11e8-84ea-486e234363cf.png)

Diese setzen eine lokale flow variable (für den aktuellen Reiter gültig) auf den Wert true oder false:

![image](https://user-images.githubusercontent.com/12692680/48487835-aa160480-e81f-11e8-86a1-901702f43e19.png)

Davon abhängig wird im eigentlichen Flow zum Schalten der Lampe über den switch Node abgefragt welchen Wert diese variable besitzt.

#### Konfiguration des Trigger

### Ablauf steuern

### Ablauf verändern

### Aktion ausführen

### Abschluss
Ist dies erledigt, wird diese Änderung aktiviert mittels des Deploy Buttons:    
![image](https://user-images.githubusercontent.com/12692680/44590937-962caa80-a7bc-11e8-9df3-592da55d8098.png)

### Flows als Download
