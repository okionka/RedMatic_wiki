Stand Juli 2019: Die CCU ist als unsicher zu betrachten und sollte nur in einer "vertrauenswürdigen" Umgebung betrieben (Netzwerke separieren, VLAN, ...) und niemals im Internet veröffentlicht werden (Kein Portforwarding nutzen!). Fernzugriff sollte nur mit weiteren Sicherheitsmaßnahmen (VPN, Reverse Proxy mit vorgeschalteter Authentifizierung, ...) realisiert werden. 

Node-RED bietet durch den "Exec" Node die Möglichkeit beliebige Prozesse zu starten. Sobald Zugriff auf Node-RED möglich ist und die Authentifizierung inaktiv ist - oder durch Sicherheitslücken in der CCU-Software, in Node-RED, oder sonstige Angriffe umgangen wird - kann die CCU komplett übernommen werden. 

Weiterführende Links:
* https://homematic-forum.de/forum/viewtopic.php?f=77&t=53582