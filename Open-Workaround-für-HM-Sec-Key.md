---
Title: Homekit - Öffnen einer Tür mit Keymatic HM-Sec-Key-(S)
Category: User Flows
---

RedMatic-Homekit unterstützt z.Z. nur das Verriegeln und Entriegeln der HM-Sec-Key-(S),
mit einem kleinen flow unter Zuhilfenahme des RedMatic-homekit universal-node kann jedoch sehr einfach ein Taster zum Öffnen der Tür nachgebildet werden.

Hiermit wird die Tür verriegelt, entriegelt und geöffnet (Zurückziehen der Türfalle)


![flow](https://github.com/holgerimbery/environment/raw/master/flow.png)

flow: 
```
[{"id":"f45edc8d.b2be4","type":"redmatic-homekit-universal","z":"466feb8e.16f864","bridgeConfig":"2772bfc.4b9434","name":"Tueröffner","services":[{"subtype":"0","service":"Switch","name":"{"}],"x":130,"y":2760,"wires":[["f75b26b6.985118"]]},{"id":"a73db50c.b39158","type":"ccu-set-value","z":"466feb8e.16f864","name":"Schliesssystem (open)","iface":"BidCos-RF","ccuConfig":"9c245f65.ab92f","rooms":"","roomsRx":"str","functions":"","functionsRx":"str","device":"","deviceRx":"str","deviceName":"","deviceNameRx":"str","deviceType":"","deviceTypeRx":"str","channel":"","channelRx":"str","channelName":"Schliesssystem","channelNameRx":"str","channelType":"","channelTypeRx":"str","datapoint":"OPEN","datapointRx":"str","delay":"500","x":600,"y":2760,"wires":[]},{"id":"f75b26b6.985118","type":"switch","z":"466feb8e.16f864","name":"if payload is true","property":"payload","propertyType":"msg","rules":[{"t":"true"}],"checkall":"true","repair":false,"outputs":1,"x":320,"y":2760,"wires":[["d09a5517.49c4f8","a73db50c.b39158"]]},{"id":"d09a5517.49c4f8","type":"delay","z":"466feb8e.16f864","name":"","pauseType":"delay","timeout":"250","timeoutUnits":"milliseconds","rate":"1","nbRateUnits":"1","rateUnits":"second","randomFirst":"1","randomLast":"5","randomUnits":"seconds","drop":false,"x":490,"y":2900,"wires":[["a17b25ea.f16828"]]},{"id":"a17b25ea.f16828","type":"change","z":"466feb8e.16f864","name":"set payload to false","rules":[{"t":"set","p":"payload","pt":"msg","to":"false","tot":"bool"}],"action":"","property":"","from":"","to":"","reg":false,"x":690,"y":2900,"wires":[["f45edc8d.b2be4"]]},{"id":"2a991049.c106b","type":"comment","z":"466feb8e.16f864","name":"Schliesssystem (open)","info":"","x":160,"y":2720,"wires":[]},{"id":"2772bfc.4b9434","type":"redmatic-homekit-bridge","z":"","name":"RedMatic Bridge","username":"CC:22:3D:E3:CE:C8","pincode":"031-45-155","port":"51826"},{"id":"9c245f65.ab92f","type":"ccu-connection","z":"","name":"CCU (localhost)","host":"127.0.0.1","regaEnabled":true,"bcrfEnabled":true,"iprfEnabled":true,"virtEnabled":true,"bcwiEnabled":false,"cuxdEnabled":true,"regaPoll":true,"regaInterval":"30","rpcPingTimeout":"60","rpcInitAddress":"127.0.0.1","rpcServerHost":"0.0.0.0","rpcBinPort":"2068","rpcXmlPort":"2069","contextStore":""}]
```

Ablauf:

Auslösen von OPEN und automatisches Zurücksetzen des Nodes auf false um einen Taster zu simulieren.

**Details für die einzelnen Nodes:**

universal-node:
![universal-node](https://github.com/holgerimbery/environment/raw/master/universal-node.png)

switch-node
![switch-node](https://github.com/holgerimbery/environment/raw/master/switch-node.png)

CCU set-value-node
![set-value-node](https://github.com/holgerimbery/environment/raw/master/set-value-node.png)

delay-node
![delay-node](https://github.com/holgerimbery/environment/raw/master/delay-node.png)
change-node
![change-node](https://github.com/holgerimbery/environment/raw/master/change-node.png)
