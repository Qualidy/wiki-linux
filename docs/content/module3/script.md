#  Modul III.4: Befehle in ein Skript umwandeln

##  Einleitung

Das **Umwandeln von Befehlen in ein Skript** ist ein entscheidender Schritt, um **wiederkehrende Aufgaben zu automatisieren** und **komplexe Abläufe zu vereinfachen**. Ein Skript ist eine **Sammlung von Befehlen**, die in einer Datei gespeichert und als Programm ausgeführt werden können.

In diesem Modul lernst du:

- Wie du **einfache Bash-Skripte** erstellst.
- Wie du **Variablen, Bedingungen und Schleifen** in Skripten verwendest.
- Wie du **Benutzereingaben** und **Argumenten** verarbeitest.
- **Best Practices** für die Skripterstellung.
- **Fehlerbehandlung** und **Debugging** in Skripten.



##  1. Grundlagen von Bash-Skripten

### 1.1 Was ist ein Bash-Skript?

- Ein **Bash-Skript** ist eine **Textdatei**, die eine Reihe von **Bash-Befehlen** enthält.
- Die Datei wird von der **Bash-Shell** interpretiert und ausgeführt.
- Skripte ermöglichen:
  - **Automatisierung** von wiederkehrenden Aufgaben.
  - **Komplexe Logik** (Bedingungen, Schleifen, Funktionen).
  - **Wiederverwendbarkeit** von Code.

---

### 1.2 Erstes Skript erstellen

#### Schritt 1: Skriptdatei erstellen

- Erstelle eine Datei mit der Endung `.sh` (z. B. `mein_skript.sh`).
- Nutze einen **Texteditor** wie `nano`, `vim` oder `gedit`.

    **Beispiel:**

    ```
    nano mein_skript.sh
    ```

#### Schritt 2: Shebang hinzufügen

- Die **erste Zeile** eines Skripts sollte die **Shebang** (`#!`) enthalten, die angibt, welche Shell das Skript ausführen soll.
- Für Bash-Skripte:
  ```bash
  #!/bin/bash
  ```

#### Schritt 3: Befehle hinzufügen

- Füge die **Befehle** hinzu, die das Skript ausführen soll.

    **Beispiel:**

    ```bash
    #!/bin/bash
    echo "Hallo, Welt!"
    date
    ```

#### Schritt 4: Skript ausführbar machen

- Nutze `chmod`, um die **Ausführungsrechte** zu setzen:
  ```
  chmod +x mein_skript.sh
  ```

#### Schritt 5: Skript ausführen

- Führe das Skript aus, indem du den **Pfad zur Datei** angibst:
  ```bash
  ./mein_skript.sh
  ```
  - `./` bedeutet: "Führe die Datei im **aktuellen Verzeichnis** aus."


### 1.3 Beispiel: Einfaches Skript

**Skriptname:** `begrüßung.sh`

```bash
#!/bin/bash
# Ein einfaches Begrüßungsskript

echo "Hallo, $USER!"
echo "Heute ist $(date +%A), der $(date +%d.%m.%Y)."
echo "Aktuelles Verzeichnis: $(pwd)"
```

**Ausführung:**

```bash
chmod +x begrüßung.sh
./begrüßung.sh
```

**Ausgabe:**

```
Hallo, Sadik!
Heute ist Montag, der 11.05.2026.
Aktuelles Verzeichnis: /home/sadik
```



## 2. Variablen in Skripten

### 2.1 Was sind Variablen?

- **Variablen** speichern **Werte**, die in einem Skript verwendet werden können.
- Variablen werden **ohne Leerzeichen** zugewiesen:
  ```bash
  VARIABLE="Wert"
  ```
- Auf Variablen wird mit `$` zugegriffen:
  ```bash
  echo $VARIABLE
  ```



### 2.2 Arten von Variablen


| Typ                              | Beschreibung                                                               | Beispiel                     |
| -------------------------------- | -------------------------------------------------------------------------- | ---------------------------- |
| **Benutzerdefinierte Variablen** | Vom Skriptautor definiert.                                                 | `NAME="Sadik"`               |
| **Umgebungsvariablen**           | Vom System bereitgestellt (z. B. `$USER`, `$HOME`, `$PATH`).               | `echo $HOME`                 |
| **Positionale Parameter**        | Argumente, die beim Aufruf des Skripts übergeben werden (`$1`, `$2`, ...). | `echo $1` (erstes Argument)  |
| **Spezielle Variablen**          | Von der Shell bereitgestellt (z. B. `$0`, `$#`, `$?`).                     | `echo $0` (Name des Skripts) |



### 2.3 Spezielle Variablen in Bash


| Variable        | Beschreibung                                                             | Beispiel                                  |
| --------------- | ------------------------------------------------------------------------ | ----------------------------------------- |
| `$0`            | Name des Skripts.                                                        | `echo "Skriptname: $0"`                   |
| `$1`, `$2`, ... | **Positionale Parameter** (Argumente, die beim Aufruf übergeben werden). | `echo "Erstes Argument: $1"`              |
| `$#`            | Anzahl der **übergebenen Argumente**.                                    | `echo "Anzahl Argumente: $#"`             |
| `$*`            | Alle Argumente als **eine Zeichenkette**.                                | `echo "Alle Argumente: $*"`               |
| `$@`            | Alle Argumente als **einzelne Zeichenketten** (für Schleifen geeignet).  | `for arg in "$@"; do echo "$arg"; done`   |
| `$?`            | **Rückgabewert** des letzten Befehls (`0` = Erfolg, `≠ 0` = Fehler).     | `if [ $? -eq 0 ]; then echo "Erfolg"; fi` |
| `$$`            | **Prozess-ID (PID)** des aktuellen Skripts.                              | `echo "PID: $$"`                          |
| `$USER`         | Aktueller Benutzername.                                                  | `echo "Benutzer: $USER"`                  |
| `$HOME`         | Home-Verzeichnis des aktuellen Benutzers.                                | `echo "Home: $HOME"`                      |
| `$PWD`          | Aktuelles Arbeitsverzeichnis.                                            | `echo "Verzeichnis: $PWD"`                |


### 2.4 Praxisbeispiele mit Variablen

#### Beispiel 1: Benutzerdefinierte Variablen

```bash
#!/bin/bash
NAME="Sadik"
ALTER=30
echo "Hallo, $NAME! Du bist $ALTER Jahre alt."
```

#### Beispiel 2: Umgebungsvariablen

```bash
#!/bin/bash
echo "Benutzer: $USER"
echo "Home-Verzeichnis: $HOME"
echo "Aktuelles Verzeichnis: $PWD"
```

#### Beispiel 3: Positionale Parameter

```bash
#!/bin/bash
echo "Skriptname: $0"
echo "Erstes Argument: $1"
echo "Zweites Argument: $2"
echo "Anzahl Argumente: $#"
```

**Aufruf:**

```bash
./skript.sh Hallo Welt
```

**Ausgabe:**

```
Skriptname: ./skript.sh
Erstes Argument: Hallo
Zweites Argument: Welt
Anzahl Argumente: 2
```

#### Beispiel 4: Rückgabewert prüfen

```bash
#!/bin/bash
ls /nonexistent
if [ $? -eq 0 ]; then
  echo "Verzeichnis existiert."
else
  echo "Verzeichnis existiert nicht."
fi
```



### 2.5 Variablen und Benutzereingaben

- Mit `read` kannst du **Benutzereingaben** in einer Variablen speichern.

**Beispiel:**

```bash
#!/bin/bash
echo "Wie heißt du?"
read NAME
echo "Hallo, $NAME!"
```

**Beispiel mit Passwortabfrage (unsichtbare Eingabe):**

```bash
#!/bin/bash
read -s -p "Gib dein Passwort ein: " PASSWORT
echo
echo "Passwort eingegeben (wird nicht angezeigt)."
```



##  3. Bedingungen in Skripten

### 3.1 `if`-Bedingungen

- `**if`-Bedingungen** ermöglichen es, **verschiedene Aktionen** basierend auf einer Bedingung auszuführen.

#### Grundlegende Syntax:

```bash
if [ Bedingung ]; then
  # Befehle, wenn Bedingung wahr ist
elif [ Bedingung ]; then
  # Befehle, wenn die erste Bedingung falsch ist, aber die zweite wahr ist
else
  # Befehle, wenn keine Bedingung wahr ist
fi
```



### 3.2 Vergleichsoperatoren

#### Für **Zeichenketten**:


| Operator | Beschreibung                                  | Beispiel           |
| -------- | --------------------------------------------- | ------------------ |
| `=`      | **Gleich** (Achtung: **kein `==**` in Bash!). | `[ "$A" = "$B" ]`  |
| `!=`     | **Ungleich**.                                 | `[ "$A" != "$B" ]` |
| `-z`     | **Zeichenkette ist leer**.                    | `[ -z "$A" ]`      |
| `-n`     | **Zeichenkette ist nicht leer**.              | `[ -n "$A" ]`      |


#### Für **Zahlen**:


| Operator | Beschreibung             | Beispiel        |
| -------- | ------------------------ | --------------- |
| `-eq`    | **Gleich**.              | `[ $A -eq $B ]` |
| `-ne`    | **Ungleich**.            | `[ $A -ne $B ]` |
| `-lt`    | **Kleiner als**.         | `[ $A -lt $B ]` |
| `-le`    | **Kleiner oder gleich**. | `[ $A -le $B ]` |
| `-gt`    | **Größer als**.          | `[ $A -gt $B ]` |
| `-ge`    | **Größer oder gleich**.  | `[ $A -ge $B ]` |


#### Für **Dateien**:


| Operator | Beschreibung                                     | Beispiel                |
| -------- | ------------------------------------------------ | ----------------------- |
| `-e`     | **Datei existiert**.                             | `[ -e "$DATEI" ]`       |
| `-f`     | **Datei existiert und ist eine reguläre Datei**. | `[ -f "$DATEI" ]`       |
| `-d`     | **Datei existiert und ist ein Verzeichnis**.     | `[ -d "$VERZEICHNIS" ]` |
| `-s`     | **Datei existiert und ist nicht leer**.          | `[ -s "$DATEI" ]`       |
| `-r`     | **Datei existiert und ist lesbar**.              | `[ -r "$DATEI" ]`       |
| `-w`     | **Datei existiert und ist beschreibbar**.        | `[ -w "$DATEI" ]`       |
| `-x`     | **Datei existiert und ist ausführbar**.          | `[ -x "$DATEI" ]`       |




### 3.3 Logische Operatoren


| Operator | Beschreibung         | Beispiel                        |
| -------- | -------------------- | ------------------------------- |
| `&&`     | **Logisches UND**.   | `[ $A -gt 0 ] && [ $B -lt 10 ]` |
| `||`     | **Logisches ODER**.  | `[ $A -eq 0 ] || [ $B -eq 0 ]`  |
| `!`      | **Logisches NICHT**. | `[ ! -f "$DATEI" ]`             |




### 3.4 Praxisbeispiele mit Bedingungen

#### Beispiel 1: Einfache `if`-Bedingung

```bash
#!/bin/bash
if [ "$USER" = "root" ]; then
  echo "Du bist der Root-Benutzer."
else
  echo "Du bist kein Root-Benutzer."
fi
```

#### Beispiel 2: Zahlen vergleichen

```bash
#!/bin/bash
A=10
B=20
if [ $A -lt $B ]; then
  echo "$A ist kleiner als $B."
elif [ $A -eq $B ]; then
  echo "$A ist gleich $B."
else
  echo "$A ist größer als $B."
fi
```

#### Beispiel 3: Datei prüfen

```bash
#!/bin/bash
DATEI="/etc/passwd"
if [ -f "$DATEI" ]; then
  echo "$DATEI existiert und ist eine Datei."
elif [ -d "$DATEI" ]; then
  echo "$DATEI existiert und ist ein Verzeichnis."
else
  echo "$DATEI existiert nicht."
fi
```

#### Beispiel 4: Logische Operatoren

```bash
#!/bin/bash
ALTER=25
if [ $ALTER -ge 18 ] && [ $ALTER -le 65 ]; then
  echo "Du bist im erwerbsfähigen Alter."
else
  echo "Du bist nicht im erwerbsfähigen Alter."
fi
```

#### Beispiel 5: Benutzereingabe prüfen

```bash
#!/bin/bash
read -p "Gib eine Zahl ein: " ZAHL
if [ $ZAHL -gt 0 ]; then
  echo "$ZAHL ist positiv."
elif [ $ZAHL -lt 0 ]; then
  echo "$ZAHL ist negativ."
else
  echo "$ZAHL ist null."
fi
```



### 3.5 `case`-Anweisungen

- `**case`-Anweisungen** sind eine Alternative zu `if-elif-else` für **mehrere Bedingungen**.

#### Grundlegende Syntax:

```bash
case "$VARIABLE" in
  Muster1)
    # Befehle für Muster1
    ;;
  Muster2)
    # Befehle für Muster2
    ;;
  *)
    # Standardfall (wenn kein Muster passt)
    ;;
esac
```

#### Beispiel:

```bash
#!/bin/bash
read -p "Wähle eine Option (a/b/c): " OPTION
case "$OPTION" in
  a)
    echo "Du hast Option A gewählt."
    ;;
  b)
    echo "Du hast Option B gewählt."
    ;;
  c)
    echo "Du hast Option C gewählt."
    ;;
  *)
    echo "Ungültige Option."
    ;;
esac
```



##  4. Schleifen in Skripten

### 4.1 `for`-Schleifen

- `for`-Schleifen** führen eine **Aktion für jedes Element in einer Liste** aus.

#### Grundlegende Syntax:

```bash
for VARIABLE in Liste; do
  # Befehle
done
```

#### Beispiel 1: Einfache `for`-Schleife

```bash
#!/bin/bash
for NAME in Alice Bob Charlie; do
  echo "Hallo, $NAME!"
done
```

#### Beispiel 2: `for`-Schleife mit Bereich

```bash
#!/bin/bash
for i in {1..5}; do
  echo "Zahl: $i"
done
```

#### Beispiel 3: `for`-Schleife mit Dateien

```bash
#!/bin/bash
for DATEI in *.txt; do
  echo "Verarbeite Datei: $DATEI"
done
```

#### Beispiel 4: `for`-Schleife mit `seq`

```bash
#!/bin/bash
for i in $(seq 1 10); do
  echo "Zahl: $i"
done
```

#### Beispiel 5: `for`-Schleife mit Positionalen Parametern

```bash
#!/bin/bash
for ARG in "$@"; do
  echo "Argument: $ARG"
done
```


### 4.2 `while`-Schleifen

- `while`-Schleifen** führen eine **Aktion aus, solange eine Bedingung wahr ist**.

#### Grundlegende Syntax:

```bash
while [ Bedingung ]; do
  # Befehle
done
```

#### Beispiel 1: Einfache `while`-Schleife

```bash
#!/bin/bash
ZAHL=1
while [ $ZAHL -le 5 ]; do
  echo "Zahl: $ZAHL"
  ZAHL=$((ZAHL + 1))
done
```

#### Beispiel 2: `while`-Schleife mit Benutzereingabe

```bash
#!/bin/bash
read -p "Gib eine Zahl ein (0 zum Beenden): " ZAHL
while [ $ZAHL -ne 0 ]; do
  echo "Du hast $ZAHL eingegeben."
  read -p "Gib eine weitere Zahl ein (0 zum Beenden): " ZAHL
done
echo "Programm beendet."
```

#### Beispiel 3: `while`-Schleife mit Datei-Inhalt

```bash
#!/bin/bash
while read ZEILE; do
  echo "Zeile: $ZEILE"
done < datei.txt
```



### 4.3 `until`-Schleifen

- `until`-Schleifen** führen eine **Aktion aus, bis eine Bedingung wahr ist** (Gegenteil von `while`).

#### Grundlegende Syntax:

```bash
until [ Bedingung ]; do
  # Befehle
done
```

#### Beispiel:

```bash
#!/bin/bash
ZAHL=1
until [ $ZAHL -gt 5 ]; do
  echo "Zahl: $ZAHL"
  ZAHL=$((ZAHL + 1))
done
```



### 4.4 Schleifen steuern


| Befehl     | Beschreibung                                                                      | Beispiel                             |
| ---------- | --------------------------------------------------------------------------------- | ------------------------------------ |
| `break`    | **Beendet die Schleife** sofort.                                                  | `if [ $i -eq 3 ]; then break; fi`    |
| `continue` | **Überspringt den Rest der aktuellen Iteration** und fährt mit der nächsten fort. | `if [ $i -eq 3 ]; then continue; fi` |


#### Beispiel:

```bash
#!/bin/bash
for i in {1..5}; do
  if [ $i -eq 3 ]; then
    continue  # Überspringt die 3
  fi
  echo "Zahl: $i"
done
```



##  5. Funktionen in Skripten

### 5.1 Was sind Funktionen?

- **Funktionen** sind **wiederverwendbare Codeblöcke**, die du in deinem Skript definieren kannst.
- Funktionen ermöglichen:
  - **Modularisierung** von Code.
  - **Wiederverwendbarkeit** von Logik.
  - **Bessere Lesbarkeit** des Skripts.



### 5.2 Grundlegende Syntax von Funktionen

```bash
funktionsname() {
  # Befehle
}
```

#### Beispiel 1: Einfache Funktion

```bash
#!/bin/bash
begrüßen() {
  echo "Hallo, $1!"
}

begrüßen "Sadik"
begrüßen "Alice"
```

#### Beispiel 2: Funktion mit Rückgabewert

```bash
#!/bin/bash
addieren() {
  local ERGEBNIS=$(( $1 + $2 ))
  echo $ERGEBNIS
}

SUMME=$(addieren 5 3)
echo "5 + 3 = $SUMME"
```

- `local`: Deklariert eine **lokale Variable**, die nur innerhalb der Funktion gültig ist.
- `echo`: Gibt den Rückgabewert der Funktion zurück.

#### Beispiel 3: Funktion mit Standardwerten

```bash
#!/bin/bash
begrüßen() {
  local NAME=${1:-"Gast"}  # Standardwert: "Gast"
  echo "Hallo, $NAME!"
}

begrüßen "Sadik"
begrüßen  # Gibt "Hallo, Gast!" aus
```



### 5.3 Funktionen mit Rückgabewerten

- In Bash geben Funktionen **keinen Rückgabewert** wie in anderen Programmiersprachen zurück.
- Stattdessen kannst du:
  - `**echo**` verwenden, um einen Wert zurückzugeben.
  - `**return**` verwenden, um einen **Exit-Code** (0-255) zurückzugeben.

#### Beispiel:

```bash
#!/bin/bash
ist_gerade() {
  if [ $(( $1 % 2 )) -eq 0 ]; then
    echo "Ja"
  else
    echo "Nein"
  fi
}

ERGEBNIS=$(ist_gerade 4)
echo "Ist 4 gerade? $ERGEBNIS"
```



##  6. Argumente und Optionen verarbeiten

### 6.1 Positionale Parameter

- **Positionale Parameter** (`$1`, `$2`, ...) sind die **Argumente**, die beim Aufruf des Skripts übergeben werden.

#### Beispiel:

```bash
#!/bin/bash
echo "Skriptname: $0"
echo "Erstes Argument: $1"
echo "Zweites Argument: $2"
echo "Alle Argumente: $@"
```

**Aufruf:**

```bash
./skript.sh Hallo Welt
```



### 6.2 `getopts` für Optionen

- `**getopts**` ermöglicht das **Parsen von Kommandozeilenoptionen** (z. B. `-h`, `-v`).

#### Grundlegende Syntax:

```bash
while getopts "Optionen" OPT; do
  case "$OPT" in
    OPTION1)
      # Befehle für Option1
      ;;
    OPTION2)
      # Befehle für Option2
      ;;
    *)
      echo "Unbekannte Option: $OPT"
      ;;
  esac
done
```

#### Beispiel:

```bash
#!/bin/bash
while getopts "hvn:" OPT; do
  case "$OPT" in
    h)
      echo "Hilfemenü:"
      echo "  -h: Hilfe anzeigen"
      echo "  -v: Verbose-Modus aktivieren"
      echo "  -n NAME: Name angeben"
      exit 0
      ;;
    v)
      VERBOSE=1
      ;;
    n)
      NAME="$OPTARG"
      ;;
    *)
      echo "Unbekannte Option: $OPT"
      exit 1
      ;;
  esac
done

if [ -n "$VERBOSE" ]; then
  echo "Verbose-Modus aktiviert."
fi

if [ -n "$NAME" ]; then
  echo "Hallo, $NAME!"
else
  echo "Kein Name angegeben."
fi
```

**Aufruf:**

```bash
./skript.sh -h
./skript.sh -v -n "Sadik"
```



### 6.3 `shift` für die Verarbeitung aller Argumente

- `**shift**` verschiebt die **positionalen Parameter** um eine Position nach links.
- Nützlich, um **alle Argumente in einer Schleife** zu verarbeiten.

#### Beispiel:

```bash
#!/bin/bash
while [ $# -gt 0 ]; do
  echo "Argument: $1"
  shift
done
```



##  7. Fehlerbehandlung und Debugging

### 7.1 Rückgabewerte prüfen

- Jeder Befehl gibt einen **Rückgabewert** (`Exit-Code`) zurück:
  - `0`: Erfolg.
  - `1-255`: Fehler (je nach Befehl).

#### Beispiel:

```bash
#!/bin/bash
if [ ! -f "datei.txt" ]; then
  echo "Fehler: datei.txt existiert nicht."
  exit 1
fi
```



### 7.2 `set -e` für automatische Fehlerbehandlung

- `**set -e**` beendet das Skript **sofort**, wenn ein Befehl einen Fehler zurückgibt.

#### Beispiel:

```bash
#!/bin/bash
set -e  # Beende das Skript bei Fehlern

# Dieser Befehl wird nur ausgeführt, wenn der vorherige erfolgreich war
ls /nonexistent
echo "Diese Zeile wird nicht ausgeführt."
```



### 7.3 `trap` für Signalbehandlung

- `**trap**` ermöglicht es, **Signale** (z. B. `SIGINT` für `Strg+C`) abzufangen und zu behandeln.

#### Beispiel:

```bash
#!/bin/bash
# Fange Strg+C ab
trap 'echo "Skript wurde durch Strg+C abgebrochen."; exit 1' SIGINT

echo "Drücke Strg+C, um das Skript abzubrechen."
sleep 10
echo "Skript wurde erfolgreich beendet."
```


### 7.4 Debugging mit `set -x`

- `**set -x**` aktiviert den **Debug-Modus**, der jeden ausgeführten Befehl anzeigt.

#### Beispiel:

```bash
#!/bin/bash
set -x  # Debug-Modus aktivieren

echo "Hallo"
DATEI="datei.txt"
ls $DATEI

set +x  # Debug-Modus deaktivieren
echo "Debug-Modus deaktiviert."
```

-

### 7.5 Logging in Skripten

- Nutze `**echo` oder `logger**`, um **Log-Nachrichten** in dein Skript einzufügen.

#### Beispiel:

```bash
#!/bin/bash
LOG_DATEI="skript.log"

echo "Skript gestartet: $(date)" >> "$LOG_DATEI"

# Skript-Logik hier

echo "Skript beendet: $(date)" >> "$LOG_DATEI"
```



##  8. Praktische Beispiele: Befehle in Skripte umwandeln

### 8.1 Beispiel 1: Backup-Skript

**Aufgabe:** Erstelle ein Skript, das ein **Backup eines Verzeichnisses** erstellt und in ein Zielverzeichnis kopiert.

**Skriptname:** `backup.sh`

```bash
#!/bin/bash

# Überprüfe, ob Quelle und Ziel angegeben wurden
if [ $# -ne 2 ]; then
  echo "Verwendung: $0 <Quelle> <Ziel>"
  exit 1
fi

QUELLE="$1"
ZIEL="$2"
DATUM=$(date +%Y-%m-%d_%H-%M-%S)
BACKUP_NAME="backup_$DATUM.tar.gz"

# Überprüfe, ob die Quelle existiert
if [ ! -d "$QUELLE" ]; then
  echo "Fehler: Quelle '$QUELLE' existiert nicht oder ist kein Verzeichnis."
  exit 1
fi

# Erstelle das Zielverzeichnis, falls es nicht existiert
mkdir -p "$ZIEL"

# Erstelle das Backup
echo "Erstelle Backup von $QUELLE..."
tar -czvf "$ZIEL/$BACKUP_NAME" "$QUELLE"

if [ $? -eq 0 ]; then
  echo "Backup erfolgreich erstellt: $ZIEL/$BACKUP_NAME"
else
  echo "Fehler beim Erstellen des Backups."
  exit 1
fi
```

**Aufruf:**

```bash
./backup.sh ~/dokumente /backup
```

---

### 8.2 Beispiel 2: Log-Analyse-Skript

**Aufgabe:** Erstelle ein Skript, das **Fehler in einer Log-Datei zählt** und die **häufigsten Fehler** anzeigt.

**Skriptname:** `log_analyse.sh`

```bash
#!/bin/bash

# Überprüfe, ob eine Log-Datei angegeben wurde
if [ $# -ne 1 ]; then
  echo "Verwendung: $0 <Log-Datei>"
  exit 1
fi

LOG_DATEI="$1"

# Überprüfe, ob die Log-Datei existiert
if [ ! -f "$LOG_DATEI" ]; then
  echo "Fehler: Log-Datei '$LOG_DATEI' existiert nicht."
  exit 1
fi

# Zähle die Anzahl der Fehler
FEHLER_ANZAHL=$(grep -c "error" "$LOG_DATEI")
echo "Anzahl der Fehler: $FEHLER_ANZAHL"

# Zeige die 10 häufigsten Fehler an
echo -e "\nHäufigste Fehler:"
grep "error" "$LOG_DATEI" | awk '{print $5}' | sort | uniq -c | sort -nr | head -n 10
```

**Aufruf:**

```bash
./log_analyse.sh /var/log/syslog
```

---

### 8.3 Beispiel 3: Benutzerverwaltungsskript

**Aufgabe:** Erstelle ein Skript, das **Benutzer hinzufügt, löscht oder auflistet**.

**Skriptname:** `benutzer_verwalten.sh`

```bash
#!/bin/bash

# Hilfemenü
hilfe() {
  echo "Verwendung: $0 [OPTION] [BENUTZERNAME]"
  echo "Optionen:"
  echo "  -a, --add    Benutzer hinzufügen"
  echo "  -d, --delete Benutzer löschen"
  echo "  -l, --list   Benutzer auflisten"
  exit 0
}

# Benutzer hinzufügen
benutzer_hinzufügen() {
  if [ -z "$1" ]; then
    echo "Fehler: Kein Benutzername angegeben."
    exit 1
  fi
  sudo useradd -m "$1"
  if [ $? -eq 0 ]; then
    echo "Benutzer '$1' wurde erfolgreich hinzugefügt."
  else
    echo "Fehler: Benutzer '$1' konnte nicht hinzugefügt werden."
    exit 1
  fi
}

# Benutzer löschen
benutzer_löschen() {
  if [ -z "$1" ]; then
    echo "Fehler: Kein Benutzername angegeben."
    exit 1
  fi
  sudo userdel -r "$1"
  if [ $? -eq 0 ]; then
    echo "Benutzer '$1' wurde erfolgreich gelöscht."
  else
    echo "Fehler: Benutzer '$1' konnte nicht gelöscht werden."
    exit 1
  fi
}

# Benutzer auflisten
benutzer_auflisten() {
  echo "Benutzer auf diesem System:"
  cut -d":" -f1 /etc/passwd
}

# Hauptprogramm
if [ $# -eq 0 ]; then
  hilfe
fi

case "$1" in
  -a|--add)
    benutzer_hinzufügen "$2"
    ;;
  -d|--delete)
    benutzer_löschen "$2"
    ;;
  -l|--list)
    benutzer_auflisten
    ;;
  -h|--help)
    hilfe
    ;;
  *)
    echo "Unbekannte Option: $1"
    hilfe
    ;;
esac
```

**Aufruf:**

```bash
./benutzer_verwalten.sh --add testuser
./benutzer_verwalten.sh --list
./benutzer_verwalten.sh --delete testuser
```

---

### 8.4 Beispiel 4: Datei-Suchskript

**Aufgabe:** Erstelle ein Skript, das **Dateien nach einem Muster sucht** und die Ergebnisse in einer Datei speichert.

**Skriptname:** `datei_suche.sh`

```bash
#!/bin/bash

# Überprüfe, ob Suchmuster und Verzeichnis angegeben wurden
if [ $# -ne 2 ]; then
  echo "Verwendung: $0 <Suchmuster> <Verzeichnis>"
  exit 1
fi

MUSTER="$1"
VERZEICHNIS="$2"
ERGEBNIS_DATEI="suchergebnisse_$(date +%Y-%m-%d).txt"

# Überprüfe, ob das Verzeichnis existiert
if [ ! -d "$VERZEICHNIS" ]; then
  echo "Fehler: Verzeichnis '$VERZEICHNIS' existiert nicht."
  exit 1
fi

echo "Suche nach '$MUSTER' in $VERZEICHNIS..."
echo "Suchergebnisse:" > "$ERGEBNIS_DATEI"
grep -r "$MUSTER" "$VERZEICHNIS" >> "$ERGEBNIS_DATEI"

if [ $? -eq 0 ]; then
  echo "Suche abgeschlossen. Ergebnisse in '$ERGEBNIS_DATEI' gespeichert."
else
  echo "Keine Treffer gefunden."
fi
```

**Aufruf:**

```bash
./datei_suche.sh "error" /var/log
```



### 8.5 Beispiel 5: Systemüberwachungsskript

**Aufgabe:** Erstelle ein Skript, das **Systeminformationen** (CPU, Speicher, Festplatten) anzeigt.

**Skriptname:** `system_info.sh`

```bash
#!/bin/bash

# Farben für die Ausgabe
GRÜN='\033[0;32m'
GELB='\033[1;33m'
NC='\033[0m' # No Color

# Funktion für CPU-Informationen
cpu_info() {
  echo -e "${GRÜN}=== CPU-Informationen ===${NC}"
  echo "Modell: $(grep "model name" /proc/cpuinfo | head -n 1 | cut -d":" -f2 | xargs)"
  echo "Anzahl Kerne: $(grep -c "processor" /proc/cpuinfo)"
  echo "Auslastung: $(top -bn1 | grep "Cpu(s)" | awk '{print $2 + $4 "%"}')"
}

# Funktion für Speicherinformationen
speicher_info() {
  echo -e "${GRÜN}=== Speicherinformationen ===${NC}"
  free -h | awk '/^Mem:/ {print "Gesamt: " $2 ", Verwendet: " $3 ", Frei: " $4}'
}

# Funktion für Festplatteninformationen
festplatte_info() {
  echo -e "${GRÜN}=== Festplatteninformationen ===${NC}"
  df -h | grep -v "tmpfs" | grep -v "udev"
}

# Funktion für Systemlast
systemlast_info() {
  echo -e "${GRÜN}=== Systemlast ===${NC}"
  uptime
  echo "Durchschnittliche Last: $(cat /proc/loadavg)"
}

# Hauptprogramm
cpu_info
echo
speicher_info
echo
festplatte_info
echo
systemlast_info
```

**Aufruf:**

```bash
./system_info.sh
```



##  9. Übungsaufgaben



###  Übung 1: Einfaches Skript erstellen

1. Erstelle ein Skript namens `begrüßung.sh`, das:
  - Den Benutzer nach seinem Namen fragt.
  - Eine Begrüßung ausgibt (z. B. "Hallo, [Name]!").

??? success "Lösung"  
    `#!/bin/bash`     
    `read -p "Wie heißt du? " NAME`     
    `echo "Hallo, $NAME!"`     


### Übung 2: Skript mit Argumenten

1. Erstelle ein Skript namens `addieren.sh`, das:
  - Zwei Zahlen als Argumente entgegennimmt.
  - Die Summe der beiden Zahlen ausgibt.

??? success "Lösung" 
``` bash
#!/bin/bash
if [ $# -ne 2 ]; then
    echo "Verwendung: $0 <Zahl1> <Zahl2>"
    exit 1
fi

ERGEBNIS=$(( $1 + $2 ))

echo "$1 + $2 = $ERGEBNIS"
```     



###  Übung 3: Skript mit Bedingungen

1. Erstelle ein Skript namens `zahl_prüfen.sh`, das:
  - Eine Zahl als Argument entgegennimmt.
  - Prüft, ob die Zahl **positiv, negativ oder null** ist.
  - Eine entsprechende Meldung ausgibt.

??? success "Lösung"  
```bash
#!/bin/bash

if [ $# -ne 1 ]; then
    echo "Verwendung: $0 <Zahl>"
    exit 1
fi

if [ $1 -gt 0 ]; then
    echo "$1 ist positiv."
elif [ $1 -lt 0 ]; then
    echo "$1 ist negativ."
else
    echo "$1 ist null."
fi

```



###  Übung 4: Skript mit `for`-Schleife

1. Erstelle ein Skript namens `dateien_auflisten.sh`, das:
  - Alle `.txt`-Dateien im aktuellen Verzeichnis auflistet.
  - Für jede Datei eine Meldung ausgibt (z. B. "Verarbeite datei1.txt").

??? success "Lösung"  
    ```bash
    #!/bin/bash

    for DATEI in *.txt; do
        echo "Verarbeite $DATEI"
    done
    ```     


###  Übung 5: Skript mit `while`-Schleife

1. Erstelle ein Skript namens `zählen.sh`, das:
  - Eine Zahl als Argument entgegennimmt.
  - Von 1 bis zu dieser Zahl zählt und jede Zahl ausgibt.

??? success "Lösung"  
    ```bash
    #!/bin/bash


    if [ $# -ne 1 ]; then
        echo "Verwendung: $0 <Zahl>"
        exit 1
    fi


    i=1

    while [ $i -le $1 ]; do
        echo $i
        i=$((i + 1))
    done
    ```  



###  Übung 6: Skript mit Funktion

1. Erstelle ein Skript namens `flaeche.sh`, das:
  - Eine Funktion `berechne_flaeche` definiert, die die Fläche eines Rechtecks berechnet (Länge × Breite).
  - Die Funktion mit zwei Argumenten aufruft und das Ergebnis ausgibt.

??? success "Lösung"  
    ```bash  
    #!/bin/bash

    berechne_flaeche() {
        # Nutzt lokale Variablen, was gut ist.
        local FLAECHE=$(( $1 * $2 ))
        echo $FLAECHE
    }

    read -p "Gib die Länge ein: " LAENGE
    read -p "Gib die Breite ein: " BREITE

    ERGEBNIS=$(berechne_flaeche $LAENGE $BREITE)

    echo "Die Fläche beträgt: $ERGEBNIS"
    ```




###  Übung 7: Skript mit `getopts`

1. Erstelle ein Skript namens `optionen.sh`, das:
  - Die Optionen `-h` (Hilfe), `-n NAME` (Name) und `-a ALTER` (Alter) unterstützt.
  - Eine Begrüßung ausgibt (z. B. "Hallo, [Name]! Du bist [Alter] Jahre alt.").

??? success "Lösung"  
    ```bash  
    #!/bin/bash

    while getopts "hn:a:" OPT; do
        case "$OPT" in
            h)
                # Hilfe anzeigen und beenden
                echo "Verwendung: $0 [-h] [-n NAME] [-a ALTER]"
                exit 0
                ;;
            n)
                # Speichert den Wert des Flags -n
                NAME="$OPTARG"
                ;;
            a)
                # Speichert den Wert des Flags -a
                ALTER="$OPTARG"
                ;;
            *)
                # Fehlerbehandlung bei unbekannten Optionen
                echo "Fehler: Unbekannte Option: $OPT"
                exit 1
                ;;
        esac
    done

    if [ -n "$NAME" ] && [ -n "$ALTER" ]; then
        echo "Hallo, $NAME! Du bist $ALTER Jahre alt."
    else
        echo "Fehler: Bitte gib sowohl Name (-n) als auch Alter (-a) an."
        # Man könnte hier auch einen Exit-Code setzen, wenn die Argumente fehlen
    fi
    ```





###  Übung 8: Backup-Skript mit Fehlerbehandlung

1. Erstelle ein Skript namens `sicheres_backup.sh`, das:
  - Ein Verzeichnis als Argument entgegennimmt.
  - Ein Backup des Verzeichnisses als `.tar.gz`-Archiv erstellt.
  - Fehler behandelt (z. B. wenn das Verzeichnis nicht existiert).

??? success "Lösung"  
    ```bash  
    #!/bin/bash

    if [ $# -ne 1 ]; then
        echo "Fehler: Bitte gib genau ein Argument an (das Verzeichnis zum sichern)."
        echo "Verwendung: $0 <Verzeichnis_Pfad>"
        exit 1
    fi


    VERZEICHNIS="$1"

    BACKUP_NAME="backup_$(date +%Y-%m-%d).tar.gz"


    if [ ! -d "$VERZEICHNIS" ]; then
        echo "Fehler: Das Verzeichnis '$VERZEICHNIS' wurde nicht gefunden oder ist kein Verzeichnis."
        exit 1
    fi


    echo "Starte Backup von '$VERZEICHNIS' nach $BACKUP_NAME ..."

    tar -czvf "$BACKUP_NAME" "$VERZEICHNIS"

    if [ $? -eq 0 ]; then
        echo "======================================="
        echo "✅ Erfolg: Backup erfolgreich erstellt: $BACKUP_NAME"
    else
        echo "======================================="
        echo "❌ Fehler: Beim Erstellen des Backups ist ein Fehler aufgetreten."
        exit 1
    fi

    ```




###  Übung 9: Log-Analyse-Skript

1. Erstelle ein Skript namens `fehler_zählen.sh`, das:
  - Eine Log-Datei als Argument entgegennimmt.
  - Die Anzahl der Zeilen zählt, die das Wort **"error"** enthalten.

??? success "Lösung"  
    ```bash  
    #!/bin/bash

    # Überprüft, ob genau ein Argument (der Pfad zur Log-Datei) übergeben wurde.
    if [ $# -ne 1 ]; then
        echo "Fehler: Bitte gib den Pfad zu einer Log-Datei an."
        echo "Verwendung: $0 <Pfad_zur_Log_Datei>"
        exit 1
    fi

    # ---------------------------------------------------

    # Variable wird mit dem ersten Argument (der Datei) gesetzt
    LOG_DATEI="$1"


    # Stellt sicher, dass die angegebene Datei existiert und tatsächlich eine Datei ist.
    if [ ! -f "$LOG_DATEI" ]; then
        echo "Fehler: Die angegebliche Log-Datei '$LOG_DATEI' existiert nicht."
        exit 1
    fi


    # Grep zählt (`-c`) die Zeilen, die das Wort "error" enthalten.
    FEHLER_ANZAHL=$(grep -c "error" "$LOG_DATEI")


    echo "Analyse abgeschlossen."
    echo "Die Log-Datei '$LOG_DATEI' enthält insgesamt $FEHLER_ANZAHL Fehler."

    ```




##  10. Best Practices für Bash-Skripte

### 10.1 Skript-Header

- Beginne jedes Skript mit einem **Header**, der **Beschreibung, Autor, Datum und Version** enthält.

**Beispiel:**

```bash
#!/bin/bash
# Skriptname: backup.sh
# Beschreibung: Erstellt ein Backup eines Verzeichnisses.
# Autor: Sadik Altuneriten
# Datum: 11.05.2026
# Version: 1.0
```



### 10.2 Fehlerbehandlung

- **Überprüfe Argumente** auf Gültigkeit.
- **Nutze** `set -e`, um das Skript bei Fehlern zu beenden.
- **Gib sinnvolle Fehlermeldungen** aus.

**Beispiel:**

```bash
#!/bin/bash
set -e  # Beende das Skript bei Fehlern

if [ $# -ne 1 ]; then
  echo "Fehler: Falsche Anzahl an Argumenten."
  echo "Verwendung: $0 <Verzeichnis>"
  exit 1
fi

if [ ! -d "$1" ]; then
  echo "Fehler: Verzeichnis '$1' existiert nicht."
  exit 1
fi
```


### 10.3 Variablen validieren

- **Überprüfe, ob Variablen gesetzt sind**, bevor du sie verwendest.

**Beispiel:**

```bash
#!/bin/bash
if [ -z "$VARIABLE" ]; then
  echo "Fehler: VARIABLE ist nicht gesetzt."
  exit 1
fi
```



### 10.4 Kommentare verwenden

- **Kommentare** (`#`) machen dein Skript **lesbarer** und **wartbarer**.

**Beispiel:**

```bash
#!/bin/bash
# Dies ist ein Kommentar
NAME="Daniela"  # Benutzername
```




### 10.5 Skripte dokumentieren

- **Dokumentiere die Verwendung** deines Skripts mit einem **Hilfemenü** (`-h` oder `--help`).

**Beispiel:**

```bash
#!/bin/bash
hilfe() {
  echo "Verwendung: $0 [OPTION]"
  echo "Optionen:"
  echo "  -h, --help    Hilfe anzeigen"
  echo "  -v, --verbose Verbose-Modus aktivieren"
  exit 0
}

while getopts "hv" OPT; do
  case "$OPT" in
    h)
      hilfe
      ;;
    v)
      VERBOSE=1
      ;;
    *)
      hilfe
      ;;
  esac
done
```



### 10.6 Skripte in `/usr/local/bin` installieren

- Wenn du ein Skript **systemweit verfügbar** machen möchtest, kopiere es nach `/usr/local/bin/` und mache es ausführbar.

**Beispiel:**

```bash
sudo cp mein_skript.sh /usr/local/bin/mein_skript
sudo chmod +x /usr/local/bin/mein_skript
```

- Jetzt kannst du das Skript **von überall** mit `mein_skript` aufrufen.



### 10.7 Skripte mit `cron` automatisieren

- Nutze `**cron**`, um Skripte **automatisch zu festgelegten Zeiten** auszuführen.

**Beispiel:**

```bash
# Bearbeite die Crontab
crontab -e
```

- Füge eine Zeile hinzu, um das Skript **täglich um 2 Uhr morgens** auszuführen:
  ```
  0 2 * * * /pfad/zum/skript.sh
  ```



##  11. Zusammenfassung und Tipps



###  Wichtige Konzepte im Überblick


| Konzept                        | Beschreibung                                       | Beispiel                                |
| ------------------------------ | -------------------------------------------------- | --------------------------------------- |
| **Shebang**                    | Gibt an, welche Shell das Skript ausführen soll.   | `#!/bin/bash`                           |
| **Variablen**                  | Speichern Werte für die spätere Verwendung.        | `NAME="Daniela"`                          |
| **Positionale Parameter**      | Argumente, die beim Aufruf übergeben werden.       | `$1`, `$2`, `$@`                        |
| **Bedingungen (`if`)**         | Führen Aktionen basierend auf Bedingungen aus.     | `if [ $A -gt $B ]; then ... fi`         |
| **Schleifen (`for`, `while`)** | Führen Aktionen wiederholt aus.                    | `for i in {1..5}; do ... done`          |
| **Funktionen**                 | Wiederverwendbare Codeblöcke.                      | `meine_funktion() { ... }`              |
| `**getopts**`                  | Verarbeitet Kommandozeilenoptionen.                | `while getopts "ab:" OPT; do ... done`  |
| **Fehlerbehandlung**           | Behandelt Fehler und gibt sinnvolle Meldungen aus. | `if [ ! -f "$DATEI" ]; then exit 1; fi` |
| **Debugging**                  | Hilft, Fehler in Skripten zu finden.               | `set -x`                                |


###  Tipps für die Praxis

1. **Beginne klein**:
  - Erstelle **einfache Skripte** und baue sie schrittweise aus.
2. **Teste häufig**:
  - Teste dein Skript **nach jeder Änderung**, um Fehler früh zu erkennen.
3. **Nutze Variablen sinnvoll**:
  - Variablen machen dein Skript **flexibler und lesbarer**.
4. **Fehlerbehandlung nicht vergessen**:
  - Überprüfe **Argumente, Dateien und Befehle** auf Gültigkeit.
5. **Dokumentiere dein Skript**:
  - Füge **Kommentare und ein Hilfemenü** hinzu, um die Verwendung zu erklären.
6. **Nutze Funktionen für wiederkehrende Aufgaben**:
  - Funktionen machen dein Skript **modularer und wartbarer**.
7. **Automatisiere mit `cron**`:
  - Nutze `cron`, um Skripte **automatisch auszuführen** (z. B. für Backups).
8. **Sicherheit beachten**:
  - Vermeide `**sudo` in Skripten**, es sei denn, es ist absolut notwendig.
  - Nutze `**set -e**`, um Skripte bei Fehlern zu beenden.


###  Häufige Fallstricke


| Problem                         | Lösung                                                              |
| ------------------------------- | ------------------------------------------------------------------- |
| **Shebang fehlt**               | Füge `#!/bin/bash` als erste Zeile hinzu.                           |
| **Skript ist nicht ausführbar** | Nutze `chmod +x skript.sh`.                                         |
| **Falsche Pfade**               | Nutze **absolute Pfade** oder `./` für relative Pfade.              |
| **Variablen nicht gesetzt**     | Überprüfe mit `[ -z "$VAR" ]`, ob eine Variable gesetzt ist.        |
| **Leerzeichen in Variablen**    | Nutze **Anführungszeichen**: `echo "$VAR"`.                         |
| **Fehlende Fehlerbehandlung**   | Überprüfe Rückgabewerte (`$?`) und nutze `set -e`.                  |
| **Endlose Schleifen**           | Nutze `break` oder `continue`, um Schleifen zu steuern.             |
| **Falsche Berechtigungen**      | Nutze `sudo` nur, wenn nötig, und setze Berechtigungen mit `chmod`. |




##  Fazit

Das **Umwandeln von Befehlen in ein Skript** ist ein **mächtiges Werkzeug**, um **wiederkehrende Aufgaben zu automatisieren** und **komplexe Abläufe zu vereinfachen**. Mit den Konzepten aus diesem Modul kannst du:

- **Einfache und komplexe Skripte** erstellen.
- **Variablen, Bedingungen und Schleifen** verwenden.
- **Benutzereingaben und Argumente** verarbeiten.
- **Fehler behandeln** und **Skripte debuggen**.
- **Skripte dokumentieren und automatisieren**.

