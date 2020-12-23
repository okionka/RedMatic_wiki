Dieser flow überwacht den aktuellen Stand des Programms einer Waschmaschine über den RPC-Event einer hmip-psm Messsteckdose

* Die Logik entscheidet ob die Waschmaschine fertig ist (in meinem Fall wenn 2 Minuten lang <4 Watt anliegen)
* Durch Waschpausen o.ä. bleibt der Stromverbrauch nicht konstant hoch sondern fällt auch <4 Watt 
* Ein Timer sorgt dafür, dass der flow beendet wird wenn die Messsteckdose 2 Minuten lang nicht >4 Watt gemeldet hat

## Voraussetzungen: 
* hmip-psm Messsteckdose / Möglichkeit den Datapoint POWER abzugreifen -> Ggf. muss die korrekte PSM ausgewählt werden
* Ggf. müssen die Entscheidungswerte angepasst werden: Meine LG-Waschmaschine hat einen Standby-Verbrauch von <1 Watt, wenn das Programm läuft >10 Watt

![flow](https://user-images.githubusercontent.com/75842297/103002835-ec968900-452f-11eb-9578-2c9e18ce5d57.PNG)

## Flow:
```
[{
        "id": "1bfd593a.e08cd7",
        "type": "tab",
        "label": "Waschmaschine",
        "disabled": false,
        "info": ""
    },
    {
        "id": "336bdfc5.e68a8",
        "type": "change",
        "z": "1bfd593a.e08cd7",
        "name": "",
        "rules": [
            {
                "t": "set",
                "p": "data",
                "pt": "flow",
                "to": "payload",
                "tot": "msg"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 160,
        "y": 160,
        "wires": [
            []
        ]
    },
    {
        "id": "2150c4af.4dd39c",
        "type": "switch",
        "z": "1bfd593a.e08cd7",
        "name": "data > / < 4?",
        "property": "payload",
        "propertyType": "msg",
        "rules": [
            {
                "t": "gte",
                "v": "4",
                "vt": "num"
            },
            {
                "t": "lt",
                "v": "4",
                "vt": "num"
            }
        ],
        "checkall": "true",
        "repair": false,
        "outputs": 2,
        "x": 380,
        "y": 340,
        "wires": [
            [
                "4f1da2a7.b97d7c",
                "c946981e.7cbee8"
            ],
            [
                "33c54679.2e169a"
            ]
        ]
    },
    {
        "id": "4f1da2a7.b97d7c",
        "type": "switch",
        "z": "1bfd593a.e08cd7",
        "name": "WamaAn 1 oder 0?",
        "property": "WaMaAn",
        "propertyType": "flow",
        "rules": [
            {
                "t": "eq",
                "v": "0",
                "vt": "num"
            },
            {
                "t": "eq",
                "v": "1",
                "vt": "num"
            }
        ],
        "checkall": "true",
        "repair": false,
        "outputs": 2,
        "x": 570,
        "y": 140,
        "wires": [
            [
                "935e516a.29b8e",
                "af687bfd.b50638"
            ],
            [
                "af687bfd.b50638"
            ]
        ]
    },
    {
        "id": "935e516a.29b8e",
        "type": "change",
        "z": "1bfd593a.e08cd7",
        "name": "Setze Flow.WaMaAn = 1; Setze Text Wama An",
        "rules": [
            {
                "t": "set",
                "p": "WaMaAn",
                "pt": "flow",
                "to": "1",
                "tot": "num"
            },
            {
                "t": "set",
                "p": "payload",
                "pt": "msg",
                "to": "Waschmaschine ist an",
                "tot": "str"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 980,
        "y": 140,
        "wires": [
            [
                "5816dc6c.d9e814"
            ]
        ]
    },
    {
        "id": "16a04a72.d57156",
        "type": "change",
        "z": "1bfd593a.e08cd7",
        "name": "Setze WaMaAn = 0; Setze Text Wama aus",
        "rules": [
            {
                "t": "set",
                "p": "payload",
                "pt": "msg",
                "to": "Waschmaschine ist aus",
                "tot": "str"
            },
            {
                "t": "set",
                "p": "WaMaAn",
                "pt": "flow",
                "to": "0",
                "tot": "num"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 310,
        "y": 560,
        "wires": [
            [
                "5816dc6c.d9e814"
            ]
        ]
    },
    {
        "id": "af687bfd.b50638",
        "type": "switch",
        "z": "1bfd593a.e08cd7",
        "name": "Flow.Data > 10?",
        "property": "data",
        "propertyType": "flow",
        "rules": [
            {
                "t": "gt",
                "v": "10",
                "vt": "num"
            }
        ],
        "checkall": "true",
        "repair": false,
        "outputs": 1,
        "x": 620,
        "y": 240,
        "wires": [
            [
                "df604cc3.046a78"
            ]
        ]
    },
    {
        "id": "df604cc3.046a78",
        "type": "change",
        "z": "1bfd593a.e08cd7",
        "name": "Setze Flow.WaLaeuft = 1; Setze Text Wama Prog läuft",
        "rules": [
            {
                "t": "set",
                "p": "WaMaLaeuft",
                "pt": "flow",
                "to": "1",
                "tot": "num"
            },
            {
                "t": "set",
                "p": "payload",
                "pt": "msg",
                "to": "Waschmaschine Programm läuft",
                "tot": "str"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 1000,
        "y": 260,
        "wires": [
            [
                "5816dc6c.d9e814"
            ]
        ]
    },
    {
        "id": "33c54679.2e169a",
        "type": "switch",
        "z": "1bfd593a.e08cd7",
        "name": "WamaWaMaLaueft 1 oder 0?",
        "property": "WaMaLaeuft",
        "propertyType": "flow",
        "rules": [
            {
                "t": "eq",
                "v": "1",
                "vt": "num"
            },
            {
                "t": "eq",
                "v": "0",
                "vt": "num"
            }
        ],
        "checkall": "true",
        "repair": false,
        "outputs": 2,
        "x": 300,
        "y": 460,
        "wires": [
            [
                "b2e5282b.5748c8"
            ],
            [
                "16a04a72.d57156"
            ]
        ]
    },
    {
        "id": "b2e5282b.5748c8",
        "type": "trigger",
        "z": "1bfd593a.e08cd7",
        "name": "",
        "op1": "",
        "op2": "false",
        "op1type": "nul",
        "op2type": "bool",
        "duration": "2",
        "extend": true,
        "overrideDelay": false,
        "units": "min",
        "reset": "",
        "bytopic": "all",
        "topic": "topic",
        "outputs": 1,
        "x": 920,
        "y": 360,
        "wires": [
            [
                "9056f15.577689"
            ]
        ]
    },
    {
        "id": "c946981e.7cbee8",
        "type": "change",
        "z": "1bfd593a.e08cd7",
        "name": "",
        "rules": [
            {
                "t": "set",
                "p": "reset",
                "pt": "msg",
                "to": "true",
                "tot": "bool"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 620,
        "y": 320,
        "wires": [
            [
                "b2e5282b.5748c8"
            ]
        ]
    },
    {
        "id": "9056f15.577689",
        "type": "change",
        "z": "1bfd593a.e08cd7",
        "name": "Setze Flow.WaLaeuft = 0; Setze Text Wama Programm fertig",
        "rules": [
            {
                "t": "set",
                "p": "WaMaLaeuft",
                "pt": "flow",
                "to": "0",
                "tot": "num"
            },
            {
                "t": "set",
                "p": "payload",
                "pt": "msg",
                "to": "Waschmaschine Programm fertig",
                "tot": "str"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 900,
        "y": 600,
        "wires": [
            [
                "5816dc6c.d9e814",
                "b4723764.1536d8"
            ]
        ]
    },
    {
        "id": "5816dc6c.d9e814",
        "type": "ui_template",
        "z": "1bfd593a.e08cd7",
        "group": "66620044.67de48",
        "name": "Ui-Widget",
        "order": 0,
        "width": 0,
        "height": 0,
        "format": "<div style=\"font-weight: bold\"><div ng-bind-html=\"msg.payload\"></div>",
        "storeOutMessages": true,
        "fwdInMessages": true,
        "resendOnRefresh": true,
        "templateScope": "local",
        "x": 700,
        "y": 500,
        "wires": [
            []
        ]
    },
    {
        "id": "36139746.d2c758",
        "type": "inject",
        "z": "1bfd593a.e08cd7",
        "name": "",
        "props": [
            {
                "p": "payload"
            },
            {
                "p": "topic",
                "vt": "str"
            }
        ],
        "repeat": "",
        "crontab": "",
        "once": true,
        "onceDelay": 0.1,
        "topic": "",
        "payload": "data",
        "payloadType": "flow",
        "x": 160,
        "y": 100,
        "wires": [
            [
                "2150c4af.4dd39c"
            ]
        ]
    },
    {
        "id": "b4723764.1536d8",
        "type": "change",
        "z": "1bfd593a.e08cd7",
        "name": "Setze msg.topic \"Fertig\"",
        "rules": [
            {
                "t": "set",
                "p": "topic",
                "pt": "msg",
                "to": "Waschmaschine ist fertig",
                "tot": "str"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 310,
        "y": 660,
        "wires": [
            [
                "55f3b329.615614"
            ]
        ]
    },
    {
        "id": "55f3b329.615614",
        "type": "link out",
        "z": "1bfd593a.e08cd7",
        "name": "Zum Telegram-Sender",
        "links": [
            "4a88077d.5d9158"
        ],
        "x": 555,
        "y": 660,
        "wires": []
    },
    {
        "id": "498d7a17.55669c",
        "type": "ccu-rpc-event",
        "z": "1bfd593a.e08cd7",
        "name": "",
        "iface": "HmIP-RF",
        "ccuConfig": "38263145.35ea0e",
        "rooms": "",
        "roomsRx": "str",
        "functions": "",
        "functionsRx": "str",
        "device": "",
        "deviceRx": "str",
        "deviceName": "",
        "deviceNameRx": "str",
        "deviceType": "HMIP-PSM",
        "deviceTypeRx": "str",
        "channel": "",
        "channelRx": "str",
        "channelName": "",
        "channelNameRx": "str",
        "channelType": "",
        "channelTypeRx": "str",
        "channelIndex": "",
        "channelIndexRx": "str",
        "datapoint": "POWER",
        "datapointRx": "str",
        "change": false,
        "working": false,
        "cache": false,
        "topic": "${CCU}/${Interface}/${channelName}/${datapoint}",
        "x": 120,
        "y": 340,
        "wires": [
            [
                "2150c4af.4dd39c",
                "336bdfc5.e68a8"
            ]
        ]
    },
    {
        "id": "60f3b4f4.483b2c",
        "type": "comment",
        "z": "1bfd593a.e08cd7",
        "name": "",
        "info": "version 1.0 - Dezember 2020 ",
        "x": 240,
        "y": 780,
        "wires": []
    },
    {
        "id": "66620044.67de48",
        "type": "ui_group",
        "name": "Waschmaschine",
        "tab": "4f956a33.92b3e4",
        "order": 3,
        "disp": true,
        "width": "6",
        "collapse": false
    },
    {
        "id": "38263145.35ea0e",
        "type": "ccu-connection",
        "name": "localhost",
        "host": "localhost",
        "regaEnabled": true,
        "bcrfEnabled": true,
        "iprfEnabled": true,
        "virtEnabled": true,
        "bcwiEnabled": false,
        "cuxdEnabled": true,
        "regaPoll": true,
        "regaInterval": "30",
        "rpcPingTimeout": "60",
        "rpcInitAddress": "127.0.0.1",
        "rpcServerHost": "127.0.0.1",
        "rpcBinPort": "2047",
        "rpcXmlPort": "2048",
        "queueTimeout": "5000",
        "queuePause": "250",
        "contextStore": "file"
    },
    {
        "id": "4f956a33.92b3e4",
        "type": "ui_tab",
        "name": "Waschmaschine",
        "icon": "dashboard",
        "order": 1,
        "disabled": false,
        "hidden": false
    }]```


## Version: 
1.0 Funktionierend, Dezember 2020