

### **Modul IV: Systemadministration und Sicherheit**
### **Thema: Backup-Strategien und Wiederherstellung**

---

#### **1. Einführung in Backup-Strategien**
Backups sind ein **kritischer Bestandteil** der Systemadministration und Datenverwaltung. Sie schützen vor:
- **Datenverlust** (z. B. durch Hardwarefehler, menschliche Fehler oder Malware).
- **Systemausfällen** (z. B. durch Festplattencrash oder Stromausfall).
- **Sicherheitsvorfällen** (z. B. Ransomware-Angriffe).

Eine **gute Backup-Strategie** sollte folgende Prinzipien beachten:
1. **3-2-1-Regel**:
   - **3 Kopien** Ihrer Daten (Original + 2 Backups).
   - **2 verschiedene Medientypen** (z. B. Festplatte + Cloud).
   - **1 Backup außerhalb des Standorts** (z. B. Cloud oder externes Laufwerk).
2. **Automatisierung**: Backups sollten **automatisch** und regelmäßig durchgeführt werden.
3. **Testen**: Backups müssen **regelmäßig getestet** werden, um sicherzustellen, dass sie wiederhergestellt werden können.
4. **Dokumentation**: Backup-Prozesse und -Standorte sollten **dokumentiert** sein.

---


#### **2. Backup-Typen**    
Es gibt verschiedene **Backup-Typen**, die sich in **Umfang, Geschwindigkeit und Speicherbedarf** unterscheiden:

| **Backup-Typ** | **Beschreibung** | **Vorteile** | **Nachteile** |
|----------------|------------------|--------------|---------------|
| **Vollbackup (Full Backup)** | Sichert **alle ausgewählten Daten**. | Einfache Wiederherstellung, keine Abhängigkeiten. | Langsam, hoher Speicherbedarf. |
| **Differenzielles Backup** | Sichert **alle Änderungen seit dem letzten Vollbackup**. | Schneller als Vollbackup, weniger Speicherbedarf. | Wiederherstellung erfordert Vollbackup + differenzielles Backup. |
| **Inkrementelles Backup** | Sichert **nur die Änderungen seit dem letzten Backup (Voll- oder Inkrementell)**. | Sehr schnell, geringer Speicherbedarf. | Wiederherstellung erfordert alle Backups seit dem letzten Vollbackup. |
| **Snapshot-Backup** | Erstellt einen **Schnappschuss des Dateisystems** zu einem bestimmten Zeitpunkt. | Sehr schnell, minimaler Speicherbedarf (nur Änderungen). | Benötigt spezielle Dateisysteme (z. B. Btrfs, ZFS). |
| **Spiegelung (Mirroring)** | Erstellt eine **exakte Kopie** der Daten. | Einfache Wiederherstellung, Echtzeit-Synchronisation möglich. | Hoher Speicherbedarf, keine Versionierung. |

---

---

#### **3. Backup-Tools unter Linux**
Linux bietet eine Vielzahl von **Backup-Tools**, die für verschiedene Szenarien geeignet sind. Hier sind die wichtigsten:

| **Tool** | **Beschreibung** | **Backup-Typ** | **Vorteile** | **Nachteile** |
|----------|------------------|----------------|--------------|---------------|
| **`tar`** | Erstellt **Archive** von Dateien und Verzeichnissen. | Vollbackup | Einfach, in allen Linux-Distributionen verfügbar. | Keine Inkrementelle Backups, keine Kompression standardmäßig. |
| **`rsync`** | Synchronisiert **Dateien und Verzeichnisse** (lokal oder remote). | Spiegelung, Inkrementell (mit `--link-dest`) | Schnell, effizient, unterstützt Remote-Backups. | Keine native Versionierung, komplexere Konfiguration für Inkrementelle Backups. |
| **`dd`** | Erstellt **Bit-für-Bit-Kopien** von Festplatten oder Partitionen. | Vollbackup | Exakte Kopie, auch für Bootloader geeignet. | Langsam, hoher Speicherbedarf, keine Selektion einzelner Dateien. |
| **`BorgBackup`** | **Deduplizierendes Backup-Tool** mit Kompression und Verschlüsselung. | Vollbackup, Inkrementell | Deduplizierung, Kompression, Verschlüsselung, Versionierung. | Komplexere Einrichtung, höhere CPU-Last. |
| **`Duplicati`** | **Grafisches Backup-Tool** mit Cloud-Unterstützung. | Vollbackup, Inkrementell | Benutzerfreundlich, Cloud-Integration, Verschlüsselung. | Langsamer als CLI-Tools, höhere Ressourcenlast. |
| **`Bacula`** | **Enterprise-Backup-Lösung** für komplexe Umgebungen. | Vollbackup, Differenziell, Inkrementell | Skalierbar, zentralisierte Verwaltung, Unterstützung für verschiedene Speichermedien. | Komplexe Einrichtung, hohe Lernkurve. |
| **`Timeshift`** | **Snapshot-Backup-Tool** für Linux-Systeme. | Snapshot | Einfache Wiederherstellung des Systems, unterstützt Btrfs und Rsync. | Nur für System-Backups, nicht für einzelne Dateien. |
| **`Déjà Dup`** | **Einfaches Backup-Tool** mit grafischer Oberfläche. | Vollbackup, Inkrementell | Benutzerfreundlich, unterstützt Cloud-Speicher, Verschlüsselung. | Begrenzte Funktionen für fortgeschrittene Nutzer. |

---

---

#### **4. Backup mit `tar`**
`tar` (**Tape Archive**) ist ein **klassisches Tool** zum Erstellen von Archiven. Es unterstützt **Kompression** (z. B. mit `gzip` oder `bzip2`) und ist in **allen Linux-Distributionen** verfügbar.

---
##### **4.1 Grundlagen von `tar`**
| **Option** | **Beschreibung** |
|------------|------------------|
| `-c` | **Erstellt** ein neues Archiv. |
| `-x` | **Extrahiert** Dateien aus einem Archiv. |
| `-t` | **Listet** den Inhalt eines Archivs auf. |
| `-f [datei]` | Gibt den **Archivnamen** an. |
| `-v` | **Ausführliche Ausgabe** (verbose). |
| `-z` | Komprimiert das Archiv mit **`gzip`**. |
| `-j` | Komprimiert das Archiv mit **`bzip2`**. |
| `-J` | Komprimiert das Archiv mit **`xz`**. |
| `-p` | **Behält Berechtigungen** bei. |
| `-P` | **Behält absolute Pfade** bei (Vorsicht: Kann Probleme bei der Wiederherstellung verursachen!). |
| `--exclude=[muster]` | **Schließt Dateien** aus, die dem Muster entsprechen. |

---
##### **4.2 Beispiele für `tar`**
###### **4.2.1 Vollbackup eines Verzeichnisses erstellen**
```bash
# Erstellen eines unkomprimierten tar-Archivs
tar -cvf backup.tar /pfad/zum/verzeichnis

# Erstellen eines komprimierten tar.gz-Archivs (gzip)
tar -czvf backup.tar.gz /pfad/zum/verzeichnis

# Erstellen eines komprimierten tar.bz2-Archivs (bzip2)
tar -cjvf backup.tar.bz2 /pfad/zum/verzeichnis

# Erstellen eines komprimierten tar.xz-Archivs (xz)
tar -cJvf backup.tar.xz /pfad/zum/verzeichnis
```

###### **4.2.2 Backup mit Ausschluss von Dateien**
```bash
# Ausschließen von temporären Dateien und Logs
tar -czvf backup.tar.gz --exclude='*.log' --exclude='/tmp/*' /pfad/zum/verzeichnis
```

###### **4.2.3 Backup eines gesamten Systems (ohne `/dev`, `/proc`, `/sys`, `/tmp`)**
```bash
sudo tar -czvf full_system_backup.tar.gz --exclude=/dev --exclude=/proc --exclude=/sys --exclude=/tmp --exclude=/mnt --exclude=/media /
```

###### **4.2.4 Archiv extrahieren**
```bash
# Extrahiere ein tar-Archiv
tar -xvf backup.tar

# Extrahiere ein tar.gz-Archiv
tar -xzvf backup.tar.gz

# Extrahiere ein tar.bz2-Archiv
tar -xjvf backup.tar.bz2

# Extrahiere ein tar.xz-Archiv
tar -xJvf backup.tar.xz
```

###### **4.2.5 Inkrementelles Backup mit `tar` (begrenzt)**
`tar` unterstützt **keine echten inkrementellen Backups**, aber Sie können **neuere Dateien** basierend auf dem **Änderungsdatum** sichern:
```bash
# Sichere nur Dateien, die in den letzten 24 Stunden geändert wurden
tar -czvf incremental_backup.tar.gz -N "2026-06-01" /pfad/zum/verzeichnis
```
- **`-N [datum]`**: Sichert nur Dateien, die **neuer als das angegebene Datum** sind.

---
---
#### **5. Backup mit `rsync`**
`rsync` (**Remote Sync**) ist ein **leistungsstarkes Tool** zum **Synchronisieren von Dateien und Verzeichnissen** (lokal oder remote). Es unterstützt:
- **Inkrementelle Backups** (nur Änderungen werden übertragen).
- **Kompression** während der Übertragung.
- **Remote-Backups** (über SSH).
- **Bandbreitenbegrenzung**.

---
##### **5.1 Grundlagen von `rsync`**
| **Option** | **Beschreibung** |
|------------|------------------|
| `-a` | **Archivmodus** (behält Berechtigungen, Eigentümer, Zeitstempel bei). |
| `-v` | **Ausführliche Ausgabe** (verbose). |
| `-z` | **Komprimiert** Daten während der Übertragung. |
| `-h` | Zeigt **menschlich lesbare Größen** an. |
| `--delete` | **Löscht Dateien** im Ziel, die nicht mehr in der Quelle existieren. |
| `--link-dest=[pfad]` | Erstellt **Hardlinks** zu unveränderten Dateien (für inkrementelle Backups). |
| `--exclude=[muster]` | **Schließt Dateien** aus, die dem Muster entsprechen. |
| `-P` | Zeigt **Fortschritt** an und setzt **teilweise Übertragungen** fort. |
| `-e ssh` | Verwendet **SSH** für die Übertragung. |

---
##### **5.2 Beispiele für `rsync`**
###### **5.2.1 Lokales Backup eines Verzeichnisses**
```bash
rsync -avz /pfad/zur/quelle /pfad/zum/ziel
```
- **`-a`**: Archivmodus (behält Metadaten bei).
- **`-v`**: Ausführliche Ausgabe.
- **`-z`**: Kompression während der Übertragung.

###### **5.2.2 Remote-Backup über SSH**
```bash
rsync -avz -e ssh /pfad/zur/quelle user@remote-host:/pfad/zum/ziel
```
- **`-e ssh`**: Verwendet SSH für die Übertragung.

###### **5.2.3 Inkrementelles Backup mit `--link-dest`**
```bash
# Erstes Vollbackup
rsync -avz /pfad/zur/quelle /pfad/zum/ziel/full_backup

# Inkrementelles Backup (nur Änderungen seit dem letzten Backup)
rsync -avz --link-dest=/pfad/zum/ziel/full_backup /pfad/zur/quelle /pfad/zum/ziel/incremental_backup_1
```
- **`--link-dest`**: Erstellt Hardlinks zu unveränderten Dateien im **Vollbackup**, um Speicherplatz zu sparen.

###### **5.2.4 Backup mit Ausschluss von Dateien**
```bash
rsync -avz --exclude='*.log' --exclude='/tmp/*' /pfad/zur/quelle /pfad/zum/ziel
```

###### **5.2.5 Bandbreitenbegrenzung**
```bash
rsync -avz --bwlimit=1000 /pfad/zur/quelle /pfad/zum/ziel
```
- **`--bwlimit=1000`**: Begrenzt die Bandbreite auf **1000 KB/s**.

###### **5.2.6 Backup mit Löschung gelöschter Dateien**
```bash
rsync -avz --delete /pfad/zur/quelle /pfad/zum/ziel
```
- **`--delete`**: Löscht Dateien im Ziel, die nicht mehr in der Quelle existieren.

---
---
#### **6. Backup mit `dd`**
`dd` ist ein **niedriges Level-Tool**, das **Bit-für-Bit-Kopien** von Festplatten, Partitionen oder Dateien erstellt. Es ist besonders nützlich für:
- **Vollständige Festplatten-Backups** (inkl. Bootloader).
- **Klonen von Festplatten**.
- **Erstellen von Images** für virtuelle Maschinen.

---
##### **6.1 Grundlagen von `dd`**
| **Option** | **Beschreibung** |
|------------|------------------|
| `if=[datei]` | **Input-Datei** (Quelle). |
| `of=[datei]` | **Output-Datei** (Ziel). |
| `bs=[größe]` | **Blockgröße** (z. B. `bs=4M` für 4 MiB). |
| `count=[anzahl]` | **Anzahl der Blöcke**, die kopiert werden sollen. |
| `status=progress` | Zeigt **Fortschritt** an. |
| `conv=sync,noerror` | **Synchronisiert Blöcke** und ignoriert Fehler. |

---
##### **6.2 Beispiele für `dd`**
###### **6.2.1 Backup einer gesamten Festplatte**
```bash
sudo dd if=/dev/sda of=/pfad/zur/backup.img bs=4M status=progress
```
- **`if=/dev/sda`**: Quelle (Festplatte `/dev/sda`).
- **`of=/pfad/zur/backup.img`**: Ziel (Backup-Datei).
- **`bs=4M`**: Blockgröße von 4 MiB für bessere Performance.
- **`status=progress`**: Zeigt den Fortschritt an.

###### **6.2.2 Backup einer Partition**
```bash
sudo dd if=/dev/sda1 of=/pfad/zur/partition_backup.img bs=4M status=progress
```

###### **6.2.3 Backup komprimieren (mit `gzip`)**
```bash
sudo dd if=/dev/sda bs=4M status=progress | gzip > /pfad/zur/backup.img.gz
```
- **`| gzip`**: Komprimiert die Ausgabe mit `gzip`.

###### **6.2.4 Backup einer Festplatte auf eine andere Festplatte klonen**
```bash
sudo dd if=/dev/sda of=/dev/sdb bs=4M status=progress
```
- **Achtung**: Dies **überschreibt alle Daten auf `/dev/sdb`!**

###### **6.2.5 Backup wiederherstellen**
```bash
sudo dd if=/pfad/zur/backup.img of=/dev/sda bs=4M status=progress
```
- **Achtung**: Dies **überschreibt alle Daten auf `/dev/sda`!**

---
---
#### **7. Backup mit `BorgBackup`**
`BorgBackup` ist ein **modernes, deduplizierendes Backup-Tool** mit **Kompression und Verschlüsselung**. Es ist besonders für **effiziente, sichere Backups** geeignet.

---
##### **7.1 Installation von `BorgBackup`**
- **Debian/Ubuntu:**
  ```bash
  sudo apt install borgbackup
  ```
- **RHEL/CentOS:**
  ```bash
  sudo yum install borgbackup
  ```
- **Arch Linux:**
  ```bash
  sudo pacman -S borg
  ```

---
##### **7.2 Grundlagen von `BorgBackup`**
| **Befehl** | **Beschreibung** |
|------------|------------------|
| `borg init [repository]` | **Initialisiert** ein neues Repository. |
| `borg create [repository]::[archivname] [quelle]` | **Erstellt** ein neues Backup-Archiv. |
| `borg list [repository]` | **Listet** alle Archive in einem Repository auf. |
| `borg extract [repository]::[archivname]` | **Extrahiert** ein Archiv. |
| `borg delete [repository]::[archivname]` | **Löscht** ein Archiv. |
| `borg prune [repository]` | **Bereinigt** alte Archive (z. B. nach Zeit oder Anzahl). |
| `borg check [repository]` | **Überprüft** die Integrität eines Repositorys. |

---
##### **7.3 Beispiele für `BorgBackup`**
###### **7.3.1 Repository initialisieren**
```bash
# Erstellen eines lokalen Repositorys
borg init --encryption=repokey /pfad/zum/repository

# Erstellen eines Remote-Repositorys (über SSH)
borg init --encryption=repokey user@remote-host:/pfad/zum/repository
```
- **`--encryption=repokey`**: Verschlüsselt das Repository mit einem **Schlüssel, der im Repository gespeichert wird**.

###### **7.3.2 Vollbackup erstellen**
```bash
borg create --stats --progress /pfad/zum/repository::full_backup-2026-06-01 /pfad/zur/quelle
```
- **`--stats`**: Zeigt Statistiken nach dem Backup an.
- **`--progress`**: Zeigt den Fortschritt an.
- **`full_backup-2026-06-01`**: Name des Archivs (kann frei gewählt werden).

###### **7.3.3 Inkrementelles Backup erstellen**
```bash
borg create --stats --progress /pfad/zum/repository::incremental_backup-2026-06-02 /pfad/zur/quelle
```
- `BorgBackup` **erkennt automatisch**, welche Dateien sich geändert haben.

###### **7.3.4 Archive auflisten**
```bash
borg list /pfad/zum/repository
```

###### **7.3.5 Backup wiederherstellen**
```bash
# Extrahiere ein bestimmtes Archiv
borg extract /pfad/zum/repository::full_backup-2026-06-01

# Extrahiere ein bestimmtes Verzeichnis aus einem Archiv
borg extract /pfad/zum/repository::full_backup-2026-06-01 pfad/zur/datei
```

###### **7.3.6 Alte Archive bereinigen**
```bash
# Behalte nur die letzten 7 Tage, 4 Wochen und 6 Monate
borg prune --keep-daily 7 --keep-weekly 4 --keep-monthly 6 /pfad/zum/repository
```

###### **7.3.7 Repository überprüfen**
```bash
borg check /pfad/zum/repository
```

---
---
#### **8. Backup mit `Timeshift`**
`Timeshift` ist ein **Snapshot-Backup-Tool**, das **System-Backups** (nicht Benutzerdaten) erstellt. Es unterstützt:
- **Btrfs-Snapshots** (sehr effizient, nur Änderungen werden gespeichert).
- **Rsync-Snapshots** (für Dateisysteme, die Btrfs nicht unterstützen).

---
##### **8.1 Installation von `Timeshift`**
- **Debian/Ubuntu:**
  ```bash
  sudo apt install timeshift
  ```
- **RHEL/CentOS:**
  ```bash
  sudo yum install timeshift
  ```
- **Arch Linux:**
  ```bash
  sudo pacman -S timeshift
  ```

---
##### **8.2 Grundlagen von `Timeshift`**
| **Befehl** | **Beschreibung** |
|------------|------------------|
| `sudo timeshift --create` | **Erstellt** einen neuen Snapshot. |
| `sudo timeshift --list` | **Listet** alle Snapshots auf. |
| `sudo timeshift --restore` | **Stellt** einen Snapshot wieder her. |
| `sudo timeshift --delete` | **Löscht** einen Snapshot. |

---
##### **8.3 Beispiele für `Timeshift`**
###### **8.3.1 Snapshot erstellen (Btrfs oder Rsync)**
```bash
# Erstellen eines Snapshots (automatisch erkanntes Dateisystem)
sudo timeshift --create --comments "Vor Update" --tags D

# Erstellen eines Snapshots mit Rsync (für nicht-Btrfs-Systeme)
sudo timeshift --create --snapshot-type rsync --comments "Vor Update" --tags D
```
- **`--comments`**: Fügt einen Kommentar hinzu.
- **`--tags D`**: Markiert den Snapshot als "D" (täglich).

###### **8.3.2 Snapshots auflisten**
```bash
sudo timeshift --list
```

###### **8.3.3 Snapshot wiederherstellen**
```bash
# Wähle einen Snapshot aus der Liste aus
sudo timeshift --restore --snapshot "2026-06-01_10-00-00"
```
- **Achtung**: Die Wiederherstellung **überschreibt das aktuelle System**!

###### **8.3.4 Snapshot löschen**
```bash
sudo timeshift --delete --snapshot "2026-06-01_10-00-00"
```

---
---
#### **9. Backup-Strategien in der Praxis**
---
##### **9.1 3-2-1-Backup-Strategie umsetzen**
| **Schritt** | **Aktion** | **Tool** | **Beispiel** |
|-------------|------------|----------|--------------|
| **1. Lokales Backup** | Erstellen Sie ein **Vollbackup** auf einer externen Festplatte. | `rsync`, `tar` | `rsync -avz /home /mnt/backup/home` |
| **2. Zweites Backup** | Erstellen Sie ein **inkrementelles Backup** auf einem NAS oder einem zweiten Server. | `BorgBackup`, `rsync` | `borg create /mnt/nas/backup::home-2026-06-01 /home` |
| **3. Cloud-Backup** | Sichern Sie kritische Daten in der **Cloud** (z. B. AWS S3, Backblaze B2). | `rclone`, `Duplicati` | `rclone copy /home remote:backup/home` |

---
##### **9.2 Automatisierte Backups mit `cron`**
Verwenden Sie `cron`, um **Backups automatisch** durchzuführen.

**Beispiel: Tägliches Backup mit `rsync`**
1. Bearbeiten Sie die Crontab:
   ```bash
   crontab -e
   ```
2. Fügen Sie eine Zeile hinzu:
   ```bash
   0 2 * * * /usr/bin/rsync -avz --delete /home /mnt/backup/home >> /var/log/backup.log 2>&1
   ```
   - **`0 2 * * *`**: Führt den Befehl **täglich um 2:00 Uhr** aus.
   - **`>> /var/log/backup.log 2>&1`**: Leitet die Ausgabe in eine **Log-Datei** um.

**Beispiel: Wöchentliches Vollbackup mit `tar`**
```bash
0 3 * * 0 /usr/bin/tar -czvf /mnt/backup/full_backup-$(date +\%Y-\%m-\%d).tar.gz /home >> /var/log/backup.log 2>&1
```
- **`0 3 * * 0`**: Führt den Befehl **sonntags um 3:00 Uhr** aus.
- **`$(date +\%Y-\%m-\%d)`**: Fügt das **aktuelle Datum** zum Dateinamen hinzu.

---
##### **9.3 Backup-Überprüfung und Testen**
- **Regelmäßige Überprüfung**:
  - Testen Sie **Wiederherstellungen** in einer **Testumgebung**.
  - Überprüfen Sie **Backup-Logs** auf Fehler.
- **Integritätsprüfung**:
  - Verwenden Sie `borg check` für BorgBackup-Repositorys.
  - Verwenden Sie `sha256sum` für tar-Archive:
    ```bash
    sha256sum /pfad/zur/backup.tar.gz
    ```
- **Wiederherstellungstest**:
  - Stellen Sie ein Backup in einer **virtuellen Maschine** wieder her, um sicherzustellen, dass es funktioniert.

---
---
#### **10. Übungsaufgaben**
---
##### **Frage 1**
Wie können Sie ein **Vollbackup** des Verzeichnisses `/home` mit `tar` erstellen und in `/mnt/backup/home.tar.gz` speichern?

??? success "Antwort"
    ```bash
    sudo tar -czvf /mnt/backup/home.tar.gz /home
    ```

---
##### **Frage 2**
Wie können Sie ein **inkrementelles Backup** mit `rsync` erstellen, das nur Änderungen seit dem letzten Backup in `/mnt/backup/full_backup` berücksichtigt?

??? success "Antwort"
    ```bash
    rsync -avz --link-dest=/mnt/backup/full_backup /home /mnt/backup/incremental_backup
    ```

---
##### **Frage 3**
Wie können Sie eine **Bit-für-Bit-Kopie** der Festplatte `/dev/sda` in die Datei `/mnt/backup/sda.img` erstellen?

??? success "Antwort"
    ```bash
    sudo dd if=/dev/sda of=/mnt/backup/sda.img bs=4M status=progress
    ```

---
##### **Frage 4**
Wie können Sie ein **BorgBackup-Repository** in `/mnt/backup/borg_repo` initialisieren und ein **Vollbackup** von `/home` erstellen?

??? success "Antwort"
    ```bash
    borg init --encryption=repokey /mnt/backup/borg_repo
    borg create --stats --progress /mnt/backup/borg_repo::home-2026-06-01 /home
    ```

---
##### **Frage 5**
Wie können Sie ein **Timeshift-Snapshot** mit dem Kommentar "Vor Systemupdate" erstellen?

??? success "Antwort"
    ```bash
    sudo timeshift --create --comments "Vor Systemupdate"
    ```

---
##### **Frage 6**
Wie können Sie ein **tägliches Backup** von `/home` mit `cron` und `rsync` um 3:00 Uhr einrichten?

??? success "Antwort"
    ```bash
    crontab -e
    ```
    Fügen Sie folgende Zeile hinzu:
    ```bash
    0 3 * * * /usr/bin/rsync -avz /home /mnt/backup/home >> /var/log/backup.log 2>&1
    ```

---
##### **Frage 7**
Wie können Sie ein **komprimiertes Backup** einer Partition `/dev/sda1` mit `dd` und `gzip` erstellen?

??? success "Antwort"
    ```bash
    sudo dd if=/dev/sda1 bs=4M status=progress | gzip > /mnt/backup/sda1.img.gz
    ```

---
##### **Frage 8**
Wie können Sie **alle BorgBackup-Archive** in `/mnt/backup/borg_repo` auflisten?

??? success "Antwort"
    ```bash
    borg list /mnt/backup/borg_repo
    ```

---
##### **Frage 9**
Wie können Sie ein **Backup-Archiv** mit `tar` extrahieren, das in `/mnt/backup/home.tar.gz` gespeichert ist?

??? success "Antwort"
    ```bash
    sudo tar -xzvf /mnt/backup/home.tar.gz -C /
    ```
    - **`-C /`**: Extrahiere in das **Root-Verzeichnis**.

---
##### **Frage 10**
Wie können Sie **alte BorgBackup-Archive** bereinigen, sodass nur die letzten **7 Tage, 4 Wochen und 6 Monate** behalten werden?

??? success "Antwort"
    ```bash
    borg prune --keep-daily 7 --keep-weekly 4 --keep-monthly 6 /mnt/backup/borg_repo
    ```

---
---
#### **11. Praktische Beispiele**
---
##### **Beispiel 1: Vollständiges System-Backup mit `tar`**
**Szenario:** Sie möchten ein **Vollbackup des gesamten Systems** (außer `/dev`, `/proc`, `/sys`, `/tmp`) erstellen.

**Lösung:**
```bash
sudo tar -czvf /mnt/backup/full_system_backup-$(date +%Y-%m-%d).tar.gz \
  --exclude=/dev --exclude=/proc --exclude=/sys --exclude=/tmp \
  --exclude=/mnt --exclude=/media /
```

---
##### **Beispiel 2: Inkrementelles Backup mit `rsync` und `--link-dest`**
**Szenario:** Sie möchten **tägliche inkrementelle Backups** von `/home` erstellen, wobei unveränderte Dateien als **Hardlinks** gespeichert werden.

**Lösung:**
1. **Erstes Vollbackup:**
   ```bash
   rsync -avz /home /mnt/backup/home/full_backup
   ```
2. **Tägliches inkrementelles Backup:**
   ```bash
   rsync -avz --link-dest=/mnt/backup/home/full_backup /home /mnt/backup/home/incremental_$(date +%Y-%m-%d)
   ```

---
##### **Beispiel 3: Automatisiertes Backup mit `BorgBackup` und `cron`**
**Szenario:** Sie möchten **tägliche Backups** von `/home` mit `BorgBackup` erstellen und **alte Backups bereinigen**.

**Lösung:**
1. **Repository initialisieren:**
   ```bash
   borg init --encryption=repokey /mnt/backup/borg_repo
   ```
2. **Cron-Job einrichten:**
   ```bash
   crontab -e
   ```
   Fügen Sie folgende Zeilen hinzu:
   ```bash
   # Tägliches Backup um 2:00 Uhr
   0 2 * * * /usr/bin/borg create --stats /mnt/backup/borg_repo::home-$(date +\%Y-\%m-\%d) /home >> /var/log/borg_backup.log 2>&1

   # Wöchentliche Bereinigung um 3:00 Uhr sonntags
   0 3 * * 0 /usr/bin/borg prune --keep-daily 7 --keep-weekly 4 --keep-monthly 6 /mnt/backup/borg_repo >> /var/log/borg_prune.log 2>&1
   ```

---
##### **Beispiel 4: Festplatten-Image mit `dd` und Kompression**
**Szenario:** Sie möchten ein **komprimiertes Image** der Festplatte `/dev/sda` erstellen.

**Lösung:**
```bash
sudo dd if=/dev/sda bs=4M status=progress | gzip > /mnt/backup/sda-$(date +%Y-%m-%d).img.gz
```

---
##### **Beispiel 5: Timeshift für System-Snapshots**
**Szenario:** Sie möchten **tägliche Snapshots** Ihres Systems mit `Timeshift` erstellen.

**Lösung:**
1. **Timeshift installieren und konfigurieren:**
   ```bash
   sudo apt install timeshift
   sudo timeshift --create --snapshot-type rsync --comments "Erster Snapshot" --tags D
   ```
2. **Automatische Snapshots einrichten:**
   - Öffnen Sie die **Timeshift-GUI** oder bearbeiten Sie die Konfiguration in `/etc/timeshift/timeshift.json`.
   - Aktivieren Sie **tägliche Snapshots**.

---
---
#### **12. Häufige Fehler und Lösungen**
| **Problem** | **Ursache** | **Lösung** |
|-------------|-------------|------------|
| **`tar: Cowardly refusing to create an empty archive`** | Keine Dateien zum Sichern gefunden. | Überprüfen Sie den Pfad zur Quelle. |
| **`rsync: failed to set permissions on`** | Berechtigungsprobleme beim Ziel. | Verwenden Sie `sudo` oder passen Sie die Berechtigungen an. |
| **`dd: No space left on device`** | Nicht genug Speicherplatz für das Backup. | Freien Speicherplatz prüfen oder Backup auf ein größeres Laufwerk umleiten. |
| **`BorgBackup: Repository not initialized`** | Repository wurde nicht initialisiert. | Führen Sie `borg init` aus. |
| **`Timeshift: No snapshots found`** | Keine Snapshots erstellt. | Überprüfen Sie die Timeshift-Konfiguration und erstellen Sie manuell einen Snapshot. |
| **`cron: command not found`** | Pfad zu `rsync` oder `tar` ist nicht in `$PATH`. | Verwenden Sie absolute Pfade (z. B. `/usr/bin/rsync`). |
| **Backup-Datei ist beschädigt** | Übertragungsfehler oder Festplattenproblem. | Überprüfen Sie die Integrität mit `sha256sum` oder `borg check`. |
| **`Permission denied` beim Wiederherstellen** | Berechtigungsprobleme. | Verwenden Sie `sudo` oder passen Sie die Berechtigungen an. |

---
---
#### **13. Vertiefung: Backup in der Cloud**
---
##### **13.1 `rclone` – Synchronisation mit Cloud-Speicher**
`rclone` ist ein **Kommandozeilen-Tool** zum **Synchronisieren von Dateien mit Cloud-Speicherdiensten** wie:
- **AWS S3**
- **Google Drive**
- **Backblaze B2**
- **Dropbox**
- **Microsoft OneDrive**

**Installation:**
- **Debian/Ubuntu:**
  ```bash
  sudo apt install rclone
  ```
- **RHEL/CentOS:**
  ```bash
  sudo yum install rclone
  ```

**Konfiguration:**
1. Führen Sie `rclone config` aus und folgen Sie den Anweisungen, um einen **Cloud-Speicher** einzurichten.
2. Testen Sie die Verbindung:
   ```bash
   rclone lsd remote:
   ```

**Beispiel: Backup in AWS S3**
```bash
# Vollbackup in S3 hochladen
rclone copy /mnt/backup/home remote:backup/home

# Inkrementelles Backup (nur neue/geänderte Dateien)
rclone sync /mnt/backup/home remote:backup/home
```

---
##### **13.2 `Duplicati` – Grafisches Backup-Tool für die Cloud**
`Duplicati` ist ein **grafisches Backup-Tool**, das **Verschlüsselung, Kompression und Cloud-Integration** unterstützt.

**Installation:**
- **Debian/Ubuntu:**
  ```bash
  sudo apt install duplicati
  ```
- **RHEL/CentOS:**
  ```bash
  sudo yum install duplicati
  ```

**Konfiguration:**
1. Starten Sie Duplicati:
   ```bash
   duplicati
   ```
2. Erstellen Sie ein **neues Backup** und wählen Sie einen **Cloud-Anbieter** (z. B. Backblaze B2, AWS S3).
3. Konfigurieren Sie **Verschlüsselung** und **Zeitplan**.

---
---
#### **14. Zusammenfassung der wichtigsten Befehle**
| **Aktion** | **`tar`** | **`rsync`** | **`dd`** | **`BorgBackup`** | **`Timeshift`** |
|------------|-----------|-------------|----------|------------------|----------------|
| **Vollbackup erstellen** | `tar -czvf backup.tar.gz /pfad` | `rsync -avz /quelle /ziel` | `dd if=/dev/sda of=backup.img` | `borg create repo::archiv /pfad` | `timeshift --create` |
| **Inkrementelles Backup** | `tar -czvf backup.tar.gz -N "datum" /pfad` | `rsync -avz --link-dest=/vollbackup /quelle /ziel` | – | `borg create repo::archiv /pfad` | – |
| **Backup extrahieren** | `tar -xzvf backup.tar.gz` | – | `dd if=backup.img of=/dev/sda` | `borg extract repo::archiv` | `timeshift --restore` |
| **Backup löschen** | `rm backup.tar.gz` | `rm -rf /ziel` | `rm backup.img` | `borg delete repo::archiv` | `timeshift --delete` |
| **Backup prüfen** | `tar -tvf backup.tar.gz` | – | – | `borg check repo` | `timeshift --list` |
| **Automatisierung** | `cron` + `tar` | `cron` + `rsync` | `cron` + `dd` | `cron` + `borg` | `cron` + `timeshift` |

