<img width="1084" alt="image" src="https://user-images.githubusercontent.com/37173958/58908532-1e0ef000-8711-11e9-8e30-63e8ed86b718.png">

[Weather Icons Lite](https://github.com/Paul-Reed/weather-icons-lite) ist eine Sammlung von Wettersymbolen/-Icons, die bereits in node-red integriert sind. Sie können somit in jedem Flow verwendet werden, das hochwertige wetterbasierte Symbole darstellen soll, die als Labels und/oder auf Tasten im Node-red Dashboard angezeigt werden können.

Der node_red Flow-Editor für z. B. das ```ui_template_widget``` 
<img width="141" alt="image" src="https://user-images.githubusercontent.com/37173958/60324605-84d89f80-9985-11e9-8e0c-bc94f8e09442.png"> verweisst in seiner Infobox selbst auf diese [in Node-Red out of-the-box verfügbaren](https://github.com/Paul-Reed/weather-icons-lite/blob/master/css_mappings.md) Wetter-Icons: 

> <img width="707" alt="image" src="https://user-images.githubusercontent.com/37173958/60266438-55c02080-98e8-11e9-91c7-2b224a41c513.png">

Es gibt darüber hinaus auf dieser Basis ein in Node-red nutzbares [noch umfangreiches Set von über 200 Wettersymbolen](https://erikflowers.github.io/weather-icons/), die insbesondere im Zusammenhang mit den [OpenWeather](https://openweathermap.org/city) verfügbaren Daten Anwendung finden können, wenn es darum geht:

* zusätzliche Wettersymbole für Tag- und Nacht-Design 
* Symbole für Mond- und Sonnen- Auf-und -Untergang
* Uhrzeit-Icons für jede volle Stunde 
* Windrichtungspfeile
* Beaufort Windstärke
* weitere verschiedene Icons im Wetter-Kontext 
 
darstellen zu wollen.

Für die Einrichtung des vollen CSS-Repositories für ```RedMatic``` sind jedoch ein paar Dateien aus dem CSS-Repository auf RedMatic zu kopieren und ist eine kleine Konfigurationen vorzunehmen.

**1) Clonen des Repositories**

Erstellen Sie ein neues Verzeichnis (z.B. "public") auf einem Rechners, der später z. B. über sFTP mit der CCU3 verbunden werden kann. Mit Git klonen Sie [dieses Repository](https://github.com/Paul-Reed/weather-icons) in das neu erstelltes Verzeichnis:

```
cd && cd ./public
git clone https://github.com/Paul-Reed/weather-icons.git
```
**2) Einrichten des Verzeichnis und Kopieren der CSS-Resourcen**

Erstellen Sie auf der CCU3 ein Verzeichnis ```weather-icons``` in dem für solche Zwecke vorgesehenen Pfad:
```
/usr/local/sdcard/www/addons/red/
```
Kopieren Sie mindestens die im folgenden Bild angegeben Dateien per sFTP in dieses Verzeichnis:

<img width="502" alt="image" src="https://user-images.githubusercontent.com/37173958/60265531-3d4f0680-98e6-11e9-89e5-bf2d9c825d50.png">

Beachten Sie die Verzeichnisstruktur und die Rechte auf Dateisystem!

**3) httpStatic aktivieren durch Anpassen der RedMatic Node-Red settings.json**

In der ```settings.json```von Node-red muss `httpStatic` aktiviert werden, damit der das UI-Dashboard beim Rendering der Webseite die Symbole aufgrund der CSS-Angaben im Template/Widget einbeziehen kann:

```
/usr/local/addons/redmatic/etc/settings.json
```

Überprüfen resp. anpassen der Parameter `httpRoot`und `httpStatic` gemäß des folgenden Beispiels:
<img width="352" alt="image" src="https://user-images.githubusercontent.com/37173958/60265630-8010de80-98e6-11e9-8147-c6e3d6a22328.png">

**4) Neustart von RedMatic**

_(selbsterklärend)_

**5) Beispiel-Flow mit Einstellungen für das UI-Template Widget**

Folgender Flow

<img width="899" alt="image" src="https://user-images.githubusercontent.com/37173958/63257494-30151f00-c27a-11e9-9ba1-c2ee9421e555.png">

```
[{"id":"f8c39451.3e2588","type":"ui_text","z":"2a69941d.ef5254","group":"632f4f94.2324a8","order":1,"width":"4","height":"1","name":"Condition Txt","label":"","format":"{{msg.payload.detail}}","layout":"row-center","x":1060,"y":140,"wires":[]},{"id":"f768b630.f413f","type":"function","z":"2a69941d.ef5254","name":"Prepare Dashboard Dat","func":"var windDirection = {};\nvar windDirectionIcon = {};\nvar windSpeed = {};\nvar windSpeedIcon = {};\nvar sunRise = {};\nvar sunSet = {};\nvar conditionIcon = {};\nvar date = new Date ();\n\n/* function for converting meteorogical degree to text */\n\nvar degToCard = function(deg){\nif (deg>11.25 && deg<=33.75){\nreturn \"Nord-Nord-Ost\";\n  }else if (deg>33.75 && deg<56.25){\nreturn \"Nord-Ost\";\n  }else if (deg>56.25 && deg<78.75){\nreturn \"Ost-Nord-Ost\";\n  }else if (deg>78.75 && deg<101.25){\nreturn \"Ost\";\n  }else if (deg>101.25 && deg<123.75){\nreturn \"Ost-Süd-Ost\";\n  }else if (deg>123.75 && deg<146.25){\nreturn \"Süd-Ost\";\n  }else if (deg>146.25 && deg<168.75){\nreturn \"Süd-Süd-Ost\";\n  }else if (deg>168.75 && deg<191.25){\nreturn \"Süd\";\n  }else if (deg>191.25 && deg<213.75){\nreturn \"Süd-Süd-West\";\n  }else if (deg>213.75 && deg<236.25){\nreturn \"Süd-West\";\n  }else if (deg>236.25 && deg<258.75){\nreturn \"West-Süd-West\";\n  }else if (deg>258.75 && deg<281.25){\nreturn \"West\";\n  }else if (deg>281.25 && deg<303.75){\nreturn \"West-Nord-West\";\n  }else if (deg>303.75 && deg<326.25){\nreturn \"Nord-West\";\n  }else if (deg>326.25 && deg<348.75){\nreturn \"Nord-Nord-West\";\n  }else{\nreturn \"Nord\"; \n  }\n}\n\n/* function for converting meteorogical degree to weather icons */\n\nvar degToCardIcon = function(deg){\nif (deg>11.25 && deg<=33.75){\nreturn \"wi-from-nne\";\n  }else if (deg>33.75 && deg<56.25){\nreturn \"wi-from-ne\";\n  }else if (deg>56.25 && deg<78.75){\nreturn \"wi-from-ene\";\n  }else if (deg>78.75 && deg<101.25){\nreturn \"wi-from-e\";\n  }else if (deg>101.25 && deg<123.75){\nreturn \"wi-from-ese\";\n  }else if (deg>123.75 && deg<146.25){\nreturn \"wi-from-se\";\n  }else if (deg>146.25 && deg<168.75){\nreturn \"wi-from-sse\";\n  }else if (deg>168.75 && deg<191.25){\nreturn \"wi-from-s\";\n  }else if (deg>191.25 && deg<213.75){\nreturn \"wi-from-ssw\";\n  }else if (deg>213.75 && deg<236.25){\nreturn \"wi-from-sw\";\n  }else if (deg>236.25 && deg<258.75){\nreturn \"wi-from-wsw\";\n  }else if (deg>258.75 && deg<281.25){\nreturn \"wi-from-w\";\n  }else if (deg>281.25 && deg<303.75){\nreturn \"wi-from-wnw\";\n  }else if (deg>303.75 && deg<326.25){\nreturn \"wi-from-nw\";\n  }else if (deg>326.25 && deg<348.75){\nreturn \"wi-from-nnw\";\n  }else{\nreturn \"wi-from-n\"; \n  }\n}\n\n/* Function for converting wind speed into Beaufort scale icon */\n\nvar speedToCardIcon = function(speed){\nif (speed>0.5 && speed<=1.5){\nreturn \"wi-wind-beaufort-1\";\n  }else if (speed>1.5 && speed<=3.3){\nreturn \"wi-wind-beaufort-2\";\n  }else if (speed>3.3 && speed<=5.5){\nreturn \"wi-wind-beaufort-3\";\n  }else if (speed>5.5 && speed<=7.9){\nreturn \"wi-wind-beaufort-4\";\n  }else if (speed>7.9 && speed<=10.7){\nreturn \"wi-wind-beaufort-5\";\n  }else if (speed>10.7 && speed<=13.8){\nreturn \"wi-wind-beaufort-6\";\n  }else if (speed>13.8 && speed<=17.1){\nreturn \"wi-wind-beaufort-7\";\n  }else if (speed>17.1 && speed<=20.7){\nreturn \"wi-wind-beaufort-8\";\n  }else if (speed>20.7 && speed<=24.4){\nreturn \"wi-wind-beaufort-9\";\n  }else if (speed>24.4 && speed<=28.4){\nreturn \"wi-wind-beaufort-10\";\n  }else if (speed>28.4 && speed<=32.6){\nreturn \"wi-wind-beaufort-11\";\n  }else if (speed>32.6){\nreturn \"wi-wind-beaufort-12\";\n  }else{\nreturn \"wi-wind-beaufort-0\"; \n  }\n}\n\n/* Function for Time Conversions */\n\nfunction timeConverter(UNIX_timestamp){\n  var a = new Date(UNIX_timestamp * 1000);\n  var hour = a.getHours();\n  var min = a.getMinutes();\n  if (min < 10) {min = \"0\" + min;}\n    else {min = min;}\n  var sec = a.getSeconds();\n  if (sec < 10) {sec = \"0\" + sec;}\n    else {sec = sec;}\n    \n  var time = hour + ':' + min + ':' + sec ;\n  return time;\n}\n\n/* Convert OpenWeeather Map Icon to https://erikflowers.github.io/weather-icons/ */\n\nconst owIconMap = new Map();\n\nowIconMap.set('01d', 'wi-day-sunny'); // clear sky\nowIconMap.set('02d', 'wi-day-cloudy'); // few clouds\nowIconMap.set('03d', 'wi-cloud'); // scattered clouds\nowIconMap.set('04d', 'wi-cloudy'); // broken clouds\nowIconMap.set('09d', 'wi-day-showers'); // shower rain\nowIconMap.set('10d', 'wi-day-rain'); // rain\nowIconMap.set('11d', 'wi-thunderstorm'); // thunderstorm\nowIconMap.set('13d', 'wi-snow'); // snow\nowIconMap.set('50d', 'wi-fog'); // mist\nowIconMap.set('01n', 'wi-night-clear'); // clear sky\nowIconMap.set('02n', 'wi-night-alt-cloudy'); // few clouds\nowIconMap.set('03n', 'wi-cloud'); // scattered clouds\nowIconMap.set('04n', 'wi-cloudy'); // broken clouds\nowIconMap.set('09n', 'wi-night-alt-showers'); // shower rain\nowIconMap.set('10n', 'wi-night-alt-rain'); // rain\nowIconMap.set('11n', 'wi-thunderstorm'); // thunderstorm\nowIconMap.set('13n', 'wi-snow'); // snow\nowIconMap.set('50n', 'wi-fog'); // mist\n\nconditionIcon.topic = \"ConditionIcon\";\nconditionIcon.payload = owIconMap.get(msg.payload.icon);\n\nwindDirection.topic = \"WindDirection\";\nwindDirection.payload = degToCard(msg.payload.winddirection);\n\nwindDirectionIcon.topic = \"WindDirectionIcon\";\nwindDirectionIcon.payload = degToCardIcon(msg.payload.winddirection);\n\nwindSpeed.topic = \"WindSpeed\";\nwindSpeed.payload = msg.payload.windspeed +  \" m/s\"; /* \" + windDirection.payload; */\n\nwindSpeedIcon.topic = \"WindSpeedIcon\";\nwindSpeedIcon.payload = speedToCardIcon(msg.payload.windspeed);\n\nsunRise.topic = \"SunRise\";\nsunRise.payload = timeConverter(msg.payload.sunrise);\n\nsunSet.topic = \"SunRet\";\nsunSet.payload = timeConverter(msg.payload.sunset);\n\nowIconMap.clear(); //freeing resource\n\nreturn [conditionIcon, windSpeedIcon, windSpeed, windDirection, windDirectionIcon, sunRise, sunSet];","outputs":7,"noerr":0,"x":710,"y":280,"wires":[["d4c31d0f.e64218"],["1d7a70ae.4a0587"],["10144e20.d1313a"],[],["788a6579.ea7e34"],["522c2d91.5ffedc"],["f0839cf9.f458a8"]]},{"id":"10144e20.d1313a","type":"ui_text","z":"2a69941d.ef5254","group":"9631a21b.1a6e48","order":2,"width":"2","height":"1","name":"WindSpeed","label":"","format":"{{msg.payload}}","layout":"row-center","x":1050,"y":260,"wires":[]},{"id":"522c2d91.5ffedc","type":"ui_text","z":"2a69941d.ef5254","group":"3917802.e83608","order":2,"width":"2","height":"1","name":"Sunrise","label":"","format":"{{msg.payload}}","layout":"col-center","x":1040,"y":400,"wires":[]},{"id":"f0839cf9.f458a8","type":"ui_text","z":"2a69941d.ef5254","group":"3917802.e83608","order":4,"width":"2","height":"1","name":"Sunset","label":"","format":"{{msg.payload}}","layout":"col-center","x":1040,"y":480,"wires":[]},{"id":"e03d7879.3389c8","type":"ui_template","z":"2a69941d.ef5254","group":"3917802.e83608","name":"Sunrise Icon","order":1,"width":"1","height":"1","format":"<link rel=\"stylesheet\" href=\"/addons/red/weather-icons/mycss/weather-icons.min.css\">\n<div style=\"display: flex;height: 100%;justify-content: left;align-items: center;\">\n<i class=\"fa-2x wi wi-sunrise\"></i>\n</div> ","storeOutMessages":true,"fwdInMessages":true,"templateScope":"local","x":1050,"y":360,"wires":[[]]},{"id":"6dd2d6ec.d2aba8","type":"ui_template","z":"2a69941d.ef5254","group":"3917802.e83608","name":"Sunset Icon","order":3,"width":"1","height":"1","format":"<link rel=\"stylesheet\" href=\"/addons/red/weather-icons/mycss/weather-icons.min.css\">\n<div style=\"display: flex;height: 100%;justify-content: left;align-items: center;\">\n<i class=\"fa-2x wi wi-sunset\"></i>\n</div> ","storeOutMessages":true,"fwdInMessages":true,"templateScope":"local","x":1050,"y":440,"wires":[[]]},{"id":"788a6579.ea7e34","type":"ui_template","z":"2a69941d.ef5254","group":"9631a21b.1a6e48","name":"WindDirection icon","order":3,"width":"1","height":"1","format":"<link rel=\"stylesheet\" href=\"/addons/red/weather-icons/mycss/weather-icons-wind.css\">\n<div style=\"display: flex;height: 100%;justify-content: center;align-items: center;\">\n<i class=\"fa-lg wi wi-wind {{msg.payload}}\"></i>\n</div> ","storeOutMessages":true,"fwdInMessages":true,"templateScope":"local","x":1070,"y":300,"wires":[[]]},{"id":"8f851902.1a086","type":"openweathermap","z":"2a69941d.ef5254","name":"Get Current Weather","wtype":"current","lon":"8.01","lat":"50.01","city":"","country":"","language":"de","x":380,"y":140,"wires":[["f768b630.f413f","f8c39451.3e2588"]]},{"id":"1d7a70ae.4a0587","type":"ui_template","z":"2a69941d.ef5254","group":"9631a21b.1a6e48","name":"WindSpeed Icon","order":1,"width":"1","height":"1","format":"<link rel=\"stylesheet\" href=\"/addons/red/weather-icons/mycss/weather-icons-wind.css\">\n<div style=\"display: flex;height: 100%;justify-content: left;align-items: center;\">\n<i class=\"fa-2x wi wi-wind {{msg.payload}}\"></i>\n</div>","storeOutMessages":true,"fwdInMessages":true,"templateScope":"local","x":1070,"y":220,"wires":[[]]},{"id":"d4c31d0f.e64218","type":"ui_template","z":"2a69941d.ef5254","group":"4fb1fda9.a150ac","name":"Condition Icon","order":1,"width":"2","height":"2","format":"<link rel=\"stylesheet\" href=\"/addons/red/weather-icons/mycss/weather-icons.min.css\">\n<div style=\"display: flex;height: 100%;justify-content: center;align-items: center;\">\n<i class=\"fa-4x wi {{msg.payload}}\"></i>\n</div>","storeOutMessages":true,"fwdInMessages":true,"templateScope":"local","x":1060,"y":180,"wires":[[]]},{"id":"780f6870.0ab52","type":"link in","z":"2a69941d.ef5254","name":"Link to Refresh Btn","links":["28574fc0.09b598"],"x":175,"y":140,"wires":[["8f851902.1a086","e6cb1247.6b6528"]]},{"id":"632f4f94.2324a8","type":"ui_group","z":"","name":"Condition","tab":"d4f13986.04113","order":4,"disp":false,"width":"4","collapse":false},{"id":"9631a21b.1a6e48","type":"ui_group","z":"","name":"Wind","tab":"d4f13986.04113","order":5,"disp":false,"width":"4","collapse":false},{"id":"3917802.e83608","type":"ui_group","z":"","name":"Ereignisse","tab":"4e9b13b2.12840c","order":5,"disp":true,"width":"6","collapse":false},{"id":"4fb1fda9.a150ac","type":"ui_group","z":"","name":"Condition","tab":"d4f13986.04113","order":2,"disp":false,"width":"2","collapse":false},{"id":"d4f13986.04113","type":"ui_tab","z":"","name":"Wetterstation","icon":"fa-thermometer-half","order":5,"disabled":false,"hidden":false},{"id":"4e9b13b2.12840c","type":"ui_tab","z":"","name":"Home","icon":"home","order":1}]
```

fragt über die [public OpenWeather-API](https://openweathermap.org/api) die aktuelle Wetterdaten ab, erstellt ein kleines Dashboard und nutzt darin die Icons aus den neuen CSS-Ressourcen.

<img width="499" alt="image" src="https://user-images.githubusercontent.com/37173958/63257678-9ef27800-c27a-11e9-8d8f-af16666341c1.png">

Exemplarisch sei hier der HTML-Code des `ui_template`-Nodes für das Symbol der aktuellen Wetterlage dargestellt:

<img width="873" alt="image" src="https://user-images.githubusercontent.com/37173958/60265799-e138b200-98e6-11e9-9c71-3cbfe171e538.png">

Wie oben erwähnt, sind ebenso die Sonnenauf- und -untergangssymbole verfügbar

<img width="303" alt="image" src="https://user-images.githubusercontent.com/37173958/60265975-560bec00-98e7-11e9-97b7-e089cff797d8.png">

Sofern die zusätzlichen Icons benötigt werden, stell dieses Beispiel eine schöne Ergänzung für Node-red im allg. und in Verbindung mit RedMatic im speziellen eine schöne Ergänzung dar, wenn man UI-Dashboard mit umfangreichen Wetterinformation nutzen will.

Vielen Dank an dieser Stelle für die [Hilfe und Anmerkungen](https://github.com/rdmtc/RedMatic/issues/220#issuecomment-499434377) von **@Hypnos3** und **@hobbyquaker** im Zusammenhang mit dieser Ergänzung für RedMatic.