---
Title: E3DC Anbindung per Modbus-TCP
Category: Von Usern bereitgestellte Flows
---

* [Einleitung](#einleitung)
  * [E3DC S10 Dashboard](#e3dc-s10-dashboard)
  * [HomeMatic Systemvariablen](#homematic-systemvariablen)
* [Installation](#installation)
  * [Modul installieren](#modul-installieren)
  * [Flow importieren](#flow-importieren)
  * [Modbus einrichten](#modbus-einrichten)
  * [Systemvariablen anpassen](#systemvariablen-anpassen)
  * [Implementieren](#implementieren)
* [Infos](#infos)
  * [Modbus am S10](#modbus-am-s10)
  * [Modbus Register](#modbus-register)
  * [Register umrechnen](#register-umrechnen)
  * [Leistungswerte umrechnen](#leistungswerte-umrechnen)
  * [Reconnect Interval](#reconnect-interval)
  * [Besonderheit E3DC Modbus](#besonderheit-e3dc-modbus)

## Einleitung

Hier ein Beispiel mit dem ein E3DC Hauskraftwerk in RedMatic integriert werden kann. Die Verbindung zum S10 Stromspeicher wird per Modbus-TCP hergestellt. Die abgefragten Leistungswerte, werden im Dashboard dargestellt und in entsprechende Systemvariablen der HomeMatic eingetragen.

### E3DC S10 Dashboard

![](https://user-images.githubusercontent.com/19279623/65816852-3d221800-e201-11e9-9365-6cef67817fe6.png)

### HomeMatic Systemvariablen

![](https://user-images.githubusercontent.com/19279623/65816885-870afe00-e201-11e9-8e4d-da582570c37d.png)

## Installation

### Modul installieren

unter [Zusätzliche Node-RED Nodes installieren](https://github.com/hobbyquaker/RedMatic/wiki/Node-Installation) ist beschrieben wie weitere Nodes installiert werden können. Hier installieren Sie Bitte den node `node-red-contrib-modbustcp`.

### Flow importieren

importieren Sie den folgenden Flow wie unter [Flows importieren](https://github.com/hobbyquaker/RedMatic/wiki/Flow-Import) beschrieben:

    [{"id":"e144f16b.b96","type":"tab","label":"E3/DC S10","disabled":false,"info":""},{"id":"92aca437.787ca8","type":"ccu-sysvar","z":"e144f16b.b96","name":"Modbus Home","ccuConfig":"38263145.35ea0e","topic":"ReGaHSS/${Name}","change":true,"cache":true,"x":920,"y":580,"wires":[[]]},{"id":"3f875bb.ff24624","type":"ccu-sysvar","z":"e144f16b.b96","name":"Modbus PV","ccuConfig":"38263145.35ea0e","topic":"ReGaHSS/${Name}","change":true,"cache":true,"x":910,"y":720,"wires":[[]]},{"id":"f545ba64.1656","type":"ccu-sysvar","z":"e144f16b.b96","name":"Modbus SOC","ccuConfig":"38263145.35ea0e","topic":"ReGaHSS/${Name}","change":true,"cache":true,"x":920,"y":1220,"wires":[[]]},{"id":"3f480d54.b9fbb2","type":"ui_gauge","z":"e144f16b.b96","name":"Hausverbrauch","group":"333e915b.9ccd5e","order":0,"width":"6","height":"6","gtype":"gage","title":"Leistung","label":"Watt","format":"{{value}}","min":0,"max":"4000","colors":["#00B500","#E6E600","#CA3838"],"seg1":"800","seg2":"2000","x":660,"y":500,"wires":[]},{"id":"6f378821.c8d2c8","type":"ui_gauge","z":"e144f16b.b96","name":"PV-Leistung","group":"6ba71bdd.5e7c44","order":0,"width":"6","height":"6","gtype":"gage","title":"Leistung","label":"Watt","format":"{{value}}","min":0,"max":"5000","colors":["#CA3838","#E6E600","#00B500"],"seg1":"800","seg2":"2000","x":650,"y":640,"wires":[]},{"id":"8040ad1a.02c3e","type":"ui_gauge","z":"e144f16b.b96","name":"Batterie-SOC","group":"e3817d3.76e","order":0,"width":"6","height":"6","gtype":"donut","title":"Füllstand","label":"%","format":"{{value}}","min":0,"max":"100","colors":["#CA3838","#E6E600","#00B500"],"seg1":"10","seg2":"50","x":660,"y":1140,"wires":[]},{"id":"9d29e28.5de362","type":"ui_chart","z":"e144f16b.b96","name":"Hausverbrauch","group":"333e915b.9ccd5e","order":0,"width":"6","height":"6","label":"Tag","chartType":"line","legend":"false","xformat":"HH:mm","interpolate":"linear","nodata":"wait ModBus","dot":false,"ymin":"0","ymax":"4000","removeOlder":1,"removeOlderPoints":"","removeOlderUnit":"86400","cutout":0,"useOneColor":false,"colors":["#D62728","#AEC7E8","#FF7F0E","#2CA02C","#98DF8A","#D62728","#FF9896","#9467BD","#C5B0D5"],"useOldStyle":false,"outputs":1,"x":660,"y":540,"wires":[[]]},{"id":"bd235f4c.a17278","type":"ui_chart","z":"e144f16b.b96","name":"PV-Leistung","group":"6ba71bdd.5e7c44","order":0,"width":"6","height":"6","label":"Tag","chartType":"line","legend":"false","xformat":"HH:mm","interpolate":"linear","nodata":"wait ModBus","dot":false,"ymin":"0","ymax":"5000","removeOlder":1,"removeOlderPoints":"","removeOlderUnit":"86400","cutout":0,"useOneColor":false,"colors":["#E6E600","#AEC7E8","#FF7F0E","#2CA02C","#98DF8A","#D62728","#FF9896","#9467BD","#C5B0D5"],"useOldStyle":false,"outputs":1,"x":650,"y":680,"wires":[[]]},{"id":"81d86ab8.a532f8","type":"ui_chart","z":"e144f16b.b96","name":"Batterie-SOC","group":"e3817d3.76e","order":0,"width":"6","height":"6","label":"Tag","chartType":"line","legend":"false","xformat":"HH:mm","interpolate":"linear","nodata":"wait ModBus","dot":false,"ymin":"0","ymax":"100","removeOlder":1,"removeOlderPoints":"","removeOlderUnit":"86400","cutout":0,"useOneColor":false,"colors":["#3ADF00","#AEC7E8","#FF7F0E","#2CA02C","#98DF8A","#D62728","#FF9896","#9467BD","#C5B0D5"],"useOldStyle":false,"outputs":1,"x":660,"y":1180,"wires":[[]]},{"id":"752e3d82.1f9264","type":"ui_gauge","z":"e144f16b.b96","name":"Batterieleistung","group":"a45e2e06.0d4a78","order":0,"width":"6","height":"6","gtype":"gage","title":"Leistung","label":"Watt","format":"{{value}}","min":"-3000","max":"3000","colors":["#CA3838","#B4B4B4","#00B500"],"seg1":"-20","seg2":"20","x":660,"y":960,"wires":[]},{"id":"36ef8f9a.e6a2","type":"ui_chart","z":"e144f16b.b96","name":"Batterieleistung","group":"a45e2e06.0d4a78","order":0,"width":"6","height":"6","label":"Batterieleistung","chartType":"line","legend":"false","xformat":"HH:mm","interpolate":"linear","nodata":"wait ModBus","dot":false,"ymin":"-3000","ymax":"3000","removeOlder":1,"removeOlderPoints":"","removeOlderUnit":"86400","cutout":0,"useOneColor":false,"colors":["#98DF8A","#AEC7E8","#FF7F0E","#2CA02C","#98DF8A","#D62728","#FF9896","#9467BD","#C5B0D5"],"useOldStyle":false,"outputs":1,"x":660,"y":1000,"wires":[[]]},{"id":"57d47377.7a09d4","type":"ccu-sysvar","z":"e144f16b.b96","name":"Modbus Entladen","ccuConfig":"38263145.35ea0e","topic":"ReGaHSS/${Name}","change":true,"cache":true,"x":930,"y":1080,"wires":[[]]},{"id":"98102a72.7df3b8","type":"ccu-sysvar","z":"e144f16b.b96","name":"Modbus Laden","ccuConfig":"38263145.35ea0e","topic":"ReGaHSS/${Name}","change":true,"cache":true,"x":920,"y":1020,"wires":[[]]},{"id":"b2e8c263.148b7","type":"function","z":"e144f16b.b96","name":"Umrechnen","func":"var energie = msg.payload;\nmsg1 = {};\nmsg2 = {};\nmsg3 = {};\nmsg1.payload = energie;\nif (energie >= 0){\n    msg2.payload = energie;\n    msg3.payload = 0;\n}\nelse{\n    var pos = energie * -1;\n    msg2.payload = 0;\n    msg3.payload = pos;\n}\nreturn [msg1,msg2,msg3];","outputs":3,"noerr":0,"x":390,"y":840,"wires":[["6f98e500.72f1ac","cd057216.b0053"],["a8546f39.5c1ad8"],["33962974.799d9e"]],"outputLabels":["Netzleistung","Bezug","Einspeisung"]},{"id":"6f98e500.72f1ac","type":"ui_gauge","z":"e144f16b.b96","name":"Netzleistung","group":"90b2f9ee.0bf5e","order":0,"width":"6","height":"6","gtype":"gage","title":"Leistung","label":"Watt","format":"{{value}}","min":"-4000","max":"4000","colors":["#58ACFA","#81F781","#FAAC58"],"seg1":"-40","seg2":"40","x":650,"y":780,"wires":[]},{"id":"cd057216.b0053","type":"ui_chart","z":"e144f16b.b96","name":"Netzleistung","group":"90b2f9ee.0bf5e","order":0,"width":"6","height":"6","label":"Tag","chartType":"line","legend":"false","xformat":"HH:mm","interpolate":"linear","nodata":"wait ModBus","dot":false,"ymin":"-3000","ymax":"3000","removeOlder":1,"removeOlderPoints":"","removeOlderUnit":"86400","cutout":0,"useOneColor":false,"colors":["#AEC7E8","#AEC7E8","#FF7F0E","#2CA02C","#98DF8A","#D62728","#FF9896","#9467BD","#C5B0D5"],"useOldStyle":false,"outputs":1,"x":650,"y":820,"wires":[[]]},{"id":"33962974.799d9e","type":"ccu-sysvar","z":"e144f16b.b96","name":"Modbus Einspeisung","ccuConfig":"38263145.35ea0e","topic":"ReGaHSS/${Name}","change":true,"cache":true,"x":940,"y":900,"wires":[[]]},{"id":"a8546f39.5c1ad8","type":"ccu-sysvar","z":"e144f16b.b96","name":"Modbus Bezug","ccuConfig":"38263145.35ea0e","topic":"ReGaHSS/${Name}","change":true,"cache":true,"x":920,"y":840,"wires":[[]]},{"id":"1e40371b.bd5731","type":"function","z":"e144f16b.b96","name":"Umrechnen","func":"var energie = msg.payload;\nmsg1 = {};\nmsg2 = {};\nmsg3 = {};\nmsg1.payload = energie;\nif (energie >= 0){\n    msg2.payload = energie;\n    msg3.payload = 0;\n}\nelse{\n    var pos = energie * -1;\n    msg2.payload = 0;\n    msg3.payload = pos;\n}\nreturn [msg1,msg2,msg3];","outputs":3,"noerr":0,"x":390,"y":1020,"wires":[["752e3d82.1f9264","36ef8f9a.e6a2"],["98102a72.7df3b8"],["57d47377.7a09d4"]],"outputLabels":["Batterieleistung","Laden","Entladen"]},{"id":"b1e4d00.4c7f8b","type":"comment","z":"e144f16b.b96","name":"E3DC > Modbus > Dashboard & HomeMatic","info":"Flow um per Modbus Daten vom E3/DC S10 abzufragen.\nDie Daten werden im Dashboard angezeigt und an die Systemvariablen der HomeMatic übertragen.","x":250,"y":60,"wires":[]},{"id":"f1cdccfc.9817","type":"modbustcp-read","z":"e144f16b.b96","name":"Modbus read","topic":"","dataType":"HoldingRegister","adr":"40067","quantity":"16","rate":"15","rateUnit":"s","server":"5cab97ab.918b48","ieeeType":"off","ieeeBE":"true","x":150,"y":280,"wires":[["5587595c.15b24"]]},{"id":"5587595c.15b24","type":"function","z":"e144f16b.b96","name":"Umrechnen","func":"var ui32a = new Uint32Array(msg.payload);\n\nmsg1 = {};\nmsg2 = {};\nmsg3 = {};\nmsg4 = {};\nmsg5 = {};\n\nvar home = 0;\nvar pvi = 0;\nvar grid = 0;\nvar bat = 0;\nvar soc = 0;\n\npvi += ui32a[0];\npvi -= ui32a[1];\nbat += ui32a[2];\nbat -= ui32a[3];\nhome += ui32a[4];\nhome -= ui32a[5];\ngrid += ui32a[6];\ngrid -= ui32a[7];\nsoc =  ui32a[15];\n\nmsg1.payload = home;\nmsg2.payload = pvi;\nmsg3.payload = grid;\nmsg4.payload = bat;\nmsg5.payload = soc;\n\nreturn [msg1,msg2,msg3,msg4,msg5];\n","outputs":5,"noerr":0,"x":390,"y":280,"wires":[["5edf6f39.c0aa5"],["37706221.fc9e76"],["de402c0c.22d58"],["2276da6f.e26d3e"],["77b00f9b.8a498"]],"outputLabels":["Hausverbrauch","PV-Leistung","Netzleistung","Batterieleistung","Batterie-SOC"]},{"id":"5edf6f39.c0aa5","type":"link out","z":"e144f16b.b96","name":"Hausverbrauch","links":["d266c4.d7aef14"],"x":660,"y":200,"wires":[],"l":true},{"id":"37706221.fc9e76","type":"link out","z":"e144f16b.b96","name":"PV-Leistung","links":["a13274a5.1aee98"],"x":650,"y":240,"wires":[],"l":true},{"id":"de402c0c.22d58","type":"link out","z":"e144f16b.b96","name":"Netzleistung","links":["b127e5df.aba128"],"x":650,"y":280,"wires":[],"l":true},{"id":"2276da6f.e26d3e","type":"link out","z":"e144f16b.b96","name":"Batterieleistung","links":["35122321.da4604"],"x":660,"y":320,"wires":[],"l":true},{"id":"77b00f9b.8a498","type":"link out","z":"e144f16b.b96","name":"Batterie-SOC","links":["fb5d5a2e.2ea3f8"],"x":660,"y":360,"wires":[],"l":true},{"id":"d266c4.d7aef14","type":"link in","z":"e144f16b.b96","name":"Hausverbrauch","links":["5edf6f39.c0aa5"],"x":160,"y":540,"wires":[["3f480d54.b9fbb2","9d29e28.5de362","92aca437.787ca8"]],"l":true},{"id":"a13274a5.1aee98","type":"link in","z":"e144f16b.b96","name":"PV-Leistung","links":["37706221.fc9e76"],"x":150,"y":680,"wires":[["6f378821.c8d2c8","bd235f4c.a17278","3f875bb.ff24624"]],"l":true},{"id":"b127e5df.aba128","type":"link in","z":"e144f16b.b96","name":"Netzleistung","links":["de402c0c.22d58"],"x":150,"y":840,"wires":[["b2e8c263.148b7"]],"l":true},{"id":"35122321.da4604","type":"link in","z":"e144f16b.b96","name":"Batterieleistung","links":["2276da6f.e26d3e"],"x":160,"y":1020,"wires":[["1e40371b.bd5731"]],"l":true},{"id":"fb5d5a2e.2ea3f8","type":"link in","z":"e144f16b.b96","name":"Batterie-SOC","links":["77b00f9b.8a498"],"x":150,"y":1180,"wires":[["8040ad1a.02c3e","81d86ab8.a532f8","f545ba64.1656"]],"l":true},{"id":"bec3f53.03ed588","type":"comment","z":"e144f16b.b96","name":"Modbus ","info":"","x":140,"y":140,"wires":[]},{"id":"ee292f12.b60f08","type":"comment","z":"e144f16b.b96","name":"Link >","info":"","x":630,"y":140,"wires":[]},{"id":"72db5d47.39e8b4","type":"comment","z":"e144f16b.b96","name":"Register teilen","info":"","x":390,"y":140,"wires":[]},{"id":"8afd0ff.fbf48f","type":"comment","z":"e144f16b.b96","name":"Dashboard","info":"","x":640,"y":440,"wires":[]},{"id":"7c3ed7a8.055238","type":"comment","z":"e144f16b.b96","name":"HomeMatic SysVar","info":"","x":930,"y":440,"wires":[]},{"id":"5917cdcb.bef1fc","type":"comment","z":"e144f16b.b96","name":"Register umrechnen","info":"","x":410,"y":440,"wires":[]},{"id":"17bdc5b5.c0af02","type":"comment","z":"e144f16b.b96","name":"> Link","info":"","x":130,"y":440,"wires":[]},{"id":"a0525507.ad1fb8","type":"comment","z":"e144f16b.b96","name":"Infos zu den Registern ","info":"Register Offset zum Magicbyte ist -1\n\n  40068 PVI  Int32  Länge 2\n  40070 BAT  Int32  Länge 2 \n  40072 HOME Int32  Länge 2 \n  40074 GRID Int32  Länge 2 \n  40083 SOC  UInt16 Länge 1 \n","x":180,"y":220,"wires":[]},{"id":"38263145.35ea0e","type":"ccu-connection","z":"","name":"AdB15","host":"localhost","regaEnabled":true,"bcrfEnabled":true,"iprfEnabled":true,"virtEnabled":true,"bcwiEnabled":false,"cuxdEnabled":false,"regaPoll":true,"regaInterval":"30","rpcPingTimeout":"60","rpcInitAddress":"127.0.0.1","rpcServerHost":"127.0.0.1","rpcBinPort":"2047","rpcXmlPort":"2048","queueTimeout":"5000","queuePause":"250","contextStore":""},{"id":"333e915b.9ccd5e","type":"ui_group","z":"","name":"Hausverbrauch","tab":"2afac8ee.335a1","order":1,"disp":true,"width":"6","collapse":false},{"id":"6ba71bdd.5e7c44","type":"ui_group","z":"","name":"PV-Leistung","tab":"2afac8ee.335a1","order":2,"disp":true,"width":"6","collapse":false},{"id":"e3817d3.76e","type":"ui_group","z":"","name":"Batterie-SOC","tab":"2afac8ee.335a1","order":5,"disp":true,"width":"6","collapse":false},{"id":"a45e2e06.0d4a78","type":"ui_group","z":"","name":"Batterieleistung","tab":"2afac8ee.335a1","order":4,"disp":true,"width":"6","collapse":false},{"id":"90b2f9ee.0bf5e","type":"ui_group","z":"","name":"Netzleistung","tab":"2afac8ee.335a1","order":3,"disp":true,"width":"6","collapse":false},{"id":"5cab97ab.918b48","type":"modbustcp-server","z":"","name":"IP-E3DC_S10","host":"192.168.123.456","port":"502","unit_id":"1","reconnecttimeout":"120"},{"id":"2afac8ee.335a1","type":"ui_tab","z":"","name":"E3/DC S10","icon":"battery_full","disabled":false,"hidden":false}]

### Modbus einrichten

![](https://user-images.githubusercontent.com/19279623/65816918-b7529c80-e201-11e9-9c3b-e027d2bf8a74.png)

IP-Adresse vom S10 Hauskraftwerk anpassen  
![](https://user-images.githubusercontent.com/19279623/65816926-c2a5c800-e201-11e9-8b39-562fc529e867.png)

### Systemvariablen anpassen

In der HomeMatic die Systemvariablen anlegen und an den Nodes entsprechend auswählen.  
![](https://user-images.githubusercontent.com/19279623/65816930-cdf8f380-e201-11e9-9fc6-bf941311fa00.png)

### Implementieren

![](https://user-images.githubusercontent.com/19279623/65816915-b15cbb80-e201-11e9-87ba-ce53f224b011.png)

## Infos

### Modbus am S10

Am Hauskraftwerk muss die Modbusschnittstelle eingerichtet werden. Im Modbusmenü die Funktion aktivieren, dann auf der nächsten Seite das Protokoll "E3DC" wählen, der Port bleibt bei "502".

### Modbus Register

Der Offset zum Magicbyte für die Register ist bei "-1", bedeutet eine Abfrage vom z.B. Register 40068 muss auf der Adresse 40067 gemacht werden. Damit nicht mehrere Poll mit je 1-2 Registern gemacht werden (Stabilität), frage ich hier im Beispiel mit einem Poll 16 Register ab.

### Register umrechnen

Die abgefragten 16 Register verteile ich hier im Flow auf 5 Ausgänge. Für die Leistungswerte (Int32) werden 2 Register zusammengefasst damit die negativen Werte dargestellt werden können. Die 5 Ausgänge werden mit "Links" im Flow verteilt.

### Leistungswerte umrechnen

Für die Leistungswerte die Negativ sein können (Netzleistung und Batterieleistung) werden die Werte für die Übergabe an die Homematic umgerechnet und mit zwei Ausgängen an die SysVar übergeben. So wird z.B. die Batterieleistung entweder als Batterieladung oder Batterieentladung angegeben. Im Dashboard werden die Leistungswerte über einen weiteren Ausgang direkt dargestellt.

### Reconnect Interval

Den "Reconnect Interval" habe ich hier auf 120 Sekunden gestellt. Wenn hier nichts eingetragen ist dann würde nach einem Neustart des S10 die Modbus-Verbindung nicht automatisch wieder aufgebaut.

### Besonderheit E3DC Modbus

Es können nur für die Wallbox Parameteränderungen gesendet werden. Die Batterieleistung oder andere Einstellungen können nicht verändert werden.
