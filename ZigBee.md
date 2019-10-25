# Installation
Im RedMatic UI (Erreichbar im CCU WebUI unter Einstellungen->Systemsteuerung) im Tab "Pakete" bei node-red-contrib-zigbee auf den Install Button klicken, danach Node-RED neustarten.

![Install Packages](images/zigbee/InstallPackage.png)

# Einrichtung
## Controller
Den Node _controller_ aus dem Ordner _zigbee_ per Drag&Drop einem Flow hinzufügen.

![Add Controller Node to Flow](images/zigbee/AddControllerNode.png)

Die Konfiguration des neu hinzugefügten Node per Doppelklick öffnen, den Button mit dem Bleistift-Icon anklicken um einen neuen Controller hinzuzufügen. Dies ist die Verbindung zu einem CC253x USB Sticks zum Beispiel welche die Admininstrationseinstellungden des Zigbee Netzwerkes zur Verfügung stellt.

![Add Coordinator](images/zigbee/AddCoordinator.png)

Folgende Einstellungen machen später ein neues Pairing der Geräte nötg und sollten daher mit Bedacht gewählt werden:
* Channels:
Dies ist der Zigbee Kanal im 2.4Ghz Netz. Da dieser Frequenzbereich auch von WLAN Netzwerken genutzt wird, sollte ein Kanal mit geringer Belegeung gewählt werden. Wer eine FritzBox sein eigen nennt, kann dies im Bereich -->WLAN --> Funkkanal nachschauen. Leider lassen sich die WLAN Kanäle nicht 1:1 in Zigbee Kanäle übernehmen. Phillips benutzt nur die Kanäle 11, 15, 20 und 25, da diese als relativ problemlos gelten ([[Quelle](https://www.digitalzimmer.de/artikel/wissen/philips-hue-zigbee-kanalwechsel/)]). Wenn man also in der Netzwerkanalyse sieht das der obere Bereich oft genutzt wird, wählt man einen unteren Kanal und Vice Versa.
* networkKey
Dieser stellt das "Password" des Netzwerkes bereit. Man sollte diesen auf einen eigenen Wert ändern, der sich aus einer 32Stelligen HEX Zahl [0..9, A..F] mit Grossbuchstaben zusammen setzt.

Der Path des Serialport gibt an, wo auf der CCU bzw. dem Raspberry der Stick eingebunden ist. Wenn es nur einen Stick gibt, ist das eigentlich immer /dev/ttyACM0, ansonsten gibt es [hier](https://www.zigbee2mqtt.io/getting_started/running_zigbee2mqtt.html) eine Anleitung wie er zu finden ist (in Englisch)

Wenn die Einstellungen gemacht sind, den ADD Button klicken.

![Setting Up Coordinator](images/zigbee/SettingsCoordinator.png)

Die Konfiguration mit _DONE_ verlassen und mit _Deploy_ speichern und aktivieren.

![Save and Deploy Coordinator](images/zigbee/SaveAndDeployCoordinator.png)

## Gerät anlernen
Auf die eben hinzugefügte Controller Node oder irgendeine andere bereits im Flow intgrierte zigbee Node doppelklicken. Als ersten Punkt findet man den Link zum "herdsman", also der zentralen Kontrolleinheit im zigbee Netzwerk, dort auch Coordinator genannt. Mit dem Bleistift die Konfiguration öffnen.

![ConfigureCoordinator.png](images/zigbee/)

1. _Permit Join_:
Den Button Permit Join anklicken. Damit läst der Coordinator zu, das sich neue Geräte im System anmelden dürfen.
1. Danach das anzulernende Gerät zurücksetzen ([Liste der unterstützten Geräte inklusive Pairing Anweisung](https://www.zigbee2mqtt.io/information/supported_devices.html)) und es sollte nach kurzer Wartezeit in der Liste mit seinem Typ, dem Hersteller und dem Modell auftauchen.
1. Mit _Stop Join_ den Anlernprozess beenden
1. Dem Device einen sinnvollen Klartextnamen geben
1. Mit _Aktualisieren_ die Konfiguration Verlassen und dann wie gehabt mit _Deploy_ speichern und aktivieren

![Join device](images/zigbee/AddDevice.png)
