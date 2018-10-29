# Deutsche Feiertage

## Generelles
Für die Hausautomatisierung kann es sein, das die Steuerung basierend auf Feiertagen, Wochenenden benötigt wird. So sollen vielleicht Rollläden an Feiertagen oder Wochenenden später öffnen und später geschlossen werden.

## Benötigte Erweiterungen
unter [Zusätzliche Node-RED Nodes installieren](https://github.com/hobbyquaker/RedMatic/wiki/Node-Installation) ist beschrieben wie weitere Nodes installiert werden können. Hier installieren Sie Bitte den node `node-red-contrib-german-holidays`.

## Wie verwenden

importieren Sie den folgenden Flow wie unter [Flows importieren](https://github.com/hobbyquaker/RedMatic/wiki/Flow-Import) beschrieben:

    [{"id":"2607227a.3c983e","type":"german-holidays","z":"c4313d2c.5d102","name":"","region":"SN","x":420,"y":140,"wires":[["dcaacec7.e1eb","15259bce.575154"]]},{"id":"dcaacec7.e1eb","type":"debug","z":"c4313d2c.5d102","name":"Holidays","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"true","x":620,"y":100,"wires":[]},{"id":"d2ed4078.52011","type":"inject","z":"c4313d2c.5d102","name":"","topic":"","payload":"","payloadType":"date","repeat":"","crontab":"05 00 * * *","once":false,"onceDelay":0.1,"x":150,"y":100,"wires":[["2607227a.3c983e"]]},{"id":"e4912846.3a1ca8","type":"inject","z":"c4313d2c.5d102","name":"","topic":"","payload":"","payloadType":"date","repeat":"","crontab":"","once":true,"onceDelay":"1","x":150,"y":180,"wires":[["2607227a.3c983e"]]},{"id":"1ab3e37c.4d15fd","type":"comment","z":"c4313d2c.5d102","name":"every day at midnight","info":"","x":180,"y":60,"wires":[]},{"id":"869da82f.484e48","type":"comment","z":"c4313d2c.5d102","name":"once on Node-Red start","info":"","x":180,"y":140,"wires":[]},{"id":"15259bce.575154","type":"change","z":"c4313d2c.5d102","name":"","rules":[{"t":"set","p":"day-info","pt":"global","to":"payload","tot":"msg"}],"action":"","property":"","from":"","to":"","reg":false,"x":650,"y":180,"wires":[[]]},{"id":"d2fe809f.3c90d","type":"switch","z":"c4313d2c.5d102","name":"","property":"day-info.today.isWeekendOrHoliday","propertyType":"global","rules":[{"t":"true"},{"t":"else"}],"checkall":"true","repair":false,"outputs":2,"x":410,"y":300,"wires":[["c73a89b5.6630f8"],["e245c8da.585928"]]},{"id":"26326493.2e010c","type":"inject","z":"c4313d2c.5d102","name":"","topic":"","payload":"true","payloadType":"bool","repeat":"","crontab":"","once":false,"onceDelay":0.1,"x":150,"y":300,"wires":[["d2fe809f.3c90d"]]},{"id":"c73a89b5.6630f8","type":"debug","z":"c4313d2c.5d102","name":"is Weekend or Holiday","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"payload","x":660,"y":300,"wires":[]},{"id":"e245c8da.585928","type":"debug","z":"c4313d2c.5d102","name":"is not a Weekend and not a Holiday","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"payload","x":700,"y":360,"wires":[]},{"id":"e427d079.51212","type":"comment","z":"c4313d2c.5d102","name":"Example for usage in switch node","info":"","x":210,"y":260,"wires":[]}]

Sie müssten dann folgendes Bild sehen:
![example2](https://user-images.githubusercontent.com/12692680/47651938-df1a2a00-db84-11e8-8f32-e1f2dfb8c5d9.png)

**Einstellen:**

Sie müssen im Node Holidays ihr Bundesland einstellen (Doppel-Klicken, ändern, speichern und deployen).

**Die Funktionsweise ist die folgende:**
 - **Der obere Flow:**
    - Dieser Flow wird täglich kurz nach Mitternacht und jedesmal nach dem Neustart von Node-Red (oder wenn sie den Flow komplett neu deployen) gestartet.
    - Daraufhin werden die Feiertage berechnet.
    - Im nachfolgenden change Node werden die berechneten Dtaen im globalen Context abgespeichert.
  - **Der untere Flow:**
    - Dieser Flow stellt ein Beispiel dar, wie sie über einen Switch node auf die Daten zugreifen können und den Ablauf der FLows entsprechend steuern können.
    - Die Möglichkeiten, welche Sie haben ist in der [Beschreibung des Nodes](https://www.npmjs.com/package/node-red-contrib-german-holidays) hinterlegt. Achten Sie Bitte, das Sie alles unter `msg.payload...` dann im globalen context als **global.** `day-info`, wobei der `global.` in der drop-down Box ausgewählt wird.
![image](https://user-images.githubusercontent.com/12692680/47652354-f7d70f80-db85-11e8-9212-17330556f675.png)

## Auszug möglicher Funktionen
Die vollständige Liste der Möglichkeiten sehen Sie in der [Beschreibung des Nodes](https://www.npmjs.com/package/node-red-contrib-german-holidays)

### Gestern
* **global.** `day-info.yesterday.isSaturday` - ist `true`, wenn gestern Samstag war
* **global.** `day-info.yesterday.isSunday` - ist `true`, wenn gestern Sonntag war
* **global.** `day-info.yesterday.isHoliday` - ist `true`, wenn gestern ein Feiertag war
* **global.** `day-info.yesterday.isWeekend` - ist `true`, wenn gestern Samstag oder Sonntag war
* **global.** `day-info.yesterday.isSunOrHoliday` - ist `true`, wenn gestern Sonntag oder ein Feiertag war
* **global.** `day-info.yesterday.isWeekendOrHoliday` - ist `true`, wenn gestern Samstag, Sonntag oder ein Feiertag war

### heute
* **global.** `day-info.today.isSaturday` - ist `true`, wenn heute Samstag ist
* **global.** `day-info.today.isSunday` - ist `true`, wenn heute Sonntag ist
* **global.** `day-info.today.isHoliday` - ist `true`, wenn heute ein Feiertag ist
* **global.** `day-info.today.isWeekend` - ist `true`, wenn heute Samstag oder Sonntag ist
* **global.** `day-info.today.isSunOrHoliday` - ist `true`, wenn heute Sonntag oder ein Feiertag ist
* **global.** `day-info.today.isWeekendOrHoliday` - ist `true`, wenn heute Samstag, Sonntag oder ein Feiertag ist
* **global.** `day-info.today.isBetweenSundayAndHoliday` (Brückentag) - ist `true`, wenn heute Montag ist und morgen ein Feiertag ist
* **global.** `day-info.today.isBetweenHolidayAndSaturday` (Brückentag) - ist `true`, wenn heute Freitag ist und gestern ein Feiertag war
* **global.** `day-info.today.isBetweenWeekendOrHoliday` (Brückentag) - ist `true`, wenn gestern ein Feiertag oder Sonntag ist und morgen ein Feiertag oder Samstag ist und heute kein Feiertag oder Samstag oder Sonntag ist

### morgen (in 1 Tag)
* **global.** `day-info.tomorrow.isSaturday` - ist `true`, wenn morgen Samstag ist
* **global.** `day-info.tomorrow.isSunday` - ist `true`, wenn morgen Sonntag ist
* **global.** `day-info.tomorrow.isHoliday` - ist `true`, wenn morgen ein Feiertag ist
* **global.** `day-info.tomorrow.isWeekend` - ist `true`, wenn morgen Samstag oder Sonntag ist
* **global.** `day-info.tomorrow.isSunOrHoliday` - ist `true`, wenn morgen Sonntag oder ein Feiertag ist
* **global.** `day-info.tomorrow.isWeekendOrHoliday` - ist `true`, wenn morgen Samstag, Sonntag oder ein Feiertag ist
* **global.** `day-info.tomorrow.isBetweenSundayAndHoliday` (Brückentag) - ist `true`, wenn morgen Montag ist und übermorgen ein Feiertag ist
* **global.** `day-info.tomorrow.isBetweenHolidayAndSaturday` (Brückentag) - ist `true`, wenn morgen Freitag ist und heute ein Feiertag ist
* **global.** `day-info.tomorrow.isBetweenWeekendOrHoliday` (Brückentag) - ist `true`, wenn heute ein Feiertag oder Sonntag ist und in 2 Tagen ein Feiertag oder Samstag ist und morgen kein Feiertag oder Samstag oder Sonntag ist

### übermorgen (in 2 Tagen)
* **global.** `day-info.dayAfterTomorrow.isSaturday` - ist `true`, wenn in 2 Tagen Samstag ist
* **global.** `day-info.dayAfterTomorrow.isSunday` - ist `true`, wenn in 2 Tagen Sonntag ist
* **global.** `day-info.dayAfterTomorrow.isHoliday` - ist `true`, wenn in 2 Tagen ein Feiertag ist
* **global.** `day-info.dayAfterTomorrow.isWeekend` - ist `true`, wenn in 2 Tagen Samstag oder Sonntag ist
* **global.** `day-info.dayAfterTomorrow.isSunOrHoliday` - ist `true`, wenn in 2 Tagen Sonntag oder ein Feiertag ist
* **global.** `day-info.dayAfterTomorrow.isWeekendOrHoliday` - ist `true`, wenn in 2 Tagen Samstag, Sonntag oder ein Feiertag ist
* **global.** `day-info.dayAfterTomorrow.isBetweenSundayAndHoliday` (Brückentag) - ist `true`, wenn in 2 Tagen Montag ist und in 3 Tagen ein Feiertag ist
* **global** `day-info.dayAfterTomorrow.isBetweenHolidayAndSaturday` (Brückentag) - ist `true`, wenn in 2 Tagen Freitag ist und morgen (in 1 Tag) ein Feiertag ist
* **global.** `day-info.dayAfterTomorrow.isBetweenWeekendOrHoliday` (Brückentag) - ist `true`, wenn morgen (in 1 Tag) ein Feiertag oder Sonntag ist und in 3 Tagen ein Feiertag oder Samstag ist und in 2 Tagen kein Feiertag oder Samstag oder Sonntag ist

### in 3 Tagen
* **global** `day-info.yesafterTheDayAfterTomorrowerday.isSaturday` - ist `true`, wenn in 3 Tagen Samstag ist
* **global** `day-info.afterTheDayAfterTomorrow.isSunday` - ist `true`, wenn in 3 Tagen Sonntag ist
* **global** `day-info.afterTheDayAfterTomorrow.isHoliday` - ist `true`, wenn in 3 Tagen ein Feiertag ist
* **global** `day-info.afterTheDayAfterTomorrow.isWeekend` - ist `true`, wenn in 3 Tagen Samstag oder Sonntag ist
* **global** `day-info.afterTheDayAfterTomorrow.isSunOrHoliday` - ist `true`, wenn in 3 Tagen Sonntag oder ein Feiertag ist
* **global** `day-info.afterTheDayAfterTomorrow.isWeekendOrHoliday` - ist `true`, wenn in 3 Tagen Samstag, Sonntag oder ein Feiertag ist

### generelles
* **global** `day-info.next.hollidayDiff` - Anzahl der Tage zum nächsten Feiertag
* **global** `day-info.next.holliday.name` - Name des nächsten Feiertages
* **global** `day-info.next.holliday.weekendOrHolidayDiff` - Anzahl der Tage zum nächsten Feiertages, Samstag oder Sonntags
* **global** `day-info.next.holliday.weekendOrHoliday.name` - Name des nächsten Feiertages, Samstag oder Sonntages
* **global** `day-info.weekNumber` - aktuelle Wochennummer
* **global** `day-info.weekNumberEven` - ist `true`, wenn die aktuelle Woche gerade ist

## Bugs, Wünsche
Bitte als issue im Github unter [https://github.com/Hypnos3/node-red-contrib-german-holidays](https://github.com/Hypnos3/node-red-contrib-german-holidays/issues) hinterlegen.
