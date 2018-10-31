### Ziel ist es, dass mit HomeKit die Harmony Activities gestartet werden können und dass gleichzeitig der korrekte Status in der Home App angezeigt wird, sollte mal direkt mit der Harmony Remote geschaltet werden.

Dazu muss zuerst der Harmony Node installiert werden. Das geht binnen Minuten.
Und der HomeKit Homematic Node muss angelegt und konfiguriert sein.

Man startet mit einem H Observe Node. Dort wählt man das gewünschte Harmony Hub aus.

![](https://up.picr.de/34212684dy.jpg)

Dann hängt man an den H Observe Node einen Debug Node und startet mit der Harmony Fernbedienung die entsprechenden Activities (inkl. ausschalten). Durch den Debug Node kommt man an die entsprechenden Activity IDs.

![](https://up.picr.de/34212689by.jpg)

In meinem Fall als Beispiel:
Fernsehen: 13121214 / AppleTV: 13121209 / Radio: 16026881 / TV Apps: 34846059 / AUS: -1

Nun kann man den Debug Node wieder entfernen.

Pro Aktivity hängt man nun einen Switch Node an den H Observe Node (ich beschreibe das hier nur am Beispiel meiner Fernsehen Activity, bei den anderen ist es bis auf die Activity ID identisch).

![](https://up.picr.de/34212702bs.jpg)

Nun wird jeder dieser Switch Nodes mit 2 Change Nodes verbunden. Der eine setzt auf true, der andere auf false.

![](https://up.picr.de/34212717gk.jpg)
![](https://up.picr.de/34212718bs.jpg)

Als nächstes legt man pro Aktivity einen Homekit Switch Node an. Dieser wird jeweils mit dem Change Node der true setzt für die zuvor per Change Node gefilterte Activity verbunden und mit allen anderen (ausser von dieser Activity), die auf false setzen.
Nun ist man schonmal so weit, dass es ein "Gerät" in HomeKit gibt, das beim Schalten der Harmony Activities per Harmony Fernbedienung immer den korrekten Status anzeigt.  

Als letztes nimmt man dann pro Activity einen H activity Node, weist diesem die gewünschte Aktivität zu und verbindet diesen mit dem jeweiligen HomeKit Switch Node. Jetzt wird auch beim Betätigen des Gerätes in der Home App oder mit Siri die Harmony Activity gestartet.

![](https://up.picr.de/34212780su.jpg)

Am Ende sieht es bei mir so aus:

![](https://up.picr.de/34212782cr.jpg)



### Als Auftrag des faulen Frauchens wurde dann noch ein Schalten der Sender mit Siri umgesetzt.
Dieses geht folgendermassen:

Mal legt einen HomeKit Switch Node pro Sender an, der mittels Delay Node und Change Node automatisch wieder auf false gesetzt wird. Diesen Switch Node verbindet man mit einem H Command Node, in dem man den gewünschten Befehl eingibt. Als Beispiel nur für ARD, was bei mir auf 1 liegt.

![](https://up.picr.de/34212821gl.jpg)

![](https://up.picr.de/34212817um.jpg)

Nun ist mit "Hey Siri ARD" ein handloser Senderwechsel beim Bügeln oder der Hometrainer Nutzung möglich.
