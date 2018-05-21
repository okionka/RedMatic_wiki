# Zusätzliche Node-RED Nodes installieren

https://flows.nodered.org


## Via Node-RED Admin UI

![](images/node-install-1.png)

![](images/node-install-2.png)


## Via Command Line

`/usr/local/addons/node-red/bin/npm install <paket-name>`


## Hinweis 

Nicht alle Nodes lassen sich auf einer CCU installieren. Es gibt Nodes die bei der Installation Binärmodule compilieren 
müssen, dies ist auf der CCU bzw. RaspberryMatic nicht praktikabel machbar (Buildroot ist nicht dafür vorgesehen die 
dafür notwendigen Tools wie z.B. gcc zu installieren). Dies betrifft u.A. Nodes die Zugriff auf Hardware (z.B. 
Bluetooth) benötigen. Falls der Wunsch besteht bestimmte Nodes zu nutzen die sich nicht installieren lassen kann gerne 
ein [https://github.com/hobbyquaker/ccu-addon-node-red/issues](Issue) angelegt werden, es ist dann u.U. möglich die 
Nodes mit vorab gebauten Binärmodulen mit in das CCU Addon Paket aufzunehmen.

