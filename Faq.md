## CCU Firewall Einstellungen? Was muss ich für die Nutzungs welcher Nodes freischalten?

##### node-red-contrib-alexa-local

##### RedMatic-HomeKit


## Wo liegt nun der Unterschied zu ioBroker, HASS, OpenHAB, ...?﻿

Node-RED beschäftigt sich nur mit dem Empfang, der Weiterleitung, dem Senden und der Manipulation von Nachrichten innerhalb Node-RED oder über bestimmte Nodes auch mit unzähligen externen Services und Systemen. 

Ein Aspekt den "ausgewachsene" Smart Home Systeme wie ioBroker abdecken bleibt bei Node-RED gänzlich unbeachtet: die komfortable Verwaltung der Metadaten aller Geräte unter einem Dach und gemeinsamen Schema. 

Das Fehlen dieses Aspektes führt dazu dass in Node-RED viele Flows ganz spezifisch für die Zielsysteme angepasst sind und völlig andere Nachrichtenstrukturen nutzen (Beispiel: ein Node der LED Lampen vom Hersteller "A" ansteuert benötigt z.B. im Payload eine JSON Struktur die die Farbe/Helligkeit/Sättigung nach dem HSL Modell enthält. Ein anderer Node der Lampen vom Hersteller "B" steuert braucht aber im Payload einfach nur einen numerischen Wert zwischen 0 und 1 für die Helligkeit und die Strings "red", "blue", ... am Eingang eines weiteren Nodes).
Smart Home Software wie ioBroker setzen zur Vermeidung der oben genannten Eigenschaft zusätzlich darauf alle Geräte möglichst generisch mittels eines eigenen Schemas zu beschreiben und somit den User davon entlasten sich mit den speziellen Eigenheiten eines Gerätes oder einer API auseinanderzusetzen. Außerdem entsteht damit auch der Vorteil dem User komfortable Funktionen zu bieten bei denen Geräte unterschiedlicher Hersteller alle "gleichberechtigt" und vor allem auf die gleiche Weise ausgewählt, verbunden, angezeigt oder gesteuert werden können. Auch die automatische Erzeugung von User Interfaces fußt darauf dass eine Datenbank aller Geräte mittels eines einheitlichen Schemas beschrieben werden können.

Node-RED hat auf der Gegenseite jedoch den Vorteil wesentlich "leichtgewichtiger" als ioBroker zu sein, alles läuft in einem Prozess und durch den vielfach geringeren RAM-Bedarf ist die Möglichkeit RedMatic auf einer CCU zu betreiben. Somit ist RedMatic unter der prämisse "ich möchte es als alternative zu einer Software wie ioBroker einsetzen" ganz besonders für diejenigen Interessant die neben der CCU keinen weiteren Server 24 Stunden laufen lassen wollen.

Eine weitere Abgrenzung ergibt sich bei RedMatic auch durch ein paar andere Anwendungsfälle die gar nicht mit einer "ausgewachsenen" Smart Home Software konkurrieren. RedMatic kann z.B. eine sehr sinnvolle Ergänzung in einem MQTT basierten Smart Home dienen und ermöglicht es die Geräte der CCU sehr einfach an MQTT anzubinden. Für Apple User können sich die interessanten Features von RedMatic sich durchaus nur auf HomeKit beschränken, er hat dann vielleicht sogar außer einem einzigen Homematic-HomeKit Node gar nichts in RedMatic konfiguriert. Viele User ersetzen mit RedMatic ihre Homematic-Scripte und -Programme. Auch denkbar ist es RedMatic in Kombination mit Software wie HASS oder ioBroker zu betreiben und nur ganz bestimmte Anwendungsfälle wie z.B. das timing-kritische Dimmen mit langem Tastendruck über Schnittstellen-Grenzen hinweg mit RedMatic realisieren.

## Beim Auswählen der Schnittstelle ist CUxD (oder BidCos-Wired) ausgegraut obwohl ich CUxD/Wired habe