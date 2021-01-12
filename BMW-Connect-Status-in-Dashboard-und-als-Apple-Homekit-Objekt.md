---
Category: User Flows
---

# Mini Cooper Online 

Nach dem ich nun mein 1. Auto mit echter API Schnittstelle bekommen habe - einen Mini Cooper SE, und ich die App nicht so praktisch fand (sie spricht nun mal nicht) hab ich mir was selber gebastelt. Ziel sollte es sein, einen Status in Apple Homekit zu haben, der mir sagt ob der Mini vollgeladen ist oder lädst oder oder ... ie das so ist, sieht man sich Logs an und sieht was man alles auslesen kann, kommt man auf verrückte Ideen.  

# Was brauche ich? 
Einen Wagen, der an BMW- Connect angeschlossen werden kann. In dem Fall hier ist es ein rein elektrischer Mini Cooper SE Baujahr 2020. Spätestens wenn man sich die Mini App oder BMW-Connect App eingerichtet hat, besitzt man die **Login Daten** und die **FIN** (Fahrzeug Identifikationsnummer.

# In der RedMatic 
Ich habe den Node 

**"car-bmw-list"** installiert und mit den Daten oben eingerichtet. Den List-Node konnte ich nicht nutzen ohne Fehler, vermutlich weil ich nur einen Wagen habe. Der sollte eine Liste an Fahrzeugen auswerfen, die da registriert sind. Der GET Node kann dann für die Abfrage von 5 Apis genutzt werden: 
* Dynamic
* Effcientcy
* Service Infos
* Navigation

Dann hab ich ein paar grafische Dashboard Erweiterungen verwendet LED und Levelbars. Aber das bleibt letztendlich Geschmacksache. 

Fast alle Daten kommen aus der API Dynamic, ein paar hole ich mir noch aus Effcientcy - wie KM Laufleitung und Trip Infos und etc. 
Eine gute Beschreibung der Wertr, die ich erwarten kann (nicht alle werden immer angeboten) hab ich hier gefunden: 

[Link zu API Beschreibung ](https://github.com/edent/BMW-i-Remote#get-vehicle-data)

# Was macht der Flow
Zum einen die Daten holen und anschließend für das Dashboard die werte lesen, ggf. aufbereiten. Nahezu alle Werte sind "Strings" und so hab ich ein paar davon in INTs oder Nummern veredelt oder in Boolean. Was hat grad wo gebraucht wird. 
Zum anderen baue ich mir mit den Daten ein Apple Homekit Objekt zusammen. Das besteht in dem FLOW aus
* einen Bewegungssensor -> weil der eine Batterie als Subelement haben kann und die kann geladen werden, melden sein, hat einen Akku status und das war schon mal recht viel. 
* Window und Doors in meinem Fall jeweils zwei und eine Heckklappe. Die Motorhaube geht auch, aber die hat mich nicht interessiert. 
* ein Schließsystem - für die Zentralverrieglung
* eine Lampe für Parklicht
* Einen Bleuchtungssensor - weil das das einzige Homekit Objekt gewesen ist, das mehr al 100 als Wert eineigen kann. Und mein Mini hat nun mal mehr als 100 KM Reichweite.

![](https://user-images.githubusercontent.com/61660957/104249095-052cfb80-546b-11eb-88b9-9be02ed332a4.png)


Das Homekit zeigt nun :
* belegt an, wenn der Mini an der Steckdose hängt
* Batterie wird geladen, wenn geladen wird
* Akkustand aktuell
* Lowbatt, wenn weniger als 20% Akku
* Status der Fenster Türen und Heckklappe und 
* Reichweite in LUX

Wenn einer eine bessere Darstellung hat - als her mit :-D ich habe keine gefunden

Der Vorteil eines Homekit ist, es wird auch aktualisiert wenn ich nicht im Auto oder zuhause bin. Wenn man Online ist mit seinem Home bei Apple ( Also Applet oder IPAD hat) Dann kann man viel mit Kurzbefehlen spielen und sich alles möglichen automatisieren. 

![](https://user-images.githubusercontent.com/61660957/104249246-50470e80-546b-11eb-856b-009fed8e5bcf.png)

im Dashboard zeige ich an: 
* Letzte Fahrt, wie weit, wie lange, wann
* Service Infos, wie Wartung ( was bei einem Stromer nur alle zwei Jahre ist), Meldungen aus der Bordelektronik, wie evtl. Fehler etc. 
* aktuelle Batterieleistung in kw/h
* aktuelle Reichweite lt. Boardcomputer
* maximale Reichweite des Akkus auf Grund von Witterung und Fahrweise und so weiter. 
* Led für Laden, 
* geladen (hellgrün) 
* angeschlossen oder nicht, 
* Stekcertyp mit dem geladen wurde, wird 
* und Restladedauer als Wert
* Eine Uhr
* die Effizienz der letzten Fahrt
* und die Außentemperatur, die man sich von OpenWeather holen kann oder schlicht aus der eigenen Homematic - wie ich. 

Ich hole die Daten alle 15 Minuten ab und das kann man mit dem aktualisieren Botton triggern und ggf. beschleunigen.

Da der BMW Server ab und an rumzickt (daher nur alle 15 Minuten) muss ab und zu das Token gelöscht werden. Sonst bekommt man keine Daten mehr. Dazu habe ich eine kleine Todtmann Schaltung gebaut. Kommen nicht innerhalb von 20 Minuten Daten, lösche ich das Token in der Rasmatic (Dir www) und gut ists. 

Nicht im Flow
- Reichweite, Laden ja/nein und Reichweiteauswertungen mit Sprachausgabe auf Alexa, Grafana Mit Effizienz und so Kram halt noch. aber das überlasse ich jedem selbst. :-) 

Den Flow habe ich aus meiner Github Seite veröffentlich und halte den auch aktuell. so was lebt ja :-) 

[https://gist.github.com/Donni1966/20ed2bcdfba6e178ac735f25fcb55b07](BMW Connect als Dashboard und Homekit Object)

Ich habe noch vor, die Objekte des Minis auch in die Homematic als Objekte zu bringen. Den Flow lege ich ab, wenn ich ihn fertig habe. 

Viel Spass ... ich hoffe einer kann mal brauchen. bBi Fragen gerne eine PN. 




