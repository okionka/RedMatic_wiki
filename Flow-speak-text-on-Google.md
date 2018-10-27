# Warning: Currently the Node-Red will crash if the copnnection to the chromeCast will fail. I'm working on a solution to that.

With the `node-red-contrib-cast` node it is possible to let the Google Home speak any text.

How to install Extensions?
* open Manager palette
* go to Tab Install
* search for `node-red-contrib-cast` and install
 

### Example Flow:
![example flow](https://user-images.githubusercontent.com/12692680/46281726-c6135e80-c56f-11e8-90e7-55d82366c30c.png)

Configure your lokal router to make sure that your home device alway gets the same ip adress.
Open the node "change: 2 rules" and add the the ip adresse of your home device to msg.ip 
(if it is working you may delete the debug node)

#### Example Flow with Text to speach:
```
[{"id":"2c459923.f48066","type":"debug","z":"41c55cf0.be39c4","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"true","x":790,"y":100,"wires":[]},{"id":"cbe16c75.2b27f","type":"inject","z":"41c55cf0.be39c4","name":"","topic":"test","payload":"Hallo","payloadType":"str","repeat":"","crontab":"","once":false,"onceDelay":0.1,"x":180,"y":100,"wires":[["98abbb78.b7f048"]]},{"id":"a406c701.d0f3b8","type":"cast-to-client","z":"41c55cf0.be39c4","name":"","url":null,"contentType":"","message":null,"language":"en","ip":"","port":"","volume":null,"x":610,"y":100,"wires":[["2c459923.f48066"]]},{"id":"98abbb78.b7f048","type":"change","z":"41c55cf0.be39c4","name":"","rules":[{"t":"set","p":"ip","pt":"msg","to":"192.168.178.35","tot":"str"},{"t":"set","p":"language","pt":"msg","to":"de","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":400,"y":100,"wires":[["a406c701.d0f3b8"]]}]
```

#### Example Flow with sending own url:
```
[{"id":"30969ad2.6669e6","type":"inject","z":"41c55cf0.be39c4","name":"","topic":"","payload":"true","payloadType":"bool","repeat":"","crontab":"","once":false,"onceDelay":0.1,"x":170,"y":180,"wires":[["e70fa4d6.b4cf38"]]},{"id":"e70fa4d6.b4cf38","type":"change","z":"41c55cf0.be39c4","name":"","rules":[{"t":"set","p":"ip","pt":"msg","to":"192.168.178.35","tot":"str"},{"t":"set","p":"language","pt":"msg","to":"de","tot":"str"},{"t":"set","p":"url","pt":"msg","to":"https://translate.google.com/translate_tts?ie=UTF-8&q=Hallo&tl=de&total=1&idx=0&textlen=5&tk=98540.459633&client=t&prev=input&ttsspeed=1","tot":"str"},{"t":"set","p":"contentType","pt":"msg","to":"audio/mp3","tot":"str"},{"t":"set","p":"lowerVolumeLimit","pt":"msg","to":"25","tot":"num"},{"t":"set","p":"upperVolumeLimit","pt":"msg","to":"50","tot":"num"}],"action":"","property":"","from":"","to":"","reg":false,"x":400,"y":180,"wires":[["38b8e2ce.7be9be"]]},{"id":"38b8e2ce.7be9be","type":"cast-to-client","z":"41c55cf0.be39c4","name":"","url":null,"contentType":"","message":null,"language":"en","ip":"","port":"","volume":null,"x":610,"y":180,"wires":[["35a22864.c9ba88"]]},{"id":"35a22864.c9ba88","type":"debug","z":"41c55cf0.be39c4","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"true","x":790,"y":180,"wires":[]}]
```

#### How to import an example
Open Node-Red and create a new table. Set a name like for instance "GoogleSpeak" to the new table by double click on the default table name ("flow..". The press "done".
Press ctrl-i to import a folowing example as a string: Copy the example und insert into the import dialog. Click on "import to new flow".