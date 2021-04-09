Dieser flow definiert eine Anrufsperre für ankommende Anrufe über die Fritzbox.

* Kann über das dashboard aktiviert / deaktiviert werden
* **Anrufe können ausgehend getätigt werden, eingehende Anrufe werden geblockt, falls gewünscht automatisch auf den Anrufbeantworter geleitet** (ACHTUNG, IHR SEID DANN VON EXTERN NICHT ÜBER FESTZNETZ ERREICHBAR!)
* Die Anrufsperre wird per default am nächsten Morgen um 08:00 automatisch wieder deaktiviert
* Vorbereitung für Telegram-Benachrichtigung
* Es wird eine globale Variable in Redmatic definiert die den Status der Anrufsperre per boolean true/false global zur Verfügung stellt und bei Neustart den toggle und Text im dashboard entsprechend einstellt


## Voraussetzungen: 
* Konfigurierter Zugriff mit Benutzername / Passwort via node-red-contrib-fritz auf die Fritzbox
* Sicherung globaler Variablen

## Installation:
1.  Den Anrufbeantworter der Fritzbox aktivieren, falls dieser nicht verwendet wird

![grafik](https://user-images.githubusercontent.com/75842297/114156002-66595380-9922-11eb-8384-9e96cb26c4eb.png)

2.  Rufumleitung unter Telefonie -> Rufumleitung anlegen

a) Alle ankommenden Anrufe auf den AB umleiten

![grafik](https://user-images.githubusercontent.com/75842297/114156219-9f91c380-9922-11eb-87e0-16373f1a0350.png)

b) Sollte so aussehen:

![grafik](https://user-images.githubusercontent.com/75842297/114156381-cea83500-9922-11eb-9f99-f4774e8137fa.png)

c) Anrufbeantworter wieder deaktivieren (sic) -> Falls gewünscht. Eingehende Anrufe werden dann geblockt und in der Anruferliste der Fritzbox angezeigt

d) flow importieren
* globale Variable prüfen
* Fritzbox-Device-Infos im Node eintragen

## Screenshot des flows:
![flow](https://user-images.githubusercontent.com/75842297/114154568-d5ce4380-9920-11eb-922c-5c0076f5ac72.png)

## Flow:
```
[
    {
        "id": "f0e7a7b2.159838",
        "type": "tab",
        "label": "Anrufsperre",
        "disabled": false,
        "info": ""
    },
    {
        "id": "3b7de6f4.fb2f82",
        "type": "fritzbox-in",
        "z": "f0e7a7b2.159838",
        "device": "432efe7b.3b5da",
        "name": "De oder aktivieren",
        "service": "urn:dslforum-org:service:X_AVM-DE_OnTel:1",
        "action": "SetDeflectionEnable",
        "arguments": "{\n  \"NewDeflectionId\": \"value\",\n  \"NewEnable\": \"value\"\n}",
        "x": 430,
        "y": 260,
        "wires": [
            [
                "d64f0179.d21ab8"
            ]
        ]
    },
    {
        "id": "f03996f6.216068",
        "type": "fritzbox-in",
        "z": "f0e7a7b2.159838",
        "device": "432efe7b.3b5da",
        "name": "Statusabfrage ",
        "service": "urn:dslforum-org:service:X_AVM-DE_OnTel:1",
        "action": "GetDeflection",
        "arguments": "{\n  \"NewDeflectionId\": \"value\"\n}",
        "x": 420,
        "y": 460,
        "wires": [
            [
                "f5f19e1d.fc0d4"
            ]
        ]
    },
    {
        "id": "5ca87dbc.2cf044",
        "type": "inject",
        "z": "f0e7a7b2.159838",
        "name": "Status",
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
        "payload": "{   \"NewDeflectionId\": \"0\" }",
        "payloadType": "json",
        "x": 190,
        "y": 460,
        "wires": [
            [
                "f03996f6.216068"
            ]
        ]
    },
    {
        "id": "e7b3b8df.476f7",
        "type": "ui_switch",
        "z": "f0e7a7b2.159838",
        "name": "",
        "label": "Aus/an (wird um 08:00 Uhr wieder deaktiviert)",
        "tooltip": "",
        "group": "176ae838.166538",
        "order": 2,
        "width": 0,
        "height": 0,
        "passthru": false,
        "decouple": "true",
        "topic": "topic",
        "topicType": "msg",
        "style": "",
        "onvalue": "true",
        "onvalueType": "bool",
        "onicon": "",
        "oncolor": "",
        "offvalue": "false",
        "offvalueType": "bool",
        "officon": "",
        "offcolor": "",
        "animate": false,
        "x": 460,
        "y": 100,
        "wires": [
            [
                "ec149f18.ca9c78"
            ]
        ]
    },
    {
        "id": "6ace399f.acdb9",
        "type": "ui_text",
        "z": "f0e7a7b2.159838",
        "group": "176ae838.166538",
        "order": 1,
        "width": 0,
        "height": 0,
        "name": "Textanzeige in Dashboard",
        "label": "",
        "format": "{{msg.payload}}",
        "layout": "row-spread",
        "x": 1310,
        "y": 260,
        "wires": []
    },
    {
        "id": "f5f19e1d.fc0d4",
        "type": "switch",
        "z": "f0e7a7b2.159838",
        "name": "",
        "property": "payload.NewEnable",
        "propertyType": "msg",
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
        "x": 830,
        "y": 540,
        "wires": [
            [
                "f56c104a.90c9b8",
                "1839813b.46ecbf"
            ],
            [
                "da8d4443.a1217",
                "e04ce442.cc90f8"
            ]
        ]
    },
    {
        "id": "da8d4443.a1217",
        "type": "change",
        "z": "f0e7a7b2.159838",
        "name": "Anrufsperre aktiv",
        "rules": [
            {
                "t": "set",
                "p": "payload",
                "pt": "msg",
                "to": "Anrufsperre ist aktiv, ankommende Anrufe werden nicht benachrichtigt",
                "tot": "str"
            },
            {
                "t": "set",
                "p": "anrufsperre",
                "pt": "global",
                "to": "true",
                "tot": "bool"
            },
            {
                "t": "set",
                "p": "topic",
                "pt": "msg",
                "to": "Anrufsperre ist aktiv, ankommende Anrufe werden nicht benachrichtigt",
                "tot": "str"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 1030,
        "y": 560,
        "wires": [
            [
                "6ace399f.acdb9",
                "ee40282d.8add88"
            ]
        ]
    },
    {
        "id": "f56c104a.90c9b8",
        "type": "change",
        "z": "f0e7a7b2.159838",
        "name": "Anrufsperre inaktiv",
        "rules": [
            {
                "t": "set",
                "p": "payload",
                "pt": "msg",
                "to": "Anrufsperre ist nicht aktiv, ankommende Anrufe werden benachrichtigt",
                "tot": "str"
            },
            {
                "t": "set",
                "p": "anrufsperre",
                "pt": "global",
                "to": "false",
                "tot": "bool"
            },
            {
                "t": "set",
                "p": "topic",
                "pt": "msg",
                "to": "Anrufsperre ist nicht aktiv, ankommende Anrufe werden benachrichtigt",
                "tot": "str"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 1030,
        "y": 520,
        "wires": [
            [
                "6ace399f.acdb9",
                "ee40282d.8add88"
            ]
        ]
    },
    {
        "id": "d64f0179.d21ab8",
        "type": "change",
        "z": "f0e7a7b2.159838",
        "name": "Statusabfrage initialisieren",
        "rules": [
            {
                "t": "delete",
                "p": "payload",
                "pt": "msg"
            },
            {
                "t": "set",
                "p": "payload",
                "pt": "msg",
                "to": "{   \"NewDeflectionId\": \"0\" }",
                "tot": "json"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 670,
        "y": 320,
        "wires": [
            [
                "f03996f6.216068"
            ]
        ]
    },
    {
        "id": "ec149f18.ca9c78",
        "type": "switch",
        "z": "f0e7a7b2.159838",
        "name": "",
        "property": "payload",
        "propertyType": "msg",
        "rules": [
            {
                "t": "true"
            },
            {
                "t": "false"
            }
        ],
        "checkall": "true",
        "repair": false,
        "outputs": 2,
        "x": 790,
        "y": 60,
        "wires": [
            [
                "d2fdf25c.b00a18"
            ],
            [
                "962c4298.f48ba"
            ]
        ]
    },
    {
        "id": "d2fdf25c.b00a18",
        "type": "change",
        "z": "f0e7a7b2.159838",
        "name": "Aktivieren",
        "rules": [
            {
                "t": "set",
                "p": "payload",
                "pt": "msg",
                "to": "{   \"NewDeflectionId\": \"0\",   \"NewEnable\": \"1\" }",
                "tot": "json"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 820,
        "y": 160,
        "wires": [
            [
                "3b7de6f4.fb2f82"
            ]
        ]
    },
    {
        "id": "962c4298.f48ba",
        "type": "change",
        "z": "f0e7a7b2.159838",
        "name": "Deaktivieren",
        "rules": [
            {
                "t": "set",
                "p": "payload",
                "pt": "msg",
                "to": "{   \"NewDeflectionId\": \"0\",   \"NewEnable\": \"0\" }",
                "tot": "json"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 840,
        "y": 220,
        "wires": [
            [
                "3b7de6f4.fb2f82"
            ]
        ]
    },
    {
        "id": "90247f81.d23268",
        "type": "inject",
        "z": "f0e7a7b2.159838",
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
        "payload": "anrufsperre",
        "payloadType": "global",
        "x": 150,
        "y": 40,
        "wires": [
            [
                "e7b3b8df.476f7"
            ]
        ]
    },
    {
        "id": "aff769ad.9f05e",
        "type": "inject",
        "z": "f0e7a7b2.159838",
        "name": "Deaktivieren nach Zeit",
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
        "crontab": "00 08 * * *",
        "once": false,
        "onceDelay": 0.1,
        "topic": "",
        "payload": "",
        "payloadType": "date",
        "x": 200,
        "y": 180,
        "wires": [
            [
                "962c4298.f48ba"
            ]
        ]
    },
    {
        "id": "e04ce442.cc90f8",
        "type": "change",
        "z": "f0e7a7b2.159838",
        "name": "Setze true",
        "rules": [
            {
                "t": "set",
                "p": "payload",
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
        "x": 1020,
        "y": 680,
        "wires": [
            [
                "e7b3b8df.476f7"
            ]
        ]
    },
    {
        "id": "1839813b.46ecbf",
        "type": "change",
        "z": "f0e7a7b2.159838",
        "name": "Setze false",
        "rules": [
            {
                "t": "set",
                "p": "payload",
                "pt": "msg",
                "to": "false",
                "tot": "bool"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 1010,
        "y": 740,
        "wires": [
            [
                "e7b3b8df.476f7"
            ]
        ]
    },
    {
        "id": "ee40282d.8add88",
        "type": "debug",
        "z": "f0e7a7b2.159838",
        "name": "Telegram",
        "active": true,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "payload",
        "targetType": "msg",
        "statusVal": "",
        "statusType": "auto",
        "x": 1300,
        "y": 540,
        "wires": []
    },
    {
        "id": "432efe7b.3b5da",
        "type": "fritzbox-config",
        "name": "fritz.box",
        "host": "192.168.137.1",
        "port": "49443",
        "ssl": true,
        "user": "automation"
    },
    {
        "id": "176ae838.166538",
        "type": "ui_group",
        "name": "Anrufsperre",
        "tab": "54130f55.d15c",
        "order": 1,
        "disp": true,
        "width": "6",
        "collapse": false
    },
    {
        "id": "54130f55.d15c",
        "type": "ui_tab",
        "name": "Anrufsperre",
        "icon": "dashboard",
        "order": 4,
        "disabled": false,
        "hidden": false
    }
]
```

## Getestete Firmware und Hardware
| Hardware/Router  | Versionsstand |
| ------------- | ------------- |
| Fritzbox 7590  | 7.21 |


## Version: 
| Version | Bemerkung | Datum |
| ------------- | ------------- |  ------------- | 
| 1.0  | Funktionierend | 09. April 2021 |