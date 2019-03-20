Da das in RedMatic enthaltene node-red-contrib-ccu über das "Loopback Interface" (=locahost/127.0.0.1) direkt auf die Schnittstellenprozesse der CCU zugreift ist es für die Nutzung von RedMatic nicht notwendig in der CCU Firewall bestimmte Ports zu öffnen. 

Allerdings erfordern bestimmte Nodes die zusätzliche Ports öffnen unter Umständen das Freigeben bestimmter Ports in der Firewall:

### RedMatic-HomeKit

### node-red-contrib-alexa-local

### node-red-contrib-alexa-home-skill

