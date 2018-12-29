### 1) Node installieren
### 2) Telegrambot erstellen
### 3) Einfacher Flow zum Nachrichten versenden
### 4) Weiterführende Informationen

- - - - - - - - - - - - - - - - - - - - 

### 1) Node installieren
In Node-Red rechts oben auf den Menübotton klicken. Auf “Manage palette“ klicken und anschließend im Tab „Install“ folgenden Node suchen und installieren: node-red-contrib-telegrambot.

### 2) Telegrambot erstellen
Zuerst in Telegram den Nutzer @botfather hinzufügen. Anschließend kann man den Bot erstellen, indem man dem neuen Nutzer Botfather fogende Nachricht schickt: „/newbot“. Auf Nachfrage den Bot-Namen vergeben (letzterer muss auf „bot“ enden). Nun bekommt Ihr den API-Token, der den Bot eindeutig identifiziert. Um eine Nachricht an einen Telegram-Chat senden zu können wird die entsprechende Chat-ID benötigt. Der einfachste Weg diese zu erhalten, ist dem Nutzer „FalconGate“ (welcher ebenfalls ein Bot ist) zu suchen und ihm folgende Nachricht zu schicken „/get_my_id“.

### 3) Einfacher Flow zum Nachrichten versenden
Zunächst mittels eines value node ein Ereignis abfragen (siehe Screenshot). 
![](https://user-images.githubusercontent.com/44581521/50490569-0fa80400-0a0e-11e9-9366-67812dc30daf.png)
Damit einer Nachricht mittels des „sender“ nodes versendet werden kann, benötigt letzterer Node drei wichtige Informationen: die Chat ID, die Art der Nachricht und den Inhalt der Nachricht. Diese Infos können unter anderem mittels eines change nodes übergeben werden. Zunächst muss der aktuelle Inhalt des payload gelöscht werden und anschließend können die benötigten Informationen hinzugefügt werden (siehe Screenshot). 
![](https://user-images.githubusercontent.com/44581521/50490575-15054e80-0a0e-11e9-8eb3-f8f4586a172d.png)
Alternativ kann auch ein function node benutzt werden der folgenden Code zum Inhalt hat:

return {
    payload: {
        chatId: 255677735,
        type: 'message',
        content: 'mein text'
    }
};

Zuletzt muss noch die Nachricht versendet werden. Hierzu ist es notwendig den change node (oder function node) mit einem „sender“ node zu verbinden. Bevor Nachrichten versendet werden können, muss noch der Bot definiert werden. Dies kann direkt im „sender“ node erfolgen indem man auf den bearbeiten-Button neben „Add new telegram bot…“ klickt. Hier nun den Botnamen (Zeile 1) und den API-Token (Zeile 2) eingeben (siehe Screenshot). 
![](https://user-images.githubusercontent.com/44581521/50490693-bab8bd80-0a0e-11e9-98a8-52f478a31271.png)

Der gesamte Flow schaut dann wie folgt aus:
![](https://user-images.githubusercontent.com/44581521/50490572-12a2f480-0a0e-11e9-87a5-598a16008ffc.png)

Fertig.


### 4) Weiterführende Informationen

Dieses System bietet viele weitere Möglichkeiten. Weiterführende Informationen kann man direkt bei Node-RED nachlesen: 

https://flows.nodered.org/node/node-red-contrib-telegrambot

 