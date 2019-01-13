### 1) [Abfrage von CCU-Variabeln beschleunigen](#abfrage-von-ccu-variablen-beschleunigen)
### 2) Datenpunktstatus von mehreren Geraeten gleichzeitig abfragen
### 3) Manuelles Backup

- - - - - - - - - - - - - - - - - - - - 

### 1) Abfrage von CCU-Variablen beschleunigen
Per Default Settings werden CCU-Variablen alle 30 Sekunden von der Rega abgeholt. Mit dem "poll" Node (unter CCU) kann man eine sofortige Abfrage erzwingen und bestimmte Prozesse somit massiv beschleunigen. Dies kann z.B. notwendig sein, wenn man eine Alarmanlage mit CCU-Variablen anlegen will.

Umsetzung:

1) "poll" Node anlegen, CCU auswählen und eventuell den Node benennen
2) Mittels eines "value" oder "rpc event" nodes einen virtuellen Taster der CCU abfragen (z.B. den BidCoS-RF:1 HM-RCV-50 BidCoS-RF:1) und mit dem "poll" node verbinden.
3) Ein Programm in der CCU-Anlegen, das bei Änderung einer der "wichtigen" Variablen den virtuellen Taster auslöst.

- - - - - - - - - - - - - - - - - - - - 

### 2) Datenpunktstatus von mehreren Geraeten gleichzeitig abfragen

Der folgende Beispielflow, ergibt am Ende als Payload ein bool "true" Ausgeben falls ein oder mehrere Lichter an sind, "false" falls alle aus sind.
![](https://user-images.githubusercontent.com/44581521/50928157-30cf1280-145a-11e9-9e73-df4739cd2a2a.png)
![](https://user-images.githubusercontent.com/44581521/50928365-c5d20b80-145a-11e9-868f-8d0d9793f200.png)
![](https://user-images.githubusercontent.com/44581521/50928621-76400f80-145b-11e9-9ac9-d818bcba06cb.png)

`[{"id":"e6f9b982.598fb8","type":"ccu-rpc-event","z":"9804491c.a6e8b8","name":"","iface":"","ccuConfig":"38263145.35ea0e","rooms":"","roomsRx":"str","functions":"Licht","functionsRx":"str","device":"","deviceRx":"str","deviceName":"","deviceNameRx":"str","deviceType":"","deviceTypeRx":"str","channel":"","channelRx":"str","channelName":"","channelNameRx":"str","channelType":"","channelTypeRx":"str","datapoint":"^STATE$|^LEVEL$","datapointRx":"re","change":true,"working":true,"cache":true,"topic":"${CCU}/${Interface}/${channelName}/${datapoint}","x":140,"y":180,"wires":[["c7910200.404d3"]]},{"id":"c7910200.404d3","type":"combine-logic","z":"9804491c.a6e8b8","name":"","topic":"","operator":"or","defer":250,"timeout":0,"distinction":"topic","x":300,"y":180,"wires":[["9b156924.74c638"]]},{"id":"9b156924.74c638","type":"debug","z":"9804491c.a6e8b8","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"true","x":440,"y":180,"wires":[]},{"id":"38263145.35ea0e","type":"ccu-connection","z":"","name":"localhost","host":"localhost","regaEnabled":true,"bcrfEnabled":true,"iprfEnabled":true,"virtEnabled":false,"bcwiEnabled":true,"cuxdEnabled":false,"regaPoll":true,"regaInterval":"30","rpcPingTimeout":"60","rpcInitAddress":"127.0.0.1","rpcServerHost":"127.0.0.1","rpcBinPort":"2047","rpcXmlPort":"2048","contextStore":"default"}]`

Wenn man den Status der Geräte bei einem bestimmten Event abfragen will (z.B. Wenn ich die Haustüre zuschließe und nicht alle Lampen ausgeschaltet sind, dann...), muss der Ausgang dieses Flows mit einem Change Node Verbindungen werden der das Ergebnis im Context (z.b. global.lights) speichert. In dem Flow der vom Öffnen der Haustüre angetriggert wird, kann man anschließend einen Switch Node verwenden der je nach Wert des vorher gespeicherten Ergebnisses die Nachricht weiterleitet oder nicht (oder an unterschiedliche Ausgänge weiterleitet).

- - - - - - - - - - - - - - - - - - - -

### 3) Manuelles Backup

Für eine manuelle Sicherung sind folgende Dateien relevant:

/usr/local/addons/redmatic/var/flows.json
/usr/local/addons/redmatic/var/flows_cred.json
/usr/local/addons/redmatic/var/homekit/*
/usr/local/addons/redmatic/etc/settings.json
/usr/local/addons/redmatic/etc/credentials.key

Falls das Node-RED Projects-Feature aktiviert ist, dann auch noch der Ordner:

/usr/local/addons/redmatic/var/projects

Das alles steckt auch mit im CCU Backup.

