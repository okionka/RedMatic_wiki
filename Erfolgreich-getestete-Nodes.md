---
Title: Erfolgreich getestete Nodes
Category: Administration
---

### Bitte diese Liste ergänzen!

| Name/Link | Beschreibung | Lässt sich installieren | Erfolgreich getestet | Anmerkungen |
| --------- | ------------ | ----------------------- | -------------------- | ----------- |
| [node-red-contrib-alexa-local](https://flows.nodered.org/node/node-red-contrib-alexa-local) | | ✅| ✅ | |
| [node-red-contrib-azure-iot-hub](https://www.npmjs.com/package/node-red-contrib-azure-iot-hub) | | ✅ |✅ |benötigt Azure subscription und aktivierten [IoT Hub](https://azure.microsoft.com/de-de/services/iot-hub/)|
| [node-red-contrib-better-sonos](https://flows.nodered.org/node/node-red-contrib-better-sonos) | | ✅| | |
| [node-red-contrib-blindcontroller](https://flows.nodered.org/node/node-red-contrib-blindcontroller) | | ✅ | ✅ | | 
| [node-red-contrib-blockly](https://flows.nodered.org/node/node-red-contrib-blockly) | | ✅ | ✅ | | 
| [node-red-contrib-boolean-logic](https://flows.nodered.org/node/node-red-contrib-boolean-logic) | | ✅ | ✅ | | 
| [node-red-contrib-broadlink](https://flows.nodered.org/node/node-red-contrib-broadlink) | | ✅ | ✅ | | 
| [node-red-contrib-bt-presence](https://flows.nodered.org/node/node-red-contrib-bt-presence) | Anwesenheitserkennung über Bluetooth| ✅ |⚠️  | Bluetooth aktivieren auf CCU: `touch /etc/config/enableBluetooth ; /etc/init.d/S31bluetooth restart` | 
| [node-red-contrib-cast](https://flows.nodered.org/node/node-red-contrib-cast) | | ✅ | ✅ | ist der Nachfolger zu [node-red-contrib-chromecast](https://flows.nodered.org/node/node-red-contrib-chromecast) |
| [node-red-contrib-chromecast](https://flows.nodered.org/node/node-red-contrib-chromecast) | | ✅ | :exclamation: | Achtung! Ein Verbindungsabbruch verursacht einen RedMatic absturz. [Issue #7](https://github.com/hobbyquaker/RedMatic/issues/7) |
| [node-red-contrib-combine](https://flows.nodered.org/node/node-red-contrib-combine) | | ✅ | ✅ | |
| [node-red-contrib-counter](https://flows.nodered.org/node/node-red-contrib-counter) | | ✅ | ✅ | |
| [node-red-contrib-cpu](https://flows.nodered.org/node/node-red-contrib-cpu) | | ✅ | ✅ | |
| [node-red-contrib-dashboard-average-bars](https://flows.nodered.org/node/node-red-contrib-dashboard-average-bars) | | ✅ | | |
| [node-red-contrib-device-stats](https://flows.nodered.org/node/node-red-contrib-device-stats) | | ✅ | ✅ | |
| [node-red-contrib-dwd](https://flows.nodered.org/node/node-red-contrib-dwd) | | ✅ | ✅ | |
| [node-red-contrib-edge-trigger](https://flows.nodered.org/node/node-red-contrib-edge-trigger) | | ✅ | ✅ | |
| [node-red-contrib-eiscp](https://github.com/estbeetoo/node-red-contrib-eiscp) | Steuerung von Integra/Onkyo-Geräten (AVR, BD-Player, etc.) mit Hilfe des eISCP-Protokolls | ✅ | ✅ | Ältere Node-red Contribution aber immer noch funktional, da Onkyo auch in seinen neueren Receivern das Protokoll noch unterstützt. |
| [node-red-contrib-filter](https://flows.nodered.org/node/node-red-contrib-filter) | | ✅ |✅  | |
| [node-red-contrib-fritz](https://flows.nodered.org/node/node-red-contrib-fritz) | Zugang zur Fritzbox mittels TR064 API | ✅ |✅  | Erfolgreich getestete Nodes bisher `fritzbox-in` und `fritzbox-calllist` auf Basis 7590 und FritzOS 7 |
| [node-red-contrib-german-holidays](https://www.npmjs.com/package/node-red-contrib-german-holidays) | Feiertagsberechnung für Deutschland | ✅ | ✅ | |
| [node-red-contrib-google-action-dialogflow-http](https://flows.nodered.org/node/node-red-contrib-google-action-dialogflow-http) | | ✅ | | |
| [node-red-contrib-google-tts](https://flows.nodered.org/node/node-red-contrib-google-tts) | | ✅ | ✅ | |
| [node-red-contrib-harmony](https://flows.nodered.org/node/node-red-contrib-harmony) | Logitech Harmony Hub | ✅ | ✅ | Installation dauert aufgrund von Dependencies die via `git clone` installiert werden aussergewöhnlich lang, UI spiegelt Installationsfortschritt nicht richtig wieder (Spinner verschwindet verfrüht), Geduld notwendig, nicht erneut auf _Install_ klicken! | 
| [node-red-contrib-huemagic](https://flows.nodered.org/node/node-red-contrib-huemagic) | | ✅ | ✅ | |
| [node-red-contrib-ifttt](https://github.com/diegopamio/node-red-contrib-ifttt) | | ✅ | |benötigt IFTTT Account https://ifttt.com/ |
| [node-red-contrib-influxdb](https://flows.nodered.org/node/node-red-contrib-influxdb) | | ✅ | ✅ | |
| [node-red-contrib-lgtv](https://flows.nodered.org/node/node-red-contrib-lgtv) | | ✅ | ✅ | |
| [node-red-contrib-light-scheduler](https://flows.nodered.org/node/node-red-contrib-light-scheduler) | | ✅ | ✅ | |
| [node-red-contrib-lodash-throttle](https://flows.nodered.org/node/node-red-contrib-lodash-throttle) | | ✅ | ✅ | |
| [node-red-contrib-mi-devices](https://flows.nodered.org/node/node-red-contrib-mi-devices) | Xiaomi Aqara Mi Home | ✅ | ✅ | |
| [node-red-contrib-milight-2](https://flows.nodered.org/node/node-red-contrib-milight-2) | | ✅ | ✅ | |
| [node-red-contrib-mysensors](https://github.com/tbowmo/node-red-contrib-mysensors) | [MySensors DIY Home Automation and IoT](https://www.mysensors.org/) | ✅ | ✅ | |
| [node-red-contrib-netatmo](https://flows.nodered.org/node/node-red-contrib-netatmo) |Netatmogeräte in Node-Red anzeigen| ✅ |✅ |benötigt API-Key und Mac-Adresse des Gerätes |
| [node-red-contrib-node-hue](https://flows.nodered.org/node/node-red-contrib-node-hue) | | ✅ | ✅ | |
| [node-red-contrib-node-lifx](https://flows.nodered.org/node/node-red-contrib-node-lifx) | | ✅ | | |
| [node-red-contrib-nora](https://flows.nodered.org/node/node-red-contrib-nora) | | ✅ | ✅ | |
| [node-red-contrib-pushover](https://flows.nodered.org/node/node-red-contrib-pushover) | | ✅ | ✅ | |
| [node-red-contrib-redis](https://flows.nodered.org/node/node-red-contrib-redis) | | ✅ | | |
| [node-red-contrib-ringdoorbell](https://flows.nodered.org/node/node-red-contrib-ringdoorbell) | | ✅ | | |
| [node-red-contrib-s7comm](https://flows.nodered.org/node/node-red-contrib-s7comm) | | ✅ | | |
| [node-red-contrib-sonoff-tasmota](https://flows.nodered.org/node/node-red-contrib-sonoff-tasmota) | | ✅ | | |
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
| [node-red-contrib-viera](https://flows.nodered.org/node/node-red-contrib-viera) | | ✅ | | |
| [node-red-contrib-xiaomi-miio](https://flows.nodered.org/node/node-red-contrib-xiaomi-miio) |  | ✅ | ✅ | |
| [node-red-node-darksky](https://www.npmjs.com/package/node-red-node-darksky) |Abruf von aktuellen Wetterdaten und Wettervorhersage | ✅ | ✅ |benötigt [API](https://darksky.net/dev/) |
| [node-red-node-mysql](https://flows.nodered.org/node/node-red-node-mysql) | | ✅ | | |
| [node-red-node-openweathermap](https://flows.nodered.org/node/node-red-node-openweathermap) |Standort Wetterdaten auslesen | ✅ | ✅ | benötigt [API Key](http://openweathermap.org/appid) | 
| [node-red-node-ping](https://flows.nodered.org/node/node-red-node-ping) | | ✅ | | |
| [node-red-node-random](https://flows.nodered.org/node/node-red-node-random) | | ✅ | ✅ | |
| [node-red-node-sentiment](https://flows.nodered.org/node/node-red-node-sentiment) | | ✅ | | |
| [node-red-node-smooth](https://flows.nodered.org/node/node-red-node-smooth) | | ✅ | ✅ | |
| [node-red-node-wol](https://flows.nodered.org/node/node-red-node-wol) | | ✅ | | |
| [node-red-contrib-pushbullet](https://flows.nodered.org/node/node-red-node-pushbullet) | | ✅ | ✅ | benötigt [API Key](https://docs.pushbullet.com/) |
| [node-red-contrib-volumio](https://flows.nodered.org/node/node-red-contrib-volumio) | | ✅ | ✅ | |