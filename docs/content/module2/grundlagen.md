#  Modul II: Die Grundlagen der Command-Line

*Einführung in die Linux-Befehlszeile mit Übungen*

---

##  Einleitung

Die **Command-Line (Kommandozeile)** ist ein mächtiges Werkzeug, um mit Linux zu interagieren. Sie ermöglicht:

- **Schnelle und effiziente** Ausführung von Aufgaben.
- **Automatisierung** durch Skripte.
- **Zugang zu Systemfunktionen**, die über grafische Oberflächen nicht verfügbar sind.

In diesem Modul lernst du die **Grundlagen der Kommandozeile** kennen und übst diese mit praktischen Aufgaben.

---

##  1. Das Terminal öffnen und verstehen

### 1.1 Terminal öffnen

- **Shortcut**: `Strg + Alt + T` (Ubuntu, Debian, etc.)
- **Über das Menü**: Suche nach "Terminal" oder "Konsole" in deiner Linux-Distribution.
- **Virtuelle Konsolen**: Drücke `Strg + Alt + F1` bis `F6` für textbasierte Konsolen (ohne GUI).

### 1.2 Die Shell

- Die **Shell** ist das Programm, das deine Befehle interpretiert.
- Standard-Shell in den meisten Linux-Distributionen: **Bash (Bourne Again SHell)**.
- Andere Shells: `zsh`, `fish`, `ksh`.

### 1.3 Prompt verstehen

Der **Prompt** (Eingabeaufforderung) sieht typischerweise so aus:

```bash
benutzername@hostname:~$
```

- `benutzername`: Dein aktueller Benutzername.
- `hostname`: Der Name deines Computers.
- `~`: Aktuelles Verzeichnis (hier: Home-Verzeichnis).
- `$`: Zeigt an, dass du ein normaler Benutzer bist (bei `root` steht `#`).

---

##  2. Grundlegende Befehle

### 2.1 Navigation im Dateisystem


| Befehl  | Beschreibung                                                       | Beispiel                       |
| ------- | ------------------------------------------------------------------ | ------------------------------ |
| `pwd`   | Zeigt das **aktuelle Arbeitsverzeichnis** an.                      | `pwd`                          |
| `ls`    | Listet **Dateien und Verzeichnisse** im aktuellen Verzeichnis auf. | `ls -l` (detaillierte Ansicht) |
| `cd`    | Wechselt das **Verzeichnis**.                                      | `cd /home/benutzer`            |
| `cd ..` | Wechselt in das **übergeordnete Verzeichnis**.                     | `cd ..`                        |
| `cd ~`  | Wechselt ins **Home-Verzeichnis**.                                 | `cd ~`                         |
| `cd -`  | Wechselt zum **vorherigen Verzeichnis**.                           | `cd -`                         |


#### Optionen für `ls`


| Option | Beschreibung                                                 |
| ------ | ------------------------------------------------------------ |
| `-l`   | Detaillierte Liste (Berechtigungen, Besitzer, Größe, Datum). |
| `-a`   | Zeigt **versteckte Dateien** (beginnen mit `.`) an.          |
| `-h`   | Zeigt Dateigrößen in **lesbarer Form** (z. B. KB, MB).       |
| `-R`   | Listet **rekursiv** alle Unterverzeichnisse auf.             |


**Beispiel:**

```bash
ls -lh
```

Ausgabe:

```
drwxr-xr-x 2 benutzername benutzername 4.0K Mai  9 10:00 Dokumente
-rw-r--r-- 1 benutzername benutzername  123 Mai  9 09:50 notizen.txt
```

---

### 2.2 Dateien und Verzeichnisse erstellen, kopieren, verschieben und löschen


| Befehl  | Beschreibung                                      | Beispiel                      |
| ------- | ------------------------------------------------- | ----------------------------- |
| `touch` | Erstellt eine **leere Datei**.                    | `touch datei.txt`             |
| `mkdir` | Erstellt ein **neues Verzeichnis**.               | `mkdir mein_ordner`           |
| `cp`    | **Kopiert** Dateien/Verzeichnisse.                | `cp datei.txt /backup/`       |
| `mv`    | **Verschiebt** oder **benennt um**.               | `mv datei.txt neuer_name.txt` |
| `rm`    | **Löscht** Dateien/Verzeichnisse.                 | `rm datei.txt`                |
| `rmdir` | Löscht **leere Verzeichnisse**.                   | `rmdir leerer_ordner`         |
| `rm -r` | Löscht **Verzeichnisse inkl. Inhalt** (rekursiv). | `rm -r ordner/`               |


#### Wichtige Optionen

- `cp -r`: Kopiert **Verzeichnisse rekursiv**.
- `mv -i`: Frag vor dem Überschreiben nach.
- `rm -i`: Frag vor dem Löschen nach.
- `rm -f`: **Erzwinge** das Löschen (ohne Nachfrage).

**Beispiel:**

```bash
# Verzeichnis erstellen
mkdir projekte

# Datei erstellen
touch projekte/readme.txt

# Datei kopieren
cp projekte/readme.txt projekte/readme_backup.txt

# Datei umbenennen
mv projekte/readme.txt projekte/anleitung.txt

# Verzeichnis löschen (inkl. Inhalt)
rm -r projekte/
```

---

### 2.3 Dateiinhalte anzeigen und bearbeiten


| Befehl | Beschreibung                                   | Beispiel              |
| ------ | ---------------------------------------------- | --------------------- |
| `cat`  | Zeigt den **Inhalt einer Datei** an.           | `cat datei.txt`       |
| `less` | Zeigt Dateiinhalte **seitenweise** an.         | `less datei.txt`      |
| `head` | Zeigt die **ersten Zeilen** einer Datei.       | `head -n 5 datei.txt` |
| `tail` | Zeigt die **letzten Zeilen** einer Datei.      | `tail -n 5 datei.txt` |
| `nano` | Einfacher **Texteditor** in der Kommandozeile. | `nano datei.txt`      |
| `vim`  | Fortgeschrittener Texteditor.                  | `vim datei.txt`       |


#### Beispiel mit `nano`:

1. Datei öffnen:
  ```bash
   nano datei.txt
  ```
2. Text eingeben.
3. Speichern: `Strg + O` (Enter bestätigen).
4. Beenden: `Strg + X`.

---

### 2.4 Suchen nach Dateien und Inhalten


| Befehl   | Beschreibung                                     | Beispiel                       |
| -------- | ------------------------------------------------ | ------------------------------ |
| `find`   | Sucht nach **Dateien/Verzeichnissen**.           | `find /home -name "datei.txt"` |
| `grep`   | Sucht nach **Textmustern** in Dateien.           | `grep "suchtext" datei.txt`    |
| `locate` | Schnelle Suche nach Dateien (Datenbank-basiert). | `locate datei.txt`             |


#### Beispiel:

```bash
# Suche nach allen .txt-Dateien im Home-Verzeichnis
find ~ -name "*.txt"

# Suche nach dem Wort "Linux" in einer Datei
grep "Linux" datei.txt

# Suche nach dem Wort "Linux" in allen Dateien im aktuellen Verzeichnis
grep -r "Linux" .
```

---

##  3. Berechtigungen und Eigentümer

### 3.1 Berechtigungen verstehen

Jede Datei und jedes Verzeichnis hat **Berechtigungen** für:

- **Besitzer (User)**
- **Gruppe (Group)**
- **Andere (Others)**

Die Berechtigungen werden in **3 Gruppen** unterteilt:

- **r (read)**: Lesen
- **w (write)**: Schreiben
- **x (execute)**: Ausführen

**Beispiel:**

```bash
ls -l datei.txt
```

Ausgabe:

```
-rw-r--r-- 1 benutzername benutzername 123 Mai  9 10:00 datei.txt
```

- `-rw-r--r--`:
  - **Besitzer**: `rw-` (Lesen + Schreiben)
  - **Gruppe**: `r--` (Nur Lesen)
  - **Andere**: `r--` (Nur Lesen)

### 3.2 Berechtigungen ändern (`chmod`)


| Befehl  | Beschreibung                                              | Beispiel              |
| ------- | --------------------------------------------------------- | --------------------- |
| `chmod` | Ändert die **Berechtigungen** einer Datei/Verzeichnisses. | `chmod 755 datei.txt` |


#### Symbolische Notation


| Symbol | Beschreibung            |
| ------ | ----------------------- |
| `u`    | Besitzer (User)         |
| `g`    | Gruppe (Group)          |
| `o`    | Andere (Others)         |
| `a`    | Alle (All)              |
| `+`    | Berechtigung hinzufügen |
| `-`    | Berechtigung entfernen  |
| `=`    | Berechtigung setzen     |


**Beispiele:**

```bash
# Füge Ausführungsrecht für den Besitzer hinzu
chmod u+x datei.txt

# Entferne Schreibrecht für die Gruppe
chmod g-w datei.txt

# Setze Berechtigungen für alle auf Lesen + Schreiben
chmod a=rw datei.txt
```

#### Numerische Notation


| Zahl | Berechtigung  |
| ---- | ------------- |
| 4    | Lesen (r)     |
| 2    | Schreiben (w) |
| 1    | Ausführen (x) |


**Beispiele:**

```bash
# Besitzer: rwx (7), Gruppe: r-x (5), Andere: r-x (5)
chmod 755 datei.txt

# Besitzer: rw- (6), Gruppe: r-- (4), Andere: --- (0)
chmod 640 datei.txt
```

### 3.3 Eigentümer und Gruppe ändern (`chown`, `chgrp`)


| Befehl  | Beschreibung                         | Beispiel                            |
| ------- | ------------------------------------ | ----------------------------------- |
| `chown` | Ändert den **Besitzer** einer Datei. | `sudo chown benutzername datei.txt` |
| `chgrp` | Ändert die **Gruppe** einer Datei.   | `sudo chgrp gruppenname datei.txt`  |


**Beispiel:**

```bash
# Besitzer und Gruppe ändern
sudo chown benutzername:gruppenname datei.txt
```

---

##  4. Umleitungen und Pipes

### 4.1 Umleitungen


| Symbol | Beschreibung                                 | Beispiel                        |
| ------ | -------------------------------------------- | ------------------------------- |
| `>`    | **Überschreibt** eine Datei mit der Ausgabe. | `echo "Hallo" > datei.txt`      |
| `>>`   | **Fügt** die Ausgabe an eine Datei an.       | `echo "Welt" >> datei.txt`      |
| `<`    | Liest die Eingabe aus einer Datei.           | `command < datei.txt`           |
| `2>`   | Leitet **Fehlermeldungen** in eine Datei um. | `ls /nonexistent 2> fehler.log` |


**Beispiel:**

```bash
# Erstelle eine Datei mit Inhalt
echo "Linux ist toll!" > motiv.txt

# Füge eine neue Zeile hinzu
echo "Ich lerne die Command-Line." >> motiv.txt
```

### 4.2 Pipes (`|`)

- **Pipes** leiten die Ausgabe eines Befehls als Eingabe an einen anderen Befehl weiter.
- **Beispiel:**
  ```bash
  # Zeige die ersten 5 Dateien im aktuellen Verzeichnis
  ls | head -n 5

  # Zähle die Anzahl der Dateien im Verzeichnis
  ls | wc -l
  ```

#### Nützliche Befehle für Pipes


| Befehl | Beschreibung                       |
| ------ | ---------------------------------- |
| `grep` | Filtert Zeilen nach einem Muster.  |
| `sort` | Sortiert Zeilen.                   |
| `wc`   | Zählt Zeilen, Wörter oder Zeichen. |
| `cut`  | Schneidet Teile aus Zeilen heraus. |


**Beispiel:**

```bash
# Zeige alle Benutzer im System, sortiert
cat /etc/passwd | cut -d: -f1 | sort

# Zähle, wie oft das Wort "Linux" in einer Datei vorkommt
grep -o "Linux" datei.txt | wc -l
```

---

##  5. Variablen und Umgebungsvariablen

### 5.1 Variablen in der Shell

- **Variablen** speichern Werte für die aktuelle Shell-Sitzung.
- **Syntax:**
  ```bash
  VARIABLE="Wert"
  echo $VARIABLE
  ```

**Beispiel:**

```bash
# Variable erstellen
NAME="Sadik"
echo "Hallo, $NAME!"

# Variable überschreiben
NAME="Max"
echo "Jetzt heißt du $NAME."
```

### 5.2 Umgebungsvariablen


- **Wichtige Umgebungsvariablen:**

  | Variable | Beschreibung                                                              |
  | -------- | ------------------------------------------------------------------------- |
  | `$HOME`  | Home-Verzeichnis des aktuellen Benutzers.                                 |
  | `$USER`  | Aktueller Benutzername.                                                   |
  | `$PWD`   | Aktuelles Arbeitsverzeichnis.                                             |
  | `$PATH`  | Liste der Verzeichnisse, in denen nach ausführbaren Dateien gesucht wird. |


**Beispiel:**

```bash
# Zeige das Home-Verzeichnis an
echo $HOME

# Zeige den aktuellen Benutzernamen an
echo $USER

# Zeige den Pfad an
echo $PATH
```

### 5.3 Variablen dauerhaft setzen

- Um Variablen **dauerhaft** zu setzen, füge sie in die **Shell-Konfigurationsdatei** ein:
  - **Bash**: `~/.bashrc` oder `~/.bash_profile`
  - **Zsh**: `~/.zshrc`

**Beispiel:**

```bash
# Öffne die .bashrc-Datei
nano ~/.bashrc

# Füge am Ende die Zeile hinzu
export MEINE_VARIABLE="Wert"

# Lade die Änderungen
source ~/.bashrc
```



##  6. Übungsaufgaben

###  Übung 1: Navigation und Dateiverwaltung

1. **Wechsle** in dein Home-Verzeichnis.
2. **Erstelle** ein Verzeichnis namens `linux_übungen`.
3. **Wechsle** in das Verzeichnis `linux_übungen`.
4. **Erstelle** eine Datei namens `notizen.txt` mit dem Inhalt:
  ```
   Linux Command-Line Übungen
   Datum: [aktuelles Datum]
  ```
5. **Kopiere** die Datei `notizen.txt` in ein neues Verzeichnis namens `backup`.
6. **Benenne** die Datei `notizen.txt` in `meine_notizen.txt` um.
7. **Lösche** das Verzeichnis `backup` inkl. Inhalt.

??? success "Lösung"
    ```bash
        cd ~
        mkdir linux_übungen
        cd linux_übungen
        echo "Linux Command-Line Übungen" > notizen.txt
        echo "Datum: $(date)" >> notizen.txt
        mkdir backup
        cp notizen.txt backup/
        mv notizen.txt meine_notizen.txt
        rm -r backup/
    ```



###  Übung 2: Berechtigungen

1. **Erstelle** eine Datei namens `geheim.txt` mit dem Inhalt:
  ```
   Dies ist eine geheime Datei.
  ```
2. **Ändere** die Berechtigungen so, dass:
  - Der **Besitzer** Lesen und Schreiben darf.
  - Die **Gruppe** nur Lesen darf.
  - **Andere** keine Berechtigungen haben.
3. **Erstelle** einen neuen Benutzer namens `testuser` (mit `sudo useradd -m testuser`).
4. **Ändere** den Besitzer der Datei `geheim.txt` zu `testuser`.
5. **Versuche**, die Datei als dein normaler Benutzer zu lesen und zu bearbeiten. Was passiert?

??? success "Lösung"
    ```bash
    echo "Dies ist eine geheime Datei." > geheim.txt
    chmod 640 geheim.txt
    sudo useradd -m testuser
    sudo chown testuser geheim.txt
    # Versuch, die Datei zu lesen/bearbeiten:
    cat geheim.txt  # Funktioniert nicht, da keine Leseberechtigung für "Andere"
    nano geheim.txt # Funktioniert nicht, da keine Schreibberechtigung für "Andere"
    ```



###  Übung 3: Suchen und Filtern

1. **Erstelle** im Verzeichnis `linux_übungen` folgende Dateien:
  - `linux.txt` mit dem Inhalt:
  - `windows.txt` mit dem Inhalt:
    ```
    Windows ist ein Betriebssystem von Microsoft.
    Es ist Closed Source.
    ```
2. **Suche** nach allen Dateien, die das Wort **"Betriebssystem"** enthalten.
3. **Filtere** die Ausgabe so, dass nur die **Dateinamen** angezeigt werden.
4. **Zähle**, wie oft das Wort **"Linux"** in allen `.txt`-Dateien vorkommt.

??? success "Lösung"
    ```bash
    mkdir -p linux_übungen
    cd linux_übungen
    echo -e "Linux ist ein Betriebssystem.\nEs ist Open Source.\nLinux ist stabil und sicher." > linux.txt
    echo -e "Windows ist ein Betriebssystem von Microsoft.\nEs ist Closed Source." > windows.txt
    grep -l "Betriebssystem" *.txt
    grep -l "Betriebssystem" *.txt | cut -d: -f1
    grep -o "Linux" *.txt | wc -l
    ```



###  Übung 4: Umleitungen und Pipes

1. **Erstelle** eine Datei namens `log.txt` und leite die Ausgabe des Befehls `date` in diese Datei um.
2. **Füge** die Ausgabe des Befehls `whoami` an die Datei `log.txt` an.
3. **Zeige** die ersten 3 Zeilen der Datei `/etc/passwd` an.
4. **Leite** die Fehlermeldung des Befehls `ls /nonexistent` in eine Datei namens `fehler.log` um.

??? success "Lösung"
    ```bash
    date > log.txt
    whoami >> log.txt
    head -n 3 /etc/passwd
    ls /nonexistent 2> fehler.log
    ```



###  Übung 5: Variablen

1. **Erstelle** eine Variable namens `BEGRÜSSUNG` mit dem Wert `"Hallo, Linux!"`.
2. **Gib** den Wert der Variable aus.
3. **Erstelle** eine neue Variable namens `BENUTZER` und weise ihr den Wert deines Benutzernamens zu (mit dem Befehl `whoami`).
4. **Gib** eine personalisierte Begrüßung aus, z. B.:
  ```
   Hallo, [Dein Benutzername]! Willkommen zur Command-Line.
  ```
5. **Füge** die Variable `BEGRÜSSUNG` zu deiner `~/.bashrc`-Datei hinzu, damit sie bei jedem Terminal-Start verfügbar ist.

??? success "Lösung"
    ```bash
    BEGRÜSSUNG="Hallo, Linux!"
    echo $BEGRÜSSUNG
    BENUTZER=$(whoami)
    echo "Hallo, $BENUTZER! Willkommen zur Command-Line."
    echo "export BEGRÜSSUNG=\"$BEGRÜSSUNG\"" >> ~/.bashrc
    source ~/.bashrc
    ```



###  Übung 6: Kombinierte Aufgaben

1. **Erstelle** ein Verzeichnis namens `projekte` in deinem Home-Verzeichnis.
2. **Wechsle** in das Verzeichnis `projekte`.
3. **Erstelle** eine Datei namens `projekt1.txt` mit dem Inhalt:
  ```
   Projekt 1: Command-Line Grundlagen
   Status: In Arbeit
  ```
4. **Erstelle** eine Kopie der Datei namens `projekt1_backup.txt`.
5. **Ändere** die Berechtigungen der Datei `projekt1.txt` so, dass nur der Besitzer Lesen und Schreiben darf.
6. **Suche** nach allen Dateien im Verzeichnis `projekte`, die das Wort **"Projekt"** enthalten, und leite die Ausgabe in eine Datei namens `suchergebnis.txt` um.
7. **Lösche** die Datei `projekt1_backup.txt`.

??? success "Lösung"
    ```bash
    mkdir ~/projekte
    cd ~/projekte
    echo -e "Projekt 1: Command-Line Grundlagen\nStatus: In Arbeit" > projekt1.txt
    cp projekt1.txt projekt1_backup.txt
    chmod 600 projekt1.txt
    grep -l "Projekt" * > suchergebnis.txt
    rm projekt1_backup.txt
    ```


##  8. Zusammenfassung und Tipps

###  Wichtige Befehle im Überblick


| Kategorie             | Befehle                                      |
| --------------------- | -------------------------------------------- |
| **Navigation**        | `pwd`, `ls`, `cd`                            |
| **Dateiverwaltung**   | `touch`, `mkdir`, `cp`, `mv`, `rm`, `rmdir`  |
| **Dateiinhalte**      | `cat`, `less`, `head`, `tail`, `nano`, `vim` |
| **Suche**             | `find`, `grep`, `locate`                     |
| **Berechtigungen**    | `chmod`, `chown`, `chgrp`                    |
| **Umleitungen/Pipes** | `>`, `>>`, `<`, `2>`, `                      |
| **Variablen**         | `echo $VAR`, `export VAR=Wert`               |


###  Tipps für die Command-Line

1. **Tab-Vervollständigung**: Tippe den Anfang eines Befehls oder Dateinamens und drücke `Tab`, um automatisch zu vervollständigen.
2. **History**: Nutze `↑` und `↓`, um durch vorherige Befehle zu navigieren.
3. **Man-Pages**: Nutze `man befehl` (z. B. `man ls`), um die Dokumentation eines Befehls anzuzeigen.
4. **Aliase**: Erstelle Abkürzungen für häufig verwendete Befehle in deiner `~/.bashrc`:
  ```bash
   alias ll='ls -lh'
   alias update='sudo apt update && sudo apt upgrade -y'
  ```
5. **Fehler analysieren**: Wenn ein Befehl nicht funktioniert, lies die Fehlermeldung genau und suche nach Lösungen mit `man` oder im Internet.
