With the `node-red-contrib-chromecast` and the `node-red-contrib-google-tts` it is possible to let the Google Home speak any text.

how to install Extensions?
* open Manager palette
* go to Tab Install
* search for `node-red-contrib-chromecast` and install
* search for `node-red-contrib-google-tts` and install

### Example Flow:
![screenshot 2018-05-21 at 01 23 56](https://user-images.githubusercontent.com/12692680/40284898-b4f68002-5c95-11e8-9891-7a14bd853c05.png)


```
[
    {
        "id": "ae518952.246df8",
        "type": "google-tts",
        "z": "4e9fd15e.9ba8a",
        "name": "tts",
        "inputField": "payload",
        "inputFieldType": "msg",
        "outputField": "payload",
        "outputFieldType": "msg",
        "languageField": "de",
        "languageFieldType": "str",
        "speedField": "1",
        "speedFieldType": "num",
        "x": 330,
        "y": 2600,
        "wires": [
            [
                "42c153c1.70611c"
            ]
        ]
    },
    {
        "id": "cbf4a6ea.930938",
        "type": "inject",
        "z": "4e9fd15e.9ba8a",
        "name": "",
        "topic": "",
        "payload": "Hallo Duda",
        "payloadType": "str",
        "repeat": "",
        "crontab": "",
        "once": false,
        "onceDelay": 0.1,
        "x": 180,
        "y": 2600,
        "wires": [
            [
                "ae518952.246df8"
            ]
        ]
    },
    {
        "id": "561c1e70.b87fb",
        "type": "debug",
        "z": "4e9fd15e.9ba8a",
        "name": "",
        "active": false,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "true",
        "x": 830,
        "y": 2600,
        "wires": []
    },
    {
        "id": "b4f153a6.32b31",
        "type": "chromecast-play",
        "z": "4e9fd15e.9ba8a",
        "name": "",
        "url": "",
        "contentType": "",
        "ip": "",
        "x": 690,
        "y": 2600,
        "wires": [
            [
                "561c1e70.b87fb"
            ]
        ]
    },
    {
        "id": "42c153c1.70611c",
        "type": "function",
        "z": "4e9fd15e.9ba8a",
        "name": "Format Message",
        "func": "let timer = context.get('timer');\nlet lastMsg  = context.get('lastMsg'); \n\nif (lastMsg === msg.payload) {\n    return null;\n}\n\nif (timer) {\n    clearTimeout(timer);\n}\ncontext.set('lastMsg',msg.payload);\n\n//make sure only send same Text only once in 5 minutes:\ntimer = setTimeout(function(){\n    context.set('timer',null);\n    context.set('lastMsg',null);\n}, 300000);\ncontext.set('timer',timer);\n\n//format outgoing message\nmsg.payload = {\n    ip: '192.168.178.35', //gogole home ore chromecast device\n    url: msg.payload,\n    contentType: 'audio/mp3'\n}\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 510,
        "y": 2600,
        "wires": [
            [
                "b4f153a6.32b31"
            ]
        ]
    }
]
```