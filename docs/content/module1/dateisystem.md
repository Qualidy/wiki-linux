

#  Dateisystem-Hierarchie in Linux 


##  Einführung: Das Systemdenken verstehen

###  Was ist das Problem?
Anders als in Windows (wo man oft mit C:/, D:/ arbeitet) oder macOS (das eigene `/Users` Schema hat), folgt Linux einem strengen, universellen Prinzip: Der **Dateisystem-Hierarchie-Standard **.

*   **Das Prinzip:** Alle Dateien und Programme, egal ob es um einen Kernel, ein Log oder ein Nutzerdokument geht, werden unter einem einzigen, logischen Root-Verzeichnis (**`/`**) organisiert.
*   **Der absolute Pfad:** Ein absoluter Pfad beginnt *immer* mit einem Schrägstrich (`/`). Dies ist der Ausgangspunkt der gesamten Hierarchie.

###  Wie navigiere ich?
Der beste Weg, dieses Wissen zu festigen, ist das aktive Befehlszeilen-Training:
*   `pwd` (Print Working Directory): Wo bin ich gerade?
*   `ls`: Was gibt es hier?
*   `man` (Manual): Dokumentation nachschlagen.
*   `tree`: (Falls verfügbar) Die gesamte Struktur visualisieren.


##  I. Die Hauptbereiche (Der Überblick)

Wir unterteilen das System in logische Blöcke, nach ihrem Zweck.

###  1. Das System-Verzeichnis (`/`)
Das Root-Verzeichnis selbst. Alles beginnt hier.

###  2. Konfiguration und Programme
Dieser Block beinhaltet alle Dateien, die das System zum Laufen bringen.

| Verzeichnis | Zweck | Was finde ich hier? | Zusammenfassend |
| :--- | :--- | :--- | :--- |
| **`/etc`** | **Konfiguration:** Hier wird das "Gehirn" des Systems gespeichert. | Konfigurationsdateien (z. B. `ssh/sshd_config`, `apache2/httpd.conf`). | **Wichtigkeit:** Hier wird festgelegt, *wie* das System läuft. Änderungen müssen hier vorgenommen werden. |
| **`/bin`** | **Binaries (Binärdateien):** Allgemeine Programme, die *alle* Benutzer benötigen. | Programme wie `ls`, `cp`, `mv`. | **Merke:** Die grundlegendsten, universal benötigten Befehle. |
| **`/sbin`** | **System Binaries:** Programme, die *nur* von Root/Administratoren benötigt werden. | Programme wie `ifconfig` (Netzwerk-Tools), `ip` (System-Setup). | **Merke:** Wenn es mit der *Verwaltung* zu tun hat, ist es wahrscheinlich hier. |
| **`/usr`** | **User System Resources:** Programme und Bibliotheken für Nutzer, aber nicht zwingend notwendig für den Start. | Viele Applikationen und Dokumentationen. | **Merke:** Der größte Ablageort für "nice to have" Programme. |

###  3. Benutzer- und Datenmanagement
Hier wird geklärt, wer was tun darf.

| Verzeichnis | Zweck | Beispielinhalt | Zusammenfassend |
| :--- | :--- | :--- | :--- |
| **`/home`** | **Benutzerdaten:** Der private Bereich des Endbenutzers. | `/home/MaxMeier`, `/home/LauraB`. | **Schlüsselbotschaft:** Hier gehört das, was der Benutzer *selbst* erstellt hat (Dokumente, Bilder, persönliche Skripte). |
| **`/root`** | **Root-Benutzerdaten:** Das Verzeichnis für den Superuser (Administrator). | Private Konfigurationen und Daten des Systemadmins. | **Sicherheitsaspekt:** Dieses Verzeichnis ist extrem geschützt. |
| **`/var`** | **Variable Daten:** Daten, die sich ständig ändern oder wachsen. | `log` (Systemprotokolle), `spool` (Mail-Queue), `cache`. | **Verständnis:** Wenn eine Datei wächst (z. B. Logfiles), landet sie hier. |

###  4. Systemzustand und Laufzeit (Temporär)
Diese Verzeichnisse zeigen, wie das System "at the moment" arbeitet.

| Verzeichnis | Zweck | Bedeutung | Zusammenfassend |
| :--- | :--- | :--- | :--- |
| **`/tmp`** | **Temporäres:** Speicher für Programme während der aktuellen Sitzung. | Dateien, die nach einem Neustart gelöscht werden dürfen. | **Verhalten:** Hier dürfen Programme Daten ablegen, die nicht persistent sind. |
| **`/boot`** | **Bootloader:** Speichert die Kernel-Images und die Konfiguration, die zum Starten des OS notwendig sind. | Kernel-Dateien (z. B. `vmlinuz`), Boot-Konfigurationsdateien. | **Wichtigkeit:** Ohne die richtigen Dateien hier, starte das System nicht! |
| **`/dev`** | **Device:** Virtuelle Dateien, die Hardware-Geräte repräsentieren. | `/dev/sda` (erste Festplatte), `/dev/tty` (Terminal). | **Paradox:** Ein Gerät wird als *Datei* behandelt. Dies ist ein zentrales Konzept. |
| **`/proc`** | **Prozess:** Ein virtuelles Dateisystem, das Informationen über alle laufenden Prozesse bereitstellt. | `/proc/cpuinfo` (CPU-Info), `/proc/meminfo` (RAM-Info). | **Fortgeschritten:** Es gibt hier keine echten Dateien, sondern das Betriebssystem liest hier aktuelle Systemwerte. |


##  III. Zusammenfassende Übersicht 


| Verzeichnis | Zweck | Was ist dort? | Beispiel-Anwendungsfall |
| :--- | :--- | :--- | :--- |
| **`/`** | Der globale Root-Anfangspunkt. | Alles. | *Alle Pfade beginnen hier.* |
| **`/etc`** | Konfiguration. | `.conf`-Dateien. | Ich muss den SSH-Dienst neu konfigurieren. |
| **`/home`** | Benutzerdaten. | Dokumente, Bilder, Skripte des Nutzers. | Ich öffne mein persönliches Arbeitsverzeichnis. |
| **`/var`** | Veränderliche Daten. | Logs, Caches, Queues. | Ich lese die Systemprotokolle der letzten Nacht. |
| **`/tmp`** | Temporäre Daten. | Hilfsprogramme, temporäre Dateien. | Ein Programm erstellt kurz eine Datei zur Zwischenspeicherung. |
| **`/dev`** | Hardware-Abstraktion. | Geräte-Dateien. | Ein Programm muss mit dem USB-Stick kommunizieren. |

***
