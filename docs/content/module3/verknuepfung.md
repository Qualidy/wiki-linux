#  Modul III.1: Verknüpfung von Befehlen




##  Einleitung

In Linux kannst du **mehrere Befehle kombinieren**, um komplexe Aufgaben in einem einzigen Schritt zu erledigen. Dies spart Zeit und macht deine Arbeit effizienter. In diesem Modul lernst du:

- Wie du **Pipes (`|`)** nutzt, um die Ausgabe eines Befehls an einen anderen weiterzuleiten.
- Wie du **Umleitungen (`>`, `>>`, `2>`, `<`)** verwendest, um Ausgaben in Dateien zu speichern oder Eingaben aus Dateien zu lesen.
- Wie du **Befehlsverknüpfungen (`;`, `&&`, `||`)** einsetzt, um mehrere Befehle hintereinander oder bedingt auszuführen.
- Wie du **Subshells (`$(...)` oder ``...``)** nutzt, um Befehle in andere Befehle einzubetten.



##  1. Pipes (`|`): Ausgabe weiterleiten

### 1.1 Was sind Pipes?

- **Pipes (`|`)** leiten die **Standardausgabe (stdout)** eines Befehls als **Standardeingabe (stdin)** an einen anderen Befehl weiter.
- **Beispiel:**
  ```bash
  ls -l | grep "txt"
  ```
  - `ls -l` listet alle Dateien im aktuellen Verzeichnis auf.
  - `grep "txt"` filtert die Ausgabe und zeigt nur Zeilen an, die "txt" enthalten.



### 1.2 Typische Anwendungsfälle für Pipes


| Anwendung                          | Beispiel           | 
| ---------------------------------- | ------------------ | 
| **Filtern von Ausgaben**           | `ps aux            | grep firefox`        |
| **Sortieren von Ausgaben**         | `ls -l             | sort -k5`            |
| **Zählen von Ergebnissen**         | `ls                | wc -l`               |





### 1.3 Wichtige Befehle für Pipes

Hier sind einige Befehle, die häufig mit Pipes kombiniert werden:


| Befehl | Beschreibung                                              | Beispiel                     |
| ------ | --------------------------------------------------------- | ---------------------------- |
| `grep` | Filtert Zeilen nach einem Muster.                         | `grep "Linux" datei.txt`     |
| `sort` | Sortiert Zeilen alphabetisch oder numerisch.              | `sort datei.txt`             |
| `wc`   | Zählt Zeilen, Wörter oder Zeichen.                        | `wc -l datei.txt`            |
| `cut`  | Schneidet Teile aus Zeilen heraus.                        | `cut -d: -f1 /etc/passwd`    |
| `awk`  | Verarbeitet Text zeilenweise (z. B. Spalten extrahieren). | `awk '{print $1}' datei.txt` |
| `sed`  | Ersetzt oder löscht Text in Zeilen.                       | `sed 's/alt/neu/' datei.txt` |
| `head` | Zeigt die ersten Zeilen einer Datei.                      | `head -n 5 datei.txt`        |
| `tail` | Zeigt die letzten Zeilen einer Datei.                     | `tail -n 5 datei.txt`        |





### 1.4 Praxisbeispiele für Pipes

#### Beispiel 1: Dateien nach Größe sortieren

```bash
ls -l | sort -k5 -n
```

- `ls -l`: Listet Dateien mit Details auf (Größe ist die 5. Spalte).
- `sort -k5 -n`: Sortiert nach der 5. Spalte (Größe) numerisch (`-n`).

#### Beispiel 2: Anzahl der Dateien im Verzeichnis zählen

```bash
ls | wc -l
```

- `ls`: Listet alle Dateien/Verzeichnisse auf.
- `wc -l`: Zählt die Anzahl der Zeilen (entspricht der Anzahl der Dateien/Verzeichnisse).


#### Beispiel 3: Die 10 größten Dateien im aktuellen Verzeichnis finden

```bash
ls -l | sort -k5 -nr | head -n 10
```

- `ls -l`: Listet Dateien mit Details auf.
- `sort -k5 -nr`: Sortiert nach der 5. Spalte (Größe) **numerisch (`-n`)** und **absteigend (`-r`)**.
- `head -n 10`: Zeigt die ersten 10 Zeilen an.

#### Beispiel 4: Alle Prozesse eines Benutzers anzeigen

```bash
ps aux | grep -i $USER
```

- `ps aux`: Zeigt alle laufenden Prozesse an.
- `grep -i $USER`: Filtert Prozesse, die zum aktuellen Benutzer (`$USER`) gehören (Groß-/Kleinschreibung ignorieren mit `-i`).



##  2. Umleitungen: Ausgabe in Dateien speichern

### 2.1 Standardausgabe (`stdout`) umleiten


| Symbol | Beschreibung                                      | Beispiel                     |
| ------ | ------------------------------------------------- | ---------------------------- |
| `>`    | **Überschreibt** eine Datei mit der Ausgabe.      | `echo "Hallo" > ausgabe.txt` |
| `>>`   | **Fügt** die Ausgabe an eine bestehende Datei an. | `echo "Welt" >> ausgabe.txt` |


**Beispiel:**

```bash
# Überschreibt die Datei
echo "Erste Zeile" > datei.txt

# Fügt eine zweite Zeile hinzu
echo "Zweite Zeile" >> datei.txt
```



### 2.2 Fehlerausgabe (`stderr`) umleiten

- Standardmäßig wird die **Fehlerausgabe (stderr)** auf dem Bildschirm angezeigt.
- Mit `2>` kannst du die Fehlerausgabe in eine Datei umleiten.


| Symbol | Beschreibung                                 | Beispiel                         |
| ------ | -------------------------------------------- | -------------------------------- |
| `2>`   | Leitet **Fehlermeldungen** in eine Datei um. | `ls /nonexistent 2> fehler.log`  |
| `2>>`  | Fügt Fehlermeldungen an eine Datei an.       | `ls /nonexistent 2>> fehler.log` |


**Beispiel:**

```bash
# Leitet Fehlermeldungen in eine Datei um
ls /nonexistent 2> fehler.log

# Leitet sowohl stdout als auch stderr in eine Datei um
ls /nonexistent > ausgabe.log 2>&1
```

- `2>&1`: Leitet `stderr` (2) in `stdout` (1) um, das dann in `ausgabe.log` geschrieben wird.



### 2.3 Eingabeumleitung (`<`)

- Leitet den Inhalt einer Datei als **Eingabe (stdin)** an einen Befehl weiter.

**Beispiel:**

```bash
# Zählt die Wörter in einer Datei
wc -w < datei.txt
```



### 2.4 `/dev/null` – Ausgabe verwerfen

- `/dev/null` ist ein **speziäles funktion**, das alle Daten verwirft.
- Nützlich, um Ausgaben zu unterdrücken.

**Beispiel:**

```bash
# Unterdrückt die Standardausgabe
echo "Hallo" > /dev/null

# Unterdrückt Fehlermeldungen
ls /nonexistent 2> /dev/null
```



### 2.5 Praxisbeispiele für Umleitungen

#### Beispiel 1: Log-Datei erstellen

```bash
# Speichert die Ausgabe von `date` in einer Log-Datei
date > log.txt

# Fügt die Ausgabe von `whoami` an die Log-Datei an
whoami >> log.txt
```

#### Beispiel 2: Fehlerprotokollierung

```bash
# Führt ein Skript aus und speichert Fehler in einer Datei
./skript.sh 2> fehler.log
```

#### Beispiel 3: Kombinierte Umleitung

```bash
# Speichert sowohl stdout als auch stderr in einer Datei
ls /existiert /nonexistent > ausgabe.log 2>&1
```

#### Beispiel 4: Eingabe aus einer Datei lesen

```bash
# Sortiert den Inhalt einer Datei
sort < unsortierte_liste.txt > sortierte_liste.txt
```



##  3. Befehlsverknüpfungen: Mehrere Befehle kombinieren

### 3.1 Semikolon (`;`): Befehle nacheinander ausführen

- Führt **mehrere Befehle hintereinander** aus, unabhängig vom Erfolg des vorherigen Befehls.

**Beispiel:**

```bash
cd ~/dokumente; ls -l; pwd
```

- Wechselt in das Verzeichnis `dokumente`, listet die Dateien auf und zeigt das aktuelle Verzeichnis an.



### 3.2 Logisches UND (`&&`): Befehle bedingt ausführen

- Führt den **nächsten Befehl nur aus, wenn der vorherige erfolgreich war** (Rückgabewert `0`).

**Beispiel:**

```bash
# Wechselt in das Verzeichnis und listet Dateien auf (nur wenn cd erfolgreich war)
cd ~/dokumente && ls -l
```

**Anwendungsfall:**

- Nützlich für **Skripte**, um sicherzustellen, dass ein Befehl nur ausgeführt wird, wenn der vorherige erfolgreich war.



### 3.3 Logisches ODER (`||`): Alternativen ausführen

- Führt den **nächsten Befehl nur aus, wenn der vorherige fehlgeschlagen ist** (Rückgabewert `≠ 0`).

**Beispiel:**

```bash
# Versucht, in das Verzeichnis zu wechseln. Falls es nicht existiert, erstellt es.
cd ~/neues_verzeichnis || mkdir ~/neues_verzeichnis
```

**Anwendungsfall:**

- Nützlich für **Fehlerbehandlung** in Skripten.



### 3.4 Kombinierte Verknüpfungen

Du kannst `;`, `&&` und `||` kombinieren, um komplexe Logik zu erstellen.

**Beispiel:**

```bash
# Versucht, eine Datei zu löschen. Falls sie nicht existiert, erstelle sie.
rm datei.txt || touch datei.txt && echo "Datei wurde erstellt oder existierte bereits."
```



### 3.5 Praxisbeispiele für Befehlsverknüpfungen

#### Beispiel 1: Backup-Skript

```bash
# Erstellt ein Backup eines Verzeichnisses, falls es existiert
[ -d ~/dokumente ] && tar -czvf backup.tar.gz ~/dokumente || echo "Verzeichnis existiert nicht."
```

- `[ -d ~/dokumente ]`: Überprüft, ob das Verzeichnis existiert.
- `&&`: Führt `tar` nur aus, wenn das Verzeichnis existiert.
- `||`: Zeigt eine Fehlermeldung an, falls das Verzeichnis nicht existiert.

#### Beispiel 2: Datei herunterladen und entpacken

```bash
wget https://example.com/datei.tar.gz && tar -xzvf datei.tar.gz
```

- `wget`: Lädt die Datei herunter.
- `&&`: Entpackt die Datei nur, wenn der Download erfolgreich war.

#### Beispiel 3: Benutzer erstellen und Berechtigungen setzen

```bash
sudo useradd -m testuser && sudo usermod -aG sudo testuser || echo "Fehler beim Erstellen des Benutzers."
```

- `useradd`: Erstellt den Benutzer.
- `&&`: Fügt den Benutzer zur `sudo`-Gruppe hinzu (nur wenn `useradd` erfolgreich war).
- `||`: Zeigt eine Fehlermeldung an, falls etwas schiefgeht.



##  4. Subshells: Befehle in andere Befehle einbetten

### 4.1 Was sind Subshells?

- **Subshells** ermöglichen es, die **Ausgabe eines Befehls als Argument für einen anderen Befehl** zu verwenden.
- `$(...)` 
- ```HEUTE=$(date +%Y-%m-%d)```




### 4.2 Syntax und Beispiele

#### Beispiel 1: Aktuelles Datum in einer Variable speichern

```bash
HEUTE=$(date +%Y-%m-%d)
echo "Heute ist $HEUTE."
```

- `date +%Y-%m-%d`: Gibt das Datum im Format `JJJJ-MM-TT` aus.
- `$(...)`: Fängt die Ausgabe ein und weist sie der Variable `HEUTE` zu.

#### Beispiel 2: Anzahl der Dateien in einem Verzeichnis zählen

```bash
ANZAHL=$(ls | wc -l)
echo "Es gibt $ANZAHL Dateien im aktuellen Verzeichnis."
```

#### Beispiel 3: Letzte Zeile einer Datei extrahieren

```bash
LETZTE_ZEILE=$(tail -n 1 datei.txt)
echo "Die letzte Zeile lautet: $LETZTE_ZEILE"
```

#### Beispiel 4: Verzeichnisgröße berechnen

```bash
GROESSE=$(du -sh ~/dokumente | cut -f1)
echo "Das Verzeichnis ~/dokumente ist $GROESSE groß."
```

- `du -sh ~/dokumente`: Berechnet die Größe des Verzeichnisses in lesbarer Form (z. B. `1.2G`).
- `cut -f1`: Schneidet das erste Feld (die Größe) heraus.



### 4.3 🌶️🌶️🌶️ Verschachtelte Subshells

Du kannst Subshells **verschachteln**, um komplexe Ausdrücke zu erstellen.

**Beispiel:**

```bash
# Zählt die Anzahl der Zeilen in allen .txt-Dateien im aktuellen Verzeichnis
ANZAHL_ZEILEN=$(find . -name "*.txt" -exec cat {} \; | wc -l)
echo "Insgesamt gibt es $ANZAHL_ZEILEN Zeilen in allen .txt-Dateien."
```

- `find . -name "*.txt"`: Findet alle `.txt`-Dateien im aktuellen Verzeichnis.
- `-exec cat {} \;`: Führt `cat` für jede gefundene Datei aus.
- `wc -l`: Zählt die Zeilen.



### 4.4 Subshells vs. Variablen


| Feature        | Subshell (`$(...)`)             | Variable                                     |
| -------------- | ------------------------------- | -------------------------------------------- |
| **Ausführung** | Wird sofort ausgeführt.         | Speichert einen Wert für spätere Verwendung. |
| **Verwendung** | Für **einmalige** Berechnungen. | Für **wiederholte** Verwendung.              |
| **Lesbarkeit** | Gut für komplexe Ausdrücke.     | Gut für einfache Werte.                      |


**Beispiel für Variablen:**

```bash
NAME="Linux"
echo "Ich liebe $NAME."
```

**Beispiel für Subshells:**

```bash
echo "Heute ist $(date +%A)."
```


##  5. Übungsaufgaben



###  Übung 1: Pipes für Filterung

1. Liste alle Dateien im Verzeichnis `/etc` auf.
2. Filtere die Ausgabe so, dass nur Dateien angezeigt werden, die mit `passwd` beginnen.

??? success "Lösung"  
    `bash     ls /etc | grep "^passwd"`       
    - `grep "^passwd"`: Filtert Zeilen, die mit "passwd" beginnen (`^` = Anfang der Zeile).

---

###  Übung 2: Pipes für Sortierung

1. Liste alle Benutzer in `/etc/passwd` auf.
2. Sortiere die Liste alphabetisch.
3. Zeige nur die ersten 5 Benutzer an.

??? success "Lösung"  
    `bash     cut -d: -f1 /etc/passwd | sort | head -n 5`       
    - `cut -d: -f1 /etc/passwd`: Extrahiere die Benutzernamen (1. Feld, getrennt durch `:`).  
    - `sort`: Sortiert die Benutzernamen alphabetisch.  
    - `head -n 5`: Zeigt die ersten 5 Zeilen an.

---

###  Übung 3: Umleitungen

1. Erstelle eine Datei namens `benutzer.txt`, die alle Benutzer aus `/etc/passwd` enthält.
2. Füge eine Zeile mit dem Text `"Ende der Liste"` am Ende der Datei hinzu.

??? success "Lösung"  
    `cut -d: -f1 /etc/passwd > benutzer.txt`     
    `echo "Ende der Liste" >> benutzer.txt`     

---

###  Übung 4: Fehlerumleitung

1. Führe den Befehl `ls /nonexistent` aus und leite die Fehlermeldung in eine Datei namens `fehler.log` um.
2. Überprüfe den Inhalt von `fehler.log`.

??? success "Lösung"  
    `ls /nonexistent 2> fehler.log`
    `cat fehler.log`

---

###  Übung 5: Befehlsverknüpfungen

1. Wechsle in das Verzeichnis `/tmp` und erstelle dort eine Datei namens `test.txt`.
2. Nutze `&&`, um sicherzustellen, dass die Datei nur erstellt wird, wenn das Wechseln des Verzeichnisses erfolgreich war.

??? success "Lösung"  
    `cd /tmp && touch test.txt`     

---

###  Übung 6: Logisches ODER

1. Versuche, in ein nicht existierendes Verzeichnis `/nonexistent` zu wechseln.
2. Falls das fehlschlägt, erstelle das Verzeichnis und wechsle dann hinein.

??? success "Lösung"  
    `cd /nonexistent || mkdir /nonexistent && cd /nonexistent`     

---

###  Übung 7: Subshells

1. Speichere das aktuelle Datum im Format `JJJJ-MM-TT` in einer Variable namens `DATUM`.
2. Erstelle eine Datei namens `datum.log` mit dem Inhalt `"Heute ist [DATUM]."`.

??? success "Lösung"  
    `DATUM=$(date +%Y-%m-%d)`     
    `echo "Heute ist $DATUM." > datum.log`     
 



###  Übung 9: Komplexe Verknüpfung

1. Erstelle ein Skript, das:
  - Ein Verzeichnis namens `backup` erstellt (falls es nicht existiert).
  - Alle `.txt`-Dateien aus dem aktuellen Verzeichnis in `backup` kopiert.
  - Eine Meldung ausgibt, wenn der Vorgang erfolgreich war.

??? success "Lösung"  
    `mkdir -p backup && cp *.txt backup/ && echo "Backup erfolgreich erstellt."`       
    - `mkdir -p backup`: Erstellt das Verzeichnis `backup` (falls es nicht existiert, `-p` unterdrückt Fehlermeldungen).  
    - `cp *.txt backup/`: Kopiert alle `.txt`-Dateien in `backup/`.  
    - `&&`: Führt den nächsten Befehl nur aus, wenn der vorherige erfolgreich war.



###  Übung 10: Fehlerbehandlung mit Subshells

1. Versuche, den Inhalt einer Datei namens `datei.txt` anzuzeigen.
2. Falls die Datei nicht existiert, erstelle sie mit dem Inhalt `"Datei wurde erstellt."`.
3. Gib in beiden Fällen den Inhalt der Datei aus.

??? success "Lösung"  
    `cat datei.txt 2> /dev/null || echo "Datei wurde erstellt." > datei.txt`     
    `cat datei.txt`       
    - `cat datei.txt 2> /dev/null`: Unterdrückt die Fehlermeldung, falls die Datei nicht existiert.  
    - `||`: Führt den nächsten Befehl nur aus, wenn `cat` fehlschlägt (Datei existiert nicht).  
    - `echo "Datei wurde erstellt." > datei.txt`: Erstellt die Datei mit dem angegebenen Inhalt.


##  6. Zusammenfassung und Tipps



###  Wichtige Konzepte im Überblick


| Konzept                            | Symbol/Operator | Beschreibung                                                           | Beispiel                                                  |
| ---------------------------------- | --------------- | ---------------------------------------------------------------------- | --------------------------------------------------------- |
| **Pipe**                           | `               | `                                                                      | Leitet die Ausgabe eines Befehls an einen anderen weiter. |
| **Standardausgabe umleiten**       | `>`             | Überschreibt eine Datei mit der Ausgabe.                               | `echo "Hallo" > datei.txt`                                |
| **Anhängen**                       | `>>`            | Fügt die Ausgabe an eine Datei an.                                     | `echo "Welt" >> datei.txt`                                |
| **Fehlerausgabe umleiten**         | `2>`            | Leitet Fehlermeldungen in eine Datei um.                               | `ls /nonexistent 2> fehler.log`                           |
| **Eingabeumleitung**               | `<`             | Liest Eingaben aus einer Datei.                                        | `wc -w < datei.txt`                                       |
| **Befehle nacheinander ausführen** | `;`             | Führt Befehle hintereinander aus.                                      | `cd /tmp; ls`                                             |
| **Logisches UND**                  | `&&`            | Führt den nächsten Befehl nur aus, wenn der vorherige erfolgreich war. | `cd /tmp && ls`                                           |
| **Logisches ODER**                 | `               | &nbsp;                                                                 | `                                                         |
| **Subshell**                       | `$(...)`        | Bettet die Ausgabe eines Befehls in einen anderen ein.                 | `echo "Heute ist $(date)."`                               |



###  Tipps für die Praxis

1. **Pipes sind mächtig**:
    - Kombiniere Befehle wie `grep`, `sort`, `awk` und `sed`, um komplexe Textverarbeitungen durchzuführen.
2. **Umleitungen sinnvoll nutzen**:
    - Speichere Ausgaben in Dateien, um sie später zu analysieren (z. B. Logs).
    - Nutze `/dev/null`, um unnötige Ausgaben zu unterdrücken.
3. **Befehlsverknüpfungen für Skripte**:
    - Nutze `&&` und `||` in Skripten, um **Fehler zu behandeln** und **Bedingungen zu prüfen**.
4. **Subshells für dynamische Werte**:
    - Verwende `$(...)` , um die Ausgabe eines Befehls in eine Variable oder einen anderen Befehl einzubetten.
5. **Lesbarkeit beachten**:
    - Komplexe Befehle können schwer lesbar sein. Nutze **Zeilenumbrüche** und **Kommentare** in Skripten:
6. **Fehlerbehandlung nicht vergessen**:
    - Überprüfe immer, ob Befehle erfolgreich waren, besonders in Skripten:

###  Häufige Fallstricke


| Problem                               | Lösung                                                                       |
| ------------------------------------- | ---------------------------------------------------------------------------- |
| **Pipes und Umleitungen verwechseln** | Pipes (`                                                                     |
| **Fehlermeldungen ignorieren**        | Nutze `2>` oder `2>&1`, um Fehlermeldungen umzuleiten oder zu unterdrücken.  |
| **Subshells falsch verschachteln**    | Achte auf die richtige Syntax: `$(...)` oder ``...``.                        |
| **Befehle ohne `&&` oder `            | &nbsp;                                                                       |
| **Leerzeichen in Pfaden**             | Nutze Anführungszeichen für Pfade mit Leerzeichen: `cd "/mein verzeichnis"`. |


