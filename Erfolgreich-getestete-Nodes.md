---
Title: Erfolgreich getestete Nodes
Category: Administration
---

### Bitte diese Liste ergänzen!

| Name/Link | Beschreibung | Lässt sich installieren | Erfolgreich getestet | Anmerkungen |
| --------- | ------------ | ----------------------- | -------------------- | ----------- |
| [node-red-contrib-aedes](https://flows.nodered.org/node/node-red-contrib-aedes)|  MQTT server (broker) z. B. für Shelly devices| ✅| ✅ | | 
| [node-red-contrib-alexa-local](https://flows.nodered.org/node/node-red-contrib-alexa-local) | | ✅| Nein | funktioniert nicht mehr seit 2019-09 -> alternative ist: [node-red-contrib-amazon-echo](https://flows.nodered.org/node/node-red-contrib-amazon-echo) oder [node-red-contrib-amazon-echo-ext](https://flows.nodered.org/node/node-red-contrib-amazon-echo-ext) | 
| [node-red-contrib-amazon-echo](https://flows.nodered.org/node/node-red-contrib-amazon-echo) | erstellt virtuelle geräte die von Alexa erkannt werden | ✅ | ✅ | zum erkennen der virtuellen Geräte muss tep. die lighttpd.conf anzupassen > [Tool](https://homematic-forum.de/forum/viewtopic.php?f=77&t=55863&p=660777#p660777) <  [Discovery-von-Geräten-mit-Echo-Dot-v3](https://github.com/rdmtc/RedMatic/wiki/Discovery-von-Ger%C3%A4ten-mit-Echo-Dot-v3-und-node-red-contrib-amazon-echo) | 
| [node-red-contrib-amazon-echo-ext](https://flows.nodered.org/node/node-red-contrib-amazon-echo-ext) | erstellt virtuelle geräte die von Alexa erkannt werden | ✅ | ✅ | zum erkennen der virtuellen Geräte muss tep. die lighttpd.conf anzupassen > [Tool](https://homematic-forum.de/forum/viewtopic.php?f=77&t=55863&p=660777#p660777) <  [Discovery-von-Geräten-mit-Echo-Dot-v3](https://github.com/rdmtc/RedMatic/wiki/Discovery-von-Ger%C3%A4ten-mit-Echo-Dot-v3-und-node-red-contrib-amazon-echo) | 
| [node-red-contrib-alexa-home-skill](https://flows.nodered.org/node/node-red-contrib-alexa-home-skill) | | ✅| ✅ | account notwendig| 
| [node-red-contrib-alexa-remote2](https://flows.nodered.org/node/node-red-contrib-alexa-remote2) | Echo ansteuern, Sprachausgabe u.v.m. | ✅| ✅ | wird aktuell nicht weiterentwickelt -> alternative ist: [node-red-contrib-alexa-cakebaked](https://flows.nodered.org/node/node-red-contrib-alexa-cakebaked) oder [node-red-contrib-alexa-remote2-v2](https://flows.nodered.org/node/node-red-contrib-alexa-remote2-v2)| 
| [node-red-contrib-alexa-smart-home](https://flows.nodered.org/node/node-red-contrib-alexa-smart-home) | Alexa und Google Home Anbindung| ✅| ✅ | account notwendig| 
| [node-red-contrib-avr-yamaha](https://flows.nodered.org/node/node-red-contrib-avr-yamaha) | Ansteuerung von Yamaha AV-Receivern | ✅ |✅ |nicht alle Befehle werden von jedem Receiver unterstützt (z. B. nur POWER und nicht POWEROFF)|
| [node-red-contrib-azure-iot-hub](https://www.npmjs.com/package/node-red-contrib-azure-iot-hub) | | ✅ |✅ |benötigt Azure subscription und aktivierten [IoT Hub](https://azure.microsoft.com/de-de/services/iot-hub/)|
| [node-red-contrib-better-sonos](https://flows.nodered.org/node/node-red-contrib-better-sonos) | | ✅| | |
| [node-red-contrib-blindcontroller](https://flows.nodered.org/node/node-red-contrib-blindcontroller) | | ✅ | ✅ | | 
| [node-red-contrib-blockly](https://flows.nodered.org/node/node-red-contrib-blockly) | | ✅ | ✅ | | 
| [node-red-contrib-boolean-logic](https://flows.nodered.org/node/node-red-contrib-boolean-logic) | | ✅ | ✅ | | 
| [node-red-contrib-bool-gate](https://flows.nodered.org/node/node-red-contrib-bool-gate) | | ✅ | ✅ | | 
| [node-red-contrib-broadlink](https://flows.nodered.org/node/node-red-contrib-broadlink) | | ✅ | ✅ | | 
| [node-red-contrib-bt-presence](https://flows.nodered.org/node/node-red-contrib-bt-presence) | Anwesenheitserkennung über Bluetooth| ✅ |⚠️  | Bluetooth aktivieren auf CCU: `touch /etc/config/enableBluetooth ; /etc/init.d/S31bluetooth restart` | 
| [node-red-contrib-cast](https://flows.nodered.org/node/node-red-contrib-cast) | | ✅ | ✅ | ist der Nachfolger zu [node-red-contrib-chromecast](https://flows.nodered.org/node/node-red-contrib-chromecast) |
| [node-red-contrib-chromecast](https://flows.nodered.org/node/node-red-contrib-chromecast) | | ✅ | :exclamation: | Achtung! Ein Verbindungsabbruch verursacht einen RedMatic absturz. [Issue #7](https://github.com/hobbyquaker/RedMatic/issues/7) |
| [node-red-contrib-color-convert](https://flows.nodered.org/node/node-red-contrib-color-convert) | Konvertieren zwischen Farbdarstellungen (z. B. RGB zu HSV) | ✅ | ✅ | |
| [node-red-contrib-combine](https://flows.nodered.org/node/node-red-contrib-combine) | | ✅ | ✅ | |
| [node-red-contrib-counter](https://flows.nodered.org/node/node-red-contrib-counter) | | ✅ | ✅ | |
| [node-red-contrib-cpu](https://flows.nodered.org/node/node-red-contrib-cpu) | | ✅ | ✅ | |
| [node-red-contrib-credentials](https://flows.nodered.org/node/node-red-contrib-credentials) | statt inject/change node bei kritischen Daten (passwords) | ✅ | ✅ | Sinnvoll, wenn die Projektfunktion in Verbindung mit einem public repository verwendet wird und tokens (AWS) verwendet werden |
| [node-red-contrib-dashboard-average-bars](https://flows.nodered.org/node/node-red-contrib-dashboard-average-bars) | | ✅ | | |
| [node-red-contrib-deconz](https://flows.nodered.org/node/node-red-contrib-deconz) | Node-Red Nodes für den Zigbee deCONZ-USB-Stick/RaspBee II HAT | ✅ | ✅ | Getestet wurde hierfür der [RaspBee II-HAT](https://phoscon.de/de/raspbee2) auf einem separatem Raspberry Pi. Es erfolgte explizit kein Test des [deCONZ Conbee II](https://phoscon.de/de/conbee2/) direkt an einem CCU USB-Port oder mit RaspberryMatic |
| [node-red-contrib-device-stats](https://flows.nodered.org/node/node-red-contrib-device-stats) | | ✅ | ✅ | |
| [node-red-contrib-dwd](https://flows.nodered.org/node/node-red-contrib-dwd) | | ✅ | ✅ | |
| [node-red-contrib-edge-trigger](https://flows.nodered.org/node/node-red-contrib-edge-trigger) | | ✅ | ✅ | |
| [node-red-contrib-timed-counter](https://github.com/tomgidden/node-red-contrib-timed-counter) | Node der Messages zählt, die in einem bestimmten Zeitlimit empfangen wurden. | ✅ | ✅ | Klassischer Anwendungsfall zum Unterscheiden von Single vs. Double Press von Buttons, die eine Message bei einem Release-Event auf diesem erzeugen (z. B. [deCONZ Conbee II/raspBee II](https://phoscon.de/de/conbee2/)). Funktioniert auch für Tripple Press usw. |
| [node-red-contrib-eiscp](https://github.com/estbeetoo/node-red-contrib-eiscp) | Steuerung von Integra/Onkyo-Geräten (AVR, BD-Player, etc.) mit Hilfe des eISCP-Protokolls | ✅ | ✅ | Ältere Node-red Contribution aber immer noch funktional, da Onkyo auch in seinen neueren Receivern das Protokoll noch unterstützt. |
| [node-red-contrib-filter](https://flows.nodered.org/node/node-red-contrib-filter) | | ✅ |✅  | |
| [node-red-contrib-fritz](https://flows.nodered.org/node/node-red-contrib-fritz) | Zugang zur Fritzbox mittels TR064 API | ✅ |✅  | Erfolgreich getestete Nodes auf Basis FritzBox 7590 und FritzOS 7 |
| [node-red-contrib-german-holidays](https://www.npmjs.com/package/node-red-contrib-german-holidays) | Feiertagsberechnung für Deutschland | ✅ | ✅ | |
| [node-red-contrib-google-action-dialogflow-http](https://flows.nodered.org/node/node-red-contrib-google-action-dialogflow-http) | | ✅ | | |
| [node-red-contrib-google-tts](https://flows.nodered.org/node/node-red-contrib-google-tts) | | ✅ | ✅ | |
| [node-red-contrib-harmony](https://flows.nodered.org/node/node-red-contrib-harmony) | Logitech Harmony Hub | ✅ | ✅ | Installation dauert aufgrund von Dependencies die via `git clone` installiert werden aussergewöhnlich lang, UI spiegelt Installationsfortschritt nicht richtig wieder (Spinner verschwindet verfrüht), Geduld notwendig, nicht erneut auf _Install_ klicken! | 
| [node-red-contrib-homekit-bridged](https://github.com/NRCHKB/node-red-contrib-homekit-bridged) | Alternative zum RedMatic-HomeKit "Universal Accessory" für die Anbindung von nicht-Homematic Geräten | ✅ | ✅ | Achtung, es kann mehr als eine Bridge konfiguriert werden. Diese müssen auf unterschiedliche Ports verweisen und in Homematic müssen diese Ports entsprechend konfiguriert sein. Die verwendeten Ports müssen in der CCU Firewall freigegeben werden. Getestet und verwendet seit RedMatic-Release ab 4.3.5 bis 7.2.1 und node-red-contrib-homekit-bridged ab 0.5.1 bis 1.3.4. Bitte auch die Mindestanforderungen and nodeJS, NPM und node-red im jeweiligen RedMatic-Release beachten |
| [node-red-contrib-huemagic](https://flows.nodered.org/node/node-red-contrib-huemagic) | | ✅ | ✅ | |
| [node-red-contrib-hyperion](https://flows.nodered.org/node/node-red-contrib-hyperion) | zur Steuerung eines Hyperion-Servers | ✅ | ✅ | |
| [node-red-contrib-ical-events](https://flows.nodered.org/node/node-red-contrib-ical-events) | Dieses Node RED-Modul ruft die Ereignisse von einer ical-URL oder von einem caldav-Server ab | ✅ | ✅ | |
| [node-red-contrib-ifttt](https://github.com/diegopamio/node-red-contrib-ifttt) | | ✅ | |benötigt IFTTT Account https://ifttt.com/ |
| [node-red-contrib-influxdb](https://flows.nodered.org/node/node-red-contrib-influxdb) | | ✅ | ✅ | |
| [node-red-contrib-lgtv](https://flows.nodered.org/node/node-red-contrib-lgtv) | | ✅ | ✅ | |
| [node-red-contrib-light-scheduler](https://flows.nodered.org/node/node-red-contrib-light-scheduler) | | ✅ | ✅ | |
| [node-red-contrib-lodash-throttle](https://flows.nodered.org/node/node-red-contrib-lodash-throttle) | | ✅ | ✅ | |
| [node-red-contrib-loxone](https://flows.nodered.org/node/node-red-contrib-loxone) | Loxone Miniserver Integration | ✅ | ✅ | |
| [node-red-contrib-mi-devices](https://flows.nodered.org/node/node-red-contrib-mi-devices) | Xiaomi Aqara Mi Home | ✅ | ✅ | |
| [node-red-contrib-milight-2](https://flows.nodered.org/node/node-red-contrib-milight-2) | | ✅ | ✅ | |
| [node-red-contrib-mysensors](https://github.com/tbowmo/node-red-contrib-mysensors) | [MySensors DIY Home Automation and IoT](https://www.mysensors.org/) | ✅ | ✅ | |
| [node-red-contrib-neato-botvac](https://flows.nodered.org/node/node-red-contrib-neato-botvac) | zur Steuerung und Werte Erfassung eines Neato Botvac-Roboter | ✅ | ✅ | benötigt ein NEATO Account |
| [node-red-contrib-netatmo](https://flows.nodered.org/node/node-red-contrib-netatmo) |Netatmogeräte in Node-Red anzeigen| ✅ |✅ |benötigt API-Key und Mac-Adresse des Gerätes |
| [node-red-contrib-node-hue](https://flows.nodered.org/node/node-red-contrib-node-hue) | | ✅ | ✅ | |
| [node-red-contrib-node-lifx](https://flows.nodered.org/node/node-red-contrib-node-lifx) | | ✅ | | |
| [node-red-contrib-nora](https://flows.nodered.org/node/node-red-contrib-nora) | | ✅ | ✅ | |
| [node-red-contrib-pushover](https://flows.nodered.org/node/node-red-contrib-pushover) | | ✅ | ✅ | |
| [node-red-contrib-redis](https://flows.nodered.org/node/node-red-contrib-redis) | | ✅ | | |
| [node-red-contrib-ringdoorbell](https://flows.nodered.org/node/node-red-contrib-ringdoorbell) | | ✅ | | |
| [node-red-contrib-s7comm](https://flows.nodered.org/node/node-red-contrib-s7comm) | | ✅ | | |
| [node-red-contrib-samsung-tv-control](https://flows.nodered.org/node/node-red-contrib-samsung-tv-control) | Ansteuerung von aktuellen Samsung TVs | ✅ | ✅ | Anleitung beachten. Hier wird zunächst MAC-Adresse und ein Token vom TV benötigt.|
| [node-red-contrib-simple-gate](https://flows.nodered.org/node/node-red-contrib-simple-gate) | zur Steuerung des Nachrichtenflusses | ✅ | ✅ | |
| [node-red-contrib-sonoff-tasmota](https://flows.nodered.org/node/node-red-contrib-sonoff-tasmota) | | ✅ | | |
| [node-red-contrib-sonos-plus](https://www.npmjs.com/package/node-red-contrib-sonos-plus) | only versions up to 6.1.0 | ✅|✅ |[Wiki](https://github.com/hklages/node-red-contrib-sonos-plus/wiki) |
| [node-red-contrib-sonos-events](https://www.npmjs.com/package/node-red-contrib-sonos-events) | SONOS events (subscribe/notify) only 1.0.0 | ✅|✅ |
| [node-red-contrib-sonospollytts](https://flows.nodered.org/node/node-red-contrib-sonospollytts) | Sprachausgabe auf Sonos | ✅ |⚠️ | Node-RED Port muss auf `80` konfiguriert werden |
| [node-red-contrib-sun-position](https://github.com/Hypnos3/node-red-contrib-sun-position) | Steuerung abhängig von Sonne, Mond oder Zeit | ✅ | ✅ | |
| [node-red-contrib-tahoma](https://github.com/hobbyquaker/RedMatic/issues/70) | Somfy Tahoma | ✅ | ✅ | siehe https://github.com/hobbyquaker/RedMatic/issues/70 https://github.com/nikkow/node-red-contrib-tahoma/pull/7| 
| [node-red-contrib-tankerkoenig](https://flows.nodered.org/node/node-red-contrib-tankerkoenig) | | ✅ | ✅ | benötigt [API Key](https://creativecommons.tankerkoenig.de/) | 
| [node-red-contrib-telegrambot-home](https://flows.nodered.org/node/node-red-contrib-telegrambot-home) | | ✅ | ✅ |Interaktion mit Telegrambot über Commands vereinfacht gegenüber herkömmlichem telegrambot |
| [node-red-contrib-telegrambot](https://flows.nodered.org/node/node-red-contrib-telegrambot) | | ✅ | ✅ | |
| [node-red-contrib-throttle](https://flows.nodered.org/node/node-red-contrib-throttle)  | | ✅ | ✅ | |
| [node-red-contrib-tplink-iot](https://flows.nodered.org/node/node-red-contrib-tplink-iot)  | TP-Link Smart Plug HS110 | ✅ | ✅ | |
| [node-red-contrib-tradfri](https://flows.nodered.org/node/node-red-contrib-tradfri) | | ✅ |⚠️  | siehe https://github.com/rdmtc/RedMatic/issues/131|
| [node-red-contrib-ui-led](https://flows.nodered.org/node/node-red-contrib-ui-led) | | ✅ | ✅ | |
| [node-red-contrib-ui_list](https://flows.nodered.org/node/node-red-contrib-ui_list) | | ✅ | | |
| [node-red-contrib-uibuilder](https://flows.nodered.org/node/node-red-contrib-uibuilder)  | | ✅ | ⚠️ | Workaround nötig [siehe #94](https://github.com/rdmtc/RedMatic/issues/94) |
| [node-red-contrib-unsafe-function](https://flows.nodered.org/node/node-red-contrib-unsafe-function) | | ✅ |✅  | |
| [node-red-contrib-velux](https://flows.nodered.org/node/node-red-contrib-velux) | Velux KLF-200 io-homecontrol Gateway | ✅ | ✅ | |
| [node-red-contrib-viera](https://flows.nodered.org/node/node-red-contrib-viera) | | ✅ | | |
| [node-red-contrib-xiaomi-miio](https://flows.nodered.org/node/node-red-contrib-xiaomi-miio) |  | ✅ | ✅ | |
| [node-red-node-base64](https://flows.nodered.org/node/node-red-node-base64) | Codieren und Decodieren von Nachrichten im Base64-Format | ✅ | ✅ | |node-red-node-base64
| [node-red-node-darksky](https://www.npmjs.com/package/node-red-node-darksky) | Abruf von aktuellen Wetterdaten und Wettervorhersage | ✅ | ✅ |benötigt [API](https://darksky.net/dev/); es werden jedoch keine neuen API-Subscriptions mehr angenommen, wohl als Folge der [Akquise von Darksky durch Apple](https://www.theverge.com/2020/3/31/21201666/apple-acquires-weather-app-dark-sky-shut-down-android-wear-os-ios) |
| [node-red-node-mysql](https://flows.nodered.org/node/node-red-node-mysql) | | ✅ | ✅ | |
| [node-red-node-openweathermap](https://flows.nodered.org/node/node-red-node-openweathermap) | Abruf von standortbasierten, aktuellen Wetterdaten und Wettervorhersage | ✅ | ✅ | benötigt [API Key](http://openweathermap.org/appid) | 
| [node-red-node-ping](https://flows.nodered.org/node/node-red-node-ping) | | ✅ | | |
| [node-red-node-random](https://flows.nodered.org/node/node-red-node-random) | | ✅ | ✅ | |
| [node-red-node-sentiment](https://flows.nodered.org/node/node-red-node-sentiment) | | ✅ | | |
| [node-red-node-smooth](https://flows.nodered.org/node/node-red-node-smooth) | | ✅ | ✅ | |
| [node-red-contrib-pushbullet](https://flows.nodered.org/node/node-red-node-pushbullet) | | ✅ | ✅ | benötigt [API Key](https://docs.pushbullet.com/) |
| [node-red-contrib-volumio](https://flows.nodered.org/node/node-red-contrib-volumio) | | ✅ | ✅ | |
| [node-red-contrib-weekday](https://flows.nodered.org/node/node-red-contrib-weekday) | | ✅ | ✅ | |
| [node-red-contrib-slack](https://flows.nodered.org/node/node-red-contrib-slack) | | ✅ | ✅ | |
| [node-red-node-pi-gpiod](https://flows.nodered.org/node/node-red-node-pi-gpiod) | | ✅ | ✅ | benötigt pigpiod-hm-addon (https://github.com/baycom/pigpiod-hm-addon/releases) |
| [node-red-contrib-light-scheduler](https://flows.nodered.org/node/node-red-contrib-light-scheduler) |Wochenzeitschaltuhr für Lichtsteuerung mit grafischer Auswahl der Schaltzeiten | ✅ | ✅ | |
| [node-red-node-wol](https://flows.nodered.org/node/node-red-node-wol) |Sendet Wake-On-LAN (WOL)-Magic-Pakete zum Aufwecken von im Netzwerk verbundenen Geräten im Ruhezustand | ✅ | ✅ |Aufzuweckende Geräte müssen das unterstützen und entsprechend konfiguriert sein |
| [node-red-contrib-pi-hole-remote](https://flows.nodered.org/node/node-red-contrib-pi-hole-remote) |  Steuern des [pi-hole](https://pi-hole.net) Network-wide Ad-Blocking servers  | ✅ | ✅ | Erlaubt das Ein-/Ausschalten der DNS-Filterung über Node-red mittels secure API-Token |
| [node-red-node-ui-table](https://flows.nodered.org/node/node-red-node-ui-table) | Beautiful tables | ✅ | ✅ | |
| [node-red-contrib-modbustcp](https://flows.nodered.org/node/node-red-contrib-modbustcp) | | ✅ | ✅ | |