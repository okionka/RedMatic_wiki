---
Category: User Flows
---

# Pillenförmige Schalter in Verbindung mit globalen Variablen

## Generelles
Häufig braucht man einen Schalter, der an eine globale Variable gekoppelt ist, bei Änderung Aktionen auslöst und den Status komprimiert/farblich anzeigt. Ich nutze diese Art für Anzeige von Nacht, Anwesend, Abwesend, etc. Es sieht dann so aus: 

![Darstellung im Browser](https://user-images.githubusercontent.com/17273119/60909649-11853680-a27f-11e9-9105-a00fd1fa5adc.png)

## Benötigte Erweiterungen
Keine.

## Einstellungen
Die Konfiguration besteht aus einem subflow und einem Dashbaord ui-template, die doppelt verknüpft sind. Änderungen der globalen Variablen steuert man links im subflow ein. Aktionen, die bei Änderung ausgelöst warden sind mit dem rechten, unteren Ausgang zu verknüpfen. 

![subflow und ui-template](https://user-images.githubusercontent.com/17273119/60909856-98d2aa00-a27f-11e9-941b-ce520d7bf03f.png)

