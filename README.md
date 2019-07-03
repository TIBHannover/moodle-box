# moodle-box

Dieses Projekt bietet die Möglichkeit, ein moodle mit minimalem Aufwand in einer virtuellen Maschine aufzusetzen. Voraussetzung ist die Installation von
[Git](https://git-scm.com/downloads),  [Vagrant](https://www.vagrantup.com/downloads.html) und [VirtualBox](https://www.virtualbox.org/wiki/Downloads).

## Installation

Soll die moodle-box mit edu-sharing verknüpft werden, dann im Vagrantfile den Eintrag "ansible.skip_tags = [ "edu-sharing-plugin" ]" entfernen/einkommentieren.

Die folgenden Schritte im Terminal (Linux/macOS) oder in der GitBash (Windows) ausführen.
```
git clone https://git.tib.eu/boxes/moodle-box.git
cd moodle-box
vagrant up
```
Wenn die Installation durchgelaufen ist (einige Minuten, abhängig von der Download-Geschwindigkeit) kann moodle im Browser aufgerufen werden mit

<http://192.168.98.105>

Die Anmeldung an moodle erfolgt mit admin/asd456

Wurde die edu-sharing Verknüpfung aktiviert, dann muss die Installation des edu-sharing-Plugins noch manuell abgeschlossen werden - [siehe unten](#verknüpfung-mit-edu-sharing)

Die Anmeldung an der VM via SSH erfolgt in diesem Beispiel noch vereinfacht und ohne Passwort mit dem Benutzer "vagrant". Der Benutzer hat das sudo-Recht.
```
vagrant ssh
```

## Verknüpfung mit edu-sharing

* Der edu-sharing-plugin Task wird ausgeführt, wenn im Vagrantfile der Eintrag "ansible.skip_tags = [ "edu-sharing-plugin" ]" entfernt/einkommentiert ist.
* Wurde bei der Installation der edu-sharing-plugin Task ausgeführt, dann wurde das edu-sharing-plugin bereits ins Moodle kopiert und muss nun noch manuell eingerichtet werden.
* Moodle-installation
    * Einloggen in Moodle als Administrator
    * http://<moodle\_host>/admin aufrufen und die Installation der Plugins abschließen.
        * Alle Dialoge nur bestätigen; Felder leer/auf Standard-Wert belassen.
    * http://<moodle\_host>/mod/edusharing/import\_metadata.php aufrufen und edu-sharing Repo eintragen:
    ```
    http://<edu-sharing-host>/edu-sharing/metadata?format=lms
    ```
    * Filter aktivieren: "Site administration"  > Plugins  > Filters  > Manage filters. => edu-sharing-Filter aktivieren und priorisieren
    * Texteditor aktivieren: "Site administration" > Plugins  > Text editors  > Manage editors. => edu-sharing-editor aktivieren und priorisieren
* Edu-Sharing-Installation
    * Einloggen in edu-sharing als Administrator
    * Admin-Tools > Applications
        * Moodle anbinden indem folgende URL eingetragen wird:
        ```
        http://<moodle_host>/mod/edusharing/metadata.php
        ```
