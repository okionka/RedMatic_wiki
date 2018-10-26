### STICKY_UNREACH ("Gerätekommunikation war gestört") Meldungen bestätigen und zählen

Dieser Flow bestätigt auftretende STICK_UNREACH Servicemeldungen sofort und erhöht dabei einen Zähler im Flow Context.

Ein _RPC Event_ Node abboniert alle Events mit dem Datenpunkt "STICKY_UNREACH", ein Switch Node leitet die Nachricht nur weiter wenn `msg.payload` `true` ist. In einem `Function` Node wird der Zähler im Flow Context erhöht und ein Homematic-Script erzeugt und an einen `CCU Script` Node übergeben.

![](images/sticky.png)

#### Function Node

```javascript
// Increment Counter
flow.set(msg.datapointName, (flow.get(msg.datapointName) || 0) + 1);

// Alarm Receipt
return {
    payload: `
        var dpAl = dom.GetObject("AL-${msg.channel}.${msg.datapoint}");
        dpAl.AlReceipt();
    `
};
```

#### Flow JSON

```
[{"id":"43a10cf7.cf3834","type":"ccu-rpc-event","z":"d93ee77.7acbf18","name":"RPC event STICKY_UNREACH","iface":"BidCos-RF","ccuConfig":"38263145.35ea0e","rooms":"","roomsRx":"str","functions":"","functionsRx":"str","device":"","deviceRx":"str","deviceName":"","deviceNameRx":"str","deviceType":"","deviceTypeRx":"str","channel":"","channelRx":"str","channelName":"","channelNameRx":"str","channelType":"MAINTENANCE","channelTypeRx":"str","datapoint":"STICKY_UNREACH","datapointRx":"str","change":false,"working":false,"cache":true,"topic":"${CCU}/${Interface}/${channelName}/${datapoint}","x":170,"y":480,"wires":[["af7f9b44.a56258"]]},{"id":"af7f9b44.a56258","type":"switch","z":"d93ee77.7acbf18","name":"is true","property":"payload","propertyType":"msg","rules":[{"t":"true"}],"checkall":"true","repair":false,"outputs":1,"x":410,"y":480,"wires":[["6bed755f.3ae26c"]]},{"id":"6bed755f.3ae26c","type":"function","z":"d93ee77.7acbf18","name":"AlReceipt, Count","func":"// Increment Counter\nflow.set(msg.datapointName, (flow.get(msg.datapointName) || 0) + 1);\n\n// Alarm Receipt\nreturn {\n    payload: `\n        var dpAl = dom.GetObject(\"AL-${msg.channel}.${msg.datapoint}\");\n        dpAl.AlReceipt();\n    `\n};","outputs":1,"noerr":0,"x":210,"y":560,"wires":[["f5c844da.8aa028"]]},{"id":"f5c844da.8aa028","type":"ccu-script","z":"d93ee77.7acbf18","name":"","script":"","ccuConfig":"38263145.35ea0e","topic":"${CCU}/${Interface}/","x":450,"y":560,"wires":[[]]},{"id":"da42b94a.e3f4c8","type":"comment","z":"d93ee77.7acbf18","name":"STICKY_UNREACH Meldungen bestätigen und zählen","info":"","x":260,"y":420,"wires":[]},{"id":"38263145.35ea0e","type":"ccu-connection","z":"","name":"localhost","host":"localhost","regaEnabled":true,"bcrfEnabled":true,"iprfEnabled":true,"virtEnabled":true,"bcwiEnabled":true,"cuxdEnabled":false,"regaPoll":true,"regaInterval":"30","rpcPingTimeout":"60","rpcInitAddress":"127.0.0.1","rpcServerHost":"127.0.0.1","rpcBinPort":"2047","rpcXmlPort":"2048","contextStore":"default"}]
```