# subFlow withinTime
## introduction
Sometimes it is needed to send a message only within a specified time frame. Example only send a message for instance between 12:00 and 18:00.

For this the following example with subFlow withinTime can be used:
![image](https://user-images.githubusercontent.com/12692680/40841302-4740b53c-65aa-11e8-83b7-7dc4e7e1cb03.png)

### Flow export
```
[{"id":"e4c6859.9fa0278","type":"subflow","name":"withinTime","info":"message will be send to first output\nif msg.currentTime (or if not defined\ncurrent time) is between\n\nmsg.startTime and msg.endTime\n\notherwise will send to second output.\n","in":[{"x":50,"y":30,"wires":[{"id":"55a09953.5c1be8"}]}],"out":[{"x":500,"y":40,"wires":[{"id":"55a09953.5c1be8","port":0}]},{"x":500,"y":100,"wires":[{"id":"55a09953.5c1be8","port":1}]}]},{"id":"55a09953.5c1be8","type":"function","z":"e4c6859.9fa0278","name":"ctrl","func":"\nmsg.withinTime = withinTime(msg.startTime, msg.endTime, msg.currentTime);\nif (msg.withinTime) {\n    //nicht innerhalb der eingestellten Zeit\n    return [msg,null]\n}\nreturn [null, msg]\n\n/********************************************\n* Funktionen:\n*********************************************/\n\n\n/**\n * Creates a new {@link Date}.\n * @param start     start time\n * @param end       end time week\n * @param test      time to test\n * @returns true if test date is in start/end \n */\nfunction withinTime(start, end, test) {\n    function minutesOfDay(t) {\n        let d = new Date();\n        if (t) {\n            let time = t.match( /(\\d+)(?::(\\d\\d))?\\s*(p?)/ );\n            d.setHours( parseInt( time[1]) + (time[3] ? 12 : 0) );\n            d.setMinutes( parseInt( time[2]) || 0 );\n        }\n        return d.getMinutes() + d.getHours() * 60;\n    }\n    \n    function getparts(s,b) {\n        if (!s) return s;\n        \n        s = s.split(/\\n|\\t|\\||\\\\|\\//);\n        let ret = [];\n     \n        for (i=s.length-1; i>=0; i--) {\n            let p = s[i].trim();\n            if (p) {\n                ret.push(p);\n            }\n        }\n        if (ret.length > 1) {\n            if (b) return ret[0];\n            return ret[1];\n        }\n      \n        if (ret.length === 0) {\n            return '';\n        }\n        return ret[0];\n    }\n    start = getparts(start, global.get(\"workingDayToday\"));\n    end = getparts(end, global.get(\"workingDayTomorrow\"));\n\n    start = minutesOfDay(start);\n    end = minutesOfDay(end);\n    test = minutesOfDay(test);\n    //node.warn( start + ' - ' + test + ' - ' + end);\n    \n    if (start < end) {\n        return (test >= start && test <= end);\n    } else {\n        return !(test > end && test < start);\n    }\n}\n\n","outputs":2,"noerr":0,"x":250,"y":40,"wires":[[],[]]},{"id":"1e05dd25.1b9c93","type":"subflow:e4c6859.9fa0278","z":"a9b2e510.3f8de8","name":"","x":530,"y":1740,"wires":[["34e12bb0.d47f84"],["6e18b325.f4c59c"]]},{"id":"21b070e7.72812","type":"change","z":"a9b2e510.3f8de8","name":"23:00 - 5:45","rules":[{"t":"set","p":"startTime","pt":"msg","to":"23:00","tot":"str"},{"t":"set","p":"endTime","pt":"msg","to":"05:45","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":350,"y":1740,"wires":[["1e05dd25.1b9c93"]]},{"id":"faa38b88.c8a838","type":"inject","z":"a9b2e510.3f8de8","name":"","topic":"","payload":"","payloadType":"date","repeat":"","crontab":"","once":false,"onceDelay":0.1,"x":180,"y":1740,"wires":[["21b070e7.72812"]]},{"id":"34e12bb0.d47f84","type":"debug","z":"a9b2e510.3f8de8","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"true","x":710,"y":1740,"wires":[]},{"id":"6e18b325.f4c59c","type":"debug","z":"a9b2e510.3f8de8","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"true","x":710,"y":1780,"wires":[]}]
```

## Input
As Input to the flow the following informations can be provided:
* `msg.startTime` - a simple time as string "8:00" in 12 hour format which is the start of the time
* `msg.endTime` - a simple time as string "20:00" in 12 hour format which is the end of the time
* `msg.currentTime` - _optional_ a simple time as string "14:00" in 12 hour format which is the time to check if it is between `msg.startTime` and `msg.endTime`

If any of the parameters is missing the current time will be used.
Typically the `msg.currentTime` will not be set so that the current time should be used.

If the `msg.endTime` is lower as the `msg.startTime` the time frame will last over midnight.

### Enhanced
If the global variables "workingDayToday" of type boolean exists, as `msg.startTime` two times could be provided seperated with |.
Example:
`msg.startTime = '8:30 | 9:00';`
Then the first time as `msg.startTime` will be used if the global variable "workingDayToday" is true, otherwise the second time will used.

If the global variables "workingDayTomorrow" of type boolean exists, as `msg.endTime` two times could be provided seperated with |.
Example:
`msg.endTime = '18:30 | 21:00';`
Then the first time as `msg.endTime` will be used if the global variable "workingDayTomorrow" is true, otherwise the second time will used.

## Output
The subFlow has two outputs. The Message will be send to the first one if `msg.currentTime` (or current time) is between `msg.startTime` and `msg.endTime`. Otherwise the message will send to second output.

Additional `msg.withinTime` will be set to true if the time is in range or not.