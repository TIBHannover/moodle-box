# moodle-box

Dieses Projekt bietet die Möglichkeit, ein moodle mit minimalem Aufwand in einer virtuellen Maschine aufzusetzen. Voraussetzung ist die Installation von
[Git](https://git-scm.com/downloads),  [Vagrant](https://www.vagrantup.com/downloads.html) und [VirtualBox](https://www.virtualbox.org/wiki/Downloads).

Außerdem kann die Moodle-Instanz mit einem edu-sharing Repositorium verbunden werden. Siehe hierfür [Edu-Sharing-Integration](#edu-sharing-integration).

## Installation

Soll die moodle-box mit edu-sharing verknüpft werden, dann in der Datei _group_vars/all.yml_ den Eintrag `install_edu_sharing_plugin` auf `true` setzen.

Die folgenden Schritte im Terminal (Linux/macOS) oder in der GitBash (Windows) ausführen.
```
git clone https://github.com/TIBHannover/moodle-box.git
cd moodle-box
vagrant up
```
Wenn die Installation durchgelaufen ist (einige Minuten, abhängig von der Download-Geschwindigkeit) kann moodle im Browser aufgerufen werden mit

<http://192.168.98.105>

Die Anmeldung an moodle erfolgt mit admin/asd456

Die Anmeldung an der VM via SSH erfolgt in diesem Beispiel noch vereinfacht und ohne Passwort mit dem Benutzer "vagrant". Der Benutzer hat das sudo-Recht.
```
vagrant ssh
```

## Moodle Mobile App Zugriff aktivieren

* Einloggen als Administrator
* Website-Administration > Mobile App > Mobile Einstellungen > Webservice für mobile Endgeräte aktivieren

## Edu-Sharing-Integration

- zunächst Edu-Sharing-Box wie in [Installation](https://github.com/TIBHannover/edu-sharing-box) geschildert installieren
- falls die Moodle-Box bereits installiert wurde, in _group_vars/all.yml_ den Eintrag `install_edu_sharing_plugin` auf `true` setzen, damit die nötigen Plugins installiert werden können
- die Edu-Sharing Version in _group_vars/all.yml_ `edu_sharing_version` ggf. entsprechend anpassen
- im moodle-box Verzeichnis den Befehl `vagrant reload --provision` ausführen
- anschließend in der Datei _group_vars/edusharing.yml_ der Edu-Sharing-Box den Eintrag `register_moodle` auf `true` setzen
- im edu-sharing-box-Verzeichnis den Befehl `vagrant reload --provision`ausführen
- nun sollte in moodle eine Einbindung des edu-sharing Repositoriums erfolgt sein
