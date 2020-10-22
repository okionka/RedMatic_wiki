---
Title: Zusätzliche Node-RED Nodes installieren
Category: Administration
---

# Zusätzliche Node-RED Nodes installieren

Node-RED kann durch zusätzliche _Nodes_ erweitert werden, eine große und aktive Community hat Stand Heute bereits weit über 1000 Nodes entwickelt die unterschiedlichste Anwendungsfälle abdecken und diverse Services und Systeme an Node-RED anbinden.

* [Verzeichnis aller verfügbarer Nodes auf nodered.org](https://flows.nodered.org/?type=node&num_pages=1)
* [Erfolgreich auf RedMatic getestete Nodes (bitte ergänzen!)](Erfolgreich-getestete-Nodes)

## Hinweise

* Zur Sicherheit vor dem Installieren zusätzlicher Nodes ein **CCU Backup anlegen!**
* Fehlerhafte Nodes können im schlimmsten Fall zum Node-RED Absturz direkt beim Start führen, falls dieses Problem auftritt kann man diese im [Safe Mode](safe-mode) wieder entfernen.
* Falls der Safe mode nicht die erwarteten Ergebnisse liefert und die Node eine Standard Node ist, die über die Palette installiert wurde, kann man versuchen diese Node per Hand zu entfernen. Dazu zuerst einen Backup machen! und sich dann bewusst sein, dass es sich hier um einen sehr kritischen Eingriff in das CCU System handelt.
  * ssh einzuloggen unter root
  * `mount -o remount,rw /`
  * `cd /usr/local/addons/redmatic/var`
  * `npm uninstall node-red-contrib-hue` alternativ einfach eine alte Version installieren
  * `mount -o remount,ro /` am besten auch noch ein reboot. 

## Installation via Node-RED Palette Manager

![](images/node-install-1.png)

![](images/node-install-2.png)

## Installation via npm auf der Kommandozeile

```
source /usr/local/addons/redmatic/home/.profile
cd /usr/local/addons/redmatic/var
npm install --save --no-package-lock --global-style --save-prefix="~" --production <paket-name>
```

## Nodes mit Binärmodulen

Nicht alle Nodes lassen sich über den Palette Manager bzw. per npm installieren. Es gibt Nodes die bei der Installation Binärmodule compilieren müssen, dies ist auf der CCU bzw. RaspberryMatic nicht praktikabel machbar (Buildroot ist nicht dafür vorgesehen die dafür notwendigen Tools wie z.B. gcc zu installieren). Dies betrifft u.A. Nodes die Zugriff auf Hardware (z.B. Bluetooth) benötigen. 

Erkennbar ist das daran wenn bei einem Installationsversuch im Log folgende Fehlermeldungen erscheinen:

```
gyp ERR! configure error
gyp ERR! stack Error: Can't find Python executable "python", you can set the PYTHON env variable.
gyp ERR! stack at PythonFinder.failNoPython 
```

Um dieses Problem zu lösen bringt RedMatic noch eine weitere eigene Paketverwaltung mit (im RedMatic UI, Tab "Packages"). Falls der Wunsch besteht bestimmte Nodes mit Binärmodulen zu nutzen die in der RedMatic Paketverwaltung noch nicht vorhanden sind bitte einen [Issue](https://github.com/rdmtc/RedMatic/issues) anlegen.

### Installation via RedMatic Package Manager

1.  RedMatic UI aufrufen: 
![image](https://user-images.githubusercontent.com/12692680/54923090-ce8a9780-4f09-11e9-8219-86ce56e4f716.png)

2. Menüpunkt "Packages" aufrufen:
![image](https://user-images.githubusercontent.com/12692680/54923099-d1858800-4f09-11e9-8ce0-2402a2bced6f.png)

3. Pakete installieren / deinstallieren:
![image](https://user-images.githubusercontent.com/12692680/54923104-d5b1a580-4f09-11e9-8668-22509a30ec3a.png)





## Kommentar: Wie kann ich die Qualität von Node-RED Nodes beurteilen?

> > V 0.0.1 (sagt vielleicht schon alles?).
>
> Mja, Node-RED krankt (wie imho auch andere Smart Home Software oder generell Open Source Frameworks mit Plugin-Konzept) an der sehr unterschiedlichen Qualität der Plugins/Adapter/Bindings/Nodes/Treiber/... Die Bandbreite reicht von "ohne Doku hingeworfen, keinerlei Support, keine Updates" bis zu "Super getestet, ausführlichst dokumentiert, spitzen Support, regelmäßige Updates" ;-)
>
> Als Tipp um die Qualität von sowas zu beurteilen würde ich raten: Github Seite anschauen. Das Projekt sollte schon ein gewisses Alter haben, der letzte Commit sollte aber auch nicht allzu lange her sein, Issue Tracker anschauen - wird anständig supportet - wird auf Issues reagiert und wie lange lässt sich der Entwickler dafür Zeit? Wird es überhaupt von einer Nennenswerten Anzahl Usern benutzt (Github Issues, Github Sternchen, Download Counter auf flows.nodered.org)? Gibt/gab es Pull Requests (sprich: beteiligen sich Leute am Projekt oder ist es eine 1-Man-Show)?, gibt es eine ordentliche Doku/Readme? Auch ein guter Hinweis auf die Aktivität des Entwicklers ist seine Github-Profilseite, da gibts es diese Grafik mit den grünen Kästchen von der Du ablesen kannst wie aktiv der Entwickler insgesamt auf Github war/ist und auch ein Blick auf seine evtl. anderen Projekte schadet nicht.
>
> Auch ganz praktisch: https://npms.io/ scannt alle Node-Module (auch alle Node-RED Nodes sind da zu finden) und erstellt 3 Bewertungen: Popularität, Qualität und Maintenance, was dort angezeigt wird ist meistens recht treffend, jedenfalls was Qualität und Maintenance angeht, Popularität ist bei so Smart Home Sachen meistens sehr niedrig und daher eher weniger aussagekräftig.

(ursprünglich aus https://homematic-forum.de/forum/viewtopic.php?f=41&t=43508&p=446462#p446462)
