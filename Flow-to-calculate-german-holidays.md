# German Holidays

## General Implementation
For home automatisation often Holidays are needed.

### Flow
For German Holidays you could use following flow:
![image](https://user-images.githubusercontent.com/12692680/40839051-15903bd8-65a1-11e8-96ee-7cf9ee3697b1.png)

### Flow export
```
[{"id":"f9ce10fb.f077a","type":"function","z":"a9b2e510.3f8de8","name":"Feiertagsberechnung","func":"const allRegions = [\n    'BW',\n    'BY',\n    'BE',\n    'BB',\n    'HB',\n    'HE',\n    'HH',\n    'MV',\n    'NI',\n    'NW',\n    'RP',\n    'SL',\n    'SN',\n    'ST',\n    'SH',\n    'TH',\n    'BUND',\n    'ALL',\n  ];\n\n    const allHolidays = [\n    'NEUJAHRSTAG',\n    'HEILIGEDREIKOENIGE',\n    'KARFREITAG',\n    'OSTERSONNTAG',\n    'OSTERMONTAG',\n    'TAG_DER_ARBEIT',\n    'CHRISTIHIMMELFAHRT',\n    'MARIAHIMMELFAHRT',\n    'PFINGSTSONNTAG',\n    'PFINGSTMONTAG',\n    'FRONLEICHNAM',\n    'DEUTSCHEEINHEIT',\n    'REFORMATIONSTAG',\n    'ALLERHEILIGEN',\n    'BUBETAG',\n    'ERSTERWEIHNACHTSFEIERTAG',\n    'ZWEITERWEIHNACHTSFEIERTAG',\n  ];\n  \n  const germanTranslations = {\n    NEUJAHRSTAG: 'Neujahrstag',\n    HEILIGEDREIKOENIGE: 'Heilige Drei Könige',\n    KARFREITAG: 'Karfreitag',\n    OSTERSONNTAG: 'Ostersonntag',\n    OSTERMONTAG: 'Ostermontag',\n    TAG_DER_ARBEIT: 'Tag der Arbeit',\n    CHRISTIHIMMELFAHRT: 'Christi Himmelfahrt',\n    PFINGSTSONNTAG: 'Pfingstsonntag',\n    PFINGSTMONTAG: 'Pfingstmontag',\n    FRONLEICHNAM: 'Fronleichnam',\n    MARIAHIMMELFAHRT: 'Mariä Himmelfahrt',\n    DEUTSCHEEINHEIT: 'Tag der Deutschen Einheit',\n    REFORMATIONSTAG: 'Reformationstag',\n    ALLERHEILIGEN: 'Allerheiligen',\n    BUBETAG: 'Buß- und Bettag',\n    ERSTERWEIHNACHTSFEIERTAG: '1. Weihnachtstag',\n    ZWEITERWEIHNACHTSFEIERTAG: '2. Weihnachtstag',\n    MONDAY: 'Montag',\n    TUESDAY: 'Dienstag',\n    WEDNESDAY: 'Mittwoch',\n    THURSDAY: 'Donnerstag',\n    FRIDAY: 'Freitag',\n    SATURDAY: 'Samstag',\n    SUNDAY: 'Sonntag',\n  };\n\n  let region = 'SN';\n  if (msg.region) {\n    region = msg.region;\n  } else if (msg.Region) {\n    region = msg.Region;\n  }\n\n  const yesterday = new Date();\n  yesterday.setDate(yesterday.getDate() - 1)\n  msg.isWeekendYesterday = isWeekend(yesterday);\n  msg.isHolidayYesterday = isHoliday(yesterday, region);\n  msg.HolidayYesterday = getHolidayByDate(yesterday, region);\n  msg.isSunOrHolidayYesterday = (yesterday.getDay() === 0) || msg.isHolidayYesterday;\n  msg.isWeekendOrHolidayYesterday = msg.isWeekendYesterday || msg.isHolidayYesterday;\n   \n  const today = new Date();\n  msg.isWeekendToday = isWeekend(today);\n  msg.isHolidayToday = isHoliday(today, region);\n  msg.HolidayToday = getHolidayByDate(today, region);\n  msg.isSunOrHolidayToday = (today.getDay() === 0) || msg.isHolidayToday;\n  msg.isWeekendOrHolidayToday = msg.isWeekendToday || msg.isHolidayToday;\n\n  const tomorrow = new Date();\n  tomorrow.setDate(tomorrow.getDate() + 1)\n  msg.isWeekendTomorrow = isWeekend(tomorrow);\n  msg.isHolidayTomorrow = isHoliday(tomorrow, region);\n  msg.HolidayTomorrow = getHolidayByDate(tomorrow, region);  \n  msg.isSunOrHolidayTomorrow = (tomorrow.getDay() === 0) || msg.isHolidayTomorrow;\n  msg.isWeekendOrHolidayTomorrow = msg.isWeekendTomorrow || msg.isHolidayTomorrow;\n\n  const dayAfterTomorrow = new Date();\n  tomorrow.setDate(tomorrow.getDate() + 2)\n  msg.isWeekendDayAfterTomorrow = isWeekend(dayAfterTomorrow);\n  msg.isHolidayDayAfterTomorrow = isHoliday(dayAfterTomorrow, region);\n  msg.HolidayDayAfterTomorrow = getHolidayByDate(dayAfterTomorrow, region);  \n  msg.isSunOrHolidayDayAfterTomorrow = (dayAfterTomorrow.getDay() === 0) || msg.isHolidayDayAfterTomorrow;\n  msg.isWeekendOrHolidayTomorrow = msg.isWeekendDayAfterTomorrow || msg.isHolidayDayAfterTomorrow;\n\n  msg.hollidays = getHolidays(today.getFullYear(), region);\n  \n  //Brückentag?\n  msg.dayBetweenSundayAndHoliday = ((yesterday.getDay() === 0) && msg.isHolidayTomorrow);\n  msg.dayBetweenHolidayAndSaturday = (msg.isHolidayYesterday && (tomorrow.getDay() === 6));\n  msg.dayBetweenWeekendOrHoliday = (msg.dayBetweenSundayAndHoliday || msg.dayBetweenHolidayAndSaturday);\n\n  /* - not needed globally\n  global.set(\"isWeekendYesterday\",msg.isWeekendYesterday);\n  global.set(\"isHolidayYesterday\",msg.isHolidayYesterday);\n  global.set(\"isSunOrHolidayYesterday\",msg.isSunOrHolidayYesterday);\n  global.set(\"isWeekendOrHolidayYesterday\",msg.isWeekendOrHolidayYesterday);\n*/\n\n  global.set(\"isWeekendToday\",msg.isWeekendToday);\n  global.set(\"isHolidayToday\",msg.isHolidayToday);\n  global.set(\"isSunOrHolidayToday\",msg.isSunOrHolidayToday);\n  global.set(\"isWeekendOrHolidayToday\",msg.isWeekendOrHolidayToday);\n\n  global.set(\"isWeekendTomorrow\",msg.isWeekendTomorrow);\n  global.set(\"isHolidayTomorrow\",msg.isHolidayTomorrow);\n  global.set(\"isSunOrHolidayTomorrow\",msg.isSunOrHolidayTomorrow);\n  global.set(\"isWeekendOrHolidayTomorrow\",msg.isWeekendOrHolidayTomorrow);\n\n  global.set(\"dayBetweenSundayAndHoliday\",msg.dayBetweenSundayAndHoliday);\n  global.set(\"dayBetweenHolidayAndSaturday\",msg.dayBetweenHolidayAndSaturday);\n  global.set(\"dayBetweenWeekendOrHoliday\",msg.dayBetweenWeekendOrHoliday);\n\n  for (i = 0; i < msg.hollidays.length; i++) { \n      let hd = msg.hollidays[i];\n      let d = hd.date;\n      \n      var timeDiff = d.getTime() - today.getTime();\n      if (timeDiff > 0) {\n          var diffDays = Math.ceil(timeDiff / (1000 * 3600 * 24));\n          msg.nextHolliday = hd;\n          msg.nextHollidayDiff = diffDays;\n          break;\n      }\n  }\n  \n  msg.workingDayToday = !msg.isWeekendOrHolidayToday;\n  msg.workingDayTomorrow = !msg.isWeekendOrHolidayTomorrow;\n  \n  //0 S 1 M 2 D 3 M 4 D 5 F 6 S 0 S\n  msg.nextWeekendOrHolidayDiff = (msg.nextHollidayDiff) ? Math.min(msg.nextHollidayDiff, 6 - today.getDay()) : 6 - today.getDay();\n  if (msg.nextHolliday && (msg.nextWeekendOrHolidayDiff == msg.nextHollidayDiff)) {\n    msg.nextWeekendOrHoliday = msg.nextHolliday;\n  } else {\n    let dayOfWeek = 6;//saturday\n    let date = new Date();\n    let diff = date.getDay() - dayOfWeek;\n    if (diff > 0) {\n        date.setDate(date.getDate() + 6);\n    }\n    else if (diff < 0) {\n        date.setDate(date.getDate() + ((-1) * diff))\n    }      \n    msg.nextWeekendOrHoliday = _newHoliday('SATURDAY',date);\n  }\n  \n  global.set(\"workingDayToday\",msg.workingDayToday); //EarlyMorning\n  global.set(\"workingDayTomorrow\",msg.workingDayTomorrow); //EarlyEvening\n  global.set(\"nextWeekendOrHolidayDiff\",msg.nextWeekendOrHolidayDiff);\n  global.set(\"nextHollidayDiff\",msg.nextHollidayDiff);\n    \n  return msg;\n  \n  // @flow\n  \n  /*!\n   * feiertage.js\n   * @repository https://github.com/sfakir/feiertagejs\n   * @docs https://github.com/sfakir/feiertagejs/blob/master/docs.md\n   *\n   * Copyright 2015-2018 Simon Fakir\n   * Released under the MIT license\n   */\n  \n  // holidays api\n   /**\n   * Checks if a specific date is saturday or sunday.\n   * @param date\n   * @returns {boolean}\n   */\n  function isWeekend(date) {\n    return date.getDay() === 0 || date.getDay() === 6;\n  }\n  \n  /**\n   * Check is specific date is holiday.\n   * @param date\n   * @param {Region} region two character {@link Region} code\n   * @returns {boolean}\n   */\n  function isHoliday(date, region) {\n    checkRegion(region);\n    date = new Date(date);\n  \n    const year = date.getFullYear();\n    const internalDate = toUtcTimestamp(date);\n    const holidays = _getHolidaysIntegerRepresentation(year, region);\n  \n    return holidays.indexOf(internalDate) !== -1;\n  }\n  \n  function getHolidayByDate(\n    date,\n    region = 'ALL'\n  ) {\n    checkRegion(region);\n    const holidays = _getHolidaysObjectRepresentation(date.getFullYear(), region);\n    return holidays.find(holiday => holiday.equals(date));\n  }\n  \n  // additional runtime checks\n  \n  /**\n   * Checks if the given region is a valid {@link Region}.\n   *\n   * @param region {@link Region} to check\n   * @throws {Error}\n   * @private\n   */\n  function checkRegion(region) {\n    if (region === null || region === undefined) {\n      throw new Error(`Region must not be undefined or null`);\n    }\n    if (allRegions.indexOf(region) === -1) {\n      throw new Error(\n        'Invalid region: ' +region + '! Must be one of ' + allRegions.toString()\n      );\n    }\n  }\n  \n  /**\n   * Checks if the given holidayName is a valid {@link HolidayType}.\n   * @param holidayName {@link HolidayType} to check\n   * @throws {Error}\n   * @private\n   */\n  function checkHolidayType(holidayName) {\n    if (holidayName === null || holidayName === undefined) {\n      throw new TypeError('holidayName must not be null or undefined');\n    }\n    if (allHolidays.indexOf(holidayName) === -1) {\n      throw new Error(\n        'feiertage.js: invalid holiday type \"' + holidayName + '\"! Must be one of ' + allHolidays.toString()\n      );\n    }\n  }\n  \n  function isSpecificHoliday(\n    date,\n    holidayName,\n    region = 'ALL'\n  ) {\n    checkRegion(region);\n    checkHolidayType(holidayName);\n    const holidays = _getHolidaysObjectRepresentation(date.getFullYear(), region);\n    return holidays.find(holiday => holiday.equals(date)) !== undefined;\n  }\n  \n  /**\n   * Returns all holidays of a year in a {@link Region}.\n   * @param year\n   * @param region\n   * @returns {Array.<Holiday>}\n   */\n  function getHolidays(year, region) {\n    year = parseInt(year);\n  \n    checkRegion(region);\n    return _getHolidaysObjectRepresentation(year, region);\n  }\n  \n  /**\n   *\n   * @param year\n   * @param region\n   * @returns {*}\n   * @private\n   */\n  function _getHolidaysIntegerRepresentation(year, region) {\n    const holidays = _getHolidaysOfYear(year, region);\n    return holidays.integers;\n  }\n  \n  /**\n   *\n   * @param year\n   * @param region\n   * @returns {Array.<Holiday>}\n   * @private\n   */\n  function _getHolidaysObjectRepresentation(year, region) {\n    const holidays = _getHolidaysOfYear(year, region);\n    return holidays.objects;\n  }\n  \n  /**\n   *\n   * @param year\n   * @param region\n   * @returns {{objects: Array.<Holiday>, integers}}\n   * @private\n   */\n  function _getHolidaysOfYear(year, region) {\n    const feiertageObjects = [\n      _newHoliday('NEUJAHRSTAG', _makeDate(year, 1, 1)),\n      _newHoliday('TAG_DER_ARBEIT', _makeDate(year, 5, 1)),\n      _newHoliday('DEUTSCHEEINHEIT', _makeDate(year, 10, 3)),\n      _newHoliday('ERSTERWEIHNACHTSFEIERTAG', _makeDate(year, 12, 25)),\n      _newHoliday('ZWEITERWEIHNACHTSFEIERTAG', _makeDate(year, 12, 26)),\n    ];\n  \n    const easter_date = getEasterDate(year);\n    let karfreitag = new Date(easter_date.getTime());\n    karfreitag = addDays(karfreitag, -2);\n    let ostermontag = new Date(easter_date.getTime());\n    ostermontag = addDays(ostermontag, 1);\n    let christi_himmelfahrt = new Date(easter_date.getTime());\n    christi_himmelfahrt = addDays(christi_himmelfahrt, 39);\n    let pfingstsonntag = new Date(easter_date.getTime());\n    pfingstsonntag = addDays(pfingstsonntag, 49);\n  \n    let pfingstmontag = new Date(easter_date.getTime());\n    pfingstmontag = addDays(pfingstmontag, 50);\n  \n    feiertageObjects.push(_newHoliday('KARFREITAG', karfreitag));\n    feiertageObjects.push(_newHoliday('OSTERMONTAG', ostermontag));\n    feiertageObjects.push(_newHoliday('CHRISTIHIMMELFAHRT', christi_himmelfahrt));\n    feiertageObjects.push(_newHoliday('PFINGSTMONTAG', pfingstmontag));\n  \n    // Heilige 3 Koenige\n    if (\n      region === 'BW' ||\n      region === 'BY' ||\n      region === 'ST' ||\n      region === 'ALL'\n    ) {\n      feiertageObjects.push(\n        _newHoliday('HEILIGEDREIKOENIGE', _makeDate(year, 1, 6))\n      );\n    }\n    if (region === 'BB' || region === 'ALL') {\n      feiertageObjects.push(_newHoliday('OSTERSONNTAG', easter_date));\n      feiertageObjects.push(_newHoliday('PFINGSTSONNTAG', pfingstsonntag));\n    }\n    // Fronleichnam\n    if (\n      region === 'BW' ||\n      region === 'BY' ||\n      region === 'HE' ||\n      region === 'NW' ||\n      region === 'RP' ||\n      region === 'SL' ||\n      region === 'ALL'\n    ) {\n      let fronleichnam = new Date(easter_date.getTime());\n      fronleichnam = addDays(fronleichnam, 60);\n      feiertageObjects.push(_newHoliday('FRONLEICHNAM', fronleichnam));\n    }\n  \n    // Maria Himmelfahrt\n    if (region === 'SL' || region === 'BY') {\n      feiertageObjects.push(\n        _newHoliday('MARIAHIMMELFAHRT', _makeDate(year, 8, 15))\n      );\n    }\n    // Reformationstag\n  \n    if (\n      year === 2017 ||\n      region === 'BB' ||\n      region === 'MV' ||\n      region === 'SN' ||\n      region === 'ST' ||\n      region === 'TH' ||\n      region === 'ALL'\n    ) {\n      feiertageObjects.push(\n        _newHoliday('REFORMATIONSTAG', _makeDate(year, 10, 31))\n      );\n    }\n  \n    // Allerheiligen\n    if (\n      region === 'BW' ||\n      region === 'BY' ||\n      region === 'NW' ||\n      region === 'RP' ||\n      region === 'SL' ||\n      region === 'ALL'\n    ) {\n      feiertageObjects.push(_newHoliday('ALLERHEILIGEN', _makeDate(year, 11, 1)));\n    }\n  \n    // Buss und Bettag\n    if (region === 'SN' || region === 'ALL') {\n      // @todo write test\n      const bussbettag = getBussBettag(year);\n      feiertageObjects.push(\n        _newHoliday(\n          'BUBETAG',\n          _makeDate(\n            bussbettag.getUTCFullYear(),\n            bussbettag.getUTCMonth() + 1,\n            bussbettag.getUTCDate()\n          )\n        )\n      );\n    }\n  \n    feiertageObjects.sort(\n      (a, b) => a.date.getTime() - b.date.getTime()\n    );\n  \n    return {\n      objects: feiertageObjects,\n      integers: generateIntegerRepresentation(feiertageObjects),\n    };\n  }\n  \n  /**\n   *\n   * @param objects\n   * @returns {Array}\n   * @private\n   */\n  function generateIntegerRepresentation(objects) {\n    return objects.map(holiday => toUtcTimestamp(holiday.date));\n  }\n  \n  /**\n   * Calculates the Easter date of a given year.\n   * @param year {number}\n   * @returns {Date} Easter date\n   * @private\n   */\n  function getEasterDate(year) {\n    const C = Math.floor(year / 100);\n    const N = year - 19 * Math.floor(year / 19);\n    const K = Math.floor((C - 17) / 25);\n    let I = C - Math.floor(C / 4) - Math.floor((C - K) / 3) + 19 * N + 15;\n    I -= 30 * Math.floor(I / 30);\n    I -=\n      Math.floor(I / 28) *\n      (1 -\n        Math.floor(I / 28) *\n          Math.floor(29 / (I + 1)) *\n          Math.floor((21 - N) / 11));\n    let J = year + Math.floor(year / 4) + I + 2 - C + Math.floor(C / 4);\n    J -= 7 * Math.floor(J / 7);\n    const L = I - J;\n    const M = 3 + Math.floor((L + 40) / 44);\n    const D = L + 28 - 31 * Math.floor(M / 4);\n    return new Date(year, M - 1, D);\n  }\n  \n  /**\n   * Computes the \"Buss- und Bettag\"'s date.\n   * @param jahr {number}\n   * @returns {Date} the year's \"Buss- und Bettag\" date\n   * @private\n   */\n  function getBussBettag(jahr) {\n    const weihnachten = new Date(jahr, 11, 25, 12, 0, 0);\n    const ersterAdventOffset = 32;\n    let wochenTagOffset = weihnachten.getDay() % 7;\n  \n    if (wochenTagOffset === 0) wochenTagOffset = 7;\n  \n    const tageVorWeihnachten = wochenTagOffset + ersterAdventOffset;\n  \n    let bbtag = new Date(weihnachten.getTime());\n    bbtag = addDays(bbtag, -tageVorWeihnachten);\n  \n    return bbtag;\n  }\n  \n  /**\n   * Adds {@code days} days to the given {@link Date}.\n   * @param date\n   * @param days\n   * @returns {Date}\n   * @private\n   */\n  function addDays(date, days) {\n    date.setDate(date.getDate() + days);\n    return date;\n  }\n  \n  /**\n   * Creates a new {@link Date}.\n   * @param year\n   * @param naturalMonth month (1-12)\n   * @param day\n   * @returns {Date}\n   * @private\n   */\n  function _makeDate(year, naturalMonth, day) {\n    return new Date(year, naturalMonth - 1, day);\n  }\n  \n  /**\n   *\n   * @param name\n   * @param date\n   * @returns {Holiday}\n   * @private\n   */\n  function _newHoliday(id, date) {\n    return {\n      id,\n      name : germanTranslations[id],\n      date,\n      dateString: _localeDateObjectToDateString(date),\n      getNormalizedDate() {\n        return toUtcTimestamp(this.date);\n      },\n      equals(date) {\n        const string = _localeDateObjectToDateString(date);\n        return this.dateString === string;\n      },\n    };\n  }\n  \n  /**\n   *\n   * @param date\n   * @returns {string}\n   * @private\n   */\n  function _localeDateObjectToDateString(date) {\n    date = new Date(date.getTime() - date.getTimezoneOffset() * 60 * 1000);\n    date.setUTCHours(0, 0, 0, 0);\n    return date.toISOString().slice(0, 10);\n  }\n  \n  /**\n   * Returns the UTC timestamp of the given date with hours, minutes, seconds, and milliseconds set to zero.\n   * @param date\n   * @returns {number} UTC timestamp\n   */\n  function toUtcTimestamp(date) {\n    date.setHours(0, 0, 0, 0);\n    return date.getTime();\n  }","outputs":1,"noerr":0,"x":520,"y":1540,"wires":[["d1813362.7391b"]]},{"id":"d1813362.7391b","type":"debug","z":"a9b2e510.3f8de8","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"true","x":710,"y":1540,"wires":[]},{"id":"38f6d2fd.efc17e","type":"inject","z":"a9b2e510.3f8de8","name":"","topic":"","payload":"","payloadType":"date","repeat":"","crontab":"","once":false,"onceDelay":0.1,"x":140,"y":1540,"wires":[["170efdde.f9fb12"]]},{"id":"170efdde.f9fb12","type":"change","z":"a9b2e510.3f8de8","name":"Region = SN","rules":[{"t":"set","p":"region","pt":"msg","to":"SN","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":310,"y":1540,"wires":[["f9ce10fb.f077a"]]}]
```

## Flow Input
As Input you can setup one of the following german regions to `msg.region`:
* BW - Baden-Württemberg
* BY - Bayern
* BE - Berlin
* BB - Brandenburg
* HB - Bremen
* HE - Hessen
* HH - Hamburg
* MV - Mecklenburg-Vorpommern
* NI - Niedersachsen
* NW - Nordrhein-Westfalen
* RP - Rheinland-Pfalz
* SL - Saarland
* SN - Sachsen
* ST - Sachsen-Anhalt
* SH - Schleswig-Holstein
* TH - Thüringen
* BUND - Gesamt-Deutschland

## Flow Output
after calculation the following output Variables will be set in the msg object:
### Yesterday
* `msg.isWeekendYesterday` - is true, if yesterday was saturday or sunday
* `msg.isHolidayYesterday` - is true, if yesterday was a holiday
* `msg.isSunOrHolidayYesterday` - is true, if yesterday was sunday or a holiday
* `msg.isWeekendOrHolidayYesterday` - is true, if yesterday was saturday, sunday or a holiday
* `msg.HolidayYesterday` - if yesterday was a holiday the  object representation of the holiday (otherwise null)
   * `msg.HolidayYesterday.id` - internal ID of the holiday like "MARIAHIMMELFAHRT"
   * `msg.HolidayYesterday.name` - name of the holiday like "Mariä Himmelfahrt"
   * `msg.HolidayYesterday.date` - date of the holiday as javascript Date object
   * `msg.HolidayYesterday.dateString` - date of the holiday as string like "2018-08-15"

### Today
* `msg.isWeekendToday` - is true, if today is saturday or sunday
* `msg.isHolidayToday` - is true, if today is a holiday
* `msg.isSunOrHolidayToday` - is true, if today is sunday or a holiday
* `msg.isWeekendOrHolidayToday` - is true, if today is saturday, sunday or a holiday
* `msg.HolidayToday` - if today is a holiday the  object representation of the holiday (otherwise null)
   * `msg.HolidayToday.id` - internal ID of the holiday like "MARIAHIMMELFAHRT"
   * `msg.HolidayToday.name` - name of the holiday like "Mariä Himmelfahrt"
   * `msg.HolidayToday.date` - date of the holiday as javascript Date object
   * `msg.HolidayToday.dateString` - date of the holiday as string like "2018-08-15"

### Tomorrow
* `msg.isWeekendTomorrow` - is true, if tomorrow will be saturday or sunday
* `msg.isHolidayTomorrow` - is true, if tomorrow will be a holiday
* `msg.isSunOrHolidayTomorrow` - is true, if tomorrow will be sunday or a holiday
* `msg.isWeekendOrHolidayTomorrow` - is true, if tomorrow will be saturday, sunday or a holiday
* `msg.HolidayTomorrow` - if tomorrow will be a holiday the  object representation of the holiday (otherwise null)
   * `msg.HolidayTomorrow.id` - internal ID of the holiday like "MARIAHIMMELFAHRT"
   * `msg.HolidayTomorrow.name` - name of the holiday like "Mariä Himmelfahrt"
   * `msg.HolidayTomorrow.date` - date of the holiday as javascript Date object
   * `msg.HolidayTomorrow.dateString` - date of the holiday as string like "2018-08-15"

### day after tomorrow
* `msg.isWeekendDayAfterTomorrow` - is true, if the day after tomorrow will be saturday or sunday
* `msg.isHolidayDayAfterTomorrow` - is true, if the day after tomorrow will be a holiday
* `msg.isSunOrHolidayDayAfterTomorrow` - is true, if the day after tomorrow will be sunday or a holiday
* `msg.isWeekendOrHolidayTomorrow` - is true, if the day after tomorrow will be saturday, sunday or a holiday
* `msg.HolidayDayAfterTomorrow` - if the day after tomorrow will be a holiday the object representation of the holiday (otherwise null)
   * `msg.HolidayDayAfterTomorrow.id` - internal ID of the holiday like "MARIAHIMMELFAHRT"
   * `msg.HolidayDayAfterTomorrow.name` - name of the holiday like "Mariä Himmelfahrt"
   * `msg.HolidayDayAfterTomorrow.date` - date of the holiday as javascript Date object
   * `msg.HolidayDayAfterTomorrow.dateString` - date of the holiday as string like "2018-08-15"

### General
is is a day between a holiday and weekend (german Brückentag)
* `msg.dayBetweenSundayAndHoliday` - is true, if tuesday is a holiday, when monday is not a holiday
* `msg.dayBetweenHolidayAndSaturday` - is true, if thursday is a holiday, when friday is not a holiday
* `msg.dayBetweenWeekendOrHoliday` - is true, if `msg.dayBetweenSundayAndHoliday` or `msg.dayBetweenHolidayAndSaturday` is true
* `msg.workingDayToday` - is true, if today is not weekend or holiday
* `msg.workingDayTomorrow` - is true, if tomorrow is not weekend or holiday
* `msg.nextHollidayDiff` - the number of days until the next holiday
* `msg.nextHolliday` - the next holiday as a object representation
   * `msg.nextHolliday.id` - internal ID of the holiday like "MARIAHIMMELFAHRT"
   * `msg.nextHolliday.name` - name of the holiday like "Mariä Himmelfahrt"
   * `msg.nextHolliday.date` - date of the holiday as javascript Date object
   * `msg.nextHolliday.dateString` - date of the holiday as string like "2018-08-15"
* `msg.nextWeekendOrHolidayDiff` - the number of days until the next weekend-day or holiday
* `msg.nextWeekendOrHoliday` - the object representation of the day


all Holidays as an array of objedts for the current year:
`msg.hollidays`

every item in the array will have the following propertys:
   * `msg.hollidays[i].id` - internal ID of the holiday like "MARIAHIMMELFAHRT"
   * `msg.hollidays[i].name` - name of the holiday like "Mariä Himmelfahrt"
   * `msg.hollidays[i].date` - date of the holiday as javascript Date object
   * `msg.hollidays[i].dateString` - date of the holiday as string like "2018-08-15"

## Global Variables
additional to the msg which was given back, the following global variables will be set, which can be used in various nodes. The value is equal to the one which is given back in the message object.
* `global.get("isWeekendOrHolidayTomorrow",msg.isWeekendOrHolidayTomorrow);`
* `global.get("isWeekendToday",msg.isWeekendToday);`
* `global.get("isHolidayToday",msg.isHolidayToday);`
* `global.get("isSunOrHolidayToday",msg.isSunOrHolidayToday);`
* `global.get("isWeekendOrHolidayToday",msg.isWeekendOrHolidayToday);`
* `global.get("isWeekendTomorrow",msg.isWeekendTomorrow);`
* `global.get("isHolidayTomorrow",msg.isHolidayTomorrow);`
* `global.get("isSunOrHolidayYesterday",msg.isSunOrHolidayYesterday);`
* `global.get("isWeekendOrHolidayTomorrow");`
* `global.get("dayBetweenSundayAndHoliday");`
* `global.get("dayBetweenHolidayAndSaturday");`
* `global.get("dayBetweenWeekendOrHoliday");`
* `global.get("workingDayToday");`
* `global.get("workingDayTomorrow");`
* `global.get("nextWeekendOrHolidayDiff");`
* `global.get("nextHollidayDiff");`
