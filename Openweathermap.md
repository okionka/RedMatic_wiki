# Openweathermap mit Virtuellem CUxD Device und Systemvariablen nutzen

## Voraussetzungen
  * OpenWeatherMap [API Key (kostenlos) bekommen](http://openweathermap.org/appid)
  * Deine Station ID: steht in der URL wenn du nach einer Seite suchst: https://openweathermap.org/city/2867714

## CCU vorbereiten
 * auf der WebUI Oberfläche unter `Startseite > Einstellungen > Systemsteuerung > Zusatssoftware` die folgenden Plun´gins installieren
   * CUxD AddOn [installieren](https://homematic-forum.de/forum/viewtopic.php?f=37&t=15298)
   * Redmatic AddOn [installieren](https://github.com/rdmtc/RedMatic/wiki/Installation)

## CUxD vorbereiten
* Die CUx-Daemon Oberfläche aufrufen (WebUI unter `Startseite > Einstellungen > Systemsteuerung > CUx-Daemon`
* Unter Geräte ein neues Gerät "90 Universal Wrapper Device" anlegen und vom Typ Thermostat:

![image](https://user-images.githubusercontent.com/12692680/55945008-2f280d00-5c4a-11e9-87cd-ccae043aaed3.png)

* Auf der CCU im Posteingang unter `Startseite > Einstellungen >Geräte - Posteingang` das Gerät konfigurieren 
  * Mode Temp & Humid
  * Haken bei `USE_HMADAPT` entfernen
  * Haken bei `zyklische Statusmeldung` und `WEATHER|STATISTIC` setzen

![image](https://user-images.githubusercontent.com/12692680/55945156-84fcb500-5c4a-11e9-8a36-cf622a659fef.png)

 * Im Posteingang Fertig wählen.

## RedMatic vorbereiten
 * Redmatic aufrufen (WebUI unter `Startseite > Einstellungen > Systemsteuerung > Redmatic`
 * Wenn Redmatic nicht läuft starten.
 * Node-Red aufrufen

![image](https://user-images.githubusercontent.com/12692680/55945658-867aad00-5c4b-11e9-81e5-908643c215e6.png)

 * In Node-Red die Node `node-red-node-openweathermap` [installieren](https://github.com/rdmtc/RedMatic/wiki/Node-Installation)

  * einen neuen Flow erstellen oder den Flow aufrufen in dem die Nodes ablegen möchte
  * aus der Palette die OpenWeathermap Node ohne Ausgang in den Flow ziehen

![image](https://user-images.githubusercontent.com/12692680/55947620-1e2dca80-5c4f-11e9-92ac-31f6c257d3c2.png)

  * nach dem ablegen die Node doppelklicken, es öffnet sich die Seitenleiste mit den EInstellungen
  * in der Seitenleiste den API key eintragen, den Ort wählen entweder über koordinaten oder den Namen
  * in der Seitenleiste fertig wählen

![image](https://user-images.githubusercontent.com/12692680/55946175-78795c00-5c4c-11e9-8419-7eba77dafba6.png)

  * Eine Change Node und eine CCU Value Node in den Flow ziehen

![image](https://user-images.githubusercontent.com/12692680/55946365-e3c32e00-5c4c-11e9-86ae-ff5f040b06e4.png)
![image](https://user-images.githubusercontent.com/12692680/55946460-0d7c5500-5c4d-11e9-965d-913df93ae0d1.png)

  * die Nodes Verbinden
  * die change Node doppelt klicken und den `msg.payload` auf den Wert `msg.payload.tempc` setzen:

![image](https://user-images.githubusercontent.com/12692680/55946893-c5a9fd80-5c4d-11e9-846d-33030635155d.png)

  * die value-node doppelt klicken und die CCU Einstellungen überprüfen

![image](https://user-images.githubusercontent.com/12692680/55946940-e2463580-5c4d-11e9-97dc-93589b9eab1b.png)

  * Hier prüfen ob der Haken bei CUxD gesetzt ist, Wenn nicht diesen setzen und mit `Aktualisieren` die Node schließen:

![image](https://user-images.githubusercontent.com/12692680/55947201-5254bb80-5c4e-11e9-88ee-c312feb8be35.png)

  * den Value Node mit Fertig schließen
  * den `Deploy` oder `Implementieren` Button betätigen, damit die Änderungen erst mal gespeichert werden

![image](https://user-images.githubusercontent.com/12692680/55947392-a6f83680-5c4e-11e9-8f99-b37d35381e41.png)

  * Nochmals den  `Deploy` oder `Implementieren` Button betätigen, diesmal den kleinen Pfeil am Ende
  * im sich öffnednen Menü die Flows neu starten (das ist nötig, damit das neu angelegte CUxD Device in der Auswahl erscheint)

![image](https://user-images.githubusercontent.com/12692680/55947485-d018c700-5c4e-11e9-8d30-26c677a792a2.png)

 * die value-node doppelt klicken und konfigurieren
    * Unter Interface CUxD wählen
    * under channel den Kanal **1** des erstellten CUxD Devices wählen (wenn man anfängt einen Teil des Namens einzugeben öffnet sich eine Auswahlliste)
    * unter datapoint `SET_TEMPERATURE` wählen
    * mit fertig schließen

![image](https://user-images.githubusercontent.com/12692680/55947858-972d2200-5c4f-11e9-9943-79047950dc76.png)

  * in den Flow eine weitere change und eine weitere value node ziehen und wie folgt verbinden:

![image](https://user-images.githubusercontent.com/12692680/55947972-d78ca000-5c4f-11e9-9a5c-2bb41ad762ad.png)

  * die neue Change Node doppelt klicken und den `msg.payload` auf den Wert `msg.payload.humidity` setzen und mit fertig schließen:

![image](https://user-images.githubusercontent.com/12692680/55948052-00149a00-5c50-11e9-9e47-e897f208f8c2.png)

 * die neue value-node doppelt klicken und konfigurieren
    * Unter Interface CUxD wählen
    * under channel den Kanal **1** des erstellten CUxD Devices wählen (wenn man anfängt einen Teil des Namens einzugeben öffnet sich eine Auswahlliste)
    * unter datapoint `SET_HUMIDITY` wählen
    * mit fertig schließen

![image](https://user-images.githubusercontent.com/12692680/55948141-318d6580-5c50-11e9-8b9a-67e15f03cc7e.png)

 * Mit dem `Deploy` oder `Implementieren` Button die Änderung abschließen

![image](https://user-images.githubusercontent.com/12692680/55947392-a6f83680-5c4e-11e9-8f99-b37d35381e41.png)

## Erweiterung mit Systemvariablen
 * Genauso wie das CUxD Device kann man auch Systemvariablen mit den Wetterdaten auf der CCU füllen.
    * dazu muss man lediglich anstelle der CCU value node die sysvar node nutzen

![image](https://user-images.githubusercontent.com/12692680/55948566-1bcc7000-5c51-11e9-82ce-73fc2eda1358.png)

![image](https://user-images.githubusercontent.com/12692680/55948610-343c8a80-5c51-11e9-8f1b-a85b27e93df2.png)

   * Die sysvar node lässt sich einfach konfigurieren. Hier muss lediglich die Systemvariable aufgewählt werden. (Wenn diese fehlt einfach mal die Node-Red Flows wie oben beschrieben neu starten)

Im Change node kann dann neben `msg.payload.tempc` oder `msg.payload.humidity` die folgenden Daten von Openweathermap ebenfalls in Systemvariablen abgelegt werden:
  * `msg.payload.weather` - Wetterlage, Beispiel `Clouds`
  * `msg.payload.detail` - Wetterlage, Beispiel `Ein paar Wolken`
  * `msg.payload.weather` - Wetterlage, Beispiel `Clouds`
  * `msg.payload.tempk` - Temperatur in Kelvin
  * `msg.payload.tempc` - Temperatur in Celsius
  * `msg.payload.temp_maxc` - maximale Temperatur in Celsius
  * `msg.payload.temp_minc` - minimale Temperatur in Celsius
  * `msg.payload.maxtemp` - maximale Temperatur in Celsius
  * `msg.payload.mintemp` - minimale Temperatur in Celsius
  * `msg.payload.windspeed` - Windgeschwindigkeit
  * `msg.payload.winddirection` - Windrichtung
  * `msg.payload.location` - Position der Wetterstation
  * `msg.payload.clouds` - Bewölkung in %
  * `msg.payload.description` - Beschreibung des Wetters, Beispiel: "The weather in Umbuktu at coordinates: 31.95, 72.74 is Clouds (Ein paar Wolken)."


