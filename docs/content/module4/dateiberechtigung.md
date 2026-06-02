**Modul IV: Systemadministration und Sicherheit**:

---

### **Modul IV: Systemadministration und Sicherheit**
### **Thema: Verwalten von Dateiberechtigungen und Eigentum**

---

#### **1. Einführung in Dateiberechtigungen und Eigentum**
In Linux ist das **Berechtigungssystem** ein zentraler Bestandteil der Sicherheit. Jede Datei und jedes Verzeichnis hat:
- **Eigentümer (Owner)**
- **Gruppe (Group)**
- **Berechtigungen (Permissions)** für Eigentümer, Gruppe und andere Benutzer.

Diese Berechtigungen legen fest, wer **lesen (r)**, **schreiben (w)** oder **ausführen (x)** darf.

---

#### **2. Berechtigungen anzeigen**
Um die Berechtigungen einer Datei oder eines Verzeichnisses anzuzeigen, verwenden wir den Befehl `ls -l`:

```bash
ls -l /pfad/zur/datei
```

**Beispielausgabe:**
```bash
-rw-r--r-- 1 user group 4096 Jun 1 10:00 beispieldatei.txt
```
- **`-rw-r--r--`**: Berechtigungen
  - `r`: Lesen
  - `w`: Schreiben
  - `x`: Ausführen
  - `-`: Keine Berechtigung
- **`user`**: Eigentümer
- **`group`**: Gruppe
- **`4096`**: Dateigröße in Bytes
- **`Jun 1 10:00`**: Datum und Uhrzeit der letzten Änderung
- **`beispieldatei.txt`**: Dateiname

---

#### **3. Berechtigungen ändern mit `chmod`**
Der Befehl `chmod` (Change Mode) ändert die Berechtigungen einer Datei oder eines Verzeichnisses.

##### **3.1 Symbolische Notation**
Die symbolische Notation verwendet Buchstaben:
- **`u`**: Eigentümer (User)
- **`g`**: Gruppe (Group)
- **`o`**: Andere (Others)
- **`a`**: Alle (All)
- **`+`**: Berechtigung hinzufügen
- **`-`**: Berechtigung entfernen
- **`=`**: Berechtigung setzen

**Beispiele:**

| Befehl | Beschreibung |
|--------|--------------|
| `chmod u+x datei.txt` | Fügt dem Eigentümer die Ausführungsberechtigung hinzu |
| `chmod g-w datei.txt` | Entfernt der Gruppe die Schreibberechtigung |
| `chmod o=r datei.txt` | Setzt die Berechtigungen für andere auf nur Lesen |
| `chmod a+rwx datei.txt` | Gibt allen Benutzern volle Berechtigungen (Lesen, Schreiben, Ausführen) |


##### **3.2 Numerische Notation (Oktal)**
Die numerische Notation verwendet Zahlen, um Berechtigungen zu setzen:
- **`4`**: Lesen (r)
- **`2`**: Schreiben (w)
- **`1`**: Ausführen (x)

Die Zahlen werden addiert, um die Berechtigungen zu kombinieren:
- **`7`** = 4 (r) + 2 (w) + 1 (x) → `rwx`
- **`6`** = 4 (r) + 2 (w) → `rw-`
- **`5`** = 4 (r) + 1 (x) → `r-x`
- **`4`** = 4 (r) → `r--`

**Beispiele:**

| Befehl | Beschreibung |
|--------|--------------|
| `chmod 755 datei.txt` | Eigentümer: `rwx`, Gruppe: `r-x`, Andere: `r-x` |
| `chmod 644 datei.txt` | Eigentümer: `rw-`, Gruppe: `r--`, Andere: `r--` |
| `chmod 600 datei.txt` | Eigentümer: `rw-`, Gruppe: `---`, Andere: `---` |


---
#### **4. Eigentümer und Gruppe ändern mit `chown` und `chgrp`**
##### **4.1 Eigentümer ändern mit `chown`**
Der Befehl `chown` (Change Owner) ändert den Eigentümer einer Datei oder eines Verzeichnisses.

**Syntax:**
```bash
chown [neuer_eigentümer] [datei_oder_verzeichnis]
```

**Beispiel:**
```bash
sudo chown alice datei.txt  # Ändert den Eigentümer von `datei.txt` zu `alice`
```

##### **4.2 Gruppe ändern mit `chown` oder `chgrp`**
Der Befehl `chgrp` (Change Group) ändert die Gruppe einer Datei oder eines Verzeichnisses.

**Syntax:**
```bash
chgrp [neue_gruppe] [datei_oder_verzeichnis]
```
**oder mit `chown`:**
```bash
chown :[neue_gruppe] [datei_oder_verzeichnis]
```

**Beispiel:**
```bash
sudo chgrp developers datei.txt  # Ändert die Gruppe von `datei.txt` zu `developers`
```
**oder:**
```bash
sudo chown :developers datei.txt
```

---
#### **5. Spezielle Berechtigungen**
##### **5.1 SUID (Set User ID)**
- **Zweck:** Führt eine Datei mit den Berechtigungen des **Eigentümers** aus.
- **Symbolische Notation:** `u+s`
- **Numerische Notation:** `4` vor den Berechtigungen (z. B. `4755`)

**Beispiel:**
```bash
chmod u+s /usr/bin/programm  # Setzt SUID für `programm`
chmod 4755 /usr/bin/programm # Numerische Notation
```

##### **5.2 SGID (Set Group ID)**
- **Zweck:** Führt eine Datei mit den Berechtigungen der **Gruppe** aus.
- **Symbolische Notation:** `g+s`
- **Numerische Notation:** `2` vor den Berechtigungen (z. B. `2755`)

**Beispiel:**
```bash
chmod g+s /pfad/zur/datei  # Setzt SGID für die Datei
chmod 2755 /pfad/zur/datei # Numerische Notation
```

##### **5.3 Sticky Bit**
- **Zweck:** Erlaubt nur dem **Eigentümer**, Dateien in einem Verzeichnis zu löschen (z. B. `/tmp`).
- **Symbolische Notation:** `o+t`
- **Numerische Notation:** `1` vor den Berechtigungen (z. B. `1777`)

**Beispiel:**
```bash
chmod o+t /tmp  # Setzt das Sticky Bit für `/tmp`
chmod 1777 /tmp # Numerische Notation
```

---
#### **6. Standardberechtigungen mit `umask` festlegen**
Die `umask` (User Mask) definiert die **Standardberechtigungen** für neu erstellte Dateien und Verzeichnisse.
- **Dateien:** Standardmäßig `666` (rw-rw-rw-) minus `umask`
- **Verzeichnisse:** Standardmäßig `777` (rwxrwxrwx) minus `umask`

**Beispiel:**
```bash
umask 022  # Standardberechtigungen: Dateien = 644, Verzeichnisse = 755
```
- **`022`**: Entfernt Schreibberechtigungen für Gruppe und Andere.

---
#### **7. Übungsaufgaben**
##### **Frage 1**
Wie können Sie die Berechtigungen einer Datei so ändern, dass der Eigentümer **Lesen, Schreiben und Ausführen**, die Gruppe **Lesen und Ausführen** und andere **nur Lesen** dürfen?

??? success "Antwort"
    ```bash
    chmod 754 datei.txt
    ```
    oder symbolisch:
    ```bash
    chmod u=rwx,g=rx,o=r datei.txt
    ```

---
##### **Frage 2**
Wie ändern Sie den Eigentümer einer Datei `script.sh` zu `bob` und die Gruppe zu `developers`?

??? success "Antwort"
    ```bash
    sudo chown bob:developers script.sh
    ```

---
##### **Frage 3**
Was bewirkt der folgende Befehl?
```bash
chmod 4755 /usr/local/bin/skript
```

??? success "Antwort"
    Der Befehl setzt das **SUID-Bit** für die Datei `/usr/local/bin/skript`. Das bedeutet, dass die Datei mit den Berechtigungen des **Eigentümers** ausgeführt wird, unabhängig davon, wer sie ausführt.

---
##### **Frage 4**
Wie setzen Sie das **Sticky Bit** für ein Verzeichnis `/shared`, damit nur der Eigentümer Dateien löschen kann?

??? success "Antwort"
    ```bash
    chmod o+t /shared
    ```
    oder numerisch:
    ```bash
    chmod 1777 /shared
    ```

---
##### **Frage 5**
Was ist der Unterschied zwischen `chmod 644 datei.txt` und `chmod 600 datei.txt`?

??? success "Antwort"
    - **`chmod 644 datei.txt`**: Eigentümer darf **Lesen und Schreiben**, Gruppe und Andere dürfen **nur Lesen**.
    - **`chmod 600 datei.txt`**: Nur der Eigentümer darf **Lesen und Schreiben**, Gruppe und Andere haben **keine Berechtigungen**.

---
##### **Frage 6**
Wie können Sie die `umask` so einstellen, dass neu erstellte Dateien die Berechtigungen `644` und Verzeichnisse `755` erhalten?

??? success "Antwort"
    ```bash
    umask 022
    ```

---
##### **Frage 7**
Was bedeutet die Berechtigung `drwxr-x---` für ein Verzeichnis?

??? success "Antwort"
    - **`d`**: Es handelt sich um ein **Verzeichnis**.
    - **`rwx`**: Der Eigentümer darf **Lesen, Schreiben und Ausführen** (d. h. in das Verzeichnis wechseln).
    - **`r-x`**: Die Gruppe darf **Lesen und Ausführen** (d. h. in das Verzeichnis wechseln, aber keine Dateien löschen oder erstellen).
    - **`---`**: Andere haben **keine Berechtigungen**.

---
#### **8. Praktische Beispiele**
##### **Beispiel 1: Berechtigungen für ein Skript setzen**
Angenommen, Sie haben ein Skript `backup.sh`, das nur der Eigentümer ausführen darf:
```bash
chmod 700 backup.sh
```

##### **Beispiel 2: Gemeinsames Verzeichnis für ein Team**
Erstellen Sie ein Verzeichnis `/team`, in dem alle Mitglieder der Gruppe `developers` Dateien erstellen und bearbeiten können:
```bash
sudo mkdir /team
sudo chown :developers /team
sudo chmod 770 /team
```

##### **Beispiel 3: SUID für ein Programm setzen**
Setzen Sie das SUID-Bit für ein Programm `/usr/local/bin/manage_users`, damit es immer mit den Berechtigungen des Eigentümers (z. B. `root`) ausgeführt wird:
```bash
sudo chown root:root /usr/local/bin/manage_users
sudo chmod 4755 /usr/local/bin/manage_users
```

---
#### **9. Zusammenfassung**

| Konzept | Befehl | Beschreibung |
|---------|--------|--------------|
| **Berechtigungen anzeigen** | `ls -l` | Zeigt Eigentümer, Gruppe und Berechtigungen an |
| **Berechtigungen ändern** | `chmod` | Ändert die Berechtigungen einer Datei oder eines Verzeichnisses |
| **Eigentümer ändern** | `chown` | Ändert den Eigentümer und/oder die Gruppe |
| **Gruppe ändern** | `chgrp` | Ändert die Gruppe einer Datei oder eines Verzeichnisses |
| **SUID/SGID/Sticky Bit** | `chmod u+s`, `chmod g+s`, `chmod o+t` | Spezielle Berechtigungen setzen |
| **Standardberechtigungen** | `umask` | Legt die Standardberechtigungen für neue Dateien und Verzeichnisse fest |

---
#### **10. Weiterführende Aufgaben**
1. **Aufgabe:** Erstellen Sie ein Verzeichnis `/project` und setzen Sie die Berechtigungen so, dass:
   - Der Eigentümer (`user1`) volle Berechtigungen hat.
   - Die Gruppe (`team`) Lesen und Ausführen darf.
   - Andere keine Berechtigungen haben.
   **Lösung:**
   ```bash
   sudo mkdir /project
   sudo chown user1:team /project
   sudo chmod 750 /project
   ```

2. **Aufgabe:** Erstellen Sie eine Datei `report.txt` und setzen Sie die Berechtigungen so, dass:
   - Der Eigentümer Lesen und Schreiben darf.
   - Die Gruppe nur Lesen darf.
   - Andere keine Berechtigungen haben.
   **Lösung:**
   ```bash
   touch report.txt
   chmod 640 report.txt
   ```

3. **Aufgabe:** Setzen Sie das **SGID-Bit** für ein Verzeichnis `/shared`, damit neue Dateien automatisch der Gruppe des Verzeichnisses zugewiesen werden.
   **Lösung:**
   ```bash
   sudo chmod g+s /shared
   ```

---
#### **11. Häufige Fehler und Lösungen**
| Problem | Ursache | Lösung |
|---------|---------|--------|
| **"Permission denied"** beim Ausführen einer Datei | Fehlende Ausführungsberechtigung | `chmod +x datei` |
| **"Operation not permitted"** beim Ändern des Eigentümers | Keine Root-Berechtigungen | `sudo chown` verwenden |
| **Dateien in `/tmp` können von allen gelöscht werden** | Fehlendes Sticky Bit | `chmod +t /tmp` |
| **Neue Dateien haben unerwünschte Berechtigungen** | Falsche `umask` | `umask 022` setzen |


---
#### **12. Vertiefung: ACLs (Access Control Lists)**

Für **feinere Berechtigungssteuerung** können **ACLs** (Access Control Lists) verwendet werden.
- **Befehl:** `setfacl` (Set File Access Control List)
- **Beispiel:** Gewähren Sie einem Benutzer `alice` Zugriff auf eine Datei:
  ```bash
  setfacl -m u:alice:rwx datei.txt
  ```
- **ACLs anzeigen:**
  ```bash
  getfacl datei.txt
  ```

