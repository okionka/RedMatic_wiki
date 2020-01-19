_RedMatic_ fasst mehrere Softwarekomponenten zu einem CCU Addon zusammen, einem Softwarepaket, dass auf einer Homematic CCU3 oder RaspberryMatic als Zusatzsoftware komfortabel über das WebUI installiert werden kann.

Die Grundlage bildet [Node-RED](https://nodered.org/about/) mit den [CCU Nodes für Node-RED](https://github.com/rdmtc/node-red-contrib-ccu). Hiermit ist es auf einfache und visuelle Weise möglich Regeln, Automationen, Scripte und Anbindungen von externen Services und Systemen für ein Homematic System zu realisieren - und das weitgehend auch ohne Programmierkenntnisse. Im [Wiki](https://github.com/rdmtc/RedMatic/wiki) gibt es weitere Informationen zu Node-RED und einige Anwendungsbeispiele (sogenannte _Flows_).

Die Einrichtung und der Betrieb von _RedMatic_ ist sehr benutzerfreundlich, es bedarf keiner Linux-Kenntnisse und es müssen keine Konfigurationsdateien o.Ä. bearbeitet werden. 

Für die Visualisierung und Steuerung sind [RedMatic WebApp](https://github.com/rdmtc/RedMatic-WebApp) und 
[Node-RED Dashboard](https://github.com/node-red/node-red-dashboard) enthalten. _RedMatic WebApp_ ist eine
Bedienoberfläche die ohne weitere Konfiguration sofort genutzt werden kann um das Homematic System mit dem PC oder Mobilgeräten zu steuern (vergleichbar mit _WebMatic_ oder _Yahui_).
_Node-RED Dashboard_ ist ein konfigurierbares User Interface, kann mehr Möglichkeiten als die _RedMatic WebApp_ bieten, ist aber mit Konfigurationsaufwand verbunden. Beispiel Screenshots: [RedMatic WebApp](https://github.com/rdmtc/RedMatic/wiki/Webapp), [Node-RED Dashboard](https://github.com/rdmtc/RedMatic/wiki/Dashboard-Screenshots).

Außerdem ist es mit der ebenfalls enthaltenen Erweiterung [RedMatic HomeKit](https://github.com/rdmtc/RedMatic/wiki/Homekit) ohne weiteren Installations- oder Einrichtungsaufwand möglich Homematic Geräte in Apple HomeKit einzubinden und über Siri und mit HomeKit-Apps anzusteuern. Darüberhinaus können auch beliebige andere an Node-RED angebundene Systeme und Kameras in HomeKit integriert werden.

Eine Anbindung der CCU an einen [MQTT](https://github.com/rdmtc/RedMatic/wiki/Flow-MQTT) Broker mit komfortabel konfigurierbarer Topic- und Payload-Struktur wird durch einen speziellen Node vereinfacht.

Eine große und aktive Community rund um Node-RED hat zudem eine 
[Bibliothek von tausenden zusätzlichen Nodes](https://flows.nodered.org/?type=node&num_pages=1) geschaffen die auf 
einfache Weise [installiert werden können](https://github.com/rdmtc/RedMatic/wiki/Node-Installation) und es 
ermöglichen spezielle Automatismen zu implementieren und diverse weitere Services und Systeme komfortabel anzubinden - wie z.B. KNX, Xiaomi/Aqara, Loxone, Somfy Tahoma, Velux KLF200, Home Connect Haushaltsgeräte, den Logitech Harmony Hub, verschiedene Smart TVs und AV-Receiver, Sonos, Netatmo, Hue/Lightify/Tradfri, Deconz, ArtNET/DMX, DALI, Modbus, Amazon Alexa, Google Home, diverse Datenbanken wie z.B. InfluxDB oder MySQL, Webservices zur Abfrage von beispielsweise Wetterdaten und vieles mehr.

_RedMatic_ kann damit - insbesondere auch für diejenigen die neben der CCU keinen weiteren Server betreiben möchten - eine Alternative zu einem "ausgewachsenen" Smart Home System wie z.B. ioBroker, Home Assistent, OpenHAB oder FHEM darstellen. Mit RedMatic-HomeKit steht des weiteren eine Alternative zum Betrieb einer Homebridge zur Verfügung die insbesondere bei der Integration von Homematic Geräten in HomeKit einige Vorteile bietet.
Auch eine Koexistenz mit vorhandener anderer Smart Home Software kann sinnvoll sein, _RedMatic_ eignet sich z.B. auch sehr gut als Schnittstelle um eine Homematic CCU an ein übergeordnetes System via MQTT anzubinden. 
Nicht zuletzt kann _RedMatic_ auch als stabile und mit wesentlich mehr Möglichkeiten aufwartende Alternative oder Ergänzung zu den WebUI-Programmen und Scripten der CCU Logikschicht "Rega" dienen.


## Voraussetzungen

_RedMatic_ ist __nur für die CCU3 und RaspberryMatic geeignet__. Da RedMatic unter Umständen über 200MB Speicher 
benötigt ist es ratsam einen RaspberryPi mit 1GB RAM zu nutzen (ab Pi 2B). 

Die RaspberryMatic-Varianten "ova" und "intelnuc" werden (noch) nicht unterstützt. Auf der CCU1/2 kann _RedMatic_ nicht verwendet werden. 

Für die Nutzung der Weboberflächen ist ein moderner Browser notwendig, der Internet Explorer wird nicht unterstützt.


## Schnellstart

Unter [Releases](https://github.com/rdmtc/RedMatic/releases/latest) steht die Datei `redmatic-<version>.tar.gz` 
zum Download zur Verfügung. Nach der Installation des Addons über das Homematic WebUI (Systemsteuerung -> 
Zusatzsoftware) und dem darauf folgenden Reboot der CCU ist Node-RED unter `http://<ccu-addresse>/addons/red` 
erreichbar. Bei der Installation ist Geduld erforderlich, es kann bis zu ~10 Minuten dauern. Einige Beispiel-Flows sowie ein einfaches Dashboard sind bereits vorkonfiguriert, das Dashboard ist unter `http://<ccu-addresse>/addons/red/ui` erreichbar.


## Support, Mitarbeit

Für Feedback jeglicher Art, Fragen, Vorschläge, Wünsche und Fehlerberichte bitte den 
[Issue Tracker](https://github.com/rdmtc/RedMatic/issues) nutzen. Alternativ steht auch 
[Slack](https://join.slack.com/t/homematicuser/shared_invite/enQtNDgyNDM2OTkyMDA2LWY1YjY0NTE0NmY0OWM3YWUzMzAzMTgxYmRjMTMyOWE3NjkxNDdlMDY5ZjlhYzM5Nzg2N2U2YjdmNzNlYWNhNTU) 
und ein [Unterforum im Homematic-Forum](https://homematic-forum.de/forum/viewforum.php?f=77) zur Verfügung. 

Beteiligung in jeder Form ist willkommen und gewünscht, insbesondere sind alle Nutzer aufgefordert die [Liste erfolgreich getesteter Nodes](https://github.com/rdmtc/RedMatic/wiki/Erfolgreich-getestete-Nodes) zu ergänzen, Beispiel-Flows zu veröffentlichen und an der Verbesserung und Erweiterung der [Dokumentation](https://github.com/rdmtc/RedMatic/wiki) mitzuarbeiten.

Es werden keine Spenden angenommen, ich würde mich jedoch darüber freuen wenn der erfolgreiche Einsatz dieser Software mit einem Github Sternchen ⭐️ honoriert wird (Github Account ist schnell angelegt! ;-)
