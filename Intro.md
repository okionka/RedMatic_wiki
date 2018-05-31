> RedMatic: Node-RED als Addon für die Homematic CCU3 und RaspberryMatic

Mit [Node-RED](https://nodered.org/about/) und den 
[CCU Nodes für Node-RED](https://github.com/hobbyquaker/node-red-contrib-ccu) ist es auf einfache und visuelle Weise 
möglich Regeln, Automationen, Scripte und Anbindungen von externen Services und Systemen für ein Homematic System zu 
realisieren - und das weitgehend auch ohne Programmierkenntnisse. Die Node-RED Erweiterung 
[Node-RED Dashboard](https://github.com/node-red/node-red-dashboard) ermöglicht es zudem individuelle und ansprechende 
User Interfaces zu erstellen.

_RedMatic_ fasst diese verschiedenen Softwarekomponenten und das zur Ausführung benötigte Node.js zu einem CCU Addon 
zusammen, einem Softwarepaket, dass auf einer Homematic CCU3 oder RaspberryMatic als Zusatzsoftware über das WebUI installiert 
werden kann. Dadurch bieten sich dann oben genannte Möglichkeiten - ohne die Notwendigkeit neben der CCU einen 
weiteren 24/7 laufenden Server zu betreiben.

_RedMatic_ ist __nur für die CCU3 und RaspberryMatic geeignet__. Auf einer CCU1/CCU2 kann es aufgrund der CPU und 
des verfügbaren RAM nicht verwendet werden.


#### Weitere Infos zu Node-RED

[Node-RED](https://nodered.org/about/) ist eine Nachrichtenflussbasierte, visuelle Programmierumgebung für das Internet 
der Dinge.  
Node-RED wird seit 2013 von [IBM Emerging Technology](https://emerging-technology.co.uk/technologies/) 
entwickelt und steht als kostenlose Open Source Software unter dem Dach der [JS Foundation](https://js.foundation/) zur 
Verfügung. Node-RED kann durch zusätzliche [Node(-Sammlungen)](https://flows.nodered.org) erweitert werden, eine große 
und aktive Community hat Stand Heute bereits weit über 1000 Nodes entwickelt.

Siehe auch:
* https://entwickler.de/online/iot/node-red-iot-prototypen-2-579809637.html
* https://jaxenter.de/baukasten-fuer-das-internet-dinge-13532

Zu Node-RED im allgemeinen gibt es unzählige Tutorials, Dokumentationen, Bücher und Youtube Videos, auch in Deutscher 
Sprache.
