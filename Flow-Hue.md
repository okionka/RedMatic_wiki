Die Hue-Integration die die Homematic CCU mitbringt bietet leider keine Möglichkeit über langen Tastendruck eine Lampe auf/ab zu dimmen. Mit Hilfe dieses Flows kann dies dennoch realisiert werden. Hierfür werden die [Huemagic Nodes](https://flows.nodered.org/node/node-red-contrib-huemagic) benötigt.

![](images/hue-1.png)

_RPC Event Nodes_ werden so konfiguriert dass sie den `PRESS_CONT` Event einer Fernbedienungstaste ausgeben (dieser Event wird bei anhaltendem Tastendruck mehrfach pro Sekunde erzeugt).

![](images/hue-2.png)

Mit Hilfe eines _Change Nodes_ wird ein JSON Payload konfiguriert der die Lampe 12% Heller bzw. Dunkler dimmt.

![](images/hue-3.png)