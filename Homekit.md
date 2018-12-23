# RedMatic HomeKit

Bitte einen [Issue anlegen](https://github.com/hobbyquaker/RedMatic-HomeKit/issues) falls ein Gerät nicht unterstützt wird und gewünscht ist. Die bereits unterstützen Geräte sind hier ersichtlich: https://github.com/hobbyquaker/RedMatic-HomeKit/tree/master/homematic-devices

## Inhalt

* [Einrichtung](#einrichtung)
* [Nutzungshinweise](#nutzungshinweise)
* [Homematic Fernbedienungen/Tasten in HomeKit nutzen](#tasten)
* [Sytemvariablen](#systemvariablen)
* [CCU Programme starten](#programme)
* [Universelles Accessory, Einbinden von nicht-Homematic Geräten](#universal-accessory)
* [HomeKit Reset](#reset)


## Einrichtung

Den Node _RedMatic HomeKit - Homematic_ per Drag&Drop einem Flow hinzufügen    
![](images/homekit/homekit1.png)    

Die Konfiguration des neu hinzugefügten Node per Doppelklick öffnen, den Button mit dem Bleistift-Icon anklicken um eine neue Bridge hinzuzufügen    
![](images/homekit/homekit2.png)    

Die Standardeinstellungen können beibehalten werden, mit einem Klick auf den Button _Add_ wird die Bridge angelegt    
![](images/homekit/homekit3.png)    

Die Konfiguration des _RedMatic HomeKit - Homematic_ mit klick auf _Done_ verlassen und dann den Button _Deploy_ anklicken     
![](images/homekit/homekit4.png)    

Nochmals die Konfiguration des _RedMatic HomeKit - Homematic_ Node per Doppelklick öffnen und nochmal über den Bleistift-Button die Bridge-Konfiguration öffnen    
![](images/homekit/homekit5.png)    

Bei einer erfolgreich aktivierten Bridge wird in dem Bridge Konfigurationsdialog nun ein QR-Code angezeigt    
![](images/homekit/homekit6.png)    


In der Home App oben rechts über den Plus-Button ein neues Gerät hinzufügen, den QR-Code vom Bildschirm abscannen    
![](images/homekit/homekit7.png)    


Die Sicherheitswarnung bestätigen    
![](images/homekit/homekit8.png)    


Nun sollten alle unterstützen Geräte der CCU in der Home App erscheinen.

### Nutzungshinweise

Nicht alle Änderungen an den in HomeKit bereitgestellten Accessories werden bei einem Deploy in Node-RED übernommen. Bestimmte Änderungen erfordern nach dem Deploy einen Neustart von RedMatic:

* Entfernen von Geräten
* Umbenennen von Geräten
* Konfigurationsänderung an Geräten (z.B. entfernen des Boost Switch bei Thermostaten)
* Ändern der Anzahl der Tasten des Event Nodes
* Die konfigurierten Services eines "Universellen Accessory" ändern


### Tasten

Zum Auslösen von Aktionen in HomeKit über Homematic Fernbedienungen/Taster kann der Node _RedMatic HomeKit - Event_ genutzt werden. Er erwartet an seinem Eingang eine Message die in `msg.topic` die zu drückende Taste und die Art des Tastendrucks (kurz/lang) enthält, z.B. `1/PRESS_LONG` für einen langen Tastendruck auf Taste 1. Dieses Topic kann direkt vom RPC Event Node erzeugt werden in dem man die Topic-Konfiguration auf `${channelIndex}/${datapoint}` setzt und den Datenpunkt mit dem regulären Ausdruck `PRESS_SHORT|PRESS_LONG` filtert:

![](images/homekit/fernbedienung.png)


### Sytemvariablen

(Boolsche) Systemvariablen können über den _Redmatic HomeKit - Switch_ Node in HomeKit bereitgestellt werden. Hierzu werden die Ein- und Ausgänge eines _CCU Sysvar_ Nodes über kreuz mit dem _Redmatic HomeKit - Switch_ Node verbunden

![](images/homekit/homekit-sysvar.png)


### Programme

Leider werden bisher von der Home App und Siri keine Taster unterstützt die einen Einmaligen Event erzeugen. Als Workaround steht mit dem _redmatic homekit - button_ Node ein Schalter zur Verfügung der sich automatisch nach dem Anschalten zurücksetzt und so als "Pseudobutton" genutzt werden kann.

Dieser kann einfach mit einem _ccu - program_ Node verbunden werden, als _Payload_ wird `timestamp` ausgewählt:

![](images/homekit/homekit-pseudobutton.png)

### Universal Accessory

Mit dem Universal Accessory ist es möglich beliebige HomeKit-Geräte zu erzeugen, z.B. um damit auch Geräte abseits von Homematic einzubinden.

Dem Accessory können beliebig viele Services hinzugefügt werden. 

Verfügbare Services sowie die dafür benötigten und optionalen Characteristiken sind in dieser Datei ersichtlich: https://github.com/KhaosT/HAP-NodeJS/blob/master/lib/gen/HomeKitTypes.js

Um eine Characteristic anzulegen müssen dem Accessory beim Start Messages gesendet werden. Siehe dazu https://github.com/HM-RedMatic/RedMatic-HomeKit/issues/44



### Reset

Um die Bridge im Fall von schwerwiegenden Problemen ("sollte" nicht passieren, aber man weiss ja nie 😉) komplett zurückzusetzen kann wie folgt vorgegangen werden:

* Bridge in iOS Home App löschen
* RedMatic stoppen
* Auf der CCU das Verzeichnis `/usr/local/addons/redmatic/var/homekit` mitsamt Inhalt löschen
* RedMatic starten

Hierbei gehen alle Raum-Zuordnungen sowie Umbenennungen in HomeKit verloren!