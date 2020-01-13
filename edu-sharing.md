# Verknüpfung mit edu-sharing manuell

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
