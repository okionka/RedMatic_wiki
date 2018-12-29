### 1) Abfrage von CCU-Variabeln beschleunigen
### 2) ...
### 3) ...

- - - - - - - - - - - - - - - - - - - - 

### 1) Abfrage von CCU-Variablen beschleunigen
Per Default Settings werden CCU-Variablen alle 30 Sekunden von der Rega abgeholt. Mit dem "poll" Node (unter CCU) kann man eine sofortige Abfrage erzwingen und bestimmte Prozesse somit massiv beschleunigen. Dies kann z.B. notwendig sein, wenn man eine Alarmanlage mit CCU-Variablen anlegen will.

Umsetzung:

1) "poll" Node anlegen, CCU auswählen und eventuell den Node benennen
2) Mittels eines "value" oder "rpc event" nodes einen virtuellen Taster der CCU abfragen (z.B. den BidCoS-RF:1 HM-RCV-50 BidCoS-RF:1) und mit dem "poll" node verbinden.
3) Ein Programm in der CCU-Anlegen, das bei Änderung einer der "wichtigen" Variablen den virtuellen Taster auslöst.
