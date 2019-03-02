_RedMatic_ fasst mehrere Softwarekomponenten zu einem CCU Addon zusammen, einem Softwarepaket, dass auf einer Homematic 
CCU3 oder RaspberryMatic als Zusatzsoftware komfortabel über das WebUI installiert werden kann.

Die Grundlage bildet [Node-RED](https://nodered.org/about/) mit den 
[CCU Nodes für Node-RED](https://github.com/HM-RedMatic/node-red-contrib-ccu). Hiermit ist es auf einfache, visuelle 
Weise möglich Regeln, Automationen, Scripte und Anbindungen von externen Services und Systemen für ein Homematic System 
zu realisieren - und das weitgehend auch ohne Programmierkenntnisse. Im 
[Wiki](https://github.com/HM-RedMatic/RedMatic/wiki) gibt es weitere Informationen zu Node-RED und einige 
Anwendungsbeispiele (sogenannte _Flows_).

Für die Visualisierung und Steuerung sind [RedMatic WebApp](https://github.com/HM-RedMatic/RedMatic-WebApp) und 
[Node-RED Dashboard](https://github.com/node-red/node-red-dashboard) enthalten. _RedMatic WebApp_ ist eine
Bedienoberfläche die ohne weitere Konfiguration sofort genutzt werden kann (vergleichbar mit _WebMatic_ oder _Yahui_).
_Node-RED Dashboard_ ist ein konfigurierbares User Interface, kann mehr Möglichkeiten als die _RedMatic WebApp_ bieten, 
ist aber mit Konfigurationsaufwand verbunden. 
Beispiel Screenshots: [RedMatic WebApp](https://github.com/HM-RedMatic/RedMatic/wiki/Webapp), 
[Node-RED Dashboard](https://github.com/HM-RedMatic/RedMatic/wiki/Dashboard-Screenshots).

Außerdem ist es mit der ebenfalls enthaltenen Erweiterung 
[RedMatic HomeKit](https://github.com/HM-RedMatic/RedMatic/wiki/Homekit) möglich Homematic Geräte und andere in Node-RED 
verfügbare Systeme über Siri und mit HomeKit-Apps anzusteuern.

Eine Anbindung der CCU an einen [MQTT](https://github.com/HM-RedMatic/RedMatic/wiki/Flow-MQTT) Broker mit komfortabel 
konfigurierbarer Topic- und Payload-Struktur wird durch einen speziellen Node vereinfacht.

Eine große und aktive Community rund um Node-RED hat zudem eine 
[Bibliothek von tausenden zusätzlichen Nodes](https://flows.nodered.org/?type=node&num_pages=1) geschaffen die auf 
einfache Weise [installiert werden können](https://github.com/HM-RedMatic/RedMatic/wiki/Node-Installation) und es 
ermöglichen spezielle Automatismen zu implementieren und diverse weitere Services und Systeme komfortabel anzubinden - 
wie z.B. das Xiaomi Aqara Smart Home System, Loxone, den Logitech Harmony Hub, verschiedene Smart TVs und AV-Receiver, 
Sonoff, Hue, Lightify, Tradfri, ArtNET/DMX, Modbus, Amazon Alexa, Google Home, diverse Datenbanken wie z.B. InfluxDB 
oder MySQL, Webservices zur Abfrage von beispielsweise Wetterdaten und vieles mehr.

_RedMatic_ kann damit - insbesondere für diejenigen die neben der CCU keinen weiteren Server betreiben möchten - eine 
Alternative zu einem "ausgewachsenen" Smart Home System wie z.B. ioBroker, Home Assistent, OpenHAB oder FHEM darstellen. 
Für die Automatisierung eines Homematic Systems kann _RedMatic_ auch als Alternative oder Ergänzung für "Rega" 
Programme/Scripte dienen. 


## Voraussetzungen

_RedMatic_ ist __nur für die CCU3 und RaspberryMatic geeignet__. Da RedMatic unter Umständen über 200MB Speicher 
benötigt ist es ratsam einen RaspberryPi mit 1GB RAM zu nutzen (ab Pi 2B). Auf der CCU1/2 kann _RedMatic_ nicht 
verwendet werden.

Für die Nutzung der Weboberflächen ist ein moderner Browser notwendig, der Internet Explorer wird nicht unterstützt.


## Schnellstart

Unter [Releases](https://github.com/HM-RedMatic/RedMatic/releases/latest) steht die Datei `redmatic-<version>.tar.gz` 
zum Download zur Verfügung. Nach der Installation des Addons über das Homematic WebUI (Systemsteuerung -> 
Zusatzsoftware) und dem darauf folgenden Reboot der CCU ist Node-RED unter `http://<ccu-addresse>/addons/red` 
erreichbar. Bei der Installation ist Geduld erforderlich, es kann bis zu ~10 Minuten dauern. Einige Beispiel-Flows sowie
ein einfaches Dashboard sind bereits vorkonfiguriert, das Dashboard ist unter `http://<ccu-addresse>/addons/red/ui` 
erreichbar.


## Support, Mitarbeit

Für Feedback jeglicher Art, Fragen, Vorschläge, Wünsche und Fehlerberichte bitte den 
[Issue Tracker](https://github.com/HM-RedMatic/RedMatic/issues) nutzen. Alternativ steht auch 
[Slack](https://join.slack.com/t/homematicuser/shared_invite/enQtNDgyNDM2OTkyMDA2LWY1YjY0NTE0NmY0OWM3YWUzMzAzMTgxYmRjMTMyOWE3NjkxNDdlMDY5ZjlhYzM5Nzg2N2U2YjdmNzNlYWNhNTU) 
und ein [Unterforum im Homematic-Forum](https://homematic-forum.de/forum/viewforum.php?f=77) zur Verfügung. 

Beteiligung in jeder Form ist willkommen und gewünscht, insbesondere sind alle Nutzer aufgefordert die [Liste erfolgreich getesteter Nodes](https://github.com/HM-RedMatic/RedMatic/wiki/Erfolgreich-getestete-Nodes) zu ergänzen, Beispiel-Flows zu veröffentlichen und an der Verbesserung und Erweiterung der [Dokumentation](https://github.com/HM-RedMatic/RedMatic/wiki) mitzuarbeiten.

Es werden keine Spenden angenommen, ich würde mich jedoch darüber freuen wenn der erfolgreiche Einsatz dieser Software mit einem Github Sternchen ⭐️ honoriert wird (Github Account ist schnell angelegt! ;-)

