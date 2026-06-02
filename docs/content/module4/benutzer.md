# 👥 Modul IV.1: Benutzer- und Gruppenverwaltung in Linux


##  Einleitung

Die **Benutzer- und Gruppenverwaltung** ist ein **zentraler Bestandteil der Linux-Systemadministration**. Sie ermöglicht es dir:

- **Benutzerkonten** zu erstellen, zu ändern und zu löschen.
- **Gruppen** zu verwalten und Benutzer zu Gruppen hinzuzufügen.
- **Berechtigungen** für Dateien und Verzeichnisse zu steuern.
- **Sicherheitsrichtlinien** durchzusetzen (z. B. Passwortrichtlinien, Account-Sperrung).

In diesem Modul lernst du:

- Wie du **Benutzer und Gruppen** erstellst und verwaltest.
- Wie du **Benutzerinformationen** abrufst und bearbeitest.
- Wie du **Passwortrichtlinien** durchsetzt.
- **Best Practices** für die Benutzerverwaltung.
- **Sicherheitsaspekte** bei der Verwaltung von Benutzern und Gruppen.



##  1. Grundlagen der Benutzerverwaltung

### 1.1 Was ist ein Benutzer?

- Ein **Benutzer** ist ein **Konto**, das den Zugriff auf das System ermöglicht.
- Jeder Benutzer hat:
  - Einen **Benutzernamen** (z. B. `sadik`).
  - Eine **Benutzer-ID (UID)** (z. B. `1000`).
  - Eine **Gruppen-ID (GID)** (z. B. `1000`).
  - Ein **Home-Verzeichnis** (z. B. `/home/sadik`).
  - Eine **Shell** (z. B. `/bin/bash`).
  - Ein **Passwort** (optional).



### 1.2 Benutzerkategorien in Linux


| Kategorie            | UID-Bereich | Beschreibung                                                |
| -------------------- | ----------- | ----------------------------------------------------------- |
| **Root-Benutzer**    | 0           | **Superuser** mit vollen Administratorrechten.              |
| **Systembenutzer**   | 1-999       | Benutzer für **Systemdienste** (z. B. `www-data`, `mysql`). |
| **Normale Benutzer** | 1000-65535  | **Reguläre Benutzerkonten** für Menschen.                   |



### 1.3 Wichtige Dateien für die Benutzerverwaltung


| Datei              | Beschreibung                                                                       | Beispielinhalt                                              |
| ------------------ | ---------------------------------------------------------------------------------- | ----------------------------------------------------------- |
| `**/etc/passwd**`  | Enthält **Benutzerkonteninformationen** (Name, UID, GID, Home-Verzeichnis, Shell). | `sadik:x:1000:1000:Sadik Altuneriten:/home/sadik:/bin/bash` |
| `**/etc/shadow**`  | Enthält **Passwort-Hashes** und Passwortrichtlinien (nur für Root lesbar).         | `sadik:$6$...:19122:0:99999:7:::`                           |
| `**/etc/group**`   | Enthält **Gruppendefinitionen** (Gruppenname, GID, Mitglieder).                    | `sadik:x:1000:`                                             |
| `**/etc/gshadow**` | Enthält **Gruppen-Passwörter** (nur für Root lesbar).                              | `sadik:!:::`                                                |
| `**/etc/shells**`  | Enthält **gültige Shells** für Benutzer.                                           | `/bin/bash`, `/bin/sh`, `/usr/bin/zsh`                      |




### 1.4 Struktur von `/etc/passwd`

Jede Zeile in `/etc/passwd` enthält **7 Felder**, getrennt durch `:`:

```
Benutzername:Passwort:UID:GID:Beschreibung:Home-Verzeichnis:Shell
```

**Beispiel:**

```
sadik:x:1000:1000:Sadik Altuneriten:/home/sadik:/bin/bash
```


| Feld | Beschreibung                                 | Wert                |
| ---- | -------------------------------------------- | ------------------- |
| 1    | **Benutzername**                             | `sadik`             |
| 2    | **Passwort** (x = Passwort in `/etc/shadow`) | `x`                 |
| 3    | **UID (Benutzer-ID)**                        | `1000`              |
| 4    | **GID (Gruppen-ID)**                         | `1000`              |
| 5    | **Beschreibung (GECOS)**                     | `Sadik Altuneriten` |
| 6    | **Home-Verzeichnis**                         | `/home/sadik`       |
| 7    | **Shell**                                    | `/bin/bash`         |




### 1.5 Struktur von `/etc/shadow`

Jede Zeile in `/etc/shadow` enthält **9 Felder**, getrennt durch `:`:

```
Benutzername:Passwort:Letzte_Änderung:Minimal:Maximal:Warnung:Inaktiv:Ablauf:Reserviert
```

**Beispiel:**

```
sadik:$6$...:19122:0:99999:7:::
```


| Feld | Beschreibung                                     | Wert                       |
| ---- | ------------------------------------------------ | -------------------------- |
| 1    | **Benutzername**                                 | `sadik`                    |
| 2    | **Passwort-Hash**                                | `$6$...` (SHA-512)         |
| 3    | **Letzte Passwortänderung** (Tage seit 1.1.1970) | `19122`                    |
| 4    | **Minimale Passwortalter** (Tage)                | `0` (keine Wartezeit)      |
| 5    | **Maximales Passwortalter** (Tage)               | `99999` (nie ablaufen)     |
| 6    | **Warnung vor Ablauf** (Tage)                    | `7` (7 Tage vorher warnen) |
| 7    | **Inaktivitätsdauer** (Tage nach Ablauf)         | (leer = deaktiviert)       |
| 8    | **Ablaufdatum** (Tage seit 1.1.1970)             | (leer = nie)               |
| 9    | **Reserviert**                                   | (leer)                     |



### 1.6 Struktur von `/etc/group`

Jede Zeile in `/etc/group` enthält **4 Felder**, getrennt durch `:`:

```
Gruppenname:Passwort:GID:Mitglieder
```

**Beispiel:**

```
sadik:x:1000:
sudo:x:27:sadik
```


| Feld | Beschreibung                                          | Wert            |
| ---- | ----------------------------------------------------- | --------------- |
| 1    | **Gruppenname**                                       | `sadik`, `sudo` |
| 2    | **Gruppen-Passwort** (x = Passwort in `/etc/gshadow`) | `x`             |
| 3    | **GID (Gruppen-ID)**                                  | `1000`, `27`    |
| 4    | **Mitglieder** (durch Komma getrennt)                 | `sadik`         |




##  2. Benutzer verwalten

### 2.1 Benutzer erstellen (`useradd`)

- `**useradd**` erstellt ein **neues Benutzerkonto**.
- **Standardmäßig** wird ein **Home-Verzeichnis** erstellt (falls `-m` verwendet wird).

#### Grundlegende Syntax:

```bash
sudo useradd [Optionen] Benutzername
```

#### Wichtige Optionen von `useradd`:


| Option | Beschreibung                                          | Beispiel                                                       |
| ------ | ----------------------------------------------------- | -------------------------------------------------------------- |
| `-m`   | **Erstellt das Home-Verzeichnis**.                    | `sudo useradd -m benutzername`                                 |
| `-d`   | **Legt das Home-Verzeichnis fest**.                   | `sudo useradd -d /home/mein_benutzer benutzername`             |
| `-s`   | **Legt die Shell fest**.                              | `sudo useradd -s /bin/zsh benutzername`                        |
| `-u`   | **Legt die UID fest**.                                | `sudo useradd -u 1005 benutzername`                            |
| `-g`   | **Legt die primäre Gruppe fest**.                     | `sudo useradd -g gruppenname benutzername`                     |
| `-G`   | **Fügt den Benutzer zu zusätzlichen Gruppen hinzu**.  | `sudo useradd -G sudo,docker benutzername`                     |
| `-c`   | **Fügt eine Beschreibung (GECOS) hinzu**.             | `sudo useradd -c "Testbenutzer" benutzername`                  |
| `-e`   | **Legt das Ablaufdatum fest** (Format: `YYYY-MM-DD`). | `sudo useradd -e 2026-12-31 benutzername`                      |
| `-p`   | **Legt ein Passwort fest** (verschlüsselt).           | `sudo useradd -p $(openssl passwd -6 "passwort") benutzername` |


#### Beispiel 1: Benutzer mit Home-Verzeichnis erstellen

```bash
sudo useradd -m testuser
```

#### Beispiel 2: Benutzer mit spezifischer UID und Shell erstellen

```bash
sudo useradd -u 1005 -s /bin/zsh -m testuser
```

#### Beispiel 3: Benutzer mit Beschreibung und Gruppen erstellen

```bash
sudo useradd -c "Testbenutzer für Projekte" -G sudo,docker -m testuser
```

### 2.2 Passwort setzen (`passwd`)

- `**passwd**` setzt oder ändert das **Passwort eines Benutzers**.

#### Grundlegende Syntax:

```bash
sudo passwd Benutzername
```

**Beispiel:**

```bash
sudo passwd testuser
```

- Du wirst aufgefordert, das **neue Passwort zweimal einzugeben**.

#### Passwort für einen Benutzer ohne Prompt setzen:

```bash
echo "testuser:neues_passwort" | sudo chpasswd
```

- **Achtung:** Dies ist **unsicher**, da das Passwort im Klartext in der Befehlshistory gespeichert wird.




### 2.3 Benutzer ändern (`usermod`)

- `**usermod**` ändert die **Eigenschaften eines bestehenden Benutzers**.

#### Grundlegende Syntax:

```bash
sudo usermod [Optionen] Benutzername
```

#### Wichtige Optionen von `usermod`:


| Option | Beschreibung                                                                   | Beispiel                                           |
| ------ | ------------------------------------------------------------------------------ | -------------------------------------------------- |
| `-l`   | **Benutzernamen ändern**.                                                      | `sudo usermod -l neuer_name alter_name`            |
| `-d`   | **Home-Verzeichnis ändern**.                                                   | `sudo usermod -d /neues/home benutzername`         |
| `-m`   | **Home-Verzeichnis verschieben** (mit `-d`).                                   | `sudo usermod -d /neues/home -m benutzername`      |
| `-s`   | **Shell ändern**.                                                              | `sudo usermod -s /bin/zsh benutzername`            |
| `-u`   | **UID ändern**.                                                                | `sudo usermod -u 1010 benutzername`                |
| `-g`   | **Primäre Gruppe ändern**.                                                     | `sudo usermod -g neue_gruppe benutzername`         |
| `-G`   | **Zusätzliche Gruppen ändern**.                                                | `sudo usermod -G gruppe1,gruppe2 benutzername`     |
| `-aG`  | **Fügt den Benutzer zu Gruppen hinzu** (ohne bestehende Gruppen zu entfernen). | `sudo usermod -aG sudo benutzername`               |
| `-c`   | **Beschreibung ändern**.                                                       | `sudo usermod -c "Neue Beschreibung" benutzername` |
| `-e`   | **Ablaufdatum ändern**.                                                        | `sudo usermod -e 2026-12-31 benutzername`          |
| `-L`   | **Benutzer sperren** (Passwort deaktivieren).                                  | `sudo usermod -L benutzername`                     |
| `-U`   | **Benutzer entsperren**.                                                       | `sudo usermod -U benutzername`                     |


#### Beispiel 1: Benutzernamen ändern

```bash
sudo usermod -l neuer_benutzername alter_benutzername
```

#### Beispiel 2: Benutzer zu einer Gruppe hinzufügen

```bash
sudo usermod -aG sudo testuser
```

#### Beispiel 3: Home-Verzeichnis verschieben

```bash
sudo usermod -d /neues/home/testuser -m testuser
```

#### Beispiel 4: Benutzer sperren

```bash
sudo usermod -L testuser
```



### 2.4 Benutzer löschen (`userdel`)

- `**userdel**` löscht ein **Benutzerkonto**.

#### Grundlegende Syntax:

```bash
sudo userdel [Optionen] Benutzername
```

#### Wichtige Optionen von `userdel`:


| Option | Beschreibung                                                          | Beispiel                   |
| ------ | --------------------------------------------------------------------- | -------------------------- |
| `-r`   | **Löscht das Home-Verzeichnis und die Mail-Spool**.                   | `sudo userdel -r testuser` |
| `-f`   | **Erzwingt das Löschen**, auch wenn der Benutzer noch angemeldet ist. | `sudo userdel -f testuser` |


#### Beispiel 1: Benutzer löschen (ohne Home-Verzeichnis)

```bash
sudo userdel testuser
```

#### Beispiel 2: Benutzer mit Home-Verzeichnis löschen

```bash
sudo userdel -r testuser
```

### 2.5 Benutzerinformationen abrufen (`id`, `finger`, `who`)


| Befehl          | Beschreibung                                                             | Beispiel                 |
| --------------- | ------------------------------------------------------------------------ | ------------------------ |
| `id`            | Zeigt **UID, GID und Gruppen** eines Benutzers an.                       | `id testuser`            |
| `finger`        | Zeigt **detaillierte Benutzerinformationen** an (muss installiert sein). | `finger testuser`        |
| `who`           | Zeigt **angemeldete Benutzer** an.                                       | `who`                    |
| `w`             | Zeigt **angemeldete Benutzer und ihre Prozesse** an.                     | `w`                      |
| `last`          | Zeigt die **Anmeldehistorie** an.                                        | `last testuser`          |
| `getent passwd` | Zeigt **Benutzerinformationen** aus `/etc/passwd` an.                    | `getent passwd testuser` |


#### Beispiel:

```bash
# Zeige UID, GID und Gruppen von testuser
id testuser

# Zeige detaillierte Informationen zu testuser
finger testuser

# Zeige alle angemeldeten Benutzer
who
```


##  3. Gruppen verwalten

### 3.1 Gruppen erstellen (`groupadd`)

- `**groupadd**` erstellt eine **neue Gruppe**.

#### Grundlegende Syntax:

```bash
sudo groupadd [Optionen] Gruppenname
```

#### Wichtige Optionen von `groupadd`:


| Option | Beschreibung                                 | Beispiel                            |
| ------ | -------------------------------------------- | ----------------------------------- |
| `-g`   | **Legt die GID fest**.                       | `sudo groupadd -g 2000 neue_gruppe` |
| `-r`   | **Erstellt eine Systemgruppe** (GID < 1000). | `sudo groupadd -r systemgruppe`     |


#### Beispiel 1: Gruppe erstellen

```bash
sudo groupadd Entwickler
```

#### Beispiel 2: Gruppe mit spezifischer GID erstellen

```bash
sudo groupadd -g 2000 Entwickler
```



### 3.2 Gruppen ändern (`groupmod`)

- `**groupmod**` ändert die **Eigenschaften einer bestehenden Gruppe**.

#### Grundlegende Syntax:

```bash
sudo groupmod [Optionen] Gruppenname
```

#### Wichtige Optionen von `groupmod`:


| Option | Beschreibung             | Beispiel                                 |
| ------ | ------------------------ | ---------------------------------------- |
| `-n`   | **Gruppennamen ändern**. | `sudo groupmod -n neuer_name alter_name` |
| `-g`   | **GID ändern**.          | `sudo groupmod -g 2001 Entwickler`       |


#### Beispiel 1: Gruppennamen ändern

```bash
sudo groupmod -n DevOps Entwickler
```

#### Beispiel 2: GID ändern

```bash
sudo groupmod -g 2001 DevOps
```



### 3.3 Gruppen löschen (`groupdel`)

- `**groupdel**` löscht eine **Gruppe**.

#### Grundlegende Syntax:

```bash
sudo groupdel Gruppenname
```

#### Beispiel:

```bash
sudo groupdel DevOps
```

- **Achtung:** Eine Gruppe kann **nicht gelöscht werden**, wenn sie noch **Mitglieder** hat.



### 3.4 Benutzer zu Gruppen hinzufügen (`usermod`, `gpasswd`)

- Nutze `**usermod -aG**`, um einen Benutzer zu einer Gruppe hinzuzufügen.
- Alternativ kannst du `**gpasswd**` verwenden.

#### Beispiel 1: Benutzer zu einer Gruppe hinzufügen

```bash
sudo usermod -aG Entwickler testuser
```

#### Beispiel 2: Benutzer mit `gpasswd` zu einer Gruppe hinzufügen

```bash
sudo gpasswd -a testuser Entwickler
```



### 3.5 Benutzer aus Gruppen entfernen (`gpasswd`)

- `**gpasswd -d**` entfernt einen Benutzer aus einer Gruppe.

#### Beispiel:

```bash
sudo gpasswd -d testuser Entwickler
```


### 3.6 Gruppeninformationen abrufen (`getent group`)

- `**getent group**` zeigt die **Mitglieder einer Gruppe** an.

#### Beispiel:

```bash
getent group Entwickler
```

**Ausgabe:**

```
Entwickler:x:2000:testuser,benutzer2
```


### 3.7 Gruppen-Passwort setzen (`gpasswd`)

- `**gpasswd**` setzt ein **Passwort für eine Gruppe** (selten verwendet).

#### Beispiel:

```bash
sudo gpasswd Entwickler
```

- Du wirst aufgefordert, ein **Passwort für die Gruppe** einzugeben.


##  4. Passwortrichtlinien und Sicherheit

### 4.1 Passwortrichtlinien mit `chage`

- `**chage**` (Change Age) ändert die **Passwortrichtlinien** für einen Benutzer.

#### Grundlegende Syntax:

```bash
sudo chage [Optionen] Benutzername
```

#### Wichtige Optionen von `chage`:


| Option | Beschreibung                                      | Beispiel                                   |
| ------ | ------------------------------------------------- | ------------------------------------------ |
| `-l`   | **Zeigt die aktuellen Passwortrichtlinien** an.   | `sudo chage -l testuser`                   |
| `-m`   | **Minimales Passwortalter** (Tage).               | `sudo chage -m 7 testuser`                 |
| `-M`   | **Maximales Passwortalter** (Tage).               | `sudo chage -M 90 testuser`                |
| `-W`   | **Warnung vor Ablauf** (Tage).                    | `sudo chage -W 14 testuser`                |
| `-I`   | **Inaktivitätsdauer** (Tage nach Ablauf).         | `sudo chage -I 30 testuser`                |
| `-E`   | **Ablaufdatum** (Format: `YYYY-MM-DD`).           | `sudo chage -E 2026-12-31 testuser`        |
| `-d`   | **Letzte Passwortänderung** (Tage seit 1.1.1970). | `sudo chage -d $(date +%s/86400) testuser` |


#### Beispiel 1: Passwortrichtlinien anzeigen

```bash
sudo chage -l testuser
```

#### Beispiel 2: Passwort alle 90 Tage ändern lassen

```bash
sudo chage -M 90 testuser
```

#### Beispiel 3: Benutzer nach 30 Tagen Inaktivität sperren

```bash
sudo chage -I 30 testuser
```



### 4.2 Passwortalter erzwingen (`passwd -x`)

- `**passwd -x**` setzt das **maximale Passwortalter**.

#### Beispiel:

```bash
sudo passwd -x 90 testuser
```



### 4.3 Benutzer sperren und entsperren

- **Benutzer sperren** (Passwort deaktivieren):
  ```bash
  sudo usermod -L testuser
  ```
- **Benutzer entsperren**:
  ```bash
  sudo usermod -U testuser
  ```



### 4.4 Benutzerkonto deaktivieren (`nologin`)

- `**/usr/sbin/nologin**` als Shell setzen, um **Anmeldungen zu verhindern**.

#### Beispiel:

```bash
sudo usermod -s /usr/sbin/nologin testuser
```


### 4.5 Benutzerkonto ablaufen lassen

- **Ablaufdatum setzen** (Benutzer kann sich nicht mehr anmelden):
  ```bash
  sudo chage -E 2026-12-31 testuser
  ```


##  5. Praktische Beispiele

### 5.1 Beispiel 1: Neuen Benutzer mit Home-Verzeichnis erstellen

```bash
sudo useradd -m -s /bin/bash -c "Testbenutzer" testuser
sudo passwd testuser
```



### 5.2 Beispiel 2: Benutzer zu mehreren Gruppen hinzufügen

```bash
sudo usermod -aG sudo,docker,Entwickler testuser
```



### 5.3 Beispiel 3: Gruppe erstellen und Benutzer hinzufügen

```bash
sudo groupadd Entwickler
sudo usermod -aG Entwickler testuser
```


### 5.4 Beispiel 4: Benutzerinformationen anzeigen

```bash
id testuser
finger testuser
getent passwd testuser
```



### 5.5 Beispiel 5: Passwortrichtlinien für einen Benutzer setzen

```bash
sudo chage -M 90 -m 7 -W 14 -I 30 testuser
```

- **Maximales Passwortalter:** 90 Tage.
- **Minimales Passwortalter:** 7 Tage.
- **Warnung vor Ablauf:** 14 Tage.
- **Inaktivitätsdauer:** 30 Tage.


### 5.6 Beispiel 6: Benutzer sperren und entsperren

```bash
# Benutzer sperren
sudo usermod -L testuser

# Benutzer entsperren
sudo usermod -U testuser
```


### 5.7 Beispiel 7: Benutzerkonto deaktivieren

```bash
sudo usermod -s /usr/sbin/nologin testuser
```



### 5.8 Beispiel 8: Benutzer mit Ablaufdatum erstellen

```bash
sudo useradd -m -e 2026-12-31 testuser
sudo passwd testuser
```


### 5.9 Beispiel 9: Alle Benutzer auflisten

```bash
cut -d: -f1 /etc/passwd
```

oder

```bash
getent passwd | cut -d: -f1
```



### 5.10 Beispiel 10: Alle Gruppen auflisten

```bash
cut -d: -f1 /etc/group
```

oder

```bash
getent group | cut -d: -f1
```



##  6. Übungsaufgaben



###  Übung 1: Benutzer erstellen

1. Erstelle einen Benutzer namens `**testuser1**` mit:
  - Home-Verzeichnis `/home/testuser1`.
  - Shell `/bin/bash`.
  - Beschreibung **"Testbenutzer 1"**.
2. Setze ein Passwort für den Benutzer.

??? success "Lösung"  
    `bash     sudo useradd -m -s /bin/bash -c "Testbenutzer 1" testuser1     sudo passwd testuser1`     


###  Übung 2: Benutzer zu Gruppen hinzufügen

1. Erstelle eine Gruppe namens `**Entwickler**`.
2. Füge den Benutzer `**testuser1**` zur Gruppe `**Entwickler**` hinzu.

??? success "Lösung"  
    `bash     sudo groupadd Entwickler     sudo usermod -aG Entwickler testuser1`     



###  Übung 3: Benutzerinformationen abrufen

1. Zeige die **UID, GID und Gruppen** des Benutzers `**testuser1**` an.
2. Zeige die **detaillierten Informationen** des Benutzers an.

??? success "Lösung"  
    `bash     id testuser1     finger testuser1`     



###  Übung 4: Passwortrichtlinien setzen

1. Setze für den Benutzer `**testuser1**` folgende Passwortrichtlinien:
  - **Maximales Passwortalter:** 60 Tage.
  - **Minimales Passwortalter:** 3 Tage.
  - **Warnung vor Ablauf:** 7 Tage.

??? success "Lösung"  
    `bash     sudo chage -M 60 -m 3 -W 7 testuser1`     



###  Übung 5: Benutzer sperren

1. Sperre den Benutzer `**testuser1**`.
2. Überprüfe, ob der Benutzer gesperrt ist.

??? success "Lösung"  
    `bash     sudo usermod -L testuser1     sudo chage -l testuser1 | grep "Password locked"`     



###  Übung 6: Benutzer entsperren

1. Entsperre den Benutzer `**testuser1**`.
2. Überprüfe, ob der Benutzer entsperrt ist.

??? success "Lösung"  
    `bash     sudo usermod -U testuser1     sudo chage -l testuser1 | grep "Password locked"`     



###  Übung 7: Benutzer löschen

1. Lösche den Benutzer `**testuser1**` **inklusive Home-Verzeichnis**.

??? success "Lösung"  
    `bash     sudo userdel -r testuser1`     


###  Übung 8: Gruppe erstellen und Benutzer hinzufügen

1. Erstelle eine Gruppe namens `**ProjektA**` mit der GID `**3000**`.
2. Erstelle einen Benutzer namens `**projektuser**` und füge ihn zur Gruppe `**ProjektA**` hinzu.

??? success "Lösung"  
    `bash     sudo groupadd -g 3000 ProjektA     sudo useradd -m -G ProjektA projektuser     sudo passwd projektuser`     


###  Übung 9: Benutzer aus Gruppe entfernen

1. Entferne den Benutzer `**projektuser**` aus der Gruppe `**ProjektA**`.

??? success "Lösung"  
    `bash     sudo gpasswd -d projektuser ProjektA`     



###  Übung 10: Benutzerkonto mit Ablaufdatum erstellen

1. Erstelle einen Benutzer namens `**tempuser**` mit:
  - Ablaufdatum **31.12.2026**.
  - Home-Verzeichnis `/home/tempuser`.
2. Überprüfe das Ablaufdatum.

??? success "Lösung"  
    `bash     sudo useradd -m -e 2026-12-31 tempuser     sudo passwd tempuser     sudo chage -l tempuser | grep "Account expires"`     



###  Übung 11: Alle Benutzer mit UID > 1000 auflisten

1. Liste alle **normalen Benutzer** (UID ≥ 1000) auf.

??? success "Lösung"  
    `bash     getent passwd | awk -F: '$3 >= 1000 {print $1}'`     



###  Übung 12: Benutzer mit spezifischer Shell finden

1. Liste alle Benutzer auf, die die Shell `**/bin/bash**` verwenden.

??? success "Lösung"  
    `bash     getent passwd | awk -F: '$7 == "/bin/bash" {print $1}'`     



###  Übung 13: Gruppenmitglieder auflisten

1. Liste alle Mitglieder der Gruppe `**sudo**` auf.

??? success "Lösung"  
    `bash     getent group sudo | cut -d: -f4 | tr ',' '\n'`     



###  Übung 14: Benutzer mit abgelaufenem Passwort finden

1. Liste alle Benutzer auf, deren **Passwort abgelaufen** ist.

??? success "Lösung"  
    `bash     sudo chage -l $(getent passwd | cut -d: -f1) | grep -B1 "Password expired" | grep -v "Password expired" | awk '{print $1}'`     



###  Übung 15: Benutzer mit `nologin`-Shell finden

1. Liste alle Benutzer auf, die die Shell `**/usr/sbin/nologin**` oder `**/bin/false**` verwenden.

??? success "Lösung"  
    `bash     getent passwd | awk -F: '$7 == "/usr/sbin/nologin" || $7 == "/bin/false" {print $1}'`     



##  7. Best Practices für die Benutzer- und Gruppenverwaltung

### 7.1 Sicherheitstipps

1. **Nutze starke Passwörter**:
  - Erzwinge **Passwortrichtlinien** (z. B. Mindestlänge, Sonderzeichen).
  - Nutze Tools wie `**pwgen**` oder `**apg**`, um sichere Passwörter zu generieren.
2. **Sperre ungenutzte Konten**:
  - Sperre Benutzerkonten, die **nicht mehr benötigt** werden (`usermod -L`).
  - Lösche Benutzerkonten, die **dauerhaft nicht mehr benötigt** werden (`userdel -r`).
3. **Vermeide Root-Zugriff für normale Benutzer**:
  - Füge Benutzer nur dann zur `**sudo`-Gruppe** hinzu, wenn sie **Administratorrechte** benötigen.
4. **Nutze `sudo` statt Root-Login**:
  - Erlaube Benutzern, **bestimmte Befehle mit `sudo**` auszuführen, statt ihnen **Root-Zugriff** zu geben.
5. **Überprüfe Benutzerkonten regelmäßig**:
  - Nutze `last` oder `who`, um **unbekannte Anmeldungen** zu erkennen.
  - Überprüfe `/etc/passwd` und `/etc/shadow` auf **unbekannte Benutzer**.
6. **Nutze Gruppen für Berechtigungen**:
  - Verwalte **Berechtigungen über Gruppen** (z. B. `sudo`, `docker`, `www-data`).
  - Vermeide es, **direkte Berechtigungen für einzelne Benutzer** zu setzen.
7. **Dokumentiere Benutzerkonten**:
  - Führe eine **Liste aller Benutzerkonten** und ihrer **Zwecke**.
  - Dokumentiere **Passwortrichtlinien** und **Ablaufdaten**.


### 7.2 Tipps für die Praxis

1. **Nutze `useradd` mit `-m` für neue Benutzer**:
  - Erstelle **immer ein Home-Verzeichnis** (`-m`), es sei denn, es ist ein **Systembenutzer**.
2. **Nutze `usermod -aG` zum Hinzufügen zu Gruppen**:
  - `-aG` fügt den Benutzer zu einer Gruppe hinzu, **ohne ihn aus anderen Gruppen zu entfernen**.
3. **Nutze `getent` statt direkter Dateizugriffe**:
  - `getent passwd` und `getent group` sind **sicherer** als direkter Zugriff auf `/etc/passwd` oder `/etc/group`.
4. **Teste Änderungen an Benutzerkonten**:
  - Melde dich als der Benutzer an (`su - benutzername`), um zu überprüfen, ob alles funktioniert.
5. **Nutze `chage` für Passwortrichtlinien**:
  - Erzwinge **regelmäßige Passwortänderungen** und **Sperren nach Inaktivität**.
6. **Automatisiere die Benutzerverwaltung**:
  - Nutze Skripte, um **Benutzer in großen Mengen** zu verwalten (z. B. für neue Mitarbeiter).
7. **Nutze `finger` für detaillierte Benutzerinformationen**:
  - Installiere `finger`, um **detaillierte Informationen** zu Benutzern anzuzeigen.



### 7.3 Häufige Fallstricke


| Problem                                  | Lösung                                                                           |
| ---------------------------------------- | -------------------------------------------------------------------------------- |
| **Benutzer kann sich nicht anmelden**    | Überprüfe, ob die **Shell** in `/etc/passwd` korrekt ist (z. B. `/bin/bash`).    |
| **Benutzer hat keine Berechtigungen**    | Überprüfe, ob der Benutzer in den **richtigen Gruppen** ist (`id benutzername`). |
| **Passwort kann nicht geändert werden**  | Überprüfe die **Passwortrichtlinien** (`chage -l benutzername`).                 |
| **Home-Verzeichnis wird nicht erstellt** | Nutze `useradd -m`, um das **Home-Verzeichnis zu erstellen**.                    |
| **Benutzer kann `sudo` nicht verwenden** | Füge den Benutzer zur `**sudo`-Gruppe** hinzu (`usermod -aG sudo benutzername`). |
| **Gruppe kann nicht gelöscht werden**    | Entferne **alle Mitglieder** aus der Gruppe (`gpasswd -d benutzername gruppe`).  |
| **Benutzerkonto ist gesperrt**           | Entsperre den Benutzer mit `usermod -U benutzername`.                            |



##  Weiterführende Themen

- **LDAP-Integration**: Verwalte Benutzer **zentral über LDAP** (z. B. mit `OpenLDAP`).
- **SSH-Zugriff verwalten**: Konfiguriere **SSH-Schlüssel** für sichere Anmeldungen.
- **Sudo-Konfiguration**: Passe die `**/etc/sudoers`-Datei** an, um **feingranulare Berechtigungen** zu vergeben.
- **PAM (Pluggable Authentication Modules)**: Konfiguriere **Authentifizierungsrichtlinien** (z. B. Passwortkomplexität).
- **Automatisierung mit Skripten**: Erstelle **Skripte**, um Benutzer und Gruppen **automatisch zu verwalten** (z. B. für neue Mitarbeiter).

w

