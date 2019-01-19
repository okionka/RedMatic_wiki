<details><summary>Hilfe! Nach der Installation fährt meine CCU/RaspberryMatic nicht mehr hoch!
</summary>
<p>
Bitte erst Sorgen machen und Maßnahmen einleiten falls der Neustart nach der Installation länger als 10 Minuten her ist. <br>RedMatic ist für ein Homematic Addon sehr groß und besteht aus sehr vielen Dateien. Das auspacken des Archivs dass bei der Installation von der CCU erledigt werden muss ist dabei je nach Raspberry CPU und io bzw. SD Karten Performance sehr Zeitintensiv. Hier ist Geduld erforderlich.
<p>
</details>
    
    

<details><summary>CCU Firewall Einstellungen? Was muss ich für die Nutzungs welcher Nodes freischalten?</summary>
<p>

##### node-red-contrib-alexa-local

##### RedMatic-HomeKit

</p>
</details>
    
    

<details><summary>Wo liegt nun der Unterschied zu ioBroker, HASS, OpenHAB, ...?﻿</summary>
<p>

Node-RED beschäftigt sich primär mit dem Empfang, der Weiterleitung, dem Senden und der Manipulation von Nachrichten innerhalb Node-RED oder über bestimmte Nodes auch mit unzähligen externen Services und Systemen.

Ein Aspekt den "ausgewachsene" Smart Home Systeme wie ioBroker abdecken bleibt bei Node-RED gänzlich unbeachtet: die komfortable Verwaltung von Metadaten die alle Geräte unter einem Dach und gemeinsamen Schema beschreiben. 

Das Fehlen dieses Aspektes führt dazu dass in Node-RED viele Flows ganz spezifisch für die Zielsysteme angepasst sind und völlig andere Nachrichtenstrukturen nutzen. _Beispiel_: ein Node der LED Lampen vom Hersteller "A" ansteuert benötigt z.B. im Payload eine JSON Struktur die die Farbe/Helligkeit/Sättigung nach dem HSL Modell enthält. Ein anderer Node der Lampen vom Hersteller "B" steuert braucht aber im Payload einfach nur einen numerischen Wert zwischen 0 und 1 für die Helligkeit und die Strings "red", "blue", ... am Eingang eines weiteren Nodes.

Smart Home Software wie ioBroker setzen zur Vermeidung der oben genannten Eigenschaft zusätzlich darauf alle Geräte möglichst generisch mittels eines eigenen Schemas zu beschreiben und somit den User davon entlasten sich mit den speziellen Eigenheiten eines Gerätes oder einer API auseinanderzusetzen. Außerdem entsteht damit auch der Vorteil dem User komfortable Funktionen zu bieten bei denen Geräte unterschiedlicher Hersteller alle "gleichberechtigt" und vor allem auf die gleiche Weise ausgewählt, verbunden, angezeigt oder gesteuert werden können. Auch die automatische Erzeugung von User Interfaces fußt darauf dass eine Datenbank aller Geräte mittels eines einheitlichen Schemas beschrieben werden können.

Node-RED hat auf der Gegenseite jedoch den Vorteil wesentlich "leichtgewichtiger" als ioBroker zu sein, alles läuft in einem Prozess und durch den vielfach geringeren RAM-Bedarf ist die Möglichkeit RedMatic bzw. Node-RED auf einer "normalen" CCU3 zu betreiben gegeben. Somit ist RedMatic unter der Prämisse "ich möchte es als alternative zu einer Software wie z.B. ioBroker einsetzen" ganz besonders für diejenigen Interessant die neben der CCU keinen weiteren Server/Raspberry 24 Stunden laufen lassen wollen - es aber in Kauf nehmen können/wollen, dass sie sich mehr mit den speziellen Eigenschaften aller angebundenen System auseinandersetzen müssen.

Eine weitere Abgrenzung ergibt sich bei RedMatic auch durch ein paar andere Anwendungsfälle die gar nicht mit einer "ausgewachsenen" Smart Home Software konkurrieren. RedMatic kann z.B. eine sehr sinnvolle Ergänzung in einem MQTT basierten Smart Home dienen und ermöglicht es die Geräte der CCU sehr einfach an MQTT anzubinden. Dabei wäre es vorstellbar dass außer dem Homematic-MQTT Node eigentlich nichts in Node-RED gemacht wird, RedMatic also zu einem schlichten Homematic-MQTT-Adapter "degradiert" wurde. 
Für Apple User können sich die interessanten Features von RedMatic sich durchaus nur auf HomeKit beschränken, der Nutzer hat dann auch hier möglicherweise außer einem einzigen Homematic-HomeKit Node gar nichts in RedMatic konfiguriert. 
Viele User ersetzen mit RedMatic ihre Homematic-Scripte und -Programme, haben aber dennoch noch weitere Software laufen oder betreiben Mischformen in dem die Automatisierung auf mehreren Ebenen implementiert ist. 
Auch denkbar ist es RedMatic in Kombination mit Software wie HASS oder ioBroker zu betreiben und nur ganz bestimmte Anwendungsfälle wie z.B. das timing-kritische Dimmen mit langem Tastendruck über Schnittstellen-Grenzen hinweg mit RedMatic realisieren.
</p>
</details>

<details><summary>Beim Auswählen der Schnittstelle ist CUxD (oder BidCos-Wired) nicht auswählbar</summary>
<p>
</p>
</details>

<details><summary>Bei anhaltendem Tastendruck werden keine PRESS_CONT Events empfangen</summary>
<p>
</p>
</details>