## A simple Flow to toggle an actor with a single button

Similar to the previous part we want to toggle an boolean input to a sequence of alternating true and false.
Thus we need to read a state from an actor. Then invert that state and put it back to the actor.

In this scenario we want to switsch a light on and off bei using one button on the dashboard.

1. Get a dashboard-button element to your flow. You set group to your dashboard item group, set label to a name of the button to be displayed on dashboard and set the payload to "true"

2. Read the actual state of the actor with a ccu-get-value node. Set Interface to e.g. "BidCose-RF", channel to your actor and datapoint to "state". 

Now we can connect both nodes und may add a debug node to the output of get-value to do some testing on the dashboard.

3. pick a combine-nor node and connect it to the get-value node of the actor. Set name to e.g."Invert State" and set operator to "nor". We dont need any other setting because the node has a default input and a default output.
In this setup the "nor" node works like a "not" node for a boolean input.



4. pick a ccu-set-value node and set interface, channel name and data point.

Now connect all nodes in a row and enjoy your simple dashboard toggle switch.


```[{"id":"f1ea16ea.15af28","type":"ui_button","z":"cdb7abff.3cf718","name":"","group":"65a72644.483318","order":3,"width":0,"height":0,"passthru":false,"label":"Wohnzimmer-Licht ","tooltip":"","color":"","bgcolor":"","icon":"","payload":"true","payloadType":"bool","topic":"toogle boolean","x":190,"y":1400,"wires":[["f6e8a64f.25cfa8"]]},{"id":"65a4a2b9.a3f68c","type":"ccu-set-value","z":"cdb7abff.3cf718","name":"SetValue Wohnzimmer-Licht","iface":"BidCos-RF","ccuConfig":"38263145.35ea0e","rooms":"","roomsRx":"str","functions":"","functionsRx":"str","device":"","deviceRx":"str","deviceName":"","deviceNameRx":"str","deviceType":"","deviceTypeRx":"str","channel":"","channelRx":"str","channelName":"Stecker-Schalter_4_ErkerLinks:1","channelNameRx":"str","channelType":"","channelTypeRx":"str","datapoint":"STATE","datapointRx":"str","delay":"100","x":900,"y":1400,"wires":[]},{"id":"f6e8a64f.25cfa8","type":"ccu-get-value","z":"cdb7abff.3cf718","name":"GetValue Wohnzimmer-Licht","ccuConfig":"38263145.35ea0e","iface":"BidCos-RF","channel":"JEQ0067462:1 Stecker-Schalter_4_ErkerLinks:1","sysvar":"Alarmmeldungen","sysvarProperty":"value","datapoint":"STATE","datapointProperty":"value","setProp":"payload","setPropType":"msg","x":440,"y":1400,"wires":[["b4c23041.64da2"]]},{"id":"b4c23041.64da2","type":"combine-logic","z":"cdb7abff.3cf718","name":"Invert State","topic":"","operator":"nor","defer":250,"timeout":0,"distinction":"topic","x":670,"y":1400,"wires":[["65a4a2b9.a3f68c"]]},{"id":"65a72644.483318","type":"ui_group","z":"","name":"Wohnzimmer","tab":"fe205248.f04ed","order":1,"disp":true,"width":"8","collapse":false},{"id":"38263145.35ea0e","type":"ccu-connection","z":"","name":"localhost","host":"localhost","regaEnabled":true,"bcrfEnabled":true,"iprfEnabled":true,"virtEnabled":true,"bcwiEnabled":false,"cuxdEnabled":false,"regaPoll":true,"regaInterval":"30","rpcPingTimeout":"60","rpcInitAddress":"127.0.0.1","rpcServerHost":"127.0.0.1","rpcBinPort":"2047","rpcXmlPort":"2048"},{"id":"fe205248.f04ed","type":"ui_tab","z":"","name":"Bedienung","icon":"dashboard","order":1}]```

