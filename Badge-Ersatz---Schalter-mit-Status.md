---
Category: User Flows
---

# Badge Ersatz - Schalter mit Status

## Generelles
Häufig möchte man einen Schalter, der zum einen Informationen angibt (Anzahl offener Jalousien, Player on / off) und zum anderen auch "clickbar" ist. In Android / iPhones kann man das mit "badges" realisieren - in NodeRED Dashboard geht das mit dem Dashboard Button. Es sieht dann so aus: 

… bild einfügen wie? … 

## Benötigte Erweiterungen
Keine.

## Einstellungen
… screenshot einfügen wie ?… 

Hier ist die Node zum import. 
`[{"id":"dc5a819e.5840b","type":"ui_button","z":"95579ba8.e8979","name":"BigBut Blinds","group":"b6335921.23f268","order":1,"width":"2","height":"2","passthru":false,"label":"<font size=6>{{msg.payload}}</font>","tooltip":"Jalousien","color":"{{(msg.payload > 0 ?\"CornflowerBlue \":\"Silver\")}}","bgcolor":" Gainsboro","icon":"fa-bars fa-3x","payload":"1","payloadType":"str","topic":"","x":1025,"y":415,"wires":[["4ff658fe.0aa218"]]},{"id":"b6335921.23f268","type":"ui_group","z":"","name":"Funktionen","tab":"bf6344f5.596528","order":2,"disp":false,"width":"10","collapse":false},{"id":"bf6344f5.596528","type":"ui_tab","z":"","name":"Übersicht","icon":"dashboard","order":1,"disabled":false,"hidden":false}]`