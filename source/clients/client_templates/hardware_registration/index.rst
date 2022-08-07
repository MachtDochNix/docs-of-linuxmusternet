.. include:: ../../../guided-inst.subst

.. _hardware-registration-label:

===============
Rechneraufnahme
===============

.. sectionauthor:: `@cweikl <https://ask.linuxmuster.net/u/cweikl>`_,
                   `@Alois <https://ask.linuxmuster.net/u/Alois>`_ ,
	               `@Tobias <https://ask.linuxmuster.net/u/Tobias>`_,
                   `@michael_kohls <https://ask.linuxmuster.net/u/michael_kohls>`_

Der PC, der als Hardware zum Aufbau des Muster-Clients genutzt werden soll, ist via Kabel mit dem Netzwerk zu verbinden.

Alternativ kann für den Aufbau des Muster-Clients eine VM in der Virtualisierungsumgebung angelegt werden.

Nachstehende Angaben stellen ein Beispiel für die Rahmendaten einer solchen VM dar:

 * 4 GiB vRAM
 * mind. 1 vCPU mit 2 Kernen
 * VGA mit 16 MiB Speicher
 * 1x vNIC (ggf. im "richtigen" VLAN)
 * PXE-Boot einstellen (Bootreihenfolge: NIC first)
 * Boot Firmware: BIOS oder UEFI (je nach später genutzten PCs) - Achtung: start.conf von linbo ggf. anpassen -> siehe Hinweise bei den Client-Systemen
 * z.B. 50 GiB HDD (20 GiB OS + 20 GiB Cache + ggf. SWAP oder andere Partitionen)

... mit der WebUI
=================

Um einen Rechner mit der Schulkonsole aufzunehmen, meldest Du Dich zunächst an der Schulkonsole als ``global-admin`` an.

Wähle dann links im Menü ``Geräteverwaltung --> Geräte``.

.. figure:: media/add-devices/01-device-management-devices-menue.png
   :align: center
   :alt: Device Management: Menue

Danach siehst Du rechts die Liste mit allen bereits in der Gerätedatei eingetragenen Geräten. Standardmäßig sind nach dem Setup die konfigurierten Server
schon in der Liste mit der Rolle ``Server`` eingetragen.

.. figure:: media/add-devices/02-device-management-devices.png
   :align: center
   :alt: Device Management: Devices

Klicke unterhalb der Liste auf den Button ``+ Gerät hinzufügen``, um ein neues Gerät einzutragen. Es wird eine neue, noch leere Zeile am Ende der Geräteliste eingefügt.

.. figure:: media/add-devices/03-device-management-add-new-device.png
   :align: center
   :alt: Device Management: Add New Device

In der neuen Zeile gibst Du nun folgenes an:

1. Raum: Name des Raums (Achtung: keine Binde- und Unterstriche verwenden, keine Umlaute,  max. 10 Zeichen)
2. Hostname: Name des Geräts (Erlaubte Zeichen ``a-z`` ``A-Z`` ``0-9`` ``-``; Achtung: Keine Unterstriche verwenden; max. 15 Zeichen)
3. Gruppe: Bezeichnung der Linbo-Hardwareklasse. ``Gleiche Bezeichnungen für Raum und Gruppe sind unzulässig``. Reservierte Wörter, wie "con" und "man", dürfen nicht verwendet werden.
4. MAC: Media Access Control - Hardware-Adresse des Netzwerkadapters. Trage 12 Hexadezimalzahlen mit einem Doppelpunkt als Trennzeichen nach zwei Ziffern ein.
5. IP: Gebe eine IP-Adresse für das Gerät an, das diesem automatisch zugewiesen werden soll. Z.B. Raum 202 im Gebäude G erhält den Bereich 10.0.202.x/16 und PC01 erhält die UP 10.0.202.1
6. Sophomorix-Rolle: Hier gibst Du an, welche Art von Gerät Du einbindest. Für PCs im Fachraum gibst Du z.B. Schüler-PC im Klassenzimmer an.
7. PXE: Lege über das Drop-down Menü fest, ob der PC mit Linbo-PXE synchronisiert werden soll oder nicht.

.. hint::

   Die Bedeutung der Sophomorix-Rolle wird auf `Github <https://github.com/linuxmuster/sophomorix4/wiki/objectClasses>`_ beschrieben.

Die o.g. Zeile könnte ausgefüllt wie folgt aussehen:

.. figure:: media/add-devices/04-device-management-add-new-device-settings.png
   :align: center
   :alt: Device Management: Add New Device Settings

Die Schaltfläche ``SPEICHERN`` überprüft die Eingabe, ``SPEICHERN & IMPORTIEREN`` werden die neuen Geräte importiert. Mit dem Button ``Im Editor öffnen`` wird die Datei ``/etc/linuxmuster/sophomorix/default-school/devices.csv`` im Editor geöffnet und kann bearbeitet werden.

.. figure:: media/add-devices/05-device-management-buttons.png
   :align: center
   :alt: Device Management: Add New Devices - Buttons

Im folgenden erscheinen einige Log-Meldungen und - wenn der Import erfolgreich war - "Import abgeschlossen"

.. figure:: media/add-devices/06-device-management-add-new-devices-import-finished.png
   :align: center
   :alt: Device Management: Import finished

Um weitere Geräte hinzuzufügen, wiederholst Du den beschriebenen Vorgang in der Schulkonsole entsprechend.

.. hint::

   Sind nun die gewünschten Geräte aufgenommen, kannst Du mit ...
    
    ... der Erstellung eines Muster-Clients fortfahren, so dass alle PCs einer Linbo Hardwareklasse ein identisches Image erhalten. Gehe zu :ref:`client-templates-label`

    ... dem Verteilen eines vorhandenen Images auf die aufgenommenen Geräte beginnen. Gehe zu :ref:`using-linbo-label` 

   .. todo Ziel im letzten Aufzählungspunkt muss angepasst werden.

... mittels der Datei devices.csv
=================================

Wenn Du sehr viele Geräte hinzufügen möchtest, deren MAC-Adressen Du bereits kennst, dann ist die o.g. Option ``Im Editor öffnen`` eine Möglichkeit, die Datei devices.csv direkt zu editieren.

.. figure:: media/add-devices/07-device-management-edit-file.png
   :align: center
   :alt: Device Management: Edit file

Die Datei kann hier auch zur lokalen Bearbeitung heruntergeladen und wieder hochgeladen werden.

.. hint:: 

  Es sind nun die gewünschten Geräte aufgenommen und Du kannst mit ...
    
  ... der Erstellung eines Muster-Clients fortfahren, so dass alle PCs einer Linbo Hardwareklasse ein identisches Image erhalten. Gehe zu :ref:`client-templates-label`

  ... dem Verteilen eines vorhandenen Images auf die aufgenommenen Geräte beginnen. Gehe zu :ref:`using-linbo-label` 

  .. todo Ziel im letzten Aufzählungspunkt muss angepasst werden.

... mittles LINBO
=================

Wurde z.B. ein neuer Schulungsraum mit 20 PCs ausgestattet, deren MAC-Adressen Du nicht kennst, dann bietet sich diese Möglichkeit an. 

Dazu hat sich folgendes Vorgehen bewährt:

1. Der Clientrechner muss mit dem Schulnetzwerk verbunden sein und den Server erreichen können.
2. Um LINBO zu starten, den PC über das Netzwerk booten (PXE). Dazu entweder im BIOS-Setup in der Bootreihenfolge PXE-Boot als erstes Bootmedium einstellen oder über das Bootmenü PXE-Boot auswählen. Dies gelingt je nach Rechner meistens über die Tasten F2, F10 oder F12. Als virtueller Rechner auf einem Hypervisor unter ``VMxyz --> Options --> Bootorder`` ist hier die Netzwerkkarte als erstes Boot-Medium zu wählen.

.. ..todo:: Kommtierte Alte Einträge Sind Zu Entfernen!!!
.. 3. In der Schulkonsole unter ``Geräteverwaltung --> LINBO 4`` auswählen.
.. 
.. .. figure:: media/add-devices/08-device-management-linbo4-menue.png
..    :align: center
..    :alt: Device Management: Linbo 4 Menue
.. 
.. 4. Es erscheint rechts eine Liste mit den bereits eingerichteten Gruppen (Linbo-Hardwareklassen). Zu Beginn ist diese noch leer.
.. 
.. .. figure:: media/add-devices/09-device-management-linbo4-groups.png
..    :align: center
..    :alt: Device Management: Linbo 4 Groups
.. 
.. 5. Klicke nun unten auf den Button ``+Erstellen``. Es erscheinen nun die Einträge des Drop-down Menüs. Wähle nun eine gewünschte Konfigurationsvorlage für die neu einzubindenden Geräte aus. Willst Du z.B. die neuen Geräte mit UEFI-Boot und Ubutnu 20.4 LTS betreiben, dann wähle den Eintrag ``start.conf.ubuntu20-efi``.
.. 
.. .. figure:: media/add-devices/10-device-management-linbo4-group-config.png
..    :align: center
..    :alt: Device Management: Linbo 4 Group Config File
.. 
.. 6. Gebe einen Namen für die neue Gruppe an, z.B. ubu20efi
.. 
.. .. figure:: media/add-devices/11-device-management-linbo4-group-name.png
..    :align: center
..    :alt: Device Management: Linbo 4 Group Name
.. 
.. 7. Hast Du den Namen bestätigt wird der Import gestartet, nach Abschluss ist die neue Gruppe nun verfügbar.
.. 
.. .. figure:: media/add-devices/12-device-management-linbo4-group-add-finsihed.png
..    :align: center
..    :alt: Device Management: Linbo 4 Groups Import finished
.. 
.. 8. Nach Abschluss siehst Du die neue Gruppe in der Übersicht und kannst mit dem Stift-Symbol die Einträge anpassen.
.. 
.. .. figure:: media/add-devices/13-device-management-linbo4-group-new-overview.png
..    :align: center
..    :alt: Device Management: Linbo 4 Groups: Overview
.. 
.. 9. Hast Du für die neue Gruppe den Stift geklickt, siehst Du die Konfigurationseinstellungen für die Hardwareklasse. Klicke auf die Reiterkarte ``Partitionen`` und Du siehst die Einstellungen für die Partitionsgrössen, die für Deine neu einzubindenden PCs ggf. anzupassen sind.
.. 
.. .. figure:: media/add-devices/14-device-management-linbo4-group-partitions.png
..    :align: center
..    :alt: Device Management: Linbo 4 Groups: Partitions
.. 
.. 10. Hast Du die Partitionen angepasst und ``Speichern`` geklickt, wird erneut ein Import ausgeführt.
.. 11. Hast Du alle einzubindenden PCs im BIOS auf PXE - Boot und für o.g. Beispiel auf UEFI eingestellt, dann starte diese, so dass Linbo4 gebootet wird.
.. 12. Es sollte bei einem erfolgreichen Boot-vorgang via PXE mit Linbo folgender Startbildschirm zu sehen sein:
.. 
.. 13. Folgende Ansicht sollte erscheinen.

3. Es sollte bei einem erfolgreichen Bootvorgang via PXE folgender Startbildschirm zu sehen sein:

.. figure:: media/add-devices/15-device-management-linbo4-bootscreen.png
   :align: center
   :alt: Device Management: Linbo 4 - bootscreen

4. Wähle in dem Linbo Startbildschirm nun rechts das werkzeug-Symvol aus. Es erscheint die Kennwortabfrage. Gebe das Kennwort des Linbo-Root-Benutzers an, wie es beim Setup erstellt wurde.
  
.. attention:: Deine Eingabe ist nicht zu sehen, es werden auch keine Sternchen für die eingegebenen Ziffern dargestellt.

.. figure:: media/add-devices/16-device-management-linbo4-password.png
   :align: center
   :alt: Device Management: Linbo 4 - password

5. Es werden nun zwei weitere Menü-Symbole dargestellt:

.. figure:: media/add-devices/17-device-management-linbo4-new-menue-symbols.png
   :align: center
   :alt: Device Management: Linbo 4 - new menue symbols

6. Wähle den Eintrag ``Register`` aus.
7. Es öffnet sich ein Fenster, um den Client zu registrieren. Fülle alle Felder aus. Achte darauf, dass Du als Host group die zuvor neu angelegte einträgst.

.. figure:: media/add-devices/18-device-management-linbo4-register-client.png
   :align: center
   :alt: Device Management: Linbo 4 - register client

8. Klicke dann auf den Eintrag ``register``. Nach Abschluss der Neuaufnahme siehst Du nachstehende Meldung:

.. figure:: media/add-devices/19-device-management-linbo4-registering-client-finished.png
   :align: center
   :alt: Device Management: Linbo 4 - registering client finished

9. führe o.g. Vorgang für alle neu aufzunehmenden Clients durch.
10. Wenn alle PCs so registriert wurden, öffne an Deinem Administrations-Rechner die Schulkonsole und melde Dich wieder als ``global-admin`` an. Wähle im Menü ``Geräteverwwaltung --> Geräte`` aus. Du siehst nun neben den schon vorhandenen Geräten ebenfalls die neu aufgenommen Geräte (in der Abb. sind dies die PCs für den Raum g202):

.. figure:: media/add-devices/20-device-management-linbo4-registered-clients.png
   :align: center
   :alt: Device Management: Linbo 4 - registered clients

11. Klicke nun auf ``Speichern & importieren``. Wurde der Vorgang abgeschlossen, siehst Du dies im Importfenster.

.. figure:: media/add-devices/21-device-management-linbo4-registered-clients-imported.png
   :align: center
   :alt: Device Management: Linbo 4 - registered clients imported

.. hint::

   Es sind nun die gewünschten Geräte aufgenommen und Du kannst mit ...
    
    ... der Erstellung eines Muster-Clients fortfahren, so dass alle PCs einer Linbo Hardwareklasse ein identisches Image erhalten. Gehe zu :ref:`client-templates-label`

    ... dem Verteilen eines vorhandenen Images auf die aufgenommenen Geräte beginnen. Gehe zu :ref:`using-linbo-label` 

   .. todo Ziel im letzten Aufzählungspunkt muss angepasst werden.

