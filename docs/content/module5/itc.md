
### **Modul V: Zusammenführung und Zielsetzung**
### **Thema: ICT-Fähigkeiten und Arbeiten in Linux**

---

---

## **1. Einführung in ICT-Fähigkeiten unter Linux**
**ICT (Information and Communication Technology)** umfasst alle Technologien, die für die **Verarbeitung, Speicherung, Übertragung und Darstellung von Informationen** verwendet werden. Linux ist ein **zentraler Bestandteil** der ICT-Welt und bietet eine **mächtige, flexible und kostengünstige Plattform** für verschiedene Anwendungsbereiche.

In diesem Modul lernst du:
- **Grundlegende und fortgeschrittene ICT-Fähigkeiten** unter Linux.
- **Arbeitsabläufe und Best Practices** für die Arbeit mit Linux.
- **Tools und Techniken** für die **Effizienzsteigerung** in der täglichen Arbeit.
- **Zusammenarbeit und Kommunikation** in Linux-Umgebungen.
- **Karrierewege und Zertifizierungen** für ICT-Profis.

---

---

## **2. Grundlegende ICT-Fähigkeiten unter Linux**

---

### **2.1 Kommandozeile (CLI) beherrschen**
Die **Kommandozeile** ist das **Herzstück von Linux** und eine der wichtigsten Fähigkeiten für ICT-Profis.

#### **2.1.1 Wichtige Bash-Befehle**
| **Kategorie** | **Befehl** | **Beschreibung** | **Beispiel** |
|--------------|------------|------------------|--------------|
| **Navigation** | `cd` | Wechseln des Verzeichnisses. | `cd /home/user` |
| | `pwd` | Zeigt das aktuelle Verzeichnis an. | `pwd` |
| | `ls` | Listet Dateien und Verzeichnisse auf. | `ls -l` |
| **Dateioperationen** | `cp` | Kopiert Dateien/Verzeichnisse. | `cp datei.txt /backup/` |
| | `mv` | Verschiebt oder benennt Dateien um. | `mv datei.txt neue_datei.txt` |
| | `rm` | Löscht Dateien/Verzeichnisse. | `rm -rf verzeichnis/` |
| | `touch` | Erstellt eine leere Datei. | `touch neue_datei.txt` |
| | `mkdir` | Erstellt ein Verzeichnis. | `mkdir neues_verzeichnis` |
| | `rmdir` | Löscht ein leeres Verzeichnis. | `rmdir leeres_verzeichnis` |
| **Dateiinhalte anzeigen** | `cat` | Zeigt den Inhalt einer Datei an. | `cat datei.txt` |
| | `less` | Zeigt Dateiinhalte seitenweise an. | `less datei.txt` |
| | `head` | Zeigt die ersten Zeilen einer Datei an. | `head -n 10 datei.txt` |
| | `tail` | Zeigt die letzten Zeilen einer Datei an. | `tail -f /var/log/syslog` |
| | `grep` | Sucht nach Mustern in Dateien. | `grep "error" /var/log/syslog` |
| **Berechtigungen** | `chmod` | Ändert Dateiberechtigungen. | `chmod 755 skript.sh` |
| | `chown` | Ändert Eigentümer und Gruppe. | `sudo chown user:group datei.txt` |
| | `chgrp` | Ändert die Gruppe einer Datei. | `sudo chgrp developers datei.txt` |
| **Prozesse** | `ps` | Zeigt laufende Prozesse an. | `ps aux` |
| | `top` | Zeigt Systemprozesse in Echtzeit an. | `top` |
| | `htop` | Interaktive Prozessanzeige. | `htop` |
| | `kill` | Beendet einen Prozess. | `kill -9 1234` |
| | `pkill` | Beendet Prozesse nach Name. | `pkill nginx` |
| **Systeminformationen** | `uname` | Zeigt Systeminformationen an. | `uname -a` |
| | `df` | Zeigt Festplattenbelegung an. | `df -h` |
| | `du` | Zeigt Verzeichnisgrößen an. | `du -sh /home` |
| | `free` | Zeigt Speichernutzung an. | `free -h` |
| | `lscpu` | Zeigt CPU-Informationen an. | `lscpu` |
| | `lsblk` | Zeigt Blockgeräte an. | `lsblk` |
| **Netzwerk** | `ip` | Zeigt Netzwerkkonfiguration an. | `ip a` |
| | `ping` | Testet die Erreichbarkeit eines Hosts. | `ping google.com` |
| | `ifconfig` | Zeigt Netzwerkinterfaces an (veraltet). | `ifconfig` |
| | `ss` | Zeigt Socket-Statistiken an. | `ss -tuln` |
| | `netstat` | Zeigt Netzwerkverbindungen an (veraltet). | `netstat -tuln` |
| | `curl` | Überträgt Daten von/bis einem Server. | `curl https://example.com` |
| | `wget` | Lädt Dateien aus dem Internet herunter. | `wget https://example.com/datei.zip` |
| **Kompression** | `tar` | Erstellt oder extrahiert Archive. | `tar -czvf backup.tar.gz /home` |
| | `gzip` | Komprimiert Dateien. | `gzip datei.txt` |
| | `bzip2` | Komprimiert Dateien (bessere Kompression). | `bzip2 datei.txt` |
| | `xz` | Komprimiert Dateien (sehr hohe Kompression). | `xz datei.txt` |
| **Suche** | `find` | Sucht nach Dateien/Verzeichnissen. | `find /home -name "*.txt"` |
| | `locate` | Sucht nach Dateien (schneller, aber weniger aktuell). | `locate datei.txt` |
| | `which` | Zeigt den Pfad eines Befehls an. | `which python` |
| | `whereis` | Zeigt alle Pfade zu einem Befehl an. | `whereis python` |

---

#### **2.1.2 Bash-Skripting-Grundlagen**
Bash-Skripte ermöglichen die **Automatisierung von Aufgaben** unter Linux.

**Beispiel: Einfaches Bash-Skript**
```bash
#!/bin/bash

# Einfaches Skript zur Begrüßung
echo "Wie heißt du?"
read name
echo "Hallo, $name! Heute ist $(date)."
```

**Wichtige Konzepte:**
- **Shebang (`#!/bin/bash`)**: Gibt den Interpreter an.
- **Variablen**: `name="Wert"`, Zugriff mit `$name`.
- **Benutzereingabe**: `read variable`.
- **Bedingungen**:
  ```bash
  if [ "$name" == "Alice" ]; then
      echo "Hallo Alice!"
  else
      echo "Hallo Fremder!"
  fi
  ```
- **Schleifen**:
  ```bash
  # For-Schleife
  for i in {1..5}; do
      echo "Zahl: $i"
  done

  # While-Schleife
  count=1
  while [ $count -le 5 ]; do
      echo "Zahl: $count"
      ((count++))
  done
  ```
- **Funktionen**:
  ```bash
  function begrüßung {
      echo "Hallo, $1!"
  }
  begrüßung "Alice"
  ```

**Beispiel: Backup-Skript**
```bash
#!/bin/bash

# Backup-Skript für /home
BACKUP_DIR="/mnt/backup"
SOURCE_DIR="/home"
DATE=$(date +%Y-%m-%d)

# Erstelle Backup-Verzeichnis, falls nicht vorhanden
mkdir -p "$BACKUP_DIR"

# Erstelle tar.gz-Backup
tar -czvf "$BACKUP_DIR/home_backup_$DATE.tar.gz" "$SOURCE_DIR"

# Lösche Backups, die älter als 7 Tage sind
find "$BACKUP_DIR" -name "home_backup_*.tar.gz" -mtime +7 -delete

echo "Backup abgeschlossen: $BACKUP_DIR/home_backup_$DATE.tar.gz"
```

---
---

### **2.2 Dateisystem und Berechtigungen**
#### **2.2.1 Linux-Dateisystemhierarchie**
| **Verzeichnis** | **Beschreibung** |
|----------------|------------------|
| `/` | Root-Verzeichnis (oberstes Verzeichnis). |
| `/bin` | Binärdateien (ausführbare Programme). |
| `/sbin` | Systembinärdateien (für Administratoren). |
| `/etc` | Konfigurationsdateien. |
| `/home` | Benutzerverzeichnisse. |
| `/root` | Home-Verzeichnis des Root-Benutzers. |
| `/var` | Variable Daten (Logs, Caches, etc.). |
| `/usr` | Benutzerprogramme und Bibliotheken. |
| `/tmp` | Temporäre Dateien. |
| `/dev` | Gerätedateien. |
| `/proc` | Prozess- und Systeminformationen. |
| `/sys` | Systeminformationen (Kernel). |
| `/opt` | Optionale Software (manuell installiert). |
| `/mnt` | Einhängepunkt für temporäre Dateisysteme. |
| `/media` | Einhängepunkt für Wechselmedien (USB, CDs). |

---
#### **2.2.2 Berechtigungen und Eigentum**
- **Berechtigungen**:
  - **`r` (read)**: Lesen.
  - **`w` (write)**: Schreiben.
  - **`x` (execute)**: Ausführen.
  - **`d` (directory)**: Verzeichnis.
- **Berechtigungsgruppen**:
  - **Eigentümer (User)**: `u`
  - **Gruppe (Group)**: `g`
  - **Andere (Others)**: `o`
  - **Alle (All)**: `a`

**Beispiele:**
```bash
# Berechtigungen ändern (symbolisch)
chmod u+x skript.sh       # Fügt Ausführungsrecht für den Eigentümer hinzu
chmod g-w datei.txt        # Entfernt Schreibrecht für die Gruppe
chmod o=r datei.txt       # Setzt Leserecht für andere
chmod a+rwx datei.txt     # Gibt allen Benutzern volle Rechte

# Berechtigungen ändern (numerisch)
chmod 755 skript.sh       # rwxr-xr-x
chmod 644 datei.txt        # rw-r--r--
chmod 600 geheim.txt      # rw-------
```

---
#### **2.2.3 Spezielle Berechtigungen**
| **Berechtigung** | **Beschreibung** | **Symbolisch** | **Numerisch** |
|------------------|------------------|----------------|---------------|
| **SUID (Set User ID)** | Führt die Datei mit den Rechten des Eigentümers aus. | `u+s` | `4` (z. B. `4755`) |
| **SGID (Set Group ID)** | Führt die Datei mit den Rechten der Gruppe aus. | `g+s` | `2` (z. B. `2755`) |
| **Sticky Bit** | Erlaubt nur dem Eigentümer, Dateien in einem Verzeichnis zu löschen. | `o+t` | `1` (z. B. `1777`) |

**Beispiele:**
```bash
# SUID setzen
chmod u+s /usr/bin/programm
chmod 4755 /usr/bin/programm

# SGID setzen
chmod g+s /pfad/zur/datei
chmod 2755 /pfad/zur/datei

# Sticky Bit setzen (z. B. für /tmp)
chmod o+t /tmp
chmod 1777 /tmp
```

---
---

### **2.3 Netzwerk-Grundlagen unter Linux**
#### **2.3.1 Netzwerkkonfiguration**
- **IP-Adresse anzeigen**:
  ```bash
  ip a
  ifconfig  # veraltet
  ```
- **Netzwerkinterface konfigurieren** (temporär):
  ```bash
  sudo ip addr add 192.168.1.100/24 dev eth0
  ```
- **Standard-Gateway setzen**:
  ```bash
  sudo ip route add default via 192.168.1.1
  ```
- **DNS-Server setzen**:
  ```bash
  sudo nano /etc/resolv.conf
  ```
  Fügen Sie folgende Zeile hinzu:
  ```
  nameserver 8.8.8.8
  nameserver 8.8.4.4
  ```

---
#### **2.3.2 Netzwerk-Tools**
| **Tool** | **Beschreibung** | **Beispiel** |
|----------|------------------|--------------|
| `ping` | Testet die Erreichbarkeit eines Hosts. | `ping google.com` |
| `traceroute` | Zeigt den Pfad zu einem Host an. | `traceroute google.com` |
| `mtr` | Kombiniert `ping` und `traceroute`. | `mtr google.com` |
| `netstat` | Zeigt Netzwerkverbindungen an. | `netstat -tuln` |
| `ss` | Moderner Ersatz für `netstat`. | `ss -tuln` |
| `iftop` | Zeigt Netzwerkverkehr in Echtzeit an. | `sudo iftop` |
| `nmap` | Netzwerk-Scanner. | `nmap -sS 192.168.1.1` |
| `curl` | Überträgt Daten von/bis einem Server. | `curl https://example.com` |
| `wget` | Lädt Dateien aus dem Internet herunter. | `wget https://example.com/datei.zip` |
| `dig` | DNS-Abfragen. | `dig example.com` |
| `nslookup` | DNS-Abfragen (veraltet). | `nslookup example.com` |

---
#### **2.3.3 Firewall-Konfiguration**
- **`ufw` (Uncomplicated Firewall)**:
  ```bash
  sudo ufw enable
  sudo ufw allow 22/tcp
  sudo ufw allow 80,443/tcp
  sudo ufw status
  ```
- **`iptables`**:
  ```bash
  sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
  sudo iptables -P INPUT DROP
  sudo iptables -L
  ```
- **`firewalld` (RHEL/CentOS)**:
  ```bash
  sudo firewall-cmd --add-service=ssh --permanent
  sudo firewall-cmd --add-service=http --permanent
  sudo firewall-cmd --reload
  ```

---
---

### **2.4 Paketverwaltung**
#### **2.4.1 Paketverwaltung unter Debian/Ubuntu (`apt`)**
| **Befehl** | **Beschreibung** | **Beispiel** |
|------------|------------------|--------------|
| `sudo apt update` | Aktualisiert die Paketlisten. | `sudo apt update` |
| `sudo apt upgrade` | Aktualisiert alle Pakete. | `sudo apt upgrade` |
| `sudo apt install [paket]` | Installiert ein Paket. | `sudo apt install nginx` |
| `sudo apt remove [paket]` | Entfernt ein Paket. | `sudo apt remove nginx` |
| `sudo apt purge [paket]` | Entfernt ein Paket inkl. Konfiguration. | `sudo apt purge nginx` |
| `sudo apt search [suchbegriff]` | Sucht nach Paketen. | `sudo apt search nginx` |
| `sudo apt show [paket]` | Zeigt Paketinformationen an. | `sudo apt show nginx` |

---
#### **2.4.2 Paketverwaltung unter RHEL/CentOS (`yum`/`dnf`)**
| **Befehl** | **Beschreibung** | **Beispiel** |
|------------|------------------|--------------|
| `sudo yum update` | Aktualisiert alle Pakete. | `sudo yum update` |
| `sudo yum install [paket]` | Installiert ein Paket. | `sudo yum install nginx` |
| `sudo yum remove [paket]` | Entfernt ein Paket. | `sudo yum remove nginx` |
| `sudo yum search [suchbegriff]` | Sucht nach Paketen. | `sudo yum search nginx` |

---
#### **2.4.3 Paketverwaltung unter Arch Linux (`pacman`)**
| **Befehl** | **Beschreibung** | **Beispiel** |
|------------|------------------|--------------|
| `sudo pacman -Syu` | Aktualisiert alle Pakete. | `sudo pacman -Syu` |
| `sudo pacman -S [paket]` | Installiert ein Paket. | `sudo pacman -S nginx` |
| `sudo pacman -R [paket]` | Entfernt ein Paket. | `sudo pacman -R nginx` |
| `sudo pacman -Ss [suchbegriff]` | Sucht nach Paketen. | `sudo pacman -Ss nginx` |

---
---

## **3. Fortgeschrittene ICT-Fähigkeiten unter Linux**

---

### **3.1 Systemüberwachung und Logging**
#### **3.1.1 Systemüberwachung**
| **Tool** | **Beschreibung** | **Beispiel** |
|----------|------------------|--------------|
| `top` | Zeigt laufende Prozesse in Echtzeit an. | `top` |
| `htop` | Interaktive Prozessanzeige. | `htop` |
| `vmstat` | Zeigt Systemleistung (CPU, Speicher, I/O). | `vmstat 1 5` |
| `iostat` | Zeigt E/A-Statistiken an. | `iostat -x 1 3` |
| `df` | Zeigt Festplattenbelegung an. | `df -h` |
| `du` | Zeigt Verzeichnisgrößen an. | `du -sh /home` |
| `free` | Zeigt Speichernutzung an. | `free -h` |
| `lsof` | Zeigt geöffnete Dateien und Prozesse an. | `lsof -i :22` |
| `glances` | All-in-One-Systemüberwachung. | `glances` |

---
#### **3.1.2 Logging**
| **Tool/Befehl** | **Beschreibung** | **Beispiel** |
|-----------------|------------------|--------------|
| `journalctl` | Zeigt Systemd-Logs an. | `journalctl -u nginx` |
| `tail -f /var/log/syslog` | Verfolgt System-Logs in Echtzeit. | `tail -f /var/log/syslog` |
| `grep` | Durchsucht Logs nach Mustern. | `grep "error" /var/log/syslog` |
| `logrotate` | Verwaltet Log-Rotation. | `sudo logrotate -f /etc/logrotate.conf` |

---
### **3.2 Automatisierung mit `cron` und `systemd`**
#### **3.2.1 `cron` für zeitgesteuerte Aufgaben**
- **Crontab-Datei bearbeiten**:
  ```bash
  crontab -e
  ```
- **Syntax**:
  ```
  * * * * * Befehl
  │ │ │ │ │
  │ │ │ │ └── Tag der Woche (0-6, 0=Sonntag)
  │ │ │ └──── Monat (1-12)
  │ │ └────── Tag des Monats (1-31)
  │ └──────── Stunde (0-23)
  └────────── Minute (0-59)
  ```
- **Beispiele**:
  ```bash
  # Täglich um 2:00 Uhr Backup erstellen
  0 2 * * * /usr/bin/tar -czvf /backup/home.tar.gz /home

  # Alle 30 Minuten Logs bereinigen
  */30 * * * * /usr/bin/find /var/log -name "*.log" -size +10M -delete
  ```

---
#### **3.2.2 `systemd`-Timer für zeitgesteuerte Aufgaben**
- **Timer-Datei erstellen** (`/etc/systemd/system/backup.timer`):
  ```ini
  [Unit]
  Description=Tägliches Backup

  [Timer]
  OnCalendar=daily
  Persistent=true

  [Install]
  WantedBy=timers.target
  ```
- **Service-Datei erstellen** (`/etc/systemd/system/backup.service`):
  ```ini
  [Unit]
  Description=Backup-Skript

  [Service]
  ExecStart=/usr/bin/tar -czvf /backup/home.tar.gz /home
  ```
- **Timer aktivieren**:
  ```bash
  sudo systemctl enable --now backup.timer
  ```

---
### **3.3 Benutzer- und Gruppenverwaltung**
| **Befehl** | **Beschreibung** | **Beispiel** |
|------------|------------------|--------------|
| `sudo adduser [benutzer]` | Erstellt einen neuen Benutzer. | `sudo adduser alice` |
| `sudo usermod -aG [gruppe] [benutzer]` | Fügt einen Benutzer zu einer Gruppe hinzu. | `sudo usermod -aG sudo alice` |
| `sudo deluser [benutzer]` | Löscht einen Benutzer. | `sudo deluser alice` |
| `sudo groupadd [gruppe]` | Erstellt eine neue Gruppe. | `sudo groupadd developers` |
| `sudo groupdel [gruppe]` | Löscht eine Gruppe. | `sudo groupdel developers` |
| `sudo passwd [benutzer]` | Ändert das Passwort eines Benutzers. | `sudo passwd alice` |
| `sudo chage [benutzer]` | Ändert Passwort-Richtlinien. | `sudo chage -M 90 alice` (Passwort alle 90 Tage ändern) |

---
### **3.4 Prozessmanagement**
| **Befehl** | **Beschreibung** | **Beispiel** |
|------------|------------------|--------------|
| `ps aux` | Zeigt alle laufenden Prozesse an. | `ps aux` |
| `pstree` | Zeigt Prozesse als Baum an. | `pstree` |
| `nice` | Startet einen Prozess mit einer bestimmten Priorität. | `nice -n 10 command` |
| `renice` | Ändert die Priorität eines laufenden Prozesses. | `renice -n 15 -p 1234` |
| `kill` | Beendet einen Prozess. | `kill -9 1234` |
| `pkill` | Beendet Prozesse nach Name. | `pkill nginx` |
| `killall` | Beendet alle Prozesse mit einem bestimmten Namen. | `killall nginx` |
| `bg` | Setzt einen Prozess in den Hintergrund. | `bg` |
| `fg` | Holt einen Prozess in den Vordergrund. | `fg %1` |
| `jobs` | Zeigt Hintergrundprozesse an. | `jobs` |

---
### **3.5 Dateisystem- und Speicherverwaltung**
#### **3.5.1 Dateisysteme**
| **Dateisystem** | **Beschreibung** | **Vorteile** | **Nachteile** |
|----------------|------------------|--------------|---------------|
| **ext4** | Standard-Dateisystem für Linux. | Schnell, stabil, weit verbreitet. | Keine native Verschlüsselung. |
| **Btrfs** | Modernes Dateisystem mit Snapshots und Deduplizierung. | Snapshots, Deduplizierung, Kompression. | Höhere CPU-Last. |
| **XFS** | Hochperformantes Dateisystem für große Dateien. | Schnell für große Dateien, skalierbar. | Keine Snapshots. |
| **ZFS** | Dateisystem mit Fokus auf Datenintegrität. | Snapshots, Deduplizierung, Checksums. | Hoher Speicherbedarf. |
| **NTFS** | Windows-Dateisystem (lesbar/schreibbar mit `ntfs-3g`). | Kompatibel mit Windows. | Langsam unter Linux. |
| **FAT32** | Einfaches Dateisystem für Wechselmedien. | Kompatibel mit allen Systemen. | Keine Dateien > 4 GB. |

---
#### **3.5.2 Speicherverwaltung**
| **Befehl** | **Beschreibung** | **Beispiel** |
|------------|------------------|--------------|
| `df -h` | Zeigt Festplattenbelegung an. | `df -h` |
| `du -sh /pfad` | Zeigt Verzeichnisgrößen an. | `du -sh /home` |
| `fdisk -l` | Zeigt Partitionen an. | `sudo fdisk -l` |
| `lsblk` | Zeigt Blockgeräte an. | `lsblk` |
| `mount` | Mountet ein Dateisystem. | `sudo mount /dev/sdb1 /mnt` |
| `umount` | Unmountet ein Dateisystem. | `sudo umount /mnt` |
| `mkfs` | Erstellt ein Dateisystem. | `sudo mkfs.ext4 /dev/sdb1` |
| `fsck` | Überprüft und repariert ein Dateisystem. | `sudo fsck /dev/sdb1` |
| `lvm` | Logical Volume Manager. | `sudo lvcreate -L 10G -n myvolume mygroup` |

---
### **3.6 Netzwerk-Dienste und Server**
#### **3.6.1 Webserver (Apache/Nginx)**
- **Apache installieren und starten**:
  ```bash
  sudo apt install apache2
  sudo systemctl start apache2
  sudo systemctl enable apache2
  ```
- **Nginx installieren und starten**:
  ```bash
  sudo apt install nginx
  sudo systemctl start nginx
  sudo systemctl enable nginx
  ```

---
#### **3.6.2 Datenbanken (MySQL/MariaDB/PostgreSQL)**
- **MySQL/MariaDB installieren**:
  ```bash
  sudo apt install mysql-server
  sudo systemctl start mysql
  sudo mysql_secure_installation
  ```
- **PostgreSQL installieren**:
  ```bash
  sudo apt install postgresql postgresql-contrib
  sudo systemctl start postgresql
  ```

---
#### **3.6.3 SSH-Server**
- **OpenSSH-Server installieren**:
  ```bash
  sudo apt install openssh-server
  sudo systemctl start ssh
  sudo systemctl enable ssh
  ```
- **Konfiguration anpassen** (`/etc/ssh/sshd_config`):
  ```ini
  Port 2222
  PermitRootLogin no
  PasswordAuthentication no
  ```
- **Dienst neu starten**:
  ```bash
  sudo systemctl restart ssh
  ```

---
#### **3.6.4 DNS-Server (Bind9)**
- **Bind9 installieren**:
  ```bash
  sudo apt install bind9
  sudo systemctl start bind9
  sudo systemctl enable bind9
  ```
- **Konfiguration anpassen** (`/etc/bind/named.conf.options`):
  ```ini
  forwarders {
      8.8.8.8;
      8.8.4.4;
  };
  ```

---
#### **3.6.5 DHCP-Server (ISC DHCP)**
- **ISC DHCP installieren**:
  ```bash
  sudo apt install isc-dhcp-server
  sudo systemctl start isc-dhcp-server
  sudo systemctl enable isc-dhcp-server
  ```
- **Konfiguration anpassen** (`/etc/dhcp/dhcpd.conf`):
  ```ini
  subnet 192.168.1.0 netmask 255.255.255.0 {
      range 192.168.1.100 192.168.1.200;
      option routers 192.168.1.1;
      option domain-name-servers 8.8.8.8, 8.8.4.4;
  }
  ```

---
---
## **4. Arbeiten in Linux: Best Practices**

---

### **4.1 Effizientes Arbeiten mit der Kommandozeile**
#### **4.1.1 Tastenkürzel für die Bash**
| **Tastenkürzel** | **Beschreibung** |
|-----------------|------------------|
| `Strg + C` | Beendet den aktuellen Befehl. |
| `Strg + Z` | Unterbricht den aktuellen Befehl (in den Hintergrund). |
| `Strg + D` | Beendet die aktuelle Shell-Sitzung (oder `exit`). |
| `Strg + R` | Durchsucht den Befehlsverlauf (reverse search). |
| `Strg + L` | Löscht den Bildschirm (wie `clear`). |
| `Strg + U` | Löscht die aktuelle Zeile. |
| `Strg + K` | Löscht von der Cursor-Position bis zum Ende der Zeile. |
| `Strg + Y` | Fügt die zuletzt gelöschte Zeile ein. |
| `Alt + .` | Fügt das letzte Argument des vorherigen Befehls ein. |
| `Tab` | Vervollständigt Befehle/Dateinamen. |
| `Strg + Alt + T` | Öffnet ein neues Terminal-Fenster (in vielen Desktop-Umgebungen). |

---
#### **4.1.2 Aliase und Funktionen**
- **Aliase erstellen** (in `~/.bashrc`):
  ```bash
  alias ll='ls -alF'
  alias la='ls -A'
  alias l='ls -CF'
  alias update='sudo apt update && sudo apt upgrade -y'
  ```
- **Funktionen erstellen** (in `~/.bashrc`):
  ```bash
  function grep_ip {
      grep -Eo '([0-9]{1,3}\.){3}[0-9]{1,3}' "$1"
  }
  ```
- **Änderungen laden**:
  ```bash
  source ~/.bashrc
  ```

---
#### **4.1.3 Pipes und Umleitungen**
| **Operator** | **Beschreibung** | **Beispiel** |
|--------------|------------------|--------------|
| `|` | Leitet die Ausgabe eines Befehls an einen anderen weiter. | `ls -l | grep "txt"` |
| `>` | Leitet die Ausgabe in eine Datei um (überschreibt). | `echo "Hallo" > datei.txt` |
| `>>` | Leitet die Ausgabe in eine Datei um (anhängen). | `echo "Welt" >> datei.txt` |
| `<` | Leitet den Inhalt einer Datei als Eingabe weiter. | `sort < datei.txt` |
| `2>` | Leitet Fehlerausgabe in eine Datei um. | `ls /nonexistent 2> fehler.log` |
| `2>>` | Leitet Fehlerausgabe in eine Datei um (anhängen). | `ls /nonexistent 2>> fehler.log` |
| `&>` | Leitet Standard- und Fehlerausgabe in eine Datei um. | `ls /nonexistent &> ausgabe.log` |

---
#### **4.1.4 Textverarbeitung mit `awk`, `sed` und `cut`**
| **Tool** | **Beschreibung** | **Beispiel** |
|----------|------------------|--------------|
| `awk` | Textverarbeitung und Mustererkennungs-Tool. | `awk '{print $1}' datei.txt` (erste Spalte anzeigen) |
| `sed` | Stream-Editor für Textmanipulation. | `sed 's/alt/neu/g' datei.txt` (Ersetze "alt" durch "neu") |
| `cut` | Extrahiert Abschnitte aus Dateien. | `cut -d',' -f1 datei.csv` (Erste Spalte einer CSV-Datei) |

---
### **4.2 Datei- und Verzeichnisverwaltung**
#### **4.2.1 Effizientes Suchen mit `find`**
| **Option** | **Beschreibung** | **Beispiel** |
|------------|------------------|--------------|
| `-name` | Sucht nach Dateinamen. | `find /home -name "*.txt"` |
| `-iname` | Sucht nach Dateinamen (case-insensitive). | `find /home -iname "*.TXT"` |
| `-type` | Filtert nach Dateityp (`f`=Datei, `d`=Verzeichnis). | `find /home -type d` |
| `-size` | Filtert nach Dateigröße. | `find /home -size +10M` (Dateien > 10 MB) |
| `-mtime` | Filtert nach Änderungszeit. | `find /home -mtime -7` (Dateien, die in den letzten 7 Tagen geändert wurden) |
| `-exec` | Führt einen Befehl auf gefundenen Dateien aus. | `find /home -name "*.log" -exec rm {} \;` |

---
#### **4.2.2 Effizientes Kopieren mit `rsync`**
```bash
# Lokales Backup
rsync -avz /quelle /ziel

# Remote-Backup (über SSH)
rsync -avz -e ssh /quelle user@remote:/ziel

# Inkrementelles Backup mit Hardlinks
rsync -avz --link-dest=/vollbackup /quelle /ziel/incremental
```

---
### **4.3 Systemadministration: Best Practices**
#### **4.3.1 Benutzerverwaltung**
- **Prinzip der geringsten Rechte**: Benutzer sollten nur die **minimalen Berechtigungen** erhalten, die sie benötigen.
- **`sudo` statt `root`**: Verwenden Sie `sudo` für administrative Aufgaben, um **Sicherheitsrisiken** zu minimieren.
- **Passwort-Richtlinien**:
  - **Länge**: Mindestens 12 Zeichen.
  - **Komplexität**: Groß-/Kleinschreibung, Zahlen, Sonderzeichen.
  - **Regelmäßige Änderung**: Alle 90 Tage.
  - **Keine Wiederverwendung**: Keine alten Passwörter wiederverwenden.

---
#### **4.3.2 Sicherheitsbest Practices**
- **Firewall aktivieren**:
  ```bash
  sudo ufw enable
  sudo ufw default deny incoming
  sudo ufw default allow outgoing
  ```
- **SSH absichern**:
  - **Port ändern** (z. B. auf `2222`).
  - **Root-Login deaktivieren** (`PermitRootLogin no`).
  - **Passwort-Authentifizierung deaktivieren** (`PasswordAuthentication no`).
  - **SSH-Schlüssel verwenden**.
- **Regelmäßige Updates**:
  ```bash
  sudo apt update && sudo apt upgrade -y
  ```
- **Fail2Ban installieren**:
  ```bash
  sudo apt install fail2ban
  sudo systemctl enable --now fail2ban
  ```
- **Log-Überwachung**:
  ```bash
  sudo tail -f /var/log/auth.log | grep "Failed password"
  ```

---
#### **4.3.3 Backup-Strategien**
- **3-2-1-Regel**:
  - **3 Kopien** Ihrer Daten.
  - **2 verschiedene Medientypen** (z. B. Festplatte + Cloud).
  - **1 Backup außerhalb des Standorts**.
- **Automatisierte Backups** (z. B. mit `cron` oder `systemd`):
  ```bash
  0 2 * * * /usr/bin/rsync -avz /home /mnt/backup/home
  ```
- **Backup-Tools**:
  - **`tar`**: Einfache Archive.
  - **`rsync`**: Inkrementelle Backups.
  - **`BorgBackup`**: Deduplizierende Backups mit Verschlüsselung.
  - **`Timeshift`**: System-Snapshots.

---
#### **4.3.4 Überwachung und Wartung**
- **Systemüberwachung**:
  - **`top`/`htop`**: Prozessüberwachung.
  - **`vmstat`/`iostat`**: Systemleistung.
  - **`df`/`du`**: Speicherbelegung.
  - **`glances`**: All-in-One-Überwachung.
- **Log-Analyse**:
  - **`journalctl`**: Systemd-Logs.
  - **`grep`**: Logs durchsuchen.
  - **`logwatch`**: Automatisierte Log-Analyse.
- **Automatisierte Wartung**:
  - **`cron`**: Zeitgesteuerte Aufgaben.
  - **`systemd`-Timer**: Modernere Alternative zu `cron`.
  - **`logrotate`**: Log-Rotation.

---
---
## **5. Zusammenarbeit und Kommunikation in Linux**

---

### **5.1 Kollaboration mit Git**
#### **5.1.1 Git-Grundlagen**
| **Befehl** | **Beschreibung** | **Beispiel** |
|------------|------------------|--------------|
| `git init` | Initialisiert ein neues Git-Repository. | `git init` |
| `git clone [url]` | Klont ein Repository. | `git clone https://github.com/user/repo.git` |
| `git add [datei]` | Fügt eine Datei zum Staging-Bereich hinzu. | `git add datei.txt` |
| `git commit -m "[nachricht]"` | Commited Änderungen. | `git commit -m "Fehler behoben"` |
| `git push` | Pushes Änderungen zum Remote-Repository. | `git push origin main` |
| `git pull` | Pullt Änderungen vom Remote-Repository. | `git pull origin main` |
| `git branch` | Listet Branches auf. | `git branch` |
| `git checkout [branch]` | Wechselt zu einem Branch. | `git checkout feature` |
| `git merge [branch]` | Merge einen Branch. | `git merge feature` |
| `git status` | Zeigt den Status des Repositorys an. | `git status` |
| `git log` | Zeigt das Commit-Protokoll an. | `git log` |

---
#### **5.1.2 Git-Workflows**
- **Feature-Branch-Workflow**:
  1. **Branch erstellen**:
     ```bash
     git checkout -b feature-neue-funktion
     ```
  2. **Änderungen commiten**:
     ```bash
     git add .
     git commit -m "Neue Funktion hinzugefügt"
     ```
  3. **Branch pushen**:
     ```bash
     git push origin feature-neue-funktion
     ```
  4. **Pull Request erstellen** (auf GitHub/GitLab).
  5. **Branch mergen** (nach Review).

- **GitFlow-Workflow**:
  - **`main`/`master`**: Stabiler Branch.
  - **`develop`**: Entwicklungsbranch.
  - **`feature/*`**: Feature-Branches.
  - **`release/*`**: Release-Branches.
  - **`hotfix/*`**: Hotfix-Branches.

---
#### **5.1.3 Git-Hosting-Plattformen**
| **Plattform** | **Beschreibung** | **Website** |
|--------------|------------------|-------------|
| **GitHub** | Größte Plattform für Open-Source-Projekte. | [github.com](https://github.com/) |
| **GitLab** | Selbstgehostete Alternative mit CI/CD. | [gitlab.com](https://about.gitlab.com/) |
| **Bitbucket** | Git-Hosting für Teams (kostenlos für kleine Teams). | [bitbucket.org](https://bitbucket.org/) |
| **Gitea** | Leichtgewichtige, selbstgehostete Alternative. | [gitea.io](https://gitea.io/) |

---
### **5.2 Kommunikationstools**
#### **5.2.1 E-Mail (Thunderbird, Mutt)**
- **Thunderbird installieren**:
  ```bash
  sudo apt install thunderbird
  ```
- **Mutt (CLI-E-Mail-Client) installieren**:
  ```bash
  sudo apt install mutt
  ```

---
#### **5.2.2 Chat und Kollaboration**
| **Tool** | **Beschreibung** | **Installation** |
|----------|------------------|------------------|
| **Signal** | Verschlüsselte Messaging-App. | [signal.org](https://signal.org/) |
| **Element (Matrix)** | Dezentrale Messaging-App. | `sudo apt install element-desktop` |
| **Mattermost** | Selbstgehosteter Slack-Alternative. | [mattermost.com](https://mattermost.com/) |
| **Rocket.Chat** | Selbstgehosteter Chat-Server. | [rocket.chat](https://rocket.chat/) |
| **IRC (Internet Relay Chat)** | Textbasierter Chat. | `sudo apt install irssi` |

---
#### **5.2.3 Videokonferenz**
| **Tool** | **Beschreibung** | **Installation** |
|----------|------------------|------------------|
| **Jitsi Meet** | Videokonferenz-Software. | [jitsi.org](https://jitsi.org/) |
| **BigBlueButton** | Webkonferenz-System für Bildung. | [bigbluebutton.org](https://bigbluebutton.org/) |
| **Zoom (Open-Source-Alternativen)** | Videokonferenz. | **Jitsi Meet** oder **BigBlueButton** |

---
### **5.3 Dokumentation und Wissensmanagement**
#### **5.3.1 Dokumentation mit Markdown**
- **Markdown** ist eine **einfache Auszeichnungssprache** für die Erstellung von Dokumentationen.
- **Beispiel**:
  ```markdown
  # Überschrift 1
  ## Überschrift 2
  - Liste
  - Liste
  **Fett**
  *Kursiv*
  [Link](https://example.com)
  ![Bild](bild.png)
  ```

---
#### **5.3.2 Wissensmanagement-Tools**
| **Tool** | **Beschreibung** | **Installation** |
|----------|------------------|------------------|
| **Joplin** | Open-Source-Notiz-App mit Markdown-Unterstützung. | `sudo apt install joplin` |
| **Wiki.js** | Selbstgehostete Wiki-Software. | [js.wiki](https://js.wiki/) |
| **DokuWiki** | Einfache Wiki-Software. | [dokuwiki.org](https://www.dokuwiki.org/) |
| **BookStack** | Plattform für Dokumentation und Wissensmanagement. | [bookstackapp.com](https://www.bookstackapp.com/) |

---
---
## **6. Karrierewege und Zertifizierungen für ICT-Profis**

---

### **6.1 Karrierewege in der ICT-Branche**
| **Berufsfeld** | **Beschreibung** | **Benötigte Fähigkeiten** |
|---------------|------------------|---------------------------|
| **Systemadministrator** | Verwaltung von Servern, Netzwerken und Systemen. | Linux, Netzwerk, Skripting, Sicherheit |
| **DevOps-Engineer** | Automatisierung von Softwarebereitstellung und Infrastruktur. | Linux, Docker, Kubernetes, CI/CD, Skripting |
| **Netzwerkadministrator** | Verwaltung von Netzwerken und Firewalls. | Linux, Netzwerkprotokolle, Firewall-Konfiguration |
| **Sicherheitsanalyst** | Analyse von Sicherheitsvorfällen und Schutz vor Bedrohungen. | Linux, Firewalls, IDS/IPS, Penetration Testing |
| **Cloud-Engineer** | Verwaltung von Cloud-Infrastrukturen (AWS, Azure, GCP). | Linux, Docker, Kubernetes, Terraform |
| **Softwareentwickler** | Entwicklung von Anwendungen und Software. | Linux, Programmierung (Python, Java, etc.), Git |
| **Datenbankadministrator** | Verwaltung von Datenbanken. | Linux, SQL, MySQL/PostgreSQL, MongoDB |
| **IT-Support** | Unterstützung von Benutzern bei technischen Problemen. | Linux, Troubleshooting, Benutzerverwaltung |

---
### **6.2 Zertifizierungen für Linux und ICT**
| **Zertifizierung** | **Anbieter** | **Beschreibung** | **Website** |
|-------------------|--------------|------------------|-------------|
| **Linux Professional Institute Certification (LPIC)** | LPI | Zertifizierung für Linux-Administratoren. | [lpi.org](https://www.lpi.org/) |
| **Red Hat Certified Engineer (RHCE)** | Red Hat | Zertifizierung für RHEL-Administratoren. | [redhat.com](https://www.redhat.com/) |
| **CompTIA Linux+** | CompTIA | Vendor-neutrale Linux-Zertifizierung. | [comptia.org](https://www.comptia.org/) |
| **Certified Kubernetes Administrator (CKA)** | CNCF | Zertifizierung für Kubernetes-Administratoren. | [cncf.io](https://www.cncf.io/) |
| **AWS Certified SysOps Administrator** | Amazon | Zertifizierung für AWS-Administratoren. | [aws.amazon.com](https://aws.amazon.com/) |
| **Microsoft Certified: Azure Administrator Associate** | Microsoft | Zertifizierung für Azure-Administratoren. | [microsoft.com](https://www.microsoft.com/) |
| **Certified Ethical Hacker (CEH)** | EC-Council | Zertifizierung für ethisches Hacking. | [eccouncil.org](https://www.eccouncil.org/) |
| **Offensive Security Certified Professional (OSCP)** | Offensive Security | Praktische Zertifizierung für Penetration Testing. | [offensive-security.com](https://www.offensive-security.com/) |

---
### **6.3 Lernressourcen für ICT-Fähigkeiten**
| **Ressource** | **Beschreibung** | **Website** |
|--------------|------------------|-------------|
| **Linux Journey** | Interaktive Lernplattform für Linux. | [linuxjourney.com](https://linuxjourney.com/) |
| **The Linux Documentation Project** | Dokumentation für Linux. | [tldp.org](https://tldp.org/) |
| **OverTheWire (Bandit)** | Praktische Übungen für Linux-Sicherheit. | [overthewire.org](https://overthewire.org/wargames/bandit/) |
| **Linux Academy (A Cloud Guru)** | Online-Kurse für Linux und Cloud. | [acloudguru.com](https://acloudguru.com/) |
| **Udemy** | Online-Kurse für verschiedene ICT-Themen. | [udemy.com](https://www.udemy.com/) |
| **Coursera** | Online-Kurse von Universitäten und Unternehmen. | [coursera.org](https://www.coursera.org/) |
| **edX** | Online-Kurse von Universitäten. | [edx.org](https://www.edx.org/) |
| **YouTube (z. B. The Linux Foundation, NetworkChuck)** | Kostenlose Tutorials. | [youtube.com](https://www.youtube.com/) |

---
---
## **7. Übungsaufgaben**

---
### **Frage 1**
Wie können Sie **alle Dateien mit der Endung `.log`** im Verzeichnis `/var/log` finden und löschen?

??? success "Antwort"
    ```bash
    sudo find /var/log -name "*.log" -delete
    ```
    oder:
    ```bash
    sudo find /var/log -name "*.log" -exec rm {} \;
    ```

---
### **Frage 2**
Wie können Sie ein **Bash-Skript** erstellen, das alle **`.txt`-Dateien** in einem Verzeichnis in ein **`backup`-Verzeichnis** kopiert?

??? success "Antwort"
    ```bash
    #!/bin/bash

    # Erstelle Backup-Verzeichnis, falls nicht vorhanden
    mkdir -p backup

    # Kopiere alle .txt-Dateien in das Backup-Verzeichnis
    find . -name "*.txt" -exec cp {} backup/ \;
    ```
    Speichern Sie das Skript als `backup_txt.sh`, machen Sie es ausführbar und führen Sie es aus:
    ```bash
    chmod +x backup_txt.sh
    ./backup_txt.sh
    ```

---
### **Frage 3**
Wie können Sie **alle Prozesse anzeigen**, die **Port 80** verwenden?

??? success "Antwort"
    ```bash
    sudo lsof -i :80
    ```
    oder:
    ```bash
    sudo ss -tulnp | grep ":80"
    ```

---
### **Frage 4**
Wie können Sie **einen neuen Benutzer `alice`** mit dem Home-Verzeichnis `/home/alice` erstellen und ihn zur Gruppe `sudo` hinzufügen?

??? success "Antwort"
    ```bash
    sudo adduser alice
    sudo usermod -aG sudo alice
    ```

---
### **Frage 5**
Wie können Sie **ein Cron-Job einrichten**, das **täglich um 3:00 Uhr** ein Backup des Verzeichnisses `/home` in `/mnt/backup` erstellt?

??? success "Antwort"
    ```bash
    crontab -e
    ```
    Fügen Sie folgende Zeile hinzu:
    ```bash
    0 3 * * * /usr/bin/rsync -avz /home /mnt/backup
    ```

---
### **Frage 6**
Wie können Sie **die letzten 10 Zeilen** der Datei `/var/log/syslog` anzeigen und nach dem Wort **"error"** filtern?

??? success "Antwort"
    ```bash
    tail -n 10 /var/log/syslog | grep "error"
    ```

---
### **Frage 7**
Wie können Sie **die Berechtigungen** der Datei `/etc/shadow` so ändern, dass **nur der Eigentümer** sie lesen und schreiben kann?

??? success "Antwort"
    ```bash
    sudo chmod 600 /etc/shadow
    ```

---
### **Frage 8**
Wie können Sie **einen SSH-Schlüssel** für den Benutzer `alice` generieren und den öffentlichen Schlüssel auf einem Remote-Server installieren?

??? success "Antwort"
    1. **Schlüssel generieren** (auf dem lokalen Rechner):
       ```bash
       ssh-keygen -t ed25519 -C "alice@example.com"
       ```
    2. **Öffentlichen Schlüssel kopieren** (auf dem Remote-Server):
       ```bash
       ssh-copy-id -i ~/.ssh/id_ed25519.pub alice@remote-server
       ```

---
### **Frage 9**
Wie können Sie **die IP-Adresse und den Hostnamen** Ihres Systems anzeigen?

??? success "Antwort"
    ```bash
    # IP-Adresse anzeigen
    ip a
    # oder
    hostname -I

    # Hostname anzeigen
    hostname
    ```

---
### **Frage 10**
Wie können Sie **ein Git-Repository klonen** und einen **neuen Branch `feature`** erstellen?

??? success "Antwort"
    ```bash
    # Repository klonen
    git clone https://github.com/user/repo.git
    cd repo

    # Neuen Branch erstellen und wechseln
    git checkout -b feature
    ```

---
---
## **8. Praktische Beispiele**

---
### **Beispiel 1: Automatisiertes Backup-Skript**
**Szenario:** Sie möchten ein **tägliches Backup** des Verzeichnisses `/home` in `/mnt/backup` erstellen und **alte Backups (älter als 7 Tage) löschen**.

**Lösung:**
```bash
#!/bin/bash

# Backup-Verzeichnis
BACKUP_DIR="/mnt/backup"
SOURCE_DIR="/home"
DATE=$(date +%Y-%m-%d)

# Erstelle Backup-Verzeichnis, falls nicht vorhanden
mkdir -p "$BACKUP_DIR"

# Erstelle tar.gz-Backup
tar -czvf "$BACKUP_DIR/home_backup_$DATE.tar.gz" "$SOURCE_DIR"

# Lösche Backups, die älter als 7 Tage sind
find "$BACKUP_DIR" -name "home_backup_*.tar.gz" -mtime +7 -delete

echo "Backup abgeschlossen: $BACKUP_DIR/home_backup_$DATE.tar.gz"
```
**Ausführbar machen und testen:**
```bash
chmod +x backup_skript.sh
./backup_skript.sh
```

---
### **Beispiel 2: Benutzerverwaltung-Skript**
**Szenario:** Sie möchten ein **Skript erstellen**, das **neue Benutzer** basierend auf einer Liste erstellt und ihnen **Standardberechtigungen** zuweist.

**Lösung:**
```bash
#!/bin/bash

# Liste der Benutzer (eine pro Zeile)
USERS="alice bob charlie"

# Gruppe, zu der die Benutzer hinzugefügt werden sollen
GROUP="developers"

# Erstelle Gruppe, falls nicht vorhanden
sudo groupadd -f "$GROUP"

# Erstelle Benutzer und füge sie zur Gruppe hinzu
for user in $USERS; do
    if ! id "$user" &>/dev/null; then
        sudo adduser "$user"
        sudo usermod -aG "$GROUP" "$user"
        echo "Benutzer $user erstellt und zur Gruppe $GROUP hinzugefügt."
    else
        echo "Benutzer $user existiert bereits."
    fi
done
```
**Ausführbar machen und testen:**
```bash
chmod +x create_users.sh
sudo ./create_users.sh
```

---
### **Beispiel 3: Systemüberwachung mit `glances`**
**Szenario:** Sie möchten **Echtzeit-Systeminformationen** (CPU, Speicher, Netzwerk, etc.) anzeigen.

**Lösung:**
1. **`glances` installieren**:
   ```bash
   sudo apt install glances
   ```
2. **`glances` starten**:
   ```bash
   glances
   ```
   - **`q`**: Beendet `glances`.
   - **`c`**: Sortiert nach CPU-Auslastung.
   - **`m`**: Sortiert nach Speichernutzung.

---
### **Beispiel 4: Netzwerk-Scan mit `nmap`**
**Szenario:** Sie möchten **alle offenen Ports** auf einem Server mit der IP `192.168.1.100` scannen.

**Lösung:**
```bash
nmap -sS -p- 192.168.1.100
```
- **`-sS`**: TCP SYN Scan (schnell und unauffällig).
- **`-p-`**: Scan aller Ports (1-65535).

---
### **Beispiel 5: Git-Workflow für ein Projekt**
**Szenario:** Sie arbeiten an einem **neuen Feature** für ein Projekt und möchten Ihre Änderungen **in einem separaten Branch** entwickeln.

**Lösung:**
1. **Branch erstellen und wechseln**:
   ```bash
   git checkout -b feature-neue-funktion
   ```
2. **Änderungen vornehmen und commiten**:
   ```bash
   git add .
   git commit -m "Neue Funktion hinzugefügt"
   ```
3. **Branch pushen**:
   ```bash
   git push origin feature-neue-funktion
   ```
4. **Pull Request erstellen** (auf GitHub/GitLab).
5. **Nach Review mergen**:
   ```bash
   git checkout main
   git merge feature-neue-funktion
   git push origin main
   ```

---
---
## **9. Häufige Fehler und Lösungen**

| **Problem** | **Ursache** | **Lösung** |
|-------------|-------------|------------|
| **`bash: command not found`** | Befehl ist nicht installiert oder nicht im `$PATH`. | Installieren Sie das Paket oder verwenden Sie den vollen Pfad. |
| **`Permission denied`** | Keine Berechtigung für die Datei/Befehl. | Verwenden Sie `sudo` oder passen Sie die Berechtigungen an. |
| **`No such file or directory`** | Datei oder Verzeichnis existiert nicht. | Überprüfen Sie den Pfad. |
| **`Disk full`** | Festplatte ist voll. | Löschen Sie unnötige Dateien oder erweitern Sie den Speicher. |
| **`Connection refused` (SSH)** | SSH-Server läuft nicht oder Firewall blockiert Port 22. | Starten Sie den SSH-Server (`sudo systemctl start ssh`) und überprüfen Sie die Firewall. |
| **`Git: fatal: not a git repository`** | Sie befinden sich nicht in einem Git-Repository. | Wechseln Sie in das Repository-Verzeichnis oder initialisieren Sie ein neues Repository (`git init`). |
| **`Cron-Job wird nicht ausgeführt`** | Falsche Syntax oder Berechtigungen. | Überprüfen Sie die Crontab-Syntax (`crontab -e`) und die Logs (`/var/log/syslog`). |
| **`rsync: failed to set permissions`** | Berechtigungsprobleme beim Ziel. | Verwenden Sie `sudo` oder passen Sie die Berechtigungen an. |
| **`tar: Cowardly refusing to create an empty archive`** | Keine Dateien zum Sichern gefunden. | Überprüfen Sie den Pfad zur Quelle. |
| **`SSH: Permission denied (publickey)`** | Falscher oder fehlender SSH-Schlüssel. | Überprüfen Sie die Berechtigungen (`chmod 600 ~/.ssh/id_rsa`) und den öffentlichen Schlüssel auf dem Server. |

---
---
## **10. Zusammenfassung: ICT-Fähigkeiten unter Linux**

| **Kategorie** | **Wichtige Fähigkeiten** | **Tools/Befehle** |
|---------------|--------------------------|------------------|
| **Kommandozeile** | Navigation, Dateioperationen, Berechtigungen, Prozesse | `cd`, `ls`, `cp`, `mv`, `rm`, `chmod`, `chown`, `ps`, `top`, `htop` |
| **Skripting** | Automatisierung, Bash-Skripte | `#!/bin/bash`, `if`, `for`, `while`, `function` |
| **Netzwerk** | Konfiguration, Überwachung, Sicherheit | `ip`, `ping`, `traceroute`, `ss`, `netstat`, `nmap`, `ufw`, `iptables` |
| **Paketverwaltung** | Installation, Aktualisierung, Entfernung | `apt`, `yum`, `dnf`, `pacman`, `dpkg`, `rpm` |
| **Systemüberwachung** | Prozesse, Speicher, Festplatten, Logs | `top`, `htop`, `vmstat`, `iostat`, `df`, `du`, `journalctl`, `tail -f` |
| **Benutzerverwaltung** | Benutzer, Gruppen, Berechtigungen | `adduser`, `usermod`, `groupadd`, `passwd`, `chage` |
| **Automatisierung** | Zeitgesteuerte Aufgaben | `cron`, `systemd`-Timer, `at` |
| **Dateisystem** | Partitionen, Mounten, Dateisysteme | `fdisk`, `mkfs`, `mount`, `umount`, `df`, `du`, `lvm` |
| **Netzwerkdienste** | Webserver, Datenbanken, SSH, DNS, DHCP | `apache2`, `nginx`, `mysql`, `postgresql`, `openssh-server`, `bind9`, `isc-dhcp-server` |
| **Zusammenarbeit** | Versionskontrolle, Kommunikation | `git`, `GitHub`, `GitLab`, `Signal`, `Jitsi Meet`, `Mattermost` |
| **Sicherheit** | Firewall, SSH, Fail2Ban, Log-Analyse | `ufw`, `iptables`, `firewalld`, `fail2ban`, `grep`, `logwatch` |
| **Backup** | Vollbackup, Inkrementell, Snapshots | `tar`, `rsync`, `dd`, `BorgBackup`, `Timeshift` |

---
---
## **11. Fazit: ICT-Fähigkeiten und Arbeiten in Linux**
Linux ist ein **mächtiges und vielseitiges Betriebssystem**, das in **nahezu allen Bereichen der ICT** eingesetzt wird. Durch das Beherrschen der in diesem Modul vorgestellten **Fähigkeiten, Tools und Best Practices** können Sie:
- **Effizienter arbeiten** (Kommandozeile, Skripting, Automatisierung).
- **Systeme verwalten** (Benutzer, Berechtigungen, Netzwerk, Speicher).
- **Sicherheit gewährleisten** (Firewall, SSH, Backups, Überwachung).
- **Zusammenarbeiten** (Git, Kommunikationstools, Dokumentation).
- **Ihre Karriere vorantreiben** (Zertifizierungen, Lernressourcen).

### **Empfehlungen für den Einstieg:**
1. **Üben, üben, üben**: Nutzen Sie die **Kommandozeile** für tägliche Aufgaben.
2. **Skripte schreiben**: Automatisieren Sie **wiederkehrende Aufgaben** mit Bash-Skripten.
3. **Projekte auf GitHub/GitLab**: Tragen Sie zu **Open-Source-Projekten** bei oder erstellen Sie eigene.
4. **Zertifizierungen anstreben**: Erlangen Sie **Linux-Zertifizierungen** (z. B. LPIC, RHCE).
5. **Community beitreten**: Tauschen Sie sich in **Foren, Chat-Gruppen und auf Konferenzen** aus.

### **Nächste Schritte:**
- **Vertiefen Sie Ihr Wissen** in spezifischen Bereichen (z. B. Netzwerk, Sicherheit, Cloud).
- **Experimentieren Sie** mit verschiedenen Linux-Distributionen (Ubuntu, Fedora, Arch Linux).
- **Bauen Sie ein Homelab** auf, um **praktische Erfahrungen** zu sammeln (z. B. mit VirtualBox, Proxmox, Raspberry Pi).
- **Bleiben Sie auf dem Laufenden** mit **ICT-Nachrichten und Trends** (z. B. über [LWN.net](https://lwn.net/), [OpenSource.com](https://opensource.com/)).

