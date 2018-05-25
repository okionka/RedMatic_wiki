Leider gibt es keine Möglichkeit an der CCU angelernte Aktoren zu deaktivieren, dies kann störend sein z.B. bei einen Zwischenstecker der nur für den Weihnachtsbaum verwendet wird und 11 Monate im Jahr in der Schublade verbleibt und dann eine ständige `UNREACH` Servicemeldung erzeugt. Es ist zwar unmöglich diese Meldung zu bestätigen, allerdings gibt es die Möglichkeit der Logikschicht "vorzugaukeln" dass der Aktor wieder erreichbar ist. Folgender Flow reagiert auf `UNREACH` Events, prüft ob der Aktor in einer Liste von zu deaktivierenden Aktoren enthalten ist und sendet der Logikschicht einen "gefakten" Event der die Meldung zurücksetzt.

#### rpc event

![](images/unreach-1.png)

#### function

![](images/unreach-2.png)

#### rpc 

![](images/unreach-3.png)