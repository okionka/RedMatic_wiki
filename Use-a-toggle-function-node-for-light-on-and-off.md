## A simpler Flow to toggle light with a boolean toggle node

Similar to the previous part we can toggle an boolean input to a sequence of true and false.
Thus we need a node that stores its boolean sate to change it to the opposite.
In advance, we store the state in an named variable (for example "togglestore"). 

We can achive this by using a function node and inserting this simple script:
> /* 
> if we receive a true we toogle output
> and store stat in a local context 
> with a unique name 
> */ 
> var fname = "togglestore";

> if(msg.payload === true){

> if(context.get(fname) === false){
>   msg.payload = true;  
> }else{
>   msg.payload = false;
> }

> context.set(fname, msg.payload);
> }

> return msg;

Now we can connect for example a simple rednode-ui input to a state of an actor:

![Example of a flow to toggle an aktor](https://github.com/drose28357/Pictures/blob/master/RedMatic-Flow-Example_toggle%20statet.png)

```[{"id":"e7819e5e.98121","type":"ccu-value","z":"cdb7abff.3cf718","name":"IEQ0007361:1 PRESS_SHORT","iface":"BidCos-RF","channel":"IEQ0007361:1 Stecker-Schalter_1_ErkerRechts:1","datapoint":"STATE","mode":"","start":true,"change":false,"cache":false,"on":0,"onType":"undefined","ramp":0,"rampType":"undefined","working":false,"ccuConfig":"38263145.35ea0e","topic":"${CCU}/${Interface}/${channel}/${datapoint}","x":728.9999084472656,"y":274.00012588500977,"wires":[[]]},{"id":"864a7dab.c5de7","type":"ui_button","z":"cdb7abff.3cf718","name":"Licht ein/aus schalten","group":"65a72644.483318","order":3,"width":0,"height":0,"passthru":false,"label":"Erker links","color":"","bgcolor":"","icon":"","payload":"true","payloadType":"bool","topic":"toogle boolean","x":251.99999618530273,"y":275.0000629425049,"wires":[["16617cd2.f754f3"]]},{"id":"16617cd2.f754f3","type":"function","z":"cdb7abff.3cf718","name":"Toogle boolean","func":"/* \nif we receive a true we toogle output\nand store stat in a local context \nwith a unique name \n*/ \nvar fname = \"toggle1\";\n\nif(msg.payload === true){\n\nif(context.get(fname) === false){\n  msg.payload = true;  \n}else{\n  msg.payload = false;\n}\ncontext.set(fname, msg.payload);\n}\nreturn msg;","outputs":1,"noerr":0,"x":478.0729751586914,"y":274.60774993896484,"wires":[["e7819e5e.98121"]]},{"id":"38263145.35ea0e","type":"ccu-connection","z":"","name":"localhost","host":"localhost","regaEnabled":true,"bcrfEnabled":true,"iprfEnabled":true,"virtEnabled":true,"bcwiEnabled":false,"cuxdEnabled":false,"regaPoll":true,"regaInterval":"30","rpcPingTimeout":"60","rpcInitAddress":"127.0.0.1","rpcServerHost":"127.0.0.1","rpcBinPort":"2047","rpcXmlPort":"2048"},{"id":"65a72644.483318","type":"ui_group","z":"","name":"Wohnzimmer Licht:1","tab":"fe205248.f04ed","disp":true,"width":"8","collapse":false},{"id":"fe205248.f04ed","type":"ui_tab","z":"","name":"Geräte","icon":"dashboard","order":1}]```