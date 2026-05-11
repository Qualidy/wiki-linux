# Modul III.5: Automatisierung von Aufgaben mit Cron



##  Einleitung

**Cron** ist der **Standard-Zeitplanungsdaemon** in Linux, der es dir ermöglicht, **Befehle oder Skripte automatisch zu festgelegten Zeiten oder Intervallen auszuführen**. Mit Cron kannst du:

- **Backups** regelmäßig erstellen.
- **Systemwartungsaufgaben** (z. B. Log-Bereinigung) automatisieren.
- **Skripte** zu bestimmten Zeiten ausführen (z. B. Datenbank-Backups, Berichte generieren).
- **Ressourcenintensive Aufgaben** in Zeiten mit geringer Auslastung durchführen.

In diesem Modul lernst du:

- Wie **Cron funktioniert** und wie du es konfigurierst.
- Die **Syntax der Crontab-Datei**.
- Wie du **Cron-Jobs erstellst, bearbeitest und löschst**.
- **Best Practices** für die Automatisierung mit Cron.
- **Fehlerbehandlung** und **Logging** für Cron-Jobs.



##  1. Grundlagen von Cron

### 1.1 Was ist Cron?

- **Cron** ist ein **Daemon** (Hintergrundprozess), der **zeitgesteuerte Aufgaben** ausführt.
- Jeder Benutzer (inkl. `root`) kann **eigene Cron-Jobs** erstellen.
- Cron-Jobs werden in der **Crontab-Datei** (`crontab`) definiert.



### 1.2 Wie funktioniert Cron?

1. **Cron-Daemon** läuft im Hintergrund und prüft regelmäßig die **Crontab-Dateien**.
2. Wenn ein **Zeitplan übereinstimmt**, führt Cron den entsprechenden **Befehl oder das Skript** aus.
3. Die **Ausgabe** (stdout/stderr) wird standardmäßig **per E-Mail an den Benutzer gesendet** (falls E-Mail konfiguriert ist).



### 1.3 Crontab-Dateien

- **Benutzerspezifische Crontabs**:
  - Jeder Benutzer hat eine **eigene Crontab-Datei** (`/var/spool/cron/crontabs/[Benutzername]`).
  - Bearbeitet mit dem Befehl `crontab -e`.
- **Systemweite Crontabs**:
  - `/etc/crontab`: Systemweite Cron-Jobs (nur für `root`).
  - `/etc/cron.d/`: Benutzerdefinierte Cron-Jobs (für Systemadministratoren).
  - `/etc/cron.hourly/`, `/etc/cron.daily/`, `/etc/cron.weekly/`, `/etc/cron.monthly/`: Skripte, die **stündlich, täglich, wöchentlich oder monatlich** ausgeführt werden.



### 1.4 Cron-Dienste verwalten


| Befehl                        | Beschreibung                          |
| ----------------------------- | ------------------------------------- |
| `sudo systemctl start cron`   | Startet den Cron-Daemon.              |
| `sudo systemctl stop cron`    | Stoppt den Cron-Daemon.               |
| `sudo systemctl restart cron` | Startet den Cron-Daemon neu.          |
| `sudo systemctl status cron`  | Zeigt den Status des Cron-Daemons an. |
| `sudo systemctl enable cron`  | Aktiviert Cron für den Autostart.     |


**Beispiel:**

```bash
# Überprüfe, ob Cron läuft
sudo systemctl status cron

# Starte Cron (falls nicht aktiv)
sudo systemctl start cron
```



##  2. Crontab-Syntax

### 2.1 Aufbau einer Crontab-Zeile

Eine Crontab-Zeile hat das folgende Format:

```
* * * * * Befehl
│ │ │ │ │
│ │ │ │ └── Tag der Woche (0-6, 0=Sonntag)
│ │ │ └──── Monat (1-12)
│ │ └────── Tag des Monats (1-31)
│ └──────── Stunde (0-23)
└────────── Minute (0-59)
```



### 2.2 Zeitangaben in Crontab


| Feld               | Wertebereich | Beschreibung                                         |
| ------------------ | ------------ | ---------------------------------------------------- |
| **Minute**         | 0-59         | Minute der Stunde.                                   |
| **Stunde**         | 0-23         | Stunde des Tages.                                    |
| **Tag des Monats** | 1-31         | Tag im Monat.                                        |
| **Monat**          | 1-12         | Monat (1=Januar, 12=Dezember).                       |
| **Tag der Woche**  | 0-6          | Tag der Woche (0=Sonntag, 1=Montag, ..., 6=Samstag). |




### 2.3 Spezielle Zeichen in Crontab


| Zeichen | Beschreibung                              | Beispiel                                    |
| ------- | ----------------------------------------- | ------------------------------------------- |
| `*`     | **Jeder Wert** (Wildcard).                | `* * * * *` = Jede Minute                   |
| `,`     | **Mehrere Werte** (durch Komma getrennt). | `1,15,30,45 * * * *` = Minute 1, 15, 30, 45 |
| `-`     | **Bereich von Werten**.                   | `1-5 * * * *` = Minuten 1 bis 5             |
| `/`     | **Schrittweite**.                         | `*/15 * * * *` = Alle 15 Minuten            |
| `@`     | **Vorgefertigte Zeitpläne**.              | `@daily` = Täglich um 00:00 Uhr             |




### 2.4 Vorgefertigte Zeitpläne


| Makro       | Beschreibung                                   | Äquivalente Crontab-Zeile |
| ----------- | ---------------------------------------------- | ------------------------- |
| `@yearly`   | **Jährlich** (am 1. Januar um 00:00 Uhr).      | `0 0 1 1 *`               |
| `@annually` | Gleich wie `@yearly`.                          | `0 0 1 1 *`               |
| `@monthly`  | **Monatlich** (am 1. des Monats um 00:00 Uhr). | `0 0 1 * *`               |
| `@weekly`   | **Wöchentlich** (am Sonntag um 00:00 Uhr).     | `0 0 * * 0`               |
| `@daily`    | **Täglich** (um 00:00 Uhr).                    | `0 0 * * *`               |
| `@midnight` | Gleich wie `@daily`.                           | `0 0 * * *`               |
| `@hourly`   | **Stündlich** (zu Beginn jeder Stunde).        | `0 * * * *`               |
| `@reboot`   | **Beim Systemstart**.                          | (Spezialfall)             |




### 2.5 Beispiele für Crontab-Zeilen


| Beschreibung                          | Crontab-Zeile                      |
| ------------------------------------- | ---------------------------------- |
| **Jede Minute**                       | `* * * * * /pfad/zum/skript.sh`    |
| **Alle 5 Minuten**                    | `*/5 * * * * /pfad/zum/skript.sh`  |
| **Stündlich um Minute 30**            | `30 * * * * /pfad/zum/skript.sh`   |
| **Täglich um 3:00 Uhr**               | `0 3 * * * /pfad/zum/skript.sh`    |
| **Montags bis Freitags um 17:00 Uhr** | `0 17 * * 1-5 /pfad/zum/skript.sh` |
| **Am 1. jedes Monats um 00:00 Uhr**   | `0 0 1 * * /pfad/zum/skript.sh`    |
| **Alle 30 Minuten**                   | `0,30 * * * * /pfad/zum/skript.sh` |
| **Jeden Sonntag um 4:00 Uhr**         | `0 4 * * 0 /pfad/zum/skript.sh`    |
| **Beim Systemstart**                  | `@reboot /pfad/zum/skript.sh`      |




## 📚 3. Crontab verwalten

### 3.1 Crontab bearbeiten

- Nutze den Befehl `crontab -e`, um die **Crontab-Datei des aktuellen Benutzers** zu bearbeiten.
- Standardmäßig wird der **Standard-Editor** (z. B. `nano` oder `vim`) geöffnet.

**Beispiel:**

```bash
crontab -e
```



### 3.2 Crontab anzeigen

- Nutze `crontab -l`, um die **aktuelle Crontab** anzuzeigen.

**Beispiel:**

```bash
crontab -l
```



### 3.3 Crontab löschen

- Nutze `crontab -r`, um die **gesamte Crontab** zu löschen.

**Beispiel:**

```bash
crontab -r
```


### 3.4 Crontab für andere Benutzer verwalten

- Als **Root-Benutzer** kannst du die Crontab eines anderen Benutzers bearbeiten:
  ```bash
  sudo crontab -u benutzername -e
  ```
- Beispiel:
  ```bash
  sudo crontab -u www-data -e
  ```


### 3.5 Systemweite Crontabs

- **Systemweite Cron-Jobs** können in `/etc/crontab` oder in Dateien unter `/etc/cron.d/` definiert werden.
- **Format von `/etc/crontab**`:
  ```
  Minute Stunde Tag_des_Monats Monat Tag_der_Woche Benutzer Befehl
  ```
  - **Unterschied zu Benutzer-Crontabs**: Enthält ein **zusätzliches Feld für den Benutzer**.

**Beispiel (`/etc/crontab`):**

```
# Beispiel: Führe ein Skript als Root aus
0 3 * * * root /pfad/zum/backup_skript.sh
```



##  4. Praktische Beispiele für Cron-Jobs

### 4.1 Beispiel 1: Tägliches Backup

**Aufgabe:** Erstelle ein **tägliches Backup** des Verzeichnisses `/home/benutzer/dokumente` um **2:00 Uhr morgens**.

**Crontab-Eintrag:**

```bash
0 2 * * * tar -czvf /backup/dokumente_$(date +\%Y-\%m-\%d).tar.gz /home/benutzer/dokumente
```

- **Problem:** `date` wird **beim Bearbeiten der Crontab** ausgeführt, nicht zur Laufzeit!
- **Lösung:** Erstelle ein **Skript** und rufe dieses auf.

**Skript (`/usr/local/bin/dokumente_backup.sh`):**

```bash
#!/bin/bash
BACKUP_DIR="/backup"
QUELLE="/home/benutzer/dokumente"
DATUM=$(date +%Y-%m-%d)
BACKUP_NAME="dokumente_$DATUM.tar.gz"

mkdir -p "$BACKUP_DIR"
tar -czvf "$BACKUP_DIR/$BACKUP_NAME" "$QUELLE"

# Lösche Backups, die älter als 30 Tage sind
find "$BACKUP_DIR" -name "dokumente_*.tar.gz" -mtime +30 -delete
```

**Crontab-Eintrag:**

```bash
0 2 * * * /usr/local/bin/dokumente_backup.sh
```



### 4.2 Beispiel 2: Log-Bereinigung

**Aufgabe:** Lösche **Log-Dateien**, die älter als **7 Tage** sind, jeden **Montag um 3:00 Uhr**.

**Crontab-Eintrag:**

```bash
0 3 * * 1 find /var/log -name "*.log" -mtime +7 -delete
```



### 4.3 Beispiel 3: Systemupdate

**Aufgabe:** Führe **täglich um 4:00 Uhr** ein **Systemupdate** durch.

**Crontab-Eintrag:**

```bash
0 4 * * * sudo apt update && sudo apt upgrade -y
```

- **Hinweis:** Nutze `sudo` nur, wenn der Cron-Job als **Root** ausgeführt wird.



### 4.4 Beispiel 4: Datenbank-Backup

**Aufgabe:** Erstelle ein **tägliches Backup einer MySQL-Datenbank** um **1:00 Uhr**.

**Skript (`/usr/local/bin/mysql_backup.sh`):**

```bash
#!/bin/bash
BACKUP_DIR="/backup/mysql"
DATUM=$(date +%Y-%m-%d)
DB_NAME="meine_datenbank"
DB_USER="benutzer"
DB_PASS="passwort"

mkdir -p "$BACKUP_DIR"
mysqldump -u "$DB_USER" -p"$DB_PASS" "$DB_NAME" > "$BACKUP_DIR/$DB_NAME_$DATUM.sql"

# Komprimiere das Backup
gzip "$BACKUP_DIR/$DB_NAME_$DATUM.sql"

# Lösche Backups, die älter als 14 Tage sind
find "$BACKUP_DIR" -name "$DB_NAME_*.sql.gz" -mtime +14 -delete
```

**Crontab-Eintrag:**

```bash
0 1 * * * /usr/local/bin/mysql_backup.sh
```


### 4.5 Beispiel 5: Skript mit Umgebungsvariablen

**Aufgabe:** Führe ein Skript aus, das **Umgebungsvariablen** benötigt (z. B. `PATH`).

**Problem:** Cron-Jobs haben eine **minimale Umgebung** (nur `SHELL`, `PATH`, `HOME`, `LOGNAME`).

- **Lösung:** Definiere die **Umgebungsvariablen** direkt in der Crontab oder im Skript.

**Crontab-Eintrag:**

```bash
0 * * * * . /home/benutzer/.profile; /pfad/zum/skript.sh
```

- `. /home/benutzer/.profile`: Lädt die **Umgebungsvariablen** des Benutzers.

**Alternative (besser):**

```bash
0 * * * * PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games /pfad/zum/skript.sh
```


### 4.6 Beispiel 6: E-Mail-Benachrichtigung bei Fehlern

**Aufgabe:** Sende eine **E-Mail-Benachrichtigung**, wenn ein Cron-Job fehlschlägt.

**Skript (`/usr/local/bin/backup_mit_benachrichtigung.sh`):**

```bash
#!/bin/bash
BACKUP_DIR="/backup"
QUELLE="/home/benutzer/dokumente"
DATUM=$(date +%Y-%m-%d)
BACKUP_NAME="dokumente_$DATUM.tar.gz"

mkdir -p "$BACKUP_DIR"
if tar -czvf "$BACKUP_DIR/$BACKUP_NAME" "$QUELLE"; then
  echo "Backup erfolgreich erstellt: $BACKUP_NAME" | mail -s "Backup Erfolgreich" benutzer@example.com
else
  echo "Fehler beim Erstellen des Backups!" | mail -s "Backup Fehlgeschlagen" benutzer@example.com
  exit 1
fi
```

**Crontab-Eintrag:**

```bash
0 2 * * * /usr/local/bin/backup_mit_benachrichtigung.sh
```



### 4.7 Beispiel 7: Cron-Job mit Logging

**Aufgabe:** Führe ein Skript aus und **protokolliere die Ausgabe** in einer Log-Datei.

**Crontab-Eintrag:**

```bash
0 * * * * /pfad/zum/skript.sh >> /var/log/skript.log 2>&1
```

- `>> /var/log/skript.log`: Fügt die **Standardausgabe (stdout)** an die Log-Datei an.
- `2>&1`: Leitet die **Fehlerausgabe (stderr)** in die Standardausgabe um.

---

### 4.8 Beispiel 8: Cron-Job mit Umleitung von stdout und stderr

**Aufgabe:** Leite **stdout und stderr** in separate Log-Dateien um.

**Crontab-Eintrag:**

```bash
0 * * * * /pfad/zum/skript.sh > /var/log/skript_out.log 2> /var/log/skript_err.log
```



##  5. Fehlerbehandlung und Debugging

### 5.1 Häufige Probleme mit Cron


| Problem                                                          | Lösung                                                                                                    |
| ---------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| **Cron-Job wird nicht ausgeführt**                               | Überprüfe, ob der **Cron-Daemon läuft** (`sudo systemctl status cron`).                                   |
| **Skript funktioniert in der Kommandozeile, aber nicht in Cron** | Überprüfe **Pfade und Umgebungsvariablen** (Cron hat eine minimale Umgebung).                             |
| **E-Mails werden nicht gesendet**                                | Überprüfe, ob **Postfix oder Sendmail** installiert ist (`sudo apt install postfix`).                     |
| **Skript hat keine Ausführungsrechte**                           | Setze die **Ausführungsrechte** (`chmod +x /pfad/zum/skript.sh`).                                         |
| **Pfad zum Skript ist falsch**                                   | Nutze **absolute Pfade** in der Crontab.                                                                  |
| **Cron-Job wird nicht in der Crontab gespeichert**               | Überprüfe, ob der **Editor korrekt geschlossen** wurde (z. B. in `nano` mit `Strg+O`, `Enter`, `Strg+X`). |




### 5.2 Debugging von Cron-Jobs

1. **Überprüfe die Crontab**:
  ```bash
   crontab -l
  ```
2. **Überprüfe die Logs von Cron**:
  ```bash
   grep CRON /var/log/syslog
  ```
  - Zeigt an, wann Cron-Jobs **ausgeführt wurden** und ob es **Fehler gab**.
3. **Führe den Cron-Job manuell aus**:
  - Kopiere den Befehl aus der Crontab und führe ihn **manuell** in der Kommandozeile aus.
4. **Überprüfe die Umgebung von Cron**:
  - Cron-Jobs haben eine **minimale Umgebung**. Nutze `env` in deinem Skript, um die Umgebung anzuzeigen:
5. **Nutze `set -x` für Debugging**:
  - Füge `set -x` am Anfang deines Skripts hinzu, um **alle ausgeführten Befehle** anzuzeigen.



### 5.3 Logging für Cron-Jobs

- **Standardmäßig** sendet Cron die **Ausgabe (stdout/stderr)** per E-Mail an den Benutzer.
- Falls keine E-Mail konfiguriert ist, kannst du die Ausgabe in eine **Log-Datei umleiten**.

**Beispiel:**

```bash
0 * * * * /pfad/zum/skript.sh >> /var/log/skript.log 2>&1
```

**Erweiterte Logging-Optionen:**

```bash
0 * * * * {
  echo "=== Start: $(date) ===" >> /var/log/skript.log
  /pfad/zum/skript.sh >> /var/log/skript.log 2>&1
  echo "=== Ende: $(date) ===" >> /var/log/skript.log
} >> /var/log/skript.log 2>&1
```



##  6. Best Practices für Cron

### 6.1 Allgemeine Best Practices

1. **Nutze absolute Pfade**:
  - Cron hat eine **andere Umgebung** als deine Shell. Nutze **absolute Pfade** für Skripte und Dateien.
  - Beispiel: `/usr/local/bin/skript.sh` statt `./skript.sh`.
2. **Definiere Umgebungsvariablen**:
  - Cron-Jobs haben eine **minimale Umgebung**. Definiere `**PATH` und andere Variablen** direkt in der Crontab oder im Skript.
  - Beispiel:
    ```bash
    PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
    0 * * * * /pfad/zum/skript.sh
    ```
3. **Nutze Skripte statt direkter Befehle**:
  - **Komplexe Befehle** sollten in ein **Skript** ausgelagert werden.
  - Beispiel:
    ```bash
    # Schlechte Praxis (komplexer Befehl direkt in Crontab)
    0 * * * * cd /pfad/zum/verzeichnis && tar -czvf backup.tar.gz * && rm -rf /tmp/*

    # Gute Praxis (Skript)
    0 * * * * /pfad/zum/backup_skript.sh
    ```
4. **Protokolliere die Ausgabe**:
  - Leite **stdout und stderr** in eine **Log-Datei** um, um Fehler zu debuggen.
  - Beispiel:
    ```bash
    0 * * * * /pfad/zum/skript.sh >> /var/log/skript.log 2>&1
    ```
5. **Nutze `set -e` in Skripten**:
  - Beende das Skript **bei Fehlern** (`set -e`).
  - Beispiel:
    ```bash
    #!/bin/bash
    set -e
    # Skript-Logik hier
    ```
6. **Vermeide `sudo` in Cron-Jobs**:
  - Führe Cron-Jobs **als der Benutzer aus**, der die Berechtigungen benötigt.
  - Falls `sudo` nötig ist, nutze es **im Skript** und nicht in der Crontab.
7. **Teste Cron-Jobs manuell**:
  - Führe den Cron-Job **manuell** aus, bevor du ihn in die Crontab einträgst.
8. **Nutze `lockfiles`, um doppelte Ausführung zu vermeiden**:
  - Falls ein Cron-Job **länger als das Intervall** läuft, kann er **mehrfach gleichzeitig ausgeführt** werden.
  - Nutze ein **Lockfile**, um dies zu vermeiden.
  - Beispiel:
    ```bash
    #!/bin/bash
    LOCKFILE="/tmp/skript.lock"
    if [ -e "$LOCKFILE" ]; then
      echo "Skript läuft bereits." | mail -s "Skript läuft bereits" benutzer@example.com
      exit 1
    fi

    # Lockfile erstellen
    touch "$LOCKFILE"

    # Skript-Logik hier

    # Lockfile löschen
    rm -f "$LOCKFILE"
    ```



### 6.2 Sicherheitstipps

1. **Beschränke den Zugriff auf `crontab**`:
  - Nur **vertrauenswürdige Benutzer** sollten Cron-Jobs erstellen können.
  - Nutze `sudo` nur, wenn nötig.
2. **Vermeide Passwörter in Cron-Jobs**:
  - Speichere **keine Passwörter** in der Crontab oder in Skripten.
  - Nutze **Umgebungsvariablen** oder **Konfigurationsdateien** mit eingeschränkten Berechtigungen.
3. **Nutze `cron.allow` und `cron.deny**`:
  - Du kannst **steuern, welche Benutzer Cron-Jobs erstellen dürfen**:
    - `/etc/cron.allow`: Benutzer, die Cron-Jobs erstellen dürfen.
    - `/etc/cron.deny`: Benutzer, die **keine** Cron-Jobs erstellen dürfen.
  - Beispiel:
    ```bash
    echo "benutzer1" | sudo tee /etc/cron.allow
    echo "benutzer2" | sudo tee -a /etc/cron.allow
    ```
4. **Überprüfe Cron-Jobs regelmäßig**:
  - Nutze `crontab -l` und `sudo crontab -u benutzername -l`, um **unbekannte Cron-Jobs** zu finden.


##  7. Alternativen zu Cron

### 7.1 `systemd`-Timer

- `**systemd`-Timer** sind eine **moderne Alternative** zu Cron.
- **Vorteile**:
  - **Bessere Integration** mit `systemd`.
  - **Mehr Flexibilität** (z. B. Zeitpläne basierend auf Kalenderereignissen).
  - **Logging über `journalctl**`.

#### Beispiel: `systemd`-Timer erstellen

1. **Service-Datei erstellen** (`/etc/systemd/system/backup.service`):
  ```ini
   [Unit]
   Description=Backup-Skript

   [Service]
   ExecStart=/usr/local/bin/backup_skript.sh
  ```
2. **Timer-Datei erstellen** (`/etc/systemd/system/backup.timer`):
  ```ini
   [Unit]
   Description=Führe Backup täglich aus

   [Timer]
   OnCalendar=daily
   Persistent=true

   [Install]
   WantedBy=timers.target
  ```
3. **Timer aktivieren**:
  ```bash
   sudo systemctl daemon-reload
   sudo systemctl enable backup.timer
   sudo systemctl start backup.timer
  ```
4. **Status überprüfen**:
  ```bash
   sudo systemctl list-timers
   journalctl -u backup.service
  ```


### 7.2 `anacron`

- `**anacron**` ist eine **Alternative zu Cron** für Systeme, die **nicht 24/7 laufen** (z. B. Laptops).
- **Vorteile**:
  - Führt Jobs aus, die **verpasst wurden**, wenn das System ausgeschaltet war.
  - **Einfacher zu konfigurieren** als Cron.

#### Beispiel: `anacron`-Job erstellen

1. **Konfigurationsdatei bearbeiten** (`/etc/anacrontab`):
  ```ini
   # Periode   Verzögerung   Job-Identifier   Befehl
   1           5             backup_job       /usr/local/bin/backup_skript.sh
  ```
  - **Periode**: Wie oft der Job ausgeführt wird (in Tagen).
  - **Verzögerung**: Verzögerung in Minuten nach dem Start von `anacron`.
  - **Job-Identifier**: Eindeutiger Name für den Job.
  - **Befehl**: Der auszuführende Befehl.
2. `**anacron` aktivieren**:
  ```bash
   sudo systemctl enable anacron
   sudo systemctl start anacron
  ```



### 7.3 Vergleich: Cron vs. `systemd`-Timer vs. `anacron`


| Feature                       | Cron               | `systemd`-Timer  | `anacron` |
| ----------------------------- | ------------------ | ---------------- | --------- |
| **Zeitplanung**               | ✅                  | ✅                | ✅         |
| **Systeme ohne 24/7-Betrieb** | ❌                  | ❌                | ✅         |
| **Einfachheit**               | ✅                  | ❌                | ✅         |
| **Verpasste Jobs ausführen**  | ❌                  | ❌                | ✅         |




##  8. Übungsaufgaben



###  Übung 1: Einfacher Cron-Job

1. Erstelle einen Cron-Job, der **jeden Tag um 12:00 Uhr** die Datei `/tmp/test.txt` mit dem aktuellen Datum und der Uhrzeit füllt.

??? success "Lösung" 
    ***mein_cron_script.sh***
    ```bash
    #!/bin/bash
    aktueller_timestamp=$(date +"Aktuelles Datum und Uhrzeit: $(date)")


    echo "$aktueller_timestamp" > /tmp/test.txt

    ```
    ***Ausführbar machen***
    ```bash
    chmod +x ./mein_cron_script.sh
    ```
    ***Cron***
    ```bash
    # Läuft täglich um 12:00 Uhr
    0 12 * * * /home/benutzer/mein_cron_script.sh
    ```



###  Übung 2: Tägliches Backup

1. Erstelle ein Skript namens `tägliches_backup.sh`, das:
  - Ein Backup des Verzeichnisses `~/dokumente` als `backup_YYYY-MM-DD.tar.gz` erstellt.
  - Das Backup in `/backup` speichert.
2. Erstelle einen Cron-Job, der das Skript **täglich um 2:00 Uhr** ausführt.

??? success "Lösung" 
    ***tägliches_backup.sh***
    ```bash
    #!/bin/bash

    # Definiere die Konstanten
    # Das Verzeichnis, in dem die Backups gespeichert werden sollen.
    BACKUP_DIR="/backup"
    # Das zu sichernde Quellenverzeichnis (Home/Dokumente).
    QUELLE="$HOME/dokumente"
    # Erzeugt einen eindeutigen Namen basierend auf dem aktuellen Datum (YYYY-MM-DD).
    DATUM=$(date +%Y-%m-%d)
    BACKUP_NAME="backup_${DATUM}.tar.gz"

    # 1. Sicherstellen, dass das Zielverzeichnis existiert
    # -p sorgt dafür, dass das Verzeichnis erstellt wird, falls es fehlt,
    # und macht keinen Fehler, falls es bereits existiert.
    mkdir -p "$BACKUP_DIR"

    # 2. Das Backup erstellen
    # -c: erstellen, -z: gzip komprimieren, -v: detailliert anzeigen, -f: Dateinamen festlegen.
    tar -czvf "$BACKUP_DIR/$BACKUP_NAME" "$QUELLE"

    # 3. Ergebnis prüfen und melden
    if [ $? -eq 0 ]; then
        echo " Backup erfolgreich erstellt: $BACKUP_NAME"
    else
        echo " Fehler: Das Backup konnte nicht erstellt werden. Überprüfe die Berechtigungen."
    fi
    ```
    ***Cron***
    ```bash
    crontab -e
    0 2 * * * /home/benutzer/tägliches_backup.sh
    ```
    



###  Übung 5: Cron-Job mit Logging

1. Erstelle einen Cron-Job, der **stündlich** das Skript `/usr/local/bin/system_check.sh` ausführt und die **Ausgabe in `/var/log/system_check.log**` speichert.

??? success "Lösung"  
    ```bash
    0 * * * * /usr/local/bin/system_check.sh >> /var/log/system_check.log 2>&1
    ```     
 




## . Zusammenfassung und Tipps



###  Wichtige Befehle im Überblick


| Befehl                            | Beschreibung                                       | Beispiel                      |
| --------------------------------- | -------------------------------------------------- | ----------------------------- |
| `crontab -e`                      | Bearbeite die **Crontab-Datei**.                   | `crontab -e`                  |
| `crontab -l`                      | Zeige die **aktuelle Crontab** an.                 | `crontab -l`                  |
| `crontab -r`                      | Lösche die **gesamte Crontab**.                    | `crontab -r`                  |
| `sudo crontab -u benutzername -e` | Bearbeite die Crontab eines **anderen Benutzers**. | `sudo crontab -u www-data -e` |
| `grep CRON /var/log/syslog`       | Zeige **Cron-Logs** an.                            | `grep CRON /var/log/syslog`   |
| `sudo systemctl status cron`      | Überprüfe den **Status des Cron-Daemons**.         | `sudo systemctl status cron`  |




###  Crontab-Syntax im Überblick

```
* * * * * Befehl
│ │ │ │ │
│ │ │ │ └── Tag der Woche (0-6, 0=Sonntag)
│ │ │ └──── Monat (1-12)
│ │ └────── Tag des Monats (1-31)
│ └──────── Stunde (0-23)
└────────── Minute (0-59)
```


###  Tipps für die Praxis

1. **Teste Cron-Jobs manuell**:
  - Führe den Befehl oder das Skript **manuell** aus, bevor du ihn in die Crontab einträgst.
2. **Nutze absolute Pfade**:
  - Cron hat eine **andere Umgebung** als deine Shell. Nutze **absolute Pfade** für Skripte und Dateien.
3. **Protokolliere die Ausgabe**:
  - Leite **stdout und stderr** in eine **Log-Datei** um, um Fehler zu debuggen.
  - Beispiel: `>> /var/log/skript.log 2>&1`
4. **Definiere Umgebungsvariablen**:
  - Cron-Jobs haben eine **minimale Umgebung**. Definiere `**PATH` und andere Variablen** direkt in der Crontab oder im Skript.
5. **Nutze Skripte für komplexe Aufgaben**:
  - **Komplexe Befehle** sollten in ein **Skript** ausgelagert werden.
6. **Vermeide `sudo` in Cron-Jobs**:
  - Führe Cron-Jobs **als der Benutzer aus**, der die Berechtigungen benötigt.
7. **Nutze Lockfiles für lange Laufzeiten**:
  - Falls ein Cron-Job **länger als das Intervall** läuft, kann er **mehrfach gleichzeitig ausgeführt** werden. Nutze ein **Lockfile**, um dies zu vermeiden.
8. **Überprüfe Cron-Logs**:
  - Nutze `grep CRON /var/log/syslog`, um zu sehen, ob Cron-Jobs **ausgeführt wurden**.
9. **Nutze `systemd`-Timer für moderne Systeme**:
  - Falls dein System `systemd` verwendet, sind `**systemd`-Timer** eine gute Alternative zu Cron.
10. **Sicherheit beachten**:
  - Beschränke den Zugriff auf `crontab` auf **vertrauenswürdige Benutzer**.
    - Speichere **keine Passwörter** in der Crontab oder in Skripten.



###  Häufige Fallstricke


| Problem                                                          | Lösung                                                                                                    |
| ---------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| **Cron-Job wird nicht ausgeführt**                               | Überprüfe, ob der **Cron-Daemon läuft** (`sudo systemctl status cron`).                                   |
| **Skript funktioniert in der Kommandozeile, aber nicht in Cron** | Überprüfe **Pfade und Umgebungsvariablen** (Cron hat eine minimale Umgebung).                             |
| **E-Mails werden nicht gesendet**                                | Überprüfe, ob **Postfix oder Sendmail** installiert ist (`sudo apt install postfix`).                     |
| **Skript hat keine Ausführungsrechte**                           | Setze die **Ausführungsrechte** (`chmod +x /pfad/zum/skript.sh`).                                         |
| **Pfad zum Skript ist falsch**                                   | Nutze **absolute Pfade** in der Crontab.                                                                  |
| **Cron-Job wird nicht gespeichert**                              | Überprüfe, ob der **Editor korrekt geschlossen** wurde (z. B. in `nano` mit `Strg+O`, `Enter`, `Strg+X`). |
| **Cron-Job läuft zu oft**                                        | Nutze ein **Lockfile**, um doppelte Ausführung zu vermeiden.                                              |
| **Umgebungsvariablen fehlen**                                    | Definiere `**PATH` und andere Variablen** direkt in der Crontab oder im Skript.                           |



## 10. Weiterführende Themen

- `**systemd`-Timer**: Lerne, wie du `**systemd`-Timer** für komplexere Zeitpläne nutzt.
- `**anacron**`: Nutze `anacron` für Systeme, die **nicht 24/7 laufen** (z. B. Laptops).
- **Log-Rotation mit `logrotate**`: Automatisiere die **Bereinigung von Log-Dateien** mit `logrotate`.
- **Automatisierung mit `at**`: Führe Befehle **einmalig zu einem bestimmten Zeitpunkt** aus.
- **Monitoring von Cron-Jobs**: Nutze Tools wie `**cronitor**` oder `**healthchecks.io**`, um Cron-Jobs zu überwachen.



##  Fazit

**Cron** ist ein **mächtiges Werkzeug**, um **Aufgaben in Linux zu automatisieren**. Mit den Konzepten aus diesem Modul kannst du:

- **Cron-Jobs erstellen, bearbeiten und löschen**.
- **Skripte und Befehle zu festgelegten Zeiten ausführen**.
- **Fehler in Cron-Jobs debuggen und beheben**.
- **Best Practices für sichere und zuverlässige Cron-Jobs** anwenden.

**Automatisiere deine Aufgaben**, um Zeit zu sparen und deine Arbeit effizienter zu gestalten!

