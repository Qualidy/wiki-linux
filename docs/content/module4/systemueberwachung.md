
### **Modul IV: Systemadministration und Sicherheit**
### **Thema: Systemüberwachung und Protokollierung**

---

#### **1. Einführung in Systemüberwachung und Protokollierung**
Die **Systemüberwachung** und **Protokollierung (Logging)** sind essenziell, um:
- **Systemzustand** zu überwachen (CPU, Speicher, Festplatten, Netzwerk).
- **Fehler und Probleme** zu identifizieren.
- **Sicherheitsvorfälle** zu erkennen und zu analysieren.
- **Leistungsengpässe** zu finden.

Linux bietet eine Vielzahl von Tools und Mechanismen, um diese Aufgaben zu erfüllen.

---

---

#### **2. Wichtige Protokolldateien und Verzeichnisse**
Linux speichert Protokolldateien (Logs) typischerweise im Verzeichnis **`/var/log/`**. Hier sind die wichtigsten Dateien:

| **Protokolldatei**          | **Beschreibung**                                                                 |
|-----------------------------|---------------------------------------------------------------------------------|
| `/var/log/syslog`           | Systemweite Protokolle (Allgemeine Systemmeldungen).                          |
| `/var/log/auth.log`         | Authentifizierungsprotokolle (Login-Versuche, SSH, sudo).                      |
| `/var/log/kern.log`         | Kernel-Protokolle (Hardware- und Treibermeldungen).                            |
| `/var/log/dmesg`            | Kernel-Nachrichten beim Systemstart.                                          |
| `/var/log/cron.log`         | Protokolle für Cron-Jobs.                                                       |
| `/var/log/mail.log`         | E-Mail-Server-Protokolle (z. B. Postfix, Sendmail).                            |
| `/var/log/apache2/`         | Protokolle für den Apache-Webserver (z. B. `access.log`, `error.log`).        |
| `/var/log/nginx/`           | Protokolle für den Nginx-Webserver.                                            |
| `/var/log/boot.log`         | Protokolle des Boot-Vorgangs.                                                   |
| `/var/log/dpkg.log`         | Protokolle für Paketinstallationen (Debian/Ubuntu).                            |
| `/var/log/yum.log`          | Protokolle für Paketinstallationen (RHEL/CentOS).                              |

---
#### **3. Protokolldateien anzeigen und analysieren**
##### **3.1 `cat`, `less` und `tail`**
- **`cat`**: Zeigt den gesamten Inhalt einer Datei an.
  ```bash
  cat /var/log/syslog
  ```
- **`less`**: Ermöglicht das Scrollen durch große Dateien.
  ```bash
  less /var/log/syslog
  ```
- **`tail`**: Zeigt die letzten Zeilen einer Datei an (nützlich für Echtzeit-Überwachung).
  ```bash
  tail /var/log/syslog
  ```
  **Echtzeit-Überwachung mit `-f` (follow):**
  ```bash
  tail -f /var/log/syslog
  ```

##### **3.2 `grep` für die Suche in Protokollen**
Mit `grep` können Sie nach bestimmten Mustern in Protokolldateien suchen.

**Beispiele:**

| Befehl | Beschreibung |
|--------|--------------|
| `grep "error" /var/log/syslog` | Sucht nach dem Wort "error" in `syslog`. |
| `grep -i "fail" /var/log/auth.log` | Sucht nach "fail" (groß-/kleinschreibung ignorieren). |
| `grep -n "ssh" /var/log/auth.log` | Zeigt Zeilennummern an, in denen "ssh" vorkommt. |
| `grep -A 5 -B 5 "connection refused" /var/log/syslog` | Zeigt 5 Zeilen **vor** und **nach** dem Suchbegriff an. |

##### **3.3 `journalctl` für Systemd-Protokolle**
Moderne Linux-Distributionen verwenden **`systemd`** und speichern Protokolle im **Binary Journal**. Mit `journalctl` können Sie diese Protokolle abrufen.

**Wichtige Optionen:**

| Befehl | Beschreibung |
|--------|--------------|
| `journalctl` | Zeigt alle Protokolle an. |
| `journalctl -u nginx` | Zeigt Protokolle für den Dienst `nginx`. |
| `journalctl -f` | Verfolgt Protokolle in Echtzeit. |
| `journalctl --since "2026-06-01"` | Zeigt Protokolle ab einem bestimmten Datum an. |
| `journalctl --until "2026-06-01 12:00"` | Zeigt Protokolle bis zu einem bestimmten Zeitpunkt an. |
| `journalctl -p err` | Zeigt nur Protokolle mit der Priorität **Error** an. |
| `journalctl -b` | Zeigt Protokolle seit dem letzten Systemstart an. |

**Prioritäten (Log Levels):**

| Priorität | Beschreibung |
|-----------|--------------|
| `0` (emerg) | System ist unbrauchbar. |
| `1` (alert) | Sofortige Aktion erforderlich. |
| `2` (crit) | Kritische Bedingungen. |
| `3` (err) | Fehlerbedingungen. |
| `4` (warning) | Warnungen. |
| `5` (notice) | Normale, aber wichtige Meldungen. |
| `6` (info) | Informative Meldungen. |
| `7` (debug) | Debug-Meldungen. |

---
#### **4. Systemüberwachung mit `top`, `htop` und `vmstat`**
##### **4.1 `top` – Echtzeit-Systemüberwachung**
`top` zeigt eine **Echtzeit-Übersicht** der laufenden Prozesse und der Systemauslastung.

**Beispielausgabe:**
```bash
top
```
- **`PID`**: Prozess-ID.
- **`USER`**: Benutzer, der den Prozess ausführt.
- **`%CPU`**: CPU-Auslastung des Prozesses.
- **`%MEM`**: Speichernutzung des Prozesses.
- **`COMMAND`**: Name des Prozesses.

**Nützliche Tastenkombinationen in `top`:**

| Taste | Beschreibung |
|-------|--------------|
| `q` | Beendet `top`. |
| `P` | Sortiert nach CPU-Auslastung. |
| `M` | Sortiert nach Speichernutzung. |
| `k` | Beendet einen Prozess (mit `PID` angeben). |
| `1` | Zeigt die Auslastung aller CPU-Kerne an. |

##### **4.2 `htop` – Interaktive Systemüberwachung**
`htop` ist eine **benutzerfreundlichere Alternative** zu `top` mit einer grafischen Oberfläche.

**Installation:**
```bash
sudo apt install htop  # Debian/Ubuntu
sudo yum install htop  # RHEL/CentOS
```
**Starten:**
```bash
htop
```
**Vorteile von `htop`:**
- Farbige Darstellung.
- Einfache Navigation mit den Pfeiltasten.
- Prozesse können direkt aus der Oberfläche beendet werden.

##### **4.3 `vmstat` – Virtueller Speicher und Systemleistung**
`vmstat` zeigt Informationen über **Prozesse, Speicher, Paging, Block-I/O, Traps und CPU-Aktivität** an.

**Beispiel:**
```bash
vmstat 1 5
```
- **`1`**: Aktualisierungsintervall in Sekunden.
- **`5`**: Anzahl der Ausgaben.

**Ausgabe:**

| Spalte | Beschreibung |
|--------|--------------|
| `r` | Anzahl der laufenden Prozesse. |
| `b` | Anzahl der blockierten Prozesse. |
| `swpd` | Ausgelagerter Speicher (Swap). |
| `free` | Freier physikalischer Speicher. |
| `buff` | Puffer-Speicher. |
| `cache` | Cache-Speicher. |
| `si` | Speicher, der pro Sekunde vom Swap eingelesen wird. |
| `so` | Speicher, der pro Sekunde in den Swap geschrieben wird. |
| `bi` | Blöcke, die pro Sekunde von einem Blockgerät eingelesen werden. |
| `bo` | Blöcke, die pro Sekunde auf ein Blockgerät geschrieben werden. |
| `in` | Anzahl der Interrupts pro Sekunde. |
| `cs` | Anzahl der Kontextwechsel pro Sekunde. |
| `us` | Zeitanteil, den die CPU im Benutzermodus verbringt. |
| `sy` | Zeitanteil, den die CPU im Kernel-Modus verbringt. |
| `id` | Zeitanteil, den die CPU im Leerlauf verbringt. |

---
#### **5. Netzwerküberwachung mit `netstat`, `ss` und `iftop`**
##### **5.1 `netstat` – Netzwerkverbindungen und Statistiken**
`netstat` zeigt **Netzwerkverbindungen, Routing-Tabellen und Interface-Statistiken** an.

**Wichtige Optionen:**

| Befehl | Beschreibung |
|--------|--------------|
| `netstat -tuln` | Zeigt alle **TCP- und UDP-Ports** an, die auf dem System geöffnet sind. |
| `netstat -r` | Zeigt die **Routing-Tabelle** an. |
| `netstat -i` | Zeigt **Netzwerk-Interface-Statistiken** an. |
| `netstat -s` | Zeigt **Netzwerk-Statistiken** (z. B. gesendete/empfangene Pakete). |

**Beispiel:**
```bash
netstat -tuln
```
- **`-t`**: Zeigt TCP-Ports an.
- **`-u`**: Zeigt UDP-Ports an.
- **`-l`**: Zeigt nur **listening** Ports an.
- **`-n`**: Zeigt IP-Adressen statt Hostnamen an.

##### **5.2 `ss` – Moderner Ersatz für `netstat`**
`ss` (Socket Statistics) ist ein **schnellerer und modernerer Ersatz** für `netstat`.

**Beispiele:**

| Befehl | Beschreibung |
|--------|--------------|
| `ss -tuln` | Zeigt alle TCP- und UDP-Ports an. |
| `ss -l` | Zeigt alle **listening** Ports an. |
| `ss -s` | Zeigt eine **Zusammenfassung** der Socket-Statistiken an. |

##### **5.3 `iftop` – Echtzeit-Netzwerkverkehr**
`iftop` zeigt den **Echtzeit-Netzwerkverkehr** pro Verbindung an.

**Installation:**
```bash
sudo apt install iftop  # Debian/Ubuntu
sudo yum install iftop  # RHEL/CentOS
```
**Starten:**
```bash
sudo iftop
```
**Ausgabe:**
- Zeigt **Quell- und Ziel-IP-Adressen** an.
- Zeigt **Datenübertragungsraten** (in KB/s, MB/s) an.
- Zeigt **Ports und Protokolle** an.

---
#### **6. Festplattenüberwachung mit `df`, `du` und `iostat`**
##### **6.1 `df` – Festplattenbelegung anzeigen**
`df` (Disk Free) zeigt die **Belegung von Festplatten und Partitionen** an.

**Beispiel:**
```bash
df -h
```
- **`-h`**: Zeigt die Größen in **menschlich lesbarer Form** (KB, MB, GB) an.

**Ausgabe:**

| Spalte | Beschreibung |
|--------|--------------|
| `Filesystem` | Dateisystem (z. B. `/dev/sda1`). |
| `Size` | Größe der Partition. |
| `Used` | Belegter Speicher. |
| `Avail` | Verfügbarer Speicher. |
| `Use%` | Auslastung in Prozent. |
| `Mounted on` | Einhängepunkt. |

##### **6.2 `du` – Verzeichnisgrößen anzeigen**
`du` (Disk Usage) zeigt die **Größe von Verzeichnissen und Dateien** an.

**Beispiele:**

| Befehl | Beschreibung |
|--------|--------------|
| `du -sh /home` | Zeigt die **Gesamtgröße** des `/home`-Verzeichnisses an. |
| `du -h --max-depth=1 /var` | Zeigt die Größen der **ersten Ebene** im `/var`-Verzeichnis an. |
| `du -ah /pfad` | Zeigt die Größen **aller Dateien und Verzeichnisse** an. |

##### **6.3 `iostat` – E/A-Statistiken (I/O)**
`iostat` zeigt **Eingabe-/Ausgabe-Statistiken (I/O)** für Festplatten und Partitionen an.

**Installation:**
```bash
sudo apt install sysstat  # Debian/Ubuntu
sudo yum install sysstat  # RHEL/CentOS
```
**Beispiel:**
```bash
iostat -x 1 3
```
- **`-x`**: Zeigt **erweiterte Statistiken** an.
- **`1`**: Aktualisierungsintervall in Sekunden.
- **`3`**: Anzahl der Ausgaben.

**Ausgabe:**

| Spalte | Beschreibung |
|--------|--------------|
| `Device` | Gerätename (z. B. `sda`). |
| `r/s` | Leseoperationen pro Sekunde. |
| `w/s` | Schreiboperationen pro Sekunde. |
| `rMB/s` | Gelesene Daten pro Sekunde (in MB). |
| `wMB/s` | Geschriebene Daten pro Sekunde (in MB). |
| `%util` | Auslastung der Festplatte in Prozent. |

---
#### **7. Log-Rotation mit `logrotate`**
Protokolldateien können sehr groß werden. **`logrotate`** hilft dabei, sie **automatisch zu rotieren, zu komprimieren und zu löschen**.

##### **7.1 `logrotate` konfigurieren**
Die Konfiguration von `logrotate` erfolgt in der Datei **`/etc/logrotate.conf`** und in den Dateien im Verzeichnis **`/etc/logrotate.d/`**.

**Beispielkonfiguration für `/var/log/syslog`:**
```bash
/var/log/syslog {
    daily           # Rotiert täglich
    missingok       # Ignoriert, wenn die Datei nicht existiert
    rotate 7        # Behält 7 rotierte Dateien
    compress        # Komprimiert die rotierten Dateien
    delaycompress   # Komprimiert nicht die aktuellste rotierte Datei
    notifempty      # Rotiert nicht, wenn die Datei leer ist
    create 0640 root adm  # Erstellt eine neue Datei mit diesen Berechtigungen
}
```

##### **7.2 `logrotate` manuell ausführen**
```bash
sudo logrotate -f /etc/logrotate.conf
```
- **`-f`**: Erzwingt die Rotation, auch wenn sie nicht fällig ist.

---
#### **8. Übungsaufgaben**
##### **Frage 1**
Wie können Sie die letzten 20 Zeilen der Datei `/var/log/syslog` in Echtzeit überwachen?

??? success "Antwort"
    ```bash
    tail -f -n 20 /var/log/syslog
    ```

---
##### **Frage 2**
Welcher Befehl zeigt alle geöffneten TCP-Ports auf Ihrem System an?

??? success "Antwort"
    ```bash
    ss -tuln
    ```
    oder
    ```bash
    netstat -tuln
    ```

---
##### **Frage 3**
Wie können Sie die CPU-Auslastung aller Prozesse in Echtzeit anzeigen?

??? success "Antwort"
    ```bash
    top
    ```
    oder
    ```bash
    htop
    ```

---
##### **Frage 4**
Welcher Befehl zeigt die Belegung aller Festplattenpartitionen in menschlich lesbarer Form an?

??? success "Antwort"
    ```bash
    df -h
    ```

---
##### **Frage 5**
Wie können Sie die Größe des `/var`-Verzeichnisses anzeigen, ohne Unterverzeichnisse zu durchsuchen?

??? success "Antwort"
    ```bash
    du -sh /var
    ```

---
##### **Frage 6**
Welcher Befehl zeigt die E/A-Statistiken (I/O) für alle Festplatten an?

??? success "Antwort"
    ```bash
    iostat -x
    ```

---
##### **Frage 7**
Wie können Sie die Protokolle des Dienstes `nginx` seit dem letzten Systemstart anzeigen?

??? success "Antwort"
    ```bash
    journalctl -u nginx -b
    ```

---
##### **Frage 8**
Wie können Sie eine Log-Rotation für `/var/log/auth.log` einrichten, die:
- **Wöchentlich** rotiert,
- **4 rotierte Dateien** behält,
- **Komprimiert** wird?

??? success "Antwort"
    Erstellen Sie eine Datei `/etc/logrotate.d/auth.log` mit folgendem Inhalt:
    ```bash
    /var/log/auth.log {
        weekly
        rotate 4
        compress
        missingok
        notifempty
        create 0640 root adm
    }
    ```

---
#### **9. Praktische Beispiele**
##### **Beispiel 1: Echtzeit-Überwachung von Systemprotokollen**
Überwachen Sie die **Authentifizierungsprotokolle** in Echtzeit, um verdächtige Login-Versuche zu erkennen:
```bash
tail -f /var/log/auth.log | grep "Failed password"
```

##### **Beispiel 2: Netzwerkverkehr analysieren**
Zeigen Sie die **Top 10 Netzwerkverbindungen** nach Datenverkehr an:
```bash
sudo iftop -n -N -P -T -t -s 10
```
- **`-n`**: Zeigt IP-Adressen statt Hostnamen an.
- **`-N`**: Zeigt Portnummern statt Dienstnamen an.
- **`-P`**: Zeigt Ports an.
- **`-T`**: Zeigt cumulative Totals an.
- **`-t`**: Textmodus (ohne Farbausgabe).
- **`-s 10`**: Zeigt die Top 10 Verbindungen an.

##### **Beispiel 3: Festplattenbelegung prüfen**
Prüfen Sie, welche Verzeichnisse im **Root-Dateisystem** am meisten Speicher verbrauchen:
```bash
sudo du -h --max-depth=1 / | sort -h
```
- **`sort -h`**: Sortiert die Ausgabe nach menschlich lesbaren Größen.

##### **Beispiel 4: Protokolle nach Fehlern durchsuchen**
Durchsuchen Sie die **Systemprotokolle** der letzten 24 Stunden nach Fehlern:
```bash
journalctl --since "24 hours ago" -p err
```

---
#### **10. Zusammenfassung der wichtigsten Befehle**

| **Kategorie**               | **Befehl**               | **Beschreibung**                                                                 |
|-----------------------------|--------------------------|---------------------------------------------------------------------------------|
| **Protokolle anzeigen**     | `cat /var/log/syslog`    | Zeigt den Inhalt von `syslog` an.                                               |
|                             | `less /var/log/auth.log` | Ermöglicht das Scrollen durch `auth.log`.                                       |
|                             | `tail -f /var/log/kern.log` | Verfolgt `kern.log` in Echtzeit.                                               |
|                             | `journalctl -u nginx`    | Zeigt Protokolle für den Dienst `nginx`.                                        |
| **Protokolle durchsuchen**  | `grep "error" /var/log/syslog` | Sucht nach "error" in `syslog`.                                               |
| **Systemüberwachung**       | `top`                    | Zeigt laufende Prozesse und Systemauslastung an.                               |
|                             | `htop`                   | Interaktive Systemüberwachung.                                                |
|                             | `vmstat 1 5`             | Zeigt Systemleistung (CPU, Speicher, I/O) an.                                  |
| **Netzwerküberwachung**     | `ss -tuln`               | Zeigt alle geöffneten TCP- und UDP-Ports an.                                   |
|                             | `netstat -r`             | Zeigt die Routing-Tabelle an.                                                   |
|                             | `iftop`                  | Zeigt Echtzeit-Netzwerkverkehr an.                                             |
| **Festplattenüberwachung**  | `df -h`                  | Zeigt Festplattenbelegung in menschlich lesbarer Form an.                       |
|                             | `du -sh /home`           | Zeigt die Größe des `/home`-Verzeichnisses an.                                 |
|                             | `iostat -x`              | Zeigt E/A-Statistiken für Festplatten an.                                      |
| **Log-Rotation**            | `logrotate -f /etc/logrotate.conf` | Erzwingt die Rotation der Protokolle.                                   |

---
#### **11. Häufige Fehler und Lösungen**

| **Problem** | **Ursache** | **Lösung** |
|-------------|-------------|------------|
| **`Permission denied` beim Lesen von `/var/log/syslog`** | Keine Leseberechtigung für die Datei. | `sudo` verwenden oder Benutzer zur Gruppe `adm` hinzufügen. |
| **`command not found` für `htop` oder `iftop`** | Tool ist nicht installiert. | `sudo apt install htop iftop` (Debian/Ubuntu) oder `sudo yum install htop iftop` (RHEL/CentOS). |
| **`journalctl` zeigt keine Protokolle an** | `systemd` ist nicht aktiv oder Protokolle sind deaktiviert. | Prüfen, ob `systemd` läuft: `systemctl status systemd-journald`. |
| **Festplatte ist voll, aber `df -h` zeigt freien Speicher an** | Gelöschte Dateien werden von laufenden Prozessen gehalten. | Prozesse identifizieren, die Dateien halten: `lsof +L1`. |
| **`logrotate` funktioniert nicht** | Falsche Konfiguration oder Berechtigungen. | Konfiguration prüfen: `logrotate -d /etc/logrotate.conf` (Debug-Modus). |

---
#### **12. Vertiefung: `rsyslog` und `syslog-ng`**
Für **fortgeschrittene Protokollierung** können Sie **`rsyslog`** oder **`syslog-ng`** verwenden, um Protokolle zu **filtern, weiterzuleiten und zu speichern**.

##### **12.1 `rsyslog` konfigurieren**
Die Hauptkonfigurationsdatei ist **`/etc/rsyslog.conf`**. Hier können Sie **Regeln für die Protokollierung** definieren.

**Beispiel: Protokolle in separate Dateien schreiben**
```bash
# /etc/rsyslog.conf
auth.*      /var/log/auth.log
kern.*      /var/log/kern.log
mail.*      /var/log/mail.log
```
- **`auth.*`**: Alle Authentifizierungsprotokolle.
- **`kern.*`**: Alle Kernel-Protokolle.
- **`mail.*`**: Alle E-Mail-Protokolle.

**Neustart von `rsyslog`:**
```bash
sudo systemctl restart rsyslog
```

##### **12.2 Protokolle an einen entfernten Server senden**
Um Protokolle an einen **zentralen Log-Server** zu senden, fügen Sie folgende Zeile zu `/etc/rsyslog.conf` hinzu:
```bash
*.* @192.168.1.100:514
```
- **`*.*`**: Alle Protokolle.
- **`@192.168.1.100:514`**: IP-Adresse und Port des Log-Servers.

