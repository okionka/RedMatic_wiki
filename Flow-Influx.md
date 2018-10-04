Als erstes alle benötigen Komponenten installieren (redmatic, TICK-Stack, grafana). Dann die Verbindung in redmatic zur ccu einrichten, Datenbank in influxdb einrichten, datasource in grafana einrichten.

Dann in redmatic influxdb adapter installieren: Burger-Menu, manage palette, dann
![](images/influx1.jpg)

Dann den Flow anlegen
![](images/influx2.jpg)

im rpc event Topic wie gewünscht anlegen, wenn gewünscht Filter einrichten, "emit only changed values" auswählen
![](images/influx3.jpg)

Mit change node die in msg.topic enthaltenen Daten in msg.measurement umspeichern, da influxdb die Daten dort erwartet
![](images/influx4.jpg)

Dann mit function-Node und folgendem Skript Leerzeichen escapen (Bug im influxdb-Connector, wenn der mal gefixt wird, erhält man evtl. doppelte \\, dann das Skript wieder löschen):

```javascript
msg.measurement = msg.measurement.replace(/ /g, '\\ ');
return msg;
```

Und dann ab in die Datenbank:
![](images/influx5.jpg)