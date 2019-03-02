_RedMatic_ combines several software components to a CCU Addon, a software package for a Homematic 
CCU3 or RaspberryMatic that can be installed comfortably via the WebUI.

The basis is formed by [Node-RED](https://nodered.org/about/) with the 
[CCU Nodes for Node-RED](https://github.com/HM-RedMatic/node-red-contrib-ccu). These components offer the possibility to visually and easily create rules, automations, scripts and connections to external services and systems for a Homematic System. To a large extent even without programming knowledge. In the
[Wiki](https://github.com/HM-RedMatic/RedMatic/wiki) you can find more information about Node-RED and some 
Application examples (so-called _Flows_).

For visualization and control [RedMatic WebApp](https://github.com/HM-RedMatic/RedMatic-WebApp) and 
[Node-RED Dashboard](https://github.com/node-red/node-red-dashboard) are included. _RedMatic WebApp_ is a
User interface that can be used immediately without further configuration (comparable to _WebMatic_ or _Yahui_).
_Node-RED Dashboard_ is a configurable user interface which can offer more possibilities than the _RedMatic WebApp_, 
but needs some configuration effort. 
Example screenshots: [RedMatic WebApp](https://github.com/HM-RedMatic/RedMatic/wiki/Webapp), 
[Node-RED Dashboard](https://github.com/HM-RedMatic/RedMatic/wiki/Dashboard-Screenshots).

Furthermore the included extension 
[RedMatic HomeKit](https://github.com/HM-RedMatic/RedMatic/wiki/Homekit) makes it possible to control Homematic devices and other in Node-RED available systems via Siri and with HomeKit apps.

A connection of the CCU to a [MQTT](https://github.com/HM-RedMatic/RedMatic/wiki/Flow-MQTT) broker with convenient 
configurable topic and payload structure is simplified by a special node.

In addition, a large and active community around Node-RED created a 
[library of thousands of additional nodes](https://flows.nodered.org/?type=node&num_pages=1) which 
[can be installed](https://github.com/HM-RedMatic/RedMatic/wiki/Node-Installation) easily and offer connections to various other services and systems - 
such as the Xiaomi Aqara Smart Home System, Loxone, the Logitech Harmony Hub, various Smart TVs and AV receivers, 
Sonoff, Hue, Lightify, Tradfri, ArtNET/DMX, Modbus, Amazon Alexa, Google Home, various databases such as InfluxDB 
or MySQL, web services to query weather data and much more.

_RedMatic_ can thus - especially for those who don't want to run another server besides the CCU - provide an alternative to a "mature" Smart Home System such as Home Assistant, ioBroker, OpenHAB or FHEM. 
For the automation of a Homematic system, _RedMatic_ can also be used as an alternative or supplement to "Rega". 
Programs/Scripts. 


## Requirements

_RedMatic_ is __only suitable for the CCU3 and RaspberryMatic__. Since RedMatic may consume more than 200MB memory 
it is advisable to use a RaspberryPi with 1GB RAM (Pi 2B and up). On the CCU1/2 _RedMatic_ can not be used.

A modern browser is required to use the web interfaces, Internet Explorer is not supported.


## Quick Start

On the [Releases](https://github.com/HM-RedMatic/RedMatic/releases/latest) Page the file `redmatic-<version>.tar.gz` is available for download. After the installation of the addon via the Homematic WebUI (Control Panel -> additional software) and the subsequent reboot of the CCU is Node-RED is reachable at `http://<ccu-addresse>/addons/red`. Patience is required during installation, it can take up to ~10 minutes. Some sample flows as well as a simple dashboard are already preconfigured, the dashboard is reachable at `http://<ccu-address>/addons/red/ui`. 


## Support, Contributing

For feedback of any kind, questions, suggestions, wishes and bug reports please use the 
[Issue Tracker](https://github.com/HM-RedMatic/RedMatic/issues). Alternatively there is [Slack](https://join.slack.com/t/homematicuser/shared_invite/enQtNDgyNDM2OTkyMDA2LWY1YjY0NTE0NmY0OWM3YWUzMzAzMTgxYmRjMTMyOWE3NjkxNDdlMDY5ZjlhYzM5Nzg2N2U2YjdmNzNlYWNhNTU) 
and a [subforum in the Homematic-Forum](https://homematic-forum.de/forum/viewforum.php?f=77). 

Participation in any form is welcome and desired, especially all users are invited to extend the [list of successfully tested nodes](https://github.com/HM-RedMatic/RedMatic/wiki/Erfolgreich-getestete-Nodes), to publish sample flows and to contribute to the improvement and extension of the [documentation](https://github.com/HM-RedMatic/RedMatic/wiki).

No donations will be accepted, but I would be happy if the successful use of this software is acknowledged by giving the project a Github star ⭐️
