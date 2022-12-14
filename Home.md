* [Einleitung](Intro)
* [FAQ - Häufig gestellte Fragen](Faq)
* Administration
  * [Installation](Installation)
  * [Update](Update)
  * [Backup](Backup)
  * [Firewall](Firewall)
  * [Context Storage Konfigurieren](Context-Storage)
  * [Passwort Schutz für Node-RED einrichten](Passwort)
  * [Sicherheits-Hinweise](Sicherheit)
  * [Zusätzliche Nodes installieren](Node-Installation)
  * [Erfolgreich mit RedMatic getestete Nodes](Erfolgreich-getestete-Nodes) - bitte diese Liste ergänzen!
  * [Log-Level erhöhen für Fehleranalyse](Loglevel)
  * [Safe Mode](Safe-Mode)
  * [Deinstallation](Deinstallation)
* Nutzung
  * [Node-RED Grundlagen](Node-RED)
  * [CCU Nodes](CCU-Nodes)
  * [Tipps](Tipps)
  * [Flows exportieren](Flow-Export)
  * [Flows importieren](Flow-Import)
* Spezielle Nodes und Erweiterungen
  * [node-red-contrib-zigbee](ZigBee) - Einbindung von Zigbee Geräten über USB-Interface (z.B. Xiaomi Aqara, Philips Hue, IKEA Tradfri, Osram/Ledvance Lightify, Müller Licht Tint, ...)
  * [RedMatic-HomeKit](Homekit) - Anbindung an Apple HomeKit, Steuerung via Siri und Home.app
  * [RedMatic-WebApp](Webapp)
  * [Node-RED Dashboard](Dashboard-Screenshots)
  * [node-red-contrib-sun-position](https://github.com/rdmtc/node-red-contrib-sun-position) Zeit- und Sonnenstandabhängige Funktionen, Komfortable Beschattungssteuerung
  * [node-red-contrib-signal-client](node-red-contrib-signal-client)

* Beispiel Flows
  * [Kostenlose Alexa (und Google) Anbindung](Node-RED-Smart-Home-Control)
  * [Sprachausgabe über Alexa/Echo](Sprachausgabe-mit-node-red-contrib-alexa-remote2)
  * [CCU an MQTT anbinden](Flow-MQTT)
  * [Anzahl und Liste offener Fenster im Dashboard anzeigen](Flow-Windows)
  * [Hue Lampen mit langem Tastendruck dimmen](Flow-Hue)
  * [UNREACH Meldung unterdrücken](Flow-Unreach)
  * [STICKY_UNREACH Meldungen bestätigen und zählen](Flow-Sticky)
  * [Anzeigen und Setzen von Systemvariablen im Dashboard](Flow-Sysvar-Dashboard)
  * [DutyCycle Graph im Dashboard anzeigen](Flow-DutyCycle)
  * [JSON Daten von Webservice abfragen und in Systemvariable schreiben](Flow-HTTP-Client)
  * [Inhalt einer Systemvariablen über einfachen Webservice bereitstellen](Flow-HTTP-Server)
  * [Per Pushover benachrichtigen wenn Fenster länger als 10 Minuten offen ist](Flow-Window-Pushover)
  * [CPU Auslastung als Graph im Dashboard anzeigen](Flow-CPU-Usage)
  * [Schnelles Blinken der LED im Offline-Betrieb unterbinden](Flow-Offline-LED)
  * [Bidcos-Wired Dimmer mit Bidcos-RF Tasten steuern](Flow-Wired-Dimmer)
  * [Discovery von Geräten mit Echo Dot v3 und node-red-contrib-amazon-echo](Discovery-von-Geräten-mit-Echo-Dot-v3-und-node-red-contrib-amazon-echo)
* Von Usern bereitgestellte Flows
  * [Licht mittels Tastendruck aus und einschalten](Flow-simple-toggle-light)
  * [Licht schalten mit einem Dashboard button](combine-logic-node-for-toggle-state)
  * [Textausgabe mittels Chromecast oder Google Home](Flow-speak-text-on-Google)
  * [Berechnung von Feiertagen](Flow-to-calculate-german-holidays)
  * [Funktion nur innerhalb einer bestimmten Uhr-Zeit ausführen](Flow-within-time)
  * [Fehlerüberwachung der CCU](Flow-Syslog)
  * [Integration Weatherman (JSON, httpStatic, SteelSeries Gauges)](https://github.com/Sineos/node-red-contrib-weatherman/blob/master/README_DE.md)
  * [Systeminformationen der CCU Zentrale](https://github.com/Sineos/redmatic-flow-sysinfo/blob/master/README_DE.md)
  * [Werte in InfluxDB speichern](Flow-Influx)
  * [Diverse Flows von](https://github.com/Sineos/redmatic-flow-misc) [@Sineos](https://github.com/Sineos/)
  * [Harmony Activities mit Homekit nutzen](Harmony-Activities-mit-Homekit-nutzen)
  * [Homekit: Kamera einbinden](https://github.com/rdmtc/RedMatic/wiki/Homekit-Kamera-einbinden)
  * [Homekit: Öffnen einer Tür mit Keymatic HM-Sec-Key-(S)](https://github.com/rdmtc/RedMatic/wiki/Open-Workaround-für-HM-Sec-Key)
  * [Nachrichten an Telegram versenden](https://github.com/rdmtc/RedMatic/wiki/Nachrichten-an-Telegram-versenden)
  * [Dashbuttons ohne zusätzliche Nodes auswerten](https://github.com/holgerimbery/redmatic_flows/blob/master/dashbutton_auswerten/README.md)
  * [Monitoring der Batteriespannung von Aktoren (hier: HM-CC-RT-DN)](https://github.com/holgerimbery/redmatic_flows/blob/master/battery_monitoring/README.md)
  * [Datenpunktstatus von mehreren Geraeten gleichzeitig abfragen](flow-geraete-abfragen)
  * [Rollladen und Jalousiesteuerung](https://github.com/rdmtc/RedMatic/wiki/Rollladen-und-Jalousiesteuerung)
  * [Zwischen zwei Zeitpunkten jede halbe Stunde einen Inject generieren](https://github.com/rdmtc/RedMatic/wiki/Zwischen-zwei-Zeitpunkten-jede-halbe-Stunde-einen-Inject-generieren)
  * [Wetterdaten mittels OpenWeatherMap in ein CUxD Device übertragen](Openweathermap)
  * [Schalter mit Statusanzeige](Schalter-mit-Status-als-Badge-Ersatz)
  * [Pillenförmige-Schalter sychron mit globaler Variable](Pillenförmige-Schalter-synchron-mit-globalen-Variablen)
  * [Zusätzliche Wettericons für UI-Dashboard in Redmatic verfügbar machen](Zusätzliche-Wettericons-für-UI-Dashboard-in-Redmatic-verfügbar-machen)
  * [E3DC Anbindung per Modbus-TCP](https://github.com/rdmtc/RedMatic/wiki/E3DC-Anbindung-per-Modbus-TCP)
  * [Steuerung von Miele Geräten](https://github.com/rdmtc/RedMatic/wiki/Steuerung-Miele)
  * [Subflow für Enigma2 Receiver](https://github.com/Matten-Matten/node-red-enigma2-flow)
  * [INSTAR Kameras anbinden](https://wiki.instar.de/Erweitert/Homematic_CCU3_und_RedMatic/)
  * [Subflow für Home24-Mediaplayer App](https://github.com/Matten-Matten/node-red-home24-mediaplayer-flow)
  * [EASY Push Subflow Push Nachrichten an EASY-Smarthome App oder Smartha App](https://github.com/Matten-Matten/Redmatic-EASY-Push-Flow)
  * [Shelly Relais zu Schalten von Leuchten](https://github.com/rdmtc/RedMatic/wiki/Shelly-Relais-zum-Schalten-von-Leuchten)
  * [Waschmaschine fertig? Waschmaschine mit HmIP-PSM Messsteckdose monitoren](https://github.com/rdmtc/RedMatic/wiki/Waschmaschine-fertig%3F-Waschmaschine-mit-hmip-psm-Messsteckdose-monitoren)
  * [SMS mit SIM800 Modul: SMS senden & empfangen](https://github.com/Matten-Matten/SIM800-NodeRed)
  * [BMW Connect Status in Dashboard und Apple HomeKit](https://github.com/rdmtc/RedMatic/wiki/BMW-Connect-Status-in-Dashboard-und-als-Apple-Homekit-Objekt)
  * [EgiGeoZone Geofence Subflow: An/abmelden von Geozonen, in Redmatic empfangen](https://github.com/Matten-Matten/EgiGeoZone-Geofence-Subfow/blob/main/README.md)
  * [Xiaomi / Roborock S1-S6 in Dashboard](https://github.com/rdmtc/RedMatic/wiki/Xiaomi-Staubsauger-in-Dashboard#roborock-oder-xiaomi-staubsauger-s1-s6-im-dashboard)
  * [Anrufsperre über Fritzbox für eingehende Anrufe](https://github.com/rdmtc/RedMatic/wiki/Anrufsperre-%C3%BCber-Fritzbox)
  * [AIO NEO Popup Subflow (öffnen von AIO-NEO Popups auf Tablet oder Smartphone)](https://github.com/Matten-Matten/AIO-NEO-Pop-up-Subflow)

* Sonstiges
  * [Berichterstattung, Blogbeiträge, Videos über RedMatic](Berichterstattung)
  * [Node-RED Link Sammlung](Links)
  * [Telemetrie](Telemetry)
  * [Danksagungen](Danke)
  * [Change History](CHANGE_HISTORY)

