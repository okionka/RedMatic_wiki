---
Category: User Flows
---

# Schalter mit Status als Badge Ersatz

## Generelles
Häufig möchte man einen Schalter, der zum einen Informationen angibt (Anzahl offener Jalousien, Player on / off) und zum anderen auch "clickbar" ist. In Android / iPhones kann man das mit "badges" realisieren - in NodeRED Dashboard geht das mit dem Dashboard Button. Ich nutzte es um die Funktionen (Jalousien, Sicherheit/Fenster, Lichter, Heizung, Media auf einem Dashboard anzuzeigen und bei "click" dorthin zu springen (Detailseiten). Es sieht dann so aus: 

![Aussehen](https://user-images.githubusercontent.com/17273119/60768123-83b01c80-a0c1-11e9-9b15-ef626cff7a8c.png)

## Benötigte Erweiterungen
Keine.

## Einstellungen

![Node Konfiguration](https://user-images.githubusercontent.com/17273119/60768199-852e1480-a0c2-11e9-8afa-3e6ec2348007.png)

Hier ist die Node zum import. 
`[{"id":"dc5a819e.5840b","type":"ui_button","z":"95579ba8.e8979","name":"BigBut Blinds","group":"b6335921.23f268","order":1,"width":"2","height":"2","passthru":false,"label":"<font size=6>{{msg.payload}}</font>","tooltip":"Jalousien","color":"{{(msg.payload > 0 ?\"CornflowerBlue \":\"Silver\")}}","bgcolor":" Gainsboro","icon":"fa-bars fa-3x","payload":"1","payloadType":"str","topic":"","x":1025,"y":415,"wires":[["4ff658fe.0aa218"]]},{"id":"b6335921.23f268","type":"ui_group","z":"","name":"Funktionen","tab":"bf6344f5.596528","order":2,"disp":false,"width":"10","collapse":false},{"id":"bf6344f5.596528","type":"ui_tab","z":"","name":"Übersicht","icon":"dashboard","order":1,"disabled":false,"hidden":false}]`