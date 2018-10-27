# speak text on Google Home or Chromecast

With the `node-red-contrib-cast` node it is possible to let the Google Home speak any text.

How to install Extensions?
* open Manager palette
* go to Tab Install
* search for `node-red-contrib-cast` and install
 
### 
The documentation can be found at [node-red-contrib-cast](https://github.com/Hypnos3/node-red-contrib-cast).

### Example Flow:
![example flow](https://user-images.githubusercontent.com/12692680/46281726-c6135e80-c56f-11e8-90e7-55d82366c30c.png)

Configure your local router to make sure that your google home device alway gets the same ip adress.
Open the node "change: 2 rules" and add the the ip adresse of your google home device to msg.ip 
(if it is working you may delete the debug node)

#### Example Flow with Text to speach:
```
[{"id":"2c459923.f48066","type":"debug","z":"41c55cf0.be39c4","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"true","x":790,"y":100,"wires":[]},{"id":"cbe16c75.2b27f","type":"inject","z":"41c55cf0.be39c4","name":"","topic":"test","payload":"Hallo","payloadType":"str","repeat":"","crontab":"","once":false,"onceDelay":0.1,"x":180,"y":100,"wires":[["98abbb78.b7f048"]]},{"id":"a406c701.d0f3b8","type":"cast-to-client","z":"41c55cf0.be39c4","name":"","url":null,"contentType":"","message":null,"language":"en","ip":"","port":"","volume":null,"x":610,"y":100,"wires":[["2c459923.f48066"]]},{"id":"98abbb78.b7f048","type":"change","z":"41c55cf0.be39c4","name":"","rules":[{"t":"set","p":"ip","pt":"msg","to":"192.168.178.35","tot":"str"},{"t":"set","p":"language","pt":"msg","to":"de","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":400,"y":100,"wires":[["a406c701.d0f3b8"]]}]
```

#### Example Flow with sending own url:
```
[{"id":"30969ad2.6669e6","type":"inject","z":"41c55cf0.be39c4","name":"","topic":"","payload":"true","payloadType":"bool","repeat":"","crontab":"","once":false,"onceDelay":0.1,"x":170,"y":180,"wires":[["e70fa4d6.b4cf38"]]},{"id":"e70fa4d6.b4cf38","type":"change","z":"41c55cf0.be39c4","name":"","rules":[{"t":"set","p":"ip","pt":"msg","to":"192.168.178.35","tot":"str"},{"t":"set","p":"language","pt":"msg","to":"de","tot":"str"},{"t":"set","p":"url","pt":"msg","to":"https://translate.google.com/translate_tts?ie=UTF-8&q=Hallo&tl=de&total=1&idx=0&textlen=5&tk=98540.459633&client=t&prev=input&ttsspeed=1","tot":"str"},{"t":"set","p":"contentType","pt":"msg","to":"audio/mp3","tot":"str"},{"t":"set","p":"lowerVolumeLimit","pt":"msg","to":"25","tot":"num"},{"t":"set","p":"upperVolumeLimit","pt":"msg","to":"50","tot":"num"}],"action":"","property":"","from":"","to":"","reg":false,"x":400,"y":180,"wires":[["38b8e2ce.7be9be"]]},{"id":"38b8e2ce.7be9be","type":"cast-to-client","z":"41c55cf0.be39c4","name":"","url":null,"contentType":"","message":null,"language":"en","ip":"","port":"","volume":null,"x":610,"y":180,"wires":[["35a22864.c9ba88"]]},{"id":"35a22864.c9ba88","type":"debug","z":"41c55cf0.be39c4","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"true","x":790,"y":180,"wires":[]}]
```

#### Example Flow : Catch door detector event and send a message to google home mini only when door is opened.
![Example: Homematic event triggers an audio message on google home mini](https://github.com/drose28357/Pictures/blob/master/RedMatic-Flow-Example_Google-speak_by_event.png)
```
[{"id":"528ea75c.ed80a8","type":"ccu-rpc-event","z":"5d68e9d1.2f6268","name":"Catch open door","iface":"BidCos-RF","ccuConfig":"38263145.35ea0e","rooms":"","roomsRx":"str","functions":"","functionsRx":"str","device":"MEQ0184967","deviceRx":"str","deviceName":"","deviceNameRx":"str","deviceType":"HM-Sec-SCo","deviceTypeRx":"str","channel":"MEQ0184967:1","channelRx":"str","channelName":"Kontakt-Haustür:1","channelNameRx":"str","channelType":"SHUTTER_CONTACT","channelTypeRx":"str","datapoint":"STATE","datapointRx":"str","change":true,"working":true,"cache":false,"topic":"${CCU}/${Interface}/${channelName}/${datapoint}","x":195,"y":162,"wires":[["4f73274b.c3fb58"]]},{"id":"4f73274b.c3fb58","type":"switch","z":"5d68e9d1.2f6268","name":"use only open door event","property":"payload","propertyType":"msg","rules":[{"t":"true"},{"t":"false"}],"checkall":"true","repair":false,"outputs":2,"x":428,"y":162,"wires":[["296fa469.fae57c"],[]]},{"id":"296fa469.fae57c","type":"change","z":"5d68e9d1.2f6268","name":"Set Message for arrival","rules":[{"t":"set","p":"payload","pt":"msg","to":"Da ist ja mein geliebter Schatz","tot":"str"},{"t":"set","p":"volume","pt":"msg","to":"80","tot":"str"},{"t":"set","p":"payload","pt":"msg","to":"","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":667,"y":156,"wires":[["1c1750f4.fbaa4f"]]},{"id":"1c1750f4.fbaa4f","type":"delay","z":"5d68e9d1.2f6268","name":"","pauseType":"delay","timeout":"1","timeoutUnits":"seconds","rate":"1","nbRateUnits":"1","rateUnits":"second","randomFirst":"1","randomLast":"5","randomUnits":"seconds","drop":false,"x":855,"y":155,"wires":[["c19487ea.173f08"]]},{"id":"c19487ea.173f08","type":"change","z":"5d68e9d1.2f6268","name":"Set Voume normal","rules":[{"t":"set","p":"volume","pt":"msg","to":"65","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":1047,"y":155,"wires":[["55209b11.f12554"]]},{"id":"55209b11.f12554","type":"cast-to-client","z":"5d68e9d1.2f6268","name":"Google Home mini","url":"","contentType":"","message":"","language":"de","ip":"192.168.101.28","port":"","volume":"40","x":1262,"y":154,"wires":[[]],"icon":"node-red-contrib-cast/google-home-mini2.svg"},{"id":"38263145.35ea0e","type":"ccu-connection","z":"","name":"localhost","host":"localhost","regaEnabled":true,"bcrfEnabled":true,"iprfEnabled":true,"virtEnabled":true,"bcwiEnabled":false,"cuxdEnabled":false,"regaPoll":true,"regaInterval":"30","rpcPingTimeout":"60","rpcInitAddress":"127.0.0.1","rpcServerHost":"127.0.0.1","rpcBinPort":"2047","rpcXmlPort":"2048"}]
```