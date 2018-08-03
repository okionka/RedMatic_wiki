Treten Fehler in Programmen oder der Logik der CCU auf werden diese in `/var/log/messages` geloggt. Der folgende Flow beschreibt eine Möglichkeit
* die Fehler auszulesen
* die Gesamtzahl der Fehler zu zählen und im Dashboard anzuzeigen
* die letzten 20 Fehler ebenfalls in einem Log-Fenster im Dashboard anzuzeigen
* nach Erreichen einer Warngrenze eine Email mit den letzten Fehlern zu versenden

Neben den standardmäßig vorhandenen Nodes verwendet dieser Flow zusätzlich [node-red-contrib-counter](https://www.npmjs.com/package/node-red-contrib-counter). Diese kann wie [hier beschrieben](https://github.com/hobbyquaker/RedMatic/wiki/Node-Installation) installiert werden.

## Flow und Dashboard
![](https://raw.githubusercontent.com/wiki/hobbyquaker/RedMatic/images/errorlog/flow.png)

![](https://raw.githubusercontent.com/wiki/hobbyquaker/RedMatic/images/errorlog/dash.png)

## Konfiguration der einzelnen Nodes

### Tail Node
![](https://raw.githubusercontent.com/wiki/hobbyquaker/RedMatic/images/errorlog/tail.png)

* Funktion: Überwacht `/var/log/messages` auf Änderungen und gibt diese als `msg.payload` aus
* `Split lines on \n?` sorgt dafür, dass bei mehreren Zeilen, nur jeweile eine pro `msg` ausgegeben wird

### Switch Node - Filter Errors
![](https://raw.githubusercontent.com/wiki/hobbyquaker/RedMatic/images/errorlog/switch.png)

* Funktion: Lässt eine `msg` nur passieren, wenn in deren Payload irgendwo `Error:` vorkommt
* `^.*Error\:.*$` ist ein sogenannter [https://de.wikipedia.org/wiki/Regul%C3%A4rer_Ausdruck](Regulärer Ausdruck) und prüft, ob in einem String neben beliebigen Zeichen auch die Zeichenfolge `Error:` vorkommt.

### Count Node - Count Errors
![](https://raw.githubusercontent.com/wiki/hobbyquaker/RedMatic/images/errorlog/count.png)

* Funktion: Zählt die Anzahl der ankommenden Nachrichten
* Output 1: Eine Message mit dem jeweilgen Zählerstand als Payload
* Output 2: Die eingegangene Nachricht wird einfach durchgeleitet (und um die Eigenschaft `msg.count` als Zählerstand ergänzt)

### Join Node - Prepare Message
![](https://raw.githubusercontent.com/wiki/hobbyquaker/RedMatic/images/errorlog/join.png)

* Funktion: Sammelt die eingehenden `msg` und fügt diese, bei Erreichen eines Grenzwerts, zu einer einzigen neuen Nachricht zusammen
* Mit `\r\n` in `joined using` wird zwischen jeder Nachricht ein Windows-Zeilenumbruch eingefügt
* `After a number of message parts` gibt den Grenzwert an, bei dem diese Anzahl `msg` zusammengefasst und ausgegeben wird

### Email Node - Send Email
![](https://raw.githubusercontent.com/wiki/hobbyquaker/RedMatic/images/errorlog/email.png)

* Funktion: Diese Node erzeugt und versendet eine Mail mit `msg.payload` als Inhalt und `msg.topic` als Betreff
* `Server` ist der Posteingangsserver der Mailadresse, von der die Nachricht versendet werden soll
* `UserID` ist der Benutzername des entsprechenden Mailkontos
* `Password` das zum Konto gehörende Passwort

### Gauge Node - Show Error Count
![](https://raw.githubusercontent.com/wiki/hobbyquaker/RedMatic/images/errorlog/gauge.png)

* Funktion: Zeigt im Dashboard eine Zähluhr mit der Gesamtzahl der bisher aufgetretenen Fehler an


### Button Node - Reset Error Count
![](https://raw.githubusercontent.com/wiki/hobbyquaker/RedMatic/images/errorlog/button_reset_count.png)

* Funktion: Zeigt im Dashboard, direkt unter der Zähleruhr, einen Reset-Knopf an, mit dem der Zähler wieder auf Null gestellt werden kann

### Change Node - Set Reset Message
![](https://raw.githubusercontent.com/wiki/hobbyquaker/RedMatic/images/errorlog/change_reset_count.png)

* Funktion: Die Counter Node erwartet eine Nachricht mit der Eigenschaft _Reset_ (`msg.reset`), um den Zähler zu nullen.
* Die Button Node kann diese Eigenschaft aber nicht erzeugen, also wird diese mit der Change Node gesetzt
* Zusätzlich wird noch die _Topic_ Eigenschaft (`msg.topic`) gesetzt, um im Log die Aktion mit dem entsprechenden Topic anzeigen zu können

### Function Node - Rotate Entries
![](https://raw.githubusercontent.com/wiki/hobbyquaker/RedMatic/images/errorlog/function.png)

```javascript
var dashboardLog = context.get('dashboardLog')|| [];
 
dashboardLog.push(msg);
if (dashboardLog.length > 20) {
    // Delete oldest message if > 20
    dashboardLog.shift();
    dashboardLog.length = 20;
} 

if (msg.resetlog) {
    dashboardLog = [];
}
 
// store the value back
context.set('dashboardLog',dashboardLog);
 
// make it part of the outgoing msg object
msg = {};
msg.payload = dashboardLog;
return msg;
```

* Funktion: Dieses Javascript erzeugt eine separaten Speicher (sog. `context`), in dem jede ankommende Nachricht gespeichert wird
* Nach 20 Nachrichten wird die älteste Nachricht aus dem Speicher entfernt, so dass rotierend immer die 20 aktuellsten Nachrichten vorgehalten werden
* Wird eine Nachricht mit der Eigenschaft `msg.resetlog` empfangen wird der gesamte Speicher geleert

### Template Node - DashLog
![](https://raw.githubusercontent.com/wiki/hobbyquaker/RedMatic/images/errorlog/template.png)

```html
<ul>
 <li ng-repeat="x in msg.payload">
 <font color="red">{{x.topic}}</font>
    <ul>
        <li>{{x.payload}}</li>
    </ul>
 </li>
</ul>
```

* Funktion: Erzeugt im Dashboard eine Aufzählung die jeweils aus den Eigenschaften `msg.topic` und `msg.payload` besteht
* Die Liste zeigt immer den gesamten Inhalt des, in der `Rotate Entries` Node erzeugten, Speichers an

### Button Node - Clear DashLog
![](https://raw.githubusercontent.com/wiki/hobbyquaker/RedMatic/images/errorlog/button_reset_count.png)

* Funktion: Zeigt im Dashboard direkt unter dem DashLog einen Reset-Knopf an, mit dem der Inhalt des Logs gelöscht wird

### Change Node - Set Reset Message
![](https://raw.githubusercontent.com/wiki/hobbyquaker/RedMatic/images/errorlog/change_reset_log.png)

* Funktion: Die `Rotate Entries` Node erwartet eine Nachricht mit der Eigenschaft `msg.resetlog`, um das Log zu löschen
* Die vorangegangene Button Node kann diese Eigenschaft aber nicht erzeugen, also wird diese mit der Change Node gesetzt

## Flow Quelltext

```
[{"id":"50104e94.8152b8","type":"tab","label":"Error Monitoring","disabled":false,"info":""},{"id":"5d48d65c.e24b48","type":"tail","z":"50104e94.8152b8","name":"","filetype":"text","split":true,"filename":"/var/log/messages","x":130,"y":200,"wires":[["6595e35d.530f24"]]},{"id":"6595e35d.530f24","type":"switch","z":"50104e94.8152b8","name":"Filter Errors","property":"payload","propertyType":"msg","rules":[{"t":"regex","v":"^.*Error\\:.*$","vt":"str","case":true}],"checkall":"true","repair":false,"outputs":1,"x":330,"y":200,"wires":[["e9d593c5.3deb1"]]},{"id":"e9d593c5.3deb1","type":"counter","z":"50104e94.8152b8","name":"Count Errors","init":"0","step":"1","lower":"","upper":"","mode":"increment","outputs":2,"x":510,"y":200,"wires":[["253f1e33.ae4aea"],["ba691feb.d30d08","bd901793.899028"]]},{"id":"253f1e33.ae4aea","type":"ui_gauge","z":"50104e94.8152b8","name":"Show Error Count","group":"d79a8eea.a905c","order":0,"width":"6","height":"4","gtype":"gage","title":"Anzahl Fehler","label":"Fehler","format":"{{value}}","min":0,"max":"100","colors":["#00b500","#e6e600","#ca3838"],"seg1":"","seg2":"","x":710,"y":140,"wires":[]},{"id":"ba691feb.d30d08","type":"function","z":"50104e94.8152b8","name":"Rotate Entries","func":"var dashboardLog = context.get('dashboardLog')|| [];\n \ndashboardLog.push(msg);\nif (dashboardLog.length > 20) {\n    // Delete oldest message if > 20\n    dashboardLog.shift();\n    dashboardLog.length = 20;\n} \n\nif (msg.resetlog) {\n    dashboardLog = [];\n}\n \n// store the value back\ncontext.set('dashboardLog',dashboardLog);\n \n// make it part of the outgoing msg object\nmsg = {};\nmsg.payload = dashboardLog;\nreturn msg;","outputs":1,"noerr":0,"x":700,"y":260,"wires":[["f4ef2a5d.f01c18"]]},{"id":"bd901793.899028","type":"join","z":"50104e94.8152b8","name":"Prepare Message","mode":"custom","build":"string","property":"payload","propertyType":"msg","key":"topic","joiner":"\\r\\n","joinerType":"str","accumulate":false,"timeout":"","count":"5","reduceRight":false,"reduceExp":"","reduceInit":"","reduceInitType":"num","reduceFixup":"","x":710,"y":200,"wires":[["2e0650.3ce4e9b"]]},{"id":"f4ef2a5d.f01c18","type":"ui_template","z":"50104e94.8152b8","group":"2bf72e51.a156aa","name":"DashLog","order":0,"width":"6","height":"4","format":"<ul>\n <li ng-repeat=\"x in msg.payload\">\n <font color=\"red\">{{x.topic}}</font>\n    <ul>\n        <li>{{x.payload}}</li>\n    </ul>\n </li>\n</ul>","storeOutMessages":true,"fwdInMessages":true,"templateScope":"local","x":900,"y":260,"wires":[[]]},{"id":"2e0650.3ce4e9b","type":"e-mail","z":"50104e94.8152b8","server":"smtp.gmail.com","port":"465","secure":true,"name":"","dname":"Send Email","x":910,"y":200,"wires":[]},{"id":"b8d3f654.c03e9","type":"comment","z":"50104e94.8152b8","name":"Fehlerüberwachung","info":"* Überwacht /var/log/messages\n* Zeigt die letzten 20 Fehler in einem Log-Fenster\n* Zeigt die Gesamtzahl der Fehler\n* Schickt Email nach 5 Fehlern mit Fehlerprotokoll","x":130,"y":60,"wires":[]},{"id":"df87c0fb.d4ab68","type":"ui_button","z":"50104e94.8152b8","name":"Reset Error Count","group":"d79a8eea.a905c","order":0,"width":0,"height":0,"passthru":false,"label":"Reset","color":"","bgcolor":"","icon":"","payload":"true","payloadType":"bool","topic":"","x":130,"y":140,"wires":[["4d33d56a.36fafc"]]},{"id":"4d33d56a.36fafc","type":"change","z":"50104e94.8152b8","name":"Set Reset Message","rules":[{"t":"set","p":"reset","pt":"msg","to":"true","tot":"bool"},{"t":"set","p":"topic","pt":"msg","to":"Reset Error Count","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":350,"y":140,"wires":[["e9d593c5.3deb1"]]},{"id":"72b39289.830fcc","type":"ui_button","z":"50104e94.8152b8","name":"Clear DashLog","group":"2bf72e51.a156aa","order":0,"width":0,"height":0,"passthru":false,"label":"Clear DashLog","color":"","bgcolor":"","icon":"","payload":"true","payloadType":"bool","topic":"","x":120,"y":260,"wires":[["cdbca45f.b62868"]]},{"id":"cdbca45f.b62868","type":"change","z":"50104e94.8152b8","name":"Set Reset Message","rules":[{"t":"set","p":"resetlog","pt":"msg","to":"true","tot":"bool"}],"action":"","property":"","from":"","to":"","reg":false,"x":350,"y":260,"wires":[["ba691feb.d30d08"]]},{"id":"d79a8eea.a905c","type":"ui_group","z":"","name":"Error Count","tab":"a5b5c3f2.ffeeb8","disp":true,"width":"6","collapse":false},{"id":"2bf72e51.a156aa","type":"ui_group","z":"","name":"DashLog","tab":"a5b5c3f2.ffeeb8","disp":true,"width":"6","collapse":false},{"id":"a5b5c3f2.ffeeb8","type":"ui_tab","z":"","name":"Error Log","icon":"dashboard"}]
```
