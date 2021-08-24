# Installation
## Signal-Nodes

* Die Signal-Nodes über den RedMatic-Package-Manager installieren: [Doku hier](https://github.com/rdmtc/RedMatic/wiki/Node-Installation#nodes-mit-binärmodulen)
* RedMatic neustarten

# Einrichtung
## Request-SMS-Node

* Neuen Account erstellen
  1. Mobilnummer eintragen (Wichtig: eine bereits registrierte Nummer wird am jeweils zuvor registrierten (Mobil) Gerät abgemeldet!).
  2. Beliebiges Passwort/PIN vergeben
  3. Beliebigen DataStorage-Namen vergeben
  4. Live-Server anhaken
* [https://signalcaptchas.org/registration/generate.html](https://signalcaptchas.org/registration/generate.html) besuchen
* Entwicklerwerkzeuge öffnen
* Zum Tab "Konsole" wechseln
* In den Konsoleneinstellungen "Log nicht leeren" anwählen
* Captcha lösen
* Nach erfolgreichem Lösen erscheint ein "Alert" mit Aufforderung den Link "signalcaptchas://CODE" mit einem Programm zu öffnen
  1. Diesen Alert ignorieren
* Stattdessen in der Konsole den Link suchen
* Alles nach signalcaptchas:// kopieren
* In die Request-SMS-Node "Captcha-Code" einfügen
* Speichern und Deploy
* Den Request triggern
* Reqister-Node hinzufügen + den Verifikations-Code reinschreiben, Speichern, Deploy + Trigger der Register-Node
* Fertig