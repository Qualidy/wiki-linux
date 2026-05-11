#  Modul III.3: Suchen und Extrahieren von Daten aus Dateien


##  Einleitung

Das **Suchen und Extrahieren von Daten** aus Dateien ist eine der **häufigsten Aufgaben** in der Linux-Kommandozeile. Ob du Log-Dateien analysierst, Konfigurationsdateien durchsuchst oder Daten aus CSV-Dateien extrahierst – Linux bietet mächtige Tools, um diese Aufgaben effizient zu erledigen.

In diesem Modul lernst du:

- Wie du **Textmuster** mit `grep`, `egrep` und `fgrep` suchst.
- Wie du **Zeilen, Wörter und Zeichen** mit `cut` und `sed` extrahierst.
- Wie du **Daten sortierst, einzigartige Einträge findest** und **Statistiken erstellst**.
- Wie du **reguläre Ausdrücke (Regex)** für komplexe Suchmuster verwendest.
- **Praktische Anwendungsfälle** für die Datenverarbeitung.



##  1. Grundlagen: Textsuche mit `grep`

### 1.1 Was ist `grep`?

- `grep` (Global Regular Expression Print) ist ein **Standard-Tool** zum Durchsuchen von Textdateien nach **Mustern**.
- Es gibt **drei Varianten** von `grep`:
  - `grep`: Standardversion (unterstützt **Grundlegende Regex**).
  - `egrep`: Erweitert `grep` (unterstützt **erweiterte Regex**, äquivalent zu `grep -E`).
  - `fgrep`: Fixes `grep` (sucht nach **exakten Zeichenketten**, äquivalent zu `grep -F`).

---

### 1.2 Grundlegende Syntax von `grep`

```bash
grep [Optionen] "Muster" [Datei(en)]
```



### 1.3 Wichtige Optionen von `grep`


| Option    | Beschreibung                                                                       | Beispiel                                         |
| --------- | ---------------------------------------------------------------------------------- | ------------------------------------------------ |
| `-i`      | **Ignoriert Groß-/Kleinschreibung**.                                               | `grep -i "linux" datei.txt`                      |
| `-v`      | **Invertiert das Muster** (zeigt Zeilen an, die **nicht** dem Muster entsprechen). | `grep -v "error" log.txt`                        |
| `-n`      | **Zeigt Zeilennummern** an.                                                        | `grep -n "fehler" log.txt`                       |
| `-c`      | **Zählt die Anzahl der Treffer**.                                                  | `grep -c "linux" datei.txt`                      |
| `-l`      | **Listet nur Dateinamen** auf, die das Muster enthalten.                           | `grep -l "muster" *.txt`                         |
| `-r`      | **Durchsucht Verzeichnisse rekursiv**.                                             | `grep -r "muster" /pfad/`                        |
| `-w`      | **Such nach ganzen Wörtern** (vermeidet Teiltreffer).                              | `grep -w "linux" datei.txt`                      |
| `-A n`    | **Zeigt `n` Zeilen nach dem Treffer** an.                                          | `grep -A 2 "error" log.txt`                      |
| `-B n`    | **Zeigt `n` Zeilen vor dem Treffer** an.                                           | `grep -B 2 "error" log.txt`                      |
| `-C n`    | **Zeigt `n` Zeilen vor und nach dem Treffer** an.                                  | `grep -C 2 "error" log.txt`                      |
| `-E`      | **Aktiviert erweiterte Regex** (wie `egrep`).                                      | `grep -E "muster1                                |
| `-F`      | **Such nach exakten Zeichenketten** (wie `fgrep`).                                 | `grep -F "muster mit [Sonderzeichen]" datei.txt` |
| `--color` | **Markiert Treffer farbig**.                                                       | `grep --color "linux" datei.txt`                 |




### 1.4 Praxisbeispiele mit `grep`

#### Beispiel 1: Einfache Suche

```bash
# Suche nach dem Wort "Linux" in einer Datei
grep "Linux" datei.txt

# Suche nach "Linux" (Groß-/Kleinschreibung ignorieren)
grep -i "linux" datei.txt
```

#### Beispiel 2: Invertierte Suche

```bash
# Zeige alle Zeilen an, die **nicht** "error" enthalten
grep -v "error" log.txt
```

#### Beispiel 3: Rekursive Suche in Verzeichnissen

```bash
# Suche nach "muster" in allen Dateien im Verzeichnis /var/log
grep -r "muster" /var/log
```

#### Beispiel 4: Zeilennummern anzeigen

```bash
# Zeige Zeilennummern für Treffer von "fehler" an
grep -n "fehler" log.txt
```

#### Beispiel 5: Anzahl der Treffer zählen

```bash
# Zähle, wie oft "Linux" in einer Datei vorkommt
grep -c "Linux" datei.txt
```

#### Beispiel 6: Kontext um Treffer anzeigen

```bash
# Zeige 2 Zeilen vor und nach jedem Treffer von "error"
grep -C 2 "error" log.txt
```

#### Beispiel 7: Suche nach ganzen Wörtern

```bash
# Suche nach dem **ganzen Wort** "linux" (nicht z. B. "Linux-Distribution")
grep -w "linux" datei.txt
```

#### Beispiel 8: Suche nach mehreren Mustern

```bash
# Suche nach "error" **oder** "warning" (mit erweiterter Regex)
grep -E "error|warning" log.txt
```


##  2. Reguläre Ausdrücke (Regex) mit `grep`

### 2.1 Was sind reguläre Ausdrücke?

- **Reguläre Ausdrücke (Regex)** sind **Muster**, die verwendet werden, um **Text zu suchen und zu manipulieren**.
- Sie ermöglichen **komplexe Suchanfragen**, z. B.:
  - Suche nach **E-Mail-Adressen**.
  - Suche nach **IP-Adressen**.
  - Suche nach **Datum- oder Zeitformaten**.


### 2.2 Grundlegende Regex-Syntax


| Symbol   | Beschreibung                                                   | Beispiel                                    |
| -------- | -------------------------------------------------------------- | ------------------------------------------- |
| `.`      | **Beliebiges einzelnes Zeichen** (außer Zeilenumbruch).        | `a.c` → "abc", "a1c", "a-c"                 |
| `*`      | **0 oder mehr Vorkommen** des vorherigen Zeichens.             | `ab*c` → "ac", "abc", "abbc"                |
| `+`      | **1 oder mehr Vorkommen** des vorherigen Zeichens.             | `ab+c` → "abc", "abbc" (nicht "ac")         |
| `?`      | **0 oder 1 Vorkommen** des vorherigen Zeichens.                | `ab?c` → "ac", "abc"                        |
| `[abc]`  | **Ein Zeichen aus der Menge** `a`, `b` oder `c`.               | `[aeiou]` → Jeder Vokal                     |
| `[^abc]` | **Ein Zeichen, das nicht** in der Menge `a`, `b` oder `c` ist. | `[^0-9]` → Keine Ziffer                     |
| `[a-z]`  | **Bereich**: Ein Zeichen von `a` bis `z`.                      | `[A-Za-z]` → Groß- oder Kleinbuchstabe      |
| `[0-9]`  | **Ziffer** (0 bis 9).                                          | `[0-9][0-9]` → Zwei Ziffern                 |
| `\`      | **Maskiert Sonderzeichen** (z. B. `.`, `*`, `?`).              | `\.` → Sucht nach einem Punkt               |
| `^`      | **Anfang der Zeile**.                                          | `^Linux` → Zeilen, die mit "Linux" beginnen |
| `$`      | **Ende der Zeile**.                                            | `Linux$` → Zeilen, die mit "Linux" enden    |
| `()`     | **Gruppierung**.                                               | `(ab)+` → "ab", "abab", "ababab"            |
| `{n}`    | **Genau `n` Vorkommen**.                                       | `a{3}` → "aaa"                              |
| `{n,}`   | **Mindestens `n` Vorkommen**.                                  | `a{2,}` → "aa", "aaa", "aaaa"               |
| `{n,m}`  | **Zwischen `n` und `m` Vorkommen**.                            | `a{2,4}` → "aa", "aaa", "aaaa"              |




### 2.3 Praxisbeispiele mit Regex

#### Beispiel 1: Suche nach E-Mail-Adressen

```bash
grep -E "[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}" datei.txt
```

- `[a-zA-Z0-9._%+-]+`: Benutzername (mindestens ein Zeichen).
- `@`: @-Symbol.
- `[a-zA-Z0-9.-]+`: Domainname.
- `\.`: Punkt (maskiert).
- `[a-zA-Z]{2,}`: Top-Level-Domain (mindestens 2 Zeichen).

#### Beispiel 2: Suche nach IP-Adressen

```bash
grep -E "[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}" log.txt
```

- `[0-9]{1,3}`: 1 bis 3 Ziffern (für jede Oktett).
- `\.`: Punkt (maskiert).

#### Beispiel 3: Suche nach Datumsangaben (YYYY-MM-DD)

```bash
grep -E "[0-9]{4}-[0-9]{2}-[0-9]{2}" datei.txt
```

- `[0-9]{4}`: Jahr (4 Ziffern).
- `-`: Bindestrich.
- `[0-9]{2}`: Monat und Tag (jeweils 2 Ziffern).

#### Beispiel 4: Suche nach Zeilen, die mit "Error" beginnen

```bash
grep -E "^Error" log.txt
```

#### Beispiel 5: Suche nach Zeilen, die mit einer Ziffer enden

```bash
grep -E "[0-9]$" datei.txt
```

#### Beispiel 6: Suche nach doppelten Wörtern

```bash
grep -E "\b([a-zA-Z]+) \1\b" datei.txt
```

- `\b`: Wortgrenze.
- `([a-zA-Z]+)`: Ein oder mehrere Buchstaben (Gruppe 1).
-  `\1`: Ein Leerzeichen gefolgt vom Inhalt von Gruppe 1 (doppeltes Wort).



##  3. Daten extrahieren mit `cut`

### 3.1 Was ist `cut`?

- `cut` extrahiert **Teile von Zeilen** aus einer Datei, z. B.:
  - **Spalten** aus CSV-Dateien.
  - **Bestimmte Zeichenbereiche** aus Textdateien.



### 3.2 Grundlegende Syntax von `cut`

```bash
cut [Optionen] [Datei]
```



### 3.3 Wichtige Optionen von `cut`


| Option | Beschreibung                                       | Beispiel                  |
| ------ | -------------------------------------------------- | ------------------------- |
| `-d`   | **Trennzeichen** für Felder (Standard: Tabulator). | `cut -d"," -f1 datei.csv` |
| `-f`   | **Wählt Felder** aus (1-basiert).                  | `cut -f1,3 datei.txt`     |
| `-c`   | **Wählt Zeichenbereiche** aus.                     | `cut -c1-10 datei.txt`    |



### 3.4 Praxisbeispiele mit `cut`

#### Beispiel 1: Erste Spalte einer CSV-Datei extrahieren

```bash
cut -d"," -f1 daten.csv
```

- `-d","`: Trennzeichen ist ein Komma (für CSV-Dateien).
- `-f1`: Erstes Feld (Spalte) extrahieren.

#### Beispiel 2: Benutzernamen aus `/etc/passwd` extrahieren

```bash
cut -d":" -f1 /etc/passwd
```

- `-d":"`: Trennzeichen ist `:` (in `/etc/passwd`).
- `-f1`: Erstes Feld (Benutzername) extrahieren.

#### Beispiel 3: UID und Benutzername aus `/etc/passwd` extrahieren

```bash
cut -d":" -f1,3 /etc/passwd
```

- `-f1,3`: Erstes und drittes Feld (Benutzername und UID).

#### Beispiel 4: Erste 10 Zeichen jeder Zeile extrahieren

```bash
cut -c1-10 datei.txt
```

- `-c1-10`: Zeichen 1 bis 10 jeder Zeile.

#### Beispiel 5: Bestimmte Zeichenbereiche extrahieren

```bash
# Extrahiere die Zeichen 5 bis 10 jeder Zeile
cut -c5-10 datei.txt
```




##  4. Text ersetzen und bearbeiten mit `sed`

### 4.1 Was ist `sed`?

- `**sed**` (Stream Editor) ist ein **Tool zur Textbearbeitung**, das:
  - **Text ersetzt** (z. B. Suchen und Ersetzen).
  - **Zeilen löscht**.
  - **Text einfügt oder anhängt**.
  - **Skripte** für komplexe Textmanipulationen ermöglicht.

---

### 4.2 Grundlegende Syntax von `sed`

```bash
sed [Optionen] 'Befehl' [Datei]
```

---

### 4.3 Wichtige Befehle in `sed`


| Befehl                 | Beschreibung                                                   | Beispiel                                                |
| ---------------------- | -------------------------------------------------------------- | ------------------------------------------------------- |
| `s/Muster/Ersatz/`     | **Ersetzt** das erste Vorkommen von `Muster` durch `Ersatz`.   | `sed 's/Linux/GNU\/Linux/' datei.txt`                   |
| `s/Muster/Ersatz/g`    | **Ersetzt alle Vorkommen** von `Muster` durch `Ersatz`.        | `sed 's/Linux/GNU\/Linux/g' datei.txt`                  |
| `s/Muster/Ersatz/gi`   | **Ersetzt alle Vorkommen** (Groß-/Kleinschreibung ignorieren). | `sed 's/linux/GNU\/Linux/gi' datei.txt`                 |
| `d`                    | **Löscht** Zeilen, die dem Muster entsprechen.                 | `sed '/error/d' log.txt`                                |
| `p`                    | **Druckt** Zeilen, die dem Muster entsprechen.                 | `sed '/Linux/p' datei.txt`                              |
| `a\Text`               | **Fügt Text nach** der Zeile ein.                              | `sed '/Linux/a\Das ist Linux' datei.txt`                |
| `i\Text`               | **Fügt Text vor** der Zeile ein.                               | `sed '/Linux/i\Linux ist toll' datei.txt`               |
| `c\Text`               | **Ersetzt die Zeile** durch `Text`.                            | `sed '/Linux/c\Linux ist ein Betriebssystem' datei.txt` |
| `y/Zeichen1/Zeichen2/` | **Ersetzt einzelne Zeichen** (z. B. für Übersetzungen).        | `sed 'y/aeiou/AEIOU/' datei.txt`                        |
| `=`                    | **Zeigt die Zeilennummer** an.                                 | `sed '=' datei.txt`                                     |
| `q`                    | **Beendet die Verarbeitung** nach der ersten Übereinstimmung.  | `sed '/error/q' log.txt`                                |




### 4.4 Adressierung in `sed`

Du kannst **Befehle auf bestimmte Zeilen oder Muster anwenden**:


| Adresse    | Beschreibung                            | Beispiel                                                                        |
| ---------- | --------------------------------------- | ------------------------------------------------------------------------------- |
| `n`        | **Zeile `n**`.                          | `sed '3s/Linux/GNU\/Linux/' datei.txt` (nur Zeile 3)                            |
| `n,m`      | **Zeilen `n` bis `m**`.                 | `sed '2,5d' datei.txt` (löscht Zeilen 2 bis 5)                                  |
| `/Muster/` | **Zeilen, die dem Muster entsprechen**. | `sed '/error/s/Linux/GNU\/Linux/' log.txt`                                      |
| `!`        | **Invertiert die Adresse**.             | `sed '/error/!d' log.txt` (löscht alle Zeilen, die **nicht** "error" enthalten) |




### 4.5 Praxisbeispiele mit `sed`

#### Beispiel 1: Einfaches Ersetzen

```bash
# Ersetze das erste Vorkommen von "Linux" durch "GNU/Linux" in jeder Zeile
sed 's/Linux/GNU\/Linux/' datei.txt
```

- `\/` maskiert den Schrägstrich in "GNU/Linux".

#### Beispiel 2: Alle Vorkommen ersetzen

```bash
# Ersetze **alle** Vorkommen von "Linux" durch "GNU/Linux"
sed 's/Linux/GNU\/Linux/g' datei.txt
```

#### Beispiel 3: Groß-/Kleinschreibung ignorieren

```bash
# Ersetze "linux" (unabhängig von Groß-/Kleinschreibung) durch "Linux"
sed 's/linux/Linux/gi' datei.txt
```

#### Beispiel 4: Zeilen löschen

```bash
# Lösche alle Zeilen, die "error" enthalten
sed '/error/d' log.txt
```

#### Beispiel 5: Zeilen drucken

```bash
# Drucke alle Zeilen, die "Linux" enthalten
sed '/Linux/p' datei.txt
```

#### Beispiel 6: Text einfügen

```bash
# Füge nach jeder Zeile, die "Linux" enthält, den Text "Das ist Linux" ein
sed '/Linux/a\Das ist Linux' datei.txt
```

#### Beispiel 7: Text vor einer Zeile einfügen

```bash
# Füge vor jeder Zeile, die "Linux" enthält, den Text "Linux ist toll" ein
sed '/Linux/i\Linux ist toll' datei.txt
```

#### Beispiel 8: Zeilen ersetzen

```bash
# Ersetze jede Zeile, die "Linux" enthält, durch "Linux ist ein Betriebssystem"
sed '/Linux/c\Linux ist ein Betriebssystem' datei.txt
```

#### Beispiel 9: Zeilennummern anzeigen

```bash
# Zeige die Zeilennummern aller Zeilen an
sed '=' datei.txt
```


#### Beispiel 10: Datei direkt bearbeiten

```bash
# Ersetze "Linux" durch "GNU/Linux" **direkt in der Datei** (Vorsicht!)
sed -i 's/Linux/GNU\/Linux/g' datei.txt
```

- `-i`: Bearbeitet die Datei **direkt** (ohne `-i` wird nur die Ausgabe angezeigt).


##  5. Daten sortieren und einzigartige Einträge finden

### 5.1 `sort`: Daten sortieren

- `sort` sortiert Zeilen einer Datei **alphabetisch oder numerisch**.

#### Wichtige Optionen von `sort`


| Option | Beschreibung                               | Beispiel                                                                    |
| ------ | ------------------------------------------ | --------------------------------------------------------------------------- |
| `-r`   | **Absteigende Sortierung**.                | `sort -r datei.txt`                                                         |
| `-n`   | **Numerische Sortierung**.                 | `sort -n zahlen.txt`                                                        |
| `-k`   | **Sortiert nach einer bestimmten Spalte**. | `sort -k2 datei.txt` (sortiert nach der 2. Spalte)                          |
| `-t`   | **Trennzeichen für Spalten**.              | `sort -t"," -k2 daten.csv` (sortiert nach der 2. Spalte in einer CSV-Datei) |
| `-u`   | **Entfernt Duplikate** (wie `uniq`).       | `sort -u datei.txt`                                                         |
| `-f`   | **Ignoriert Groß-/Kleinschreibung**.       | `sort -f datei.txt`                                                         |


#### Praxisbeispiele mit `sort`

```bash
# Sortiere eine Datei alphabetisch
sort datei.txt

# Sortiere eine Datei absteigend
sort -r datei.txt

# Sortiere eine Datei numerisch
sort -n zahlen.txt

# Sortiere nach der 2. Spalte (Trennzeichen: Komma)
sort -t"," -k2 daten.csv

# Sortiere und entferne Duplikate
sort -u datei.txt
```

---

### 5.2 `uniq`: Einzigartige Einträge finden

- `uniq` entfernt **aufeinanderfolgende Duplikate** aus einer sortierten Datei.

#### Wichtige Optionen von `uniq`


| Option | Beschreibung                                          | Beispiel            |
| ------ | ----------------------------------------------------- | ------------------- |
| `-c`   | **Zählt die Vorkommen** jedes einzigartigen Eintrags. | `uniq -c datei.txt` |
| `-d`   | **Zeigt nur Duplikate** an.                           | `uniq -d datei.txt` |
| `-u`   | **Zeigt nur einzigartige Einträge** an.               | `uniq -u datei.txt` |


#### Praxisbeispiele mit `uniq`

```bash
# Zeige nur einzigartige Zeilen an (Datei muss sortiert sein!)
sort datei.txt | uniq

# Zähle die Vorkommen jeder Zeile
sort datei.txt | uniq -c

# Zeige nur Duplikate an
sort datei.txt | uniq -d

# Zeige nur einzigartige Einträge an
sort datei.txt | uniq -u
```



### 5.3 Kombinierte Beispiele: `sort` und `uniq`

#### Beispiel 1: Häufigste Wörter in einer Datei finden

```bash
# Zähle die Häufigkeit jedes Wortes in einer Datei
cat datei.txt | tr ' ' '\n' | sort | uniq -c | sort -nr
```

- `tr ' ' '\n'`: Ersetzt Leerzeichen durch Zeilenumbrüche (ein Wort pro Zeile).
- `sort`: Sortiert die Wörter alphabetisch.
- `uniq -c`: Zählt die Vorkommen jedes Wortes.
- `sort -nr`: Sortiert nach der Häufigkeit (absteigend).

#### Beispiel 2: Einzigartige IP-Adressen aus einer Log-Datei extrahieren

```bash
grep -E "[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}" access.log | sort | uniq
```

- `grep -E`: Filtert IP-Adressen aus der Log-Datei.
- `sort | uniq`: Sortiert und entfernt Duplikate.



##  6. Kombinierte Beispiele: Datenverarbeitung in der Praxis

### 6.1 Log-Dateien analysieren

#### Beispiel 1: Anzahl der Fehler in einer Log-Datei zählen

```bash
grep -c "error" /var/log/syslog
```



### 6.2 CSV-Dateien verarbeiten

#### Beispiel 1: Erste Spalte einer CSV-Datei extrahieren

```bash
cut -d"," -f1 daten.csv
```



### 6.3 Textdateien durchsuchen und bearbeiten

#### Beispiel 1: Alle E-Mail-Adressen aus einer Datei extrahieren

```bash
grep -Eo "[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}" datei.txt
```

#### Beispiel 2: Alle Zeilen, die mit "Error" beginnen, in eine neue Datei schreiben

```bash
grep "^Error" log.txt > fehler.txt
```




##  7. Übungsaufgaben



###  Übung 1: Einfache Suche mit `grep`

1. Suche nach dem Wort **"Linux"** in der Datei `/etc/os-release`.
2. Zeige die **Zeilennummern** der Treffer an.

??? success "Lösung"  
    `grep -n "Linux" /etc/os-release`     



###  Übung 2: Invertierte Suche

1. Zeige alle Zeilen in `/etc/passwd` an, die **nicht** mit `#` beginnen (d. h. keine Kommentare).

??? success "Lösung"  
    `grep -v "^#" /etc/passwd`     



###  Übung 3: Rekursive Suche

1. Suche **rekursiv** nach dem Wort **"error"** in allen Dateien im Verzeichnis `/var/log`.
2. Zeige nur die **Dateinamen** an, die Treffer enthalten.

??? success "Lösung"  
    `grep -rl "error" /var/log`     



###  Übung 4: Regex für E-Mail-Adressen

1. Suche nach **E-Mail-Adressen** in der Datei `kontakte.txt`.

??? success "Lösung"  
    `grep -E "[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}" kontakte.txt`     


###  Übung 5: Spalten extrahieren mit `cut`

1. Extrahiere die **Benutzernamen** (1. Spalte) und **UIDs** (3. Spalte) aus `/etc/passwd`.

??? success "Lösung"  
    `cut -d":" -f1,3 /etc/passwd`     

   



### Übung 6: Text ersetzen mit `sed`

1. Ersetze **alle Vorkommen** von **"Linux"** durch **"GNU/Linux"** in der Datei `text.txt`.
2. Speichere die Änderungen **direkt in der Datei**.

??? success "Lösung"  
    `sed -i 's/Linux/GNU\/Linux/g' text.txt`     


###  Übung 7: Zeilen löschen mit `sed`

1. Lösche **alle Zeilen**, die das Wort **"error"** enthalten, aus der Datei `log.txt`.
2. Speichere die Änderungen **direkt in der Datei**.

??? success "Lösung"  
    `sed -i '/error/d' log.txt`     



###  Übung 8: Daten sortieren und Duplikate entfernen

1. Sortiere die Datei `namen.txt` alphabetisch.
2. Entferne **aufeinanderfolgende Duplikate**.

??? success "Lösung"  
    `sort namen.txt | uniq`     




###  Übung 9: Textbearbeitung mit `sed`

1. Füge vor **jeder Zeile**, die mit **"Error"** beginnt, den Text **"FEHLER: "** ein.
2. Speichere die Änderungen in einer neuen Datei namens `fehler_log.txt`.

??? success "Lösung"  
    `sed '/^Error/s/^/FEHLER: /' log.txt > fehler_log.txt`     




##  8. Zusammenfassung und Tipps



###  Wichtige Befehle im Überblick


| Befehl  | Beschreibung                                                          | Beispiel                                       |
| ------- | --------------------------------------------------------------------- | ---------------------------------------------- |
| `grep`  | Sucht nach **Textmustern** in Dateien.                                | `grep "Linux" datei.txt`                       |
| `egrep` | Sucht mit **erweiterten Regex**.                                      | `egrep "error|warning" log.txt`                |
| `fgrep` | Sucht nach **exakten Zeichenketten**.                                 | `fgrep "muster mit [Sonderzeichen]" datei.txt` |
| `cut`   | Extrahiere **Spalten oder Zeichenbereiche**.                          | `cut -d"," -f1 datei.csv`                      |

| `sed`   | **Ersetzt, löscht oder fügt Text** ein.                               | `sed 's/Linux/GNU\/Linux/g' datei.txt`         |
| `sort`  | **Sortiert** Zeilen alphabetisch oder numerisch.                      | `sort -n zahlen.txt`                           |
| `uniq`  | **Entfernt Duplikate** aus sortierten Dateien.                        | `sort datei.txt                                |
| `tr`    | **Ersetzt oder löscht Zeichen**.                                      | `tr 'a-z' 'A-Z' < datei.txt`                   |



###  Tipps für die Praxis

1. **Kombiniere Befehle mit Pipes (`|`)**:
  - Pipes ermöglichen es, die **Ausgabe eines Befehls** als **Eingabe für einen anderen Befehl** zu verwenden.
  - Beispiel: `grep "error" log.txt | sort | uniq -c | sort -nr`
2. **Nutze `grep` für einfache Suchen**:
  - `grep` ist ideal für **schnelle Textsuche** in Dateien.
  - Nutze `-i` für **Groß-/Kleinschreibung ignorieren**.
  - Nutze `-v` für **invertierte Suche**.
4. **Nutze `sed` für Textersetzungen**:
  - `sed` ist ideal für **Suchen und Ersetzen** in Dateien.
  - Nutze `-i` für **direkte Bearbeitung von Dateien** (Vorsicht!).
5. **Sortiere und entferne Duplikate**:
  - `sort` + `uniq` ist eine **mächtige Kombination**, um **einzigartige Einträge** zu finden oder **Häufigkeiten zu zählen**.
6. **Nutze `tr` für Zeichenersetzungen**:
  - `tr` ist nützlich, um **Zeichen zu ersetzen oder zu löschen** (z. B. `tr 'a-z' 'A-Z'` für Großbuchstaben).
7. **Reguläre Ausdrücke (Regex) meistern**:
  - Regex ermöglicht **komplexe Suchmuster** (z. B. E-Mail-Adressen, IP-Adressen).
  - Nutze **Online-Tools** wie [Regex101](https://regex101.com/) zum Testen von Regex.
8. **Dokumentation nutzen**:
  - Nutze `man grep`, `man sed`, um die **Dokumentation** der Befehle zu lesen.
  - Nutze `--help` für eine **kurze Übersicht** der Optionen.



###  Häufige Fallstricke


| Problem                              | Lösung                                                                                               |
| ------------------------------------ | ---------------------------------------------------------------------------------------------------- |
| `**grep` findet keine Treffer**      | Überprüfe die **Groß-/Kleinschreibung** (`-i`) oder **Sonderzeichen** (maskieren mit `\`).           |
| `**cut` extrahiert falsche Spalten** | Überprüfe das **Trennzeichen** (`-d`) und die **Spaltennummern** (`-f`).                             |
| `**sed` ändert die Datei nicht**     | Nutze `-i` für **direkte Bearbeitung** oder leite die Ausgabe in eine neue Datei um (`> datei.txt`). |
| `**sort` sortiert falsch**           | Nutze `-n` für **numerische Sortierung** oder `-r` für **absteigende Sortierung**.                   |
| `**uniq` entfernt keine Duplikate**  | Die Datei muss **zuvor sortiert** werden (`sort datei.txt                                            |
| **Regex funktioniert nicht**         | Überprüfe die **Syntax** (z. B. `\` für Sonderzeichen maskieren).                                    |




## Fazit

Das **Suchen und Extrahieren von Daten aus Dateien** ist eine der **wichtigsten Fähigkeiten** in der Linux-Kommandozeile. Mit den Tools `grep`, `cut`, `sed`, `sort` und `uniq` kannst du:

- **Textmuster suchen** und **Daten filtern**.
- **Spalten und Zeichenbereiche extrahieren**.
- **Text ersetzen, löschen oder einfügen**.
- **Daten sortieren und Duplikate entfernen**.
- **Komplexe Datenverarbeitungen** durchführen.

**Übe regelmäßig**, um dich mit diesen Tools vertraut zu machen, und kombiniere sie, um **mächtige Datenpipelines** zu erstellen!
