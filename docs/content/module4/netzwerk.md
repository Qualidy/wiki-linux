
### **Modul IV: Systemadministration und Sicherheit**
### **Thema: Netzwerksicherheit und Firewall-Konfiguration**

---

#### **1. Einführung in Netzwerksicherheit**
Netzwerksicherheit ist ein **kritischer Bestandteil** der Systemadministration. Sie umfasst:
- **Zugangskontrolle** (Wer darf auf das Netzwerk zugreifen?)
- **Datenintegrität** (Sind die Daten unverändert?)
- **Vertraulichkeit** (Sind die Daten geschützt?)
- **Verfügbarkeit** (Ist das Netzwerk verfügbar, wenn es gebraucht wird?)

Die **Firewall** ist ein zentrales Werkzeug, um **unautorisierten Zugriff** zu blockieren und den **Netzwerkverkehr** zu kontrollieren.

---

#### **2. Grundlagen der Firewall**
Eine **Firewall** ist eine **Netzwerkkomponente**, die den **Datenverkehr** zwischen Netzwerken oder Hosts **filtert und überwacht**. Sie kann:
- **Erlaubten Verkehr** durchlassen.
- **Blockierten Verkehr** abweisen.
- **Protokolle und Ports** steuern.
- **IP-Adressen und Subnetze** filtern.

---
##### **2.1 Firewall-Typen**

| **Typ** | **Beschreibung** | **Beispiele** |
|---------|------------------|---------------|
| **Paketfilter-Firewall** | Filtert Datenpakete basierend auf **IP-Adressen, Ports und Protokollen**. | `iptables`, `nftables` |
| **Stateful Firewall** | Verfolgt den **Zustand von Verbindungen** (z. B. TCP-Handshake). | `iptables` (mit Stateful Rules), `nftables` |
| **Application-Layer Firewall** | Filtert basierend auf **Anwendungsdaten** (z. B. HTTP, FTP). | `ufw` (mit Erweiterungen), `pf` (OpenBSD) |
| **Proxy-Firewall** | Agiert als **Vermittler** zwischen Client und Server. | Squid, Nginx (als Reverse Proxy) |

---
##### **2.2 Firewall-Regeln**
Firewall-Regeln bestehen aus:
- **Aktion** (z. B. `ACCEPT`, `DROP`, `REJECT`).
- **Protokoll** (z. B. `TCP`, `UDP`, `ICMP`).
- **Quell-IP** (z. B. `192.168.1.0/24`).
- **Ziel-IP** (z. B. `10.0.0.1`).
- **Quell-Port** (z. B. `80`).
- **Ziel-Port** (z. B. `443`).

---

#### **3. `iptables` – Klassische Firewall unter Linux**
`iptables` ist das **traditionelle Firewall-Tool** unter Linux. Es arbeitet mit **Netfilter**, dem Firewall-Subsystem des Linux-Kernels.

---
##### **3.1 Grundlagen von `iptables`**
`iptables` verwendet **Tabellen** und **Ketten (Chains)**, um Regeln zu organisieren:
- **Tabellen:**
  - `filter` (Standardtabelle für Paketfilterung).
  - `nat` (für Network Address Translation).
  - `mangle` (für Paketmodifikation).
  - `raw` (für spezielle Verarbeitung).

- **Ketten (Chains):**
  - `INPUT` (Eingehender Verkehr).
  - `OUTPUT` (Ausgehender Verkehr).
  - `FORWARD` (Weitergeleiteter Verkehr).

---
##### **3.2 Wichtige `iptables`-Befehle**

| **Befehl** | **Beschreibung** |
|------------|------------------|
| `sudo iptables -L` | Listet **alle Regeln** in der `filter`-Tabelle auf. |
| `sudo iptables -L -n -v` | Listet Regeln mit **IP-Adressen (nicht aufgelöst)** und **Zählern** auf. |
| `sudo iptables -F` | **Löscht alle Regeln** in der `filter`-Tabelle. |
| `sudo iptables -X` | **Löscht alle benutzerdefinierten Ketten**. |
| `sudo iptables -Z` | Setzt **alle Zähler** auf Null zurück. |
| `sudo iptables -A [chain] [regel]` | **Fügt eine Regel** zu einer Kette hinzu. |
| `sudo iptables -D [chain] [regel]` | **Löscht eine Regel** aus einer Kette. |
| `sudo iptables -I [chain] [position] [regel]` | **Fügt eine Regel an einer bestimmten Position** ein. |
| `sudo iptables -P [chain] [aktion]` | Setzt die **Standardaktion** für eine Kette (z. B. `DROP`). |

---
##### **3.3 Beispiele für `iptables`-Regeln**
###### **3.3.1 Standardrichtlinien setzen**
```bash
# Alle eingehenden Pakete standardmäßig blockieren
sudo iptables -P INPUT DROP

# Alle ausgehenden Pakete standardmäßig erlauben
sudo iptables -P OUTPUT ACCEPT

# Weitergeleitete Pakete standardmäßig blockieren
sudo iptables -P FORWARD DROP
```

###### **3.3.2 Erlauben von SSH-Zugriff (Port 22)**
```bash
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```

###### **3.3.3 Erlauben von HTTP/HTTPS (Ports 80 und 443)**
```bash
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 443 -j ACCEPT
```

###### **3.3.4 Erlauben von ICMP (Ping)**
```bash
sudo iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT
```

###### **3.3.5 Erlauben von Verbindungen aus einem bestimmten Subnetz**
```bash
sudo iptables -A INPUT -s 192.168.1.0/24 -j ACCEPT
```

###### **3.3.6 Blockieren einer bestimmten IP-Adresse**
```bash
sudo iptables -A INPUT -s 192.168.1.100 -j DROP
```

###### **3.3.7 Port-Weiterleitung (Port Forwarding)**
```bash
# Aktiviert NAT für die Weiterleitung
sudo iptables -t nat -A PREROUTING -p tcp --dport 80 -j DNAT --to-destination 192.168.1.10:80
sudo iptables -t nat -A POSTROUTING -j MASQUERADE
```

###### **3.3.8 Speichern und Wiederherstellen von Regeln**
`iptables`-Regeln gehen nach einem **Neustart verloren**. Um sie dauerhaft zu speichern:
- **Debian/Ubuntu:**
  ```bash
  sudo apt install iptables-persistent
  sudo netfilter-persistent save
  ```
- **RHEL/CentOS:**
  ```bash
  sudo yum install iptables-services
  sudo service iptables save
  sudo systemctl enable iptables
  sudo systemctl start iptables
  ```

---
#### **4. `nftables` – Moderner Ersatz für `iptables`**
`nftables` ist der **Nachfolger von `iptables`** und bietet eine **einfachere Syntax** und **bessere Leistung**. Es wird ab **Linux Kernel 3.13** unterstützt.

---
##### **4.1 Grundlagen von `nftables`**
`nftables` verwendet **eine einzige Tabelle** für alle Firewall-Regeln und unterstützt:
- **IPv4 und IPv6** in einer Regel.
- **Vereinfachte Syntax** (keine separaten Tabellen für `filter`, `nat`, etc.).
- **Bessere Performance** (weniger Overhead).

---
##### **4.2 Wichtige `nft`-Befehle**

| **Befehl** | **Beschreibung** |
|------------|------------------|
| `sudo nft list ruleset` | Listet **alle Regeln** auf. |
| `sudo nft flush ruleset` | **Löscht alle Regeln**. |
| `sudo nft add table [name]` | Erstellt eine **neue Tabelle**. |
| `sudo nft add chain [table] [name] [type]` | Erstellt eine **neue Kette**. |
| `sudo nft add rule [table] [chain] [regel]` | **Fügt eine Regel** hinzu. |
| `sudo nft delete rule [table] [chain] [handle]` | **Löscht eine Regel**. |

---
##### **4.3 Beispiele für `nftables`-Regeln**
###### **4.3.1 Tabelle und Ketten erstellen**
```bash
# Tabelle erstellen
sudo nft add table inet filter

# Ketten erstellen
sudo nft add chain inet filter input { type filter hook input priority 0 \; }
sudo nft add chain inet filter output { type filter hook output priority 0 \; }
sudo nft add chain inet filter forward { type filter hook forward priority 0 \; }
```

###### **4.3.2 Standardrichtlinien setzen**
```bash
# Alle eingehenden Pakete standardmäßig blockieren
sudo nft add rule inet filter input counter drop

# Alle ausgehenden Pakete standardmäßig erlauben
sudo nft add rule inet filter output counter accept

# Weitergeleitete Pakete standardmäßig blockieren
sudo nft add rule inet filter forward counter drop
```

###### **4.3.3 Erlauben von SSH-Zugriff (Port 22)**
```bash
sudo nft add rule inet filter input tcp dport 22 counter accept
```

###### **4.3.4 Erlauben von HTTP/HTTPS (Ports 80 und 443)**
```bash
sudo nft add rule inet filter input tcp dport { 80, 443 } counter accept
```

###### **4.3.5 Erlauben von ICMP (Ping)**
```bash
sudo nft add rule inet filter input icmp type echo-request counter accept
```

###### **4.3.6 Blockieren einer bestimmten IP-Adresse**
```bash
sudo nft add rule inet filter input ip saddr 192.168.1.100 counter drop
```

###### **4.3.7 Speichern und Wiederherstellen von Regeln**
`nftables`-Regeln können in einer **Konfigurationsdatei** gespeichert werden (z. B. `/etc/nftables.conf`).

**Beispielkonfiguration (`/etc/nftables.conf`):**
```bash
#!/usr/sbin/nft -f

flush ruleset

table inet filter {
    chain input {
        type filter hook input priority 0;
        policy drop;

        # Erlaube SSH
        tcp dport 22 accept

        # Erlaube HTTP/HTTPS
        tcp dport { 80, 443 } accept

        # Erlaube ICMP (Ping)
        icmp type echo-request accept

        # Erlaube Verbindungen aus dem lokalen Netzwerk
        ip saddr 192.168.1.0/24 accept
    }

    chain output {
        type filter hook output priority 0;
        policy accept;
    }

    chain forward {
        type filter hook forward priority 0;
        policy drop;
    }
}
```
**Regeln laden:**
```bash
sudo nft -f /etc/nftables.conf
```
**Regeln dauerhaft speichern:**
- **Debian/Ubuntu:**
  ```bash
  sudo systemctl enable nftables
  sudo systemctl start nftables
  ```
- **RHEL/CentOS:**
  ```bash
  sudo systemctl enable nftables
  sudo systemctl start nftables
  ```

---

#### **5. `ufw` – Benutzerfreundliche Firewall**
`ufw` (**Uncomplicated Firewall**) ist eine **einfache Frontend-Oberfläche** für `iptables` und `nftables`. Es ist besonders für **Einsteiger** geeignet.

---
##### **5.1 Installation von `ufw`**
- **Debian/Ubuntu:**
  ```bash
  sudo apt install ufw
  ```
- **RHEL/CentOS:**
  ```bash
  sudo yum install ufw
  ```
- **Arch Linux:**
  ```bash
  sudo pacman -S ufw
  ```

---
##### **5.2 Wichtige `ufw`-Befehle**

| **Befehl** | **Beschreibung** |
|------------|------------------|
| `sudo ufw enable` | **Aktiviert** die Firewall. |
| `sudo ufw disable` | **Deaktiviert** die Firewall. |
| `sudo ufw status` | Zeigt den **Status der Firewall** an. |
| `sudo ufw status verbose` | Zeigt **detaillierte Informationen** an. |
| `sudo ufw default deny incoming` | Setzt die **Standardrichtlinie für eingehenden Verkehr** auf `deny`. |
| `sudo ufw default allow outgoing` | Setzt die **Standardrichtlinie für ausgehenden Verkehr** auf `allow`. |
| `sudo ufw allow [port]` | **Erlaubt** einen Port (z. B. `22`). |
| `sudo ufw deny [port]` | **Blockiert** einen Port. |
| `sudo ufw allow from [ip] to any port [port]` | Erlaubt **Verbindungen von einer bestimmten IP** zu einem Port. |
| `sudo ufw delete [regel]` | **Löscht eine Regel**. |

---
##### **5.3 Beispiele für `ufw`-Regeln**
###### **5.3.1 Firewall aktivieren und Status prüfen**
```bash
sudo ufw enable
sudo ufw status
```

###### **5.3.2 Standardrichtlinien setzen**
```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
```

###### **5.3.3 Erlauben von SSH (Port 22)**
```bash
sudo ufw allow 22
```
oder explizit für TCP:
```bash
sudo ufw allow 22/tcp
```

###### **5.3.4 Erlauben von HTTP/HTTPS (Ports 80 und 443)**
```bash
sudo ufw allow 80
sudo ufw allow 443
```
oder als Bereich:
```bash
sudo ufw allow 80:443/tcp
```

###### **5.3.5 Erlauben von Verbindungen aus einem bestimmten Subnetz**
```bash
sudo ufw allow from 192.168.1.0/24
```

###### **5.3.6 Blockieren einer bestimmten IP-Adresse**
```bash
sudo ufw deny from 192.168.1.100
```

###### **5.3.7 Erlauben von Ping (ICMP)**
```bash
sudo ufw allow in icmp
```

###### **5.3.8 Löschen einer Regel**
```bash
# Regelnummern anzeigen
sudo ufw status numbered

# Regel löschen (z. B. Regel 1)
sudo ufw delete 1
```

---
---
#### **6. `firewalld` – Dynamische Firewall unter RHEL/CentOS/Fedora**
`firewalld` ist die **Standard-Firewall** unter RHEL, CentOS und Fedora. Sie bietet **dynamische Zonen** und **Dienstprofile**, um Regeln flexibel zu verwalten.

---
##### **6.1 Grundlagen von `firewalld`**
- **Zonen:** Definieren **Vertrauensstufen** für Netzwerkverbindungen (z. B. `public`, `internal`, `trusted`).
- **Dienste:** Vordefinierte **Dienstprofile** (z. B. `http`, `ssh`, `ftp`).
- **Rich Rules:** **Erweiterte Regeln** für feinere Steuerung.

---
##### **6.2 Wichtige `firewalld`-Befehle**

| **Befehl** | **Beschreibung** |
|------------|------------------|
| `sudo systemctl start firewalld` | Startet `firewalld`. |
| `sudo systemctl enable firewalld` | Aktiviert `firewalld` beim Systemstart. |
| `sudo firewall-cmd --state` | Zeigt den **Status von `firewalld`** an. |
| `sudo firewall-cmd --reload` | **Lädt die Konfiguration neu**, ohne die Firewall zu stoppen. |
| `sudo firewall-cmd --list-all` | Zeigt **alle Regeln** für die Standardzone an. |
| `sudo firewall-cmd --get-zones` | Listet **alle Zonen** auf. |
| `sudo firewall-cmd --set-default-zone=[zone]` | Setzt die **Standardzone**. |
| `sudo firewall-cmd --zone=[zone] --add-service=[dienst]` | **Fügt einen Dienst** zu einer Zone hinzu. |
| `sudo firewall-cmd --zone=[zone] --add-port=[port]/[protokoll]` | **Fügt einen Port** zu einer Zone hinzu. |
| `sudo firewall-cmd --zone=[zone] --add-source=[ip/subnetz]` | **Fügt eine IP/Subnetz** zu einer Zone hinzu. |
| `sudo firewall-cmd --zone=[zone] --remove-service=[dienst]` | **Entfernt einen Dienst** aus einer Zone. |
| `sudo firewall-cmd --permanent --zone=[zone] --add-service=[dienst]` | **Fügt einen Dienst dauerhaft** hinzu. |

---
##### **6.3 Beispiele für `firewalld`-Regeln**
###### **6.3.1 Firewall starten und aktivieren**
```bash
sudo systemctl start firewalld
sudo systemctl enable firewalld
```

###### **6.3.2 Standardzone prüfen und ändern**
```bash
# Aktuelle Standardzone anzeigen
sudo firewall-cmd --get-default-zone

# Standardzone auf "public" setzen
sudo firewall-cmd --set-default-zone=public
```

###### **6.3.3 Erlauben von SSH (Port 22)**
```bash
sudo firewall-cmd --add-service=ssh --permanent
sudo firewall-cmd --reload
```

###### **6.3.4 Erlauben von HTTP/HTTPS (Ports 80 und 443)**
```bash
sudo firewall-cmd --add-service=http --permanent
sudo firewall-cmd --add-service=https --permanent
sudo firewall-cmd --reload
```

###### **6.3.5 Erlauben eines bestimmten Ports (z. B. 8080)**
```bash
sudo firewall-cmd --add-port=8080/tcp --permanent
sudo firewall-cmd --reload
```

###### **6.3.6 Erlauben von Verbindungen aus einem bestimmten Subnetz**
```bash
sudo firewall-cmd --zone=public --add-source=192.168.1.0/24 --permanent
sudo firewall-cmd --reload
```

###### **6.3.7 Blockieren einer bestimmten IP-Adresse**
```bash
sudo firewall-cmd --zone=public --add-rich-rule='rule family="ipv4" source address="192.168.1.100" reject' --permanent
sudo firewall-cmd --reload
```

###### **6.3.8 Erlauben von Ping (ICMP)**
```bash
sudo firewall-cmd --add-icmp-block=echo-request --permanent
sudo firewall-cmd --reload
```

###### **6.3.9 Alle Regeln anzeigen**
```bash
sudo firewall-cmd --list-all
```

---
---
#### **7. Netzwerksicherheit: Weitere Tools und Techniken**
---
##### **7.1 `fail2ban` – Schutz vor Brute-Force-Angriffen**
`fail2ban` ist ein Tool, das **automatisch IP-Adressen blockiert**, die **wiederholte fehlgeschlagene Login-Versuche** unternehmen (z. B. SSH, FTP, Web-Formulare).

**Installation:**
- **Debian/Ubuntu:**
  ```bash
  sudo apt install fail2ban
  ```
- **RHEL/CentOS:**
  ```bash
  sudo yum install fail2ban
  ```

**Konfiguration:**
Die Hauptkonfigurationsdatei ist `/etc/fail2ban/jail.local`. Hier können Sie **Jails** (Gefängnisse) für verschiedene Dienste definieren.

**Beispielkonfiguration (`/etc/fail2ban/jail.local`):**
```ini
[DEFAULT]
bantime = 3600      # Blockierungsdauer in Sekunden (1 Stunde)
findtime = 600       # Zeitfenster für fehlgeschlagene Versuche (10 Minuten)
maxretry = 5        # Maximale Anzahl fehlgeschlagener Versuche

[sshd]
enabled = true      # SSH-Jail aktivieren
port = ssh
filter = sshd
logpath = /var/log/auth.log
```

**Dienst starten und aktivieren:**
```bash
sudo systemctl start fail2ban
sudo systemctl enable fail2ban
```

**Status prüfen:**
```bash
sudo fail2ban-client status
sudo fail2ban-client status sshd
```

---
##### **7.2 `ssh` – Sichere Remote-Verbindungen**
SSH (**Secure Shell**) ist ein **Protokoll für sichere Remote-Verbindungen**. Es verschlüsselt den gesamten Datenverkehr zwischen Client und Server.

**Installation:**
- **Debian/Ubuntu:**
  ```bash
  sudo apt install openssh-server
  ```
- **RHEL/CentOS:**
  ```bash
  sudo yum install openssh-server
  ```

**Konfiguration:**
Die Hauptkonfigurationsdatei ist `/etc/ssh/sshd_config`.

**Wichtige Einstellungen:**

| **Einstellung** | **Beschreibung** | **Empfohlener Wert** |
|-----------------|------------------|----------------------|
| `Port` | Port für SSH-Verbindungen. | `22` (Standard) oder ein **benutzerdefinierter Port** (z. B. `2222`). |
| `PermitRootLogin` | Erlaubt Root-Login. | `no` (aus Sicherheitsgründen). |
| `PasswordAuthentication` | Erlaubt Passwort-Authentifizierung. | `no` (verwenden Sie stattdessen **SSH-Schlüssel**). |
| `AllowUsers` | Erlaubt nur bestimmte Benutzer. | `AllowUsers alice bob` |
| `MaxAuthTries` | Maximale Anzahl fehlgeschlagener Login-Versuche. | `3` |
| `LoginGraceTime` | Zeitfenster für Login-Versuche. | `60` (Sekunden). |

**Beispielkonfiguration (`/etc/ssh/sshd_config`):**
```ini
Port 2222
PermitRootLogin no
PasswordAuthentication no
AllowUsers alice bob
MaxAuthTries 3
LoginGraceTime 60
```

**Dienst neu starten:**
```bash
sudo systemctl restart sshd
```

**SSH-Schlüssel generieren und verwenden:**
1. **Schlüsselpaar generieren (auf dem Client):**
   ```bash
   ssh-keygen -t ed25519 -C "your_email@example.com"
   ```
   - **`-t ed25519`**: Verwenden Sie den **Ed25519-Algorithmus** (sicherer als RSA).
   - **`-C`**: Kommentar (z. B. Ihre E-Mail-Adresse).

2. **Öffentlichen Schlüssel auf den Server kopieren:**
   ```bash
   ssh-copy-id -i ~/.ssh/id_ed25519.pub alice@192.168.1.100 -p 2222
   ```
   - **`-i`**: Gibt den **öffentlichen Schlüssel** an.
   - **`-p`**: Gibt den **SSH-Port** an (falls nicht Standard).

3. **Verbindung herstellen:**
   ```bash
   ssh -p 2222 alice@192.168.1.100
   ```

---
##### **7.3 `tcpdump` – Netzwerkverkehr analysieren**
`tcpdump` ist ein **Kommandozeilen-Tool**, um **Netzwerkverkehr zu erfassen und zu analysieren**.

**Installation:**
- **Debian/Ubuntu:**
  ```bash
  sudo apt install tcpdump
  ```
- **RHEL/CentOS:**
  ```bash
  sudo yum install tcpdump
  ```

**Wichtige Optionen:**

| **Option** | **Beschreibung** |
|------------|------------------|
| `-i [interface]` | Gibt das **Netzwerkinterface** an (z. B. `eth0`, `ens33`). |
| `-n` | Zeigt **IP-Adressen** statt Hostnamen an. |
| `-c [anzahl]` | Begrenzt die Anzahl der **erfassten Pakete**. |
| `-w [datei]` | Speichert die **erfassten Pakete** in einer Datei. |
| `-r [datei]` | Liest **erfasste Pakete** aus einer Datei. |
| `port [port]` | Filtert nach **Port** (z. B. `port 80`). |
| `host [ip]` | Filtert nach **IP-Adresse** (z. B. `host 192.168.1.100`). |
| `icmp` | Filtert nach **ICMP-Paketen** (Ping). |
| `tcp` | Filtert nach **TCP-Paketen**. |
| `udp` | Filtert nach **UDP-Paketen**. |

**Beispiele:**
```bash
# Erfasse alle Pakete auf dem Interface `eth0`
sudo tcpdump -i eth0

# Erfasse nur TCP-Pakete auf Port 80
sudo tcpdump -i eth0 tcp port 80

# Erfasse nur Pakete von/bis 192.168.1.100
sudo tcpdump -i eth0 host 192.168.1.100

# Erfasse 100 Pakete und speichere sie in einer Datei
sudo tcpdump -i eth0 -c 100 -w capture.pcap

# Lese eine erfasste Datei
sudo tcpdump -r capture.pcap
```

---
##### **7.4 `netstat` und `ss` – Netzwerkverbindungen überwachen**
- **`netstat`** (veraltet, aber noch weit verbreitet):
  ```bash
  netstat -tuln  # Zeigt alle TCP/UDP-Ports an
  netstat -r     # Zeigt die Routing-Tabelle an
  ```

- **`ss`** (modernere Alternative zu `netstat`):
  ```bash
  ss -tuln       # Zeigt alle TCP/UDP-Ports an
  ss -l          # Zeigt alle listening Ports an
  ss -s          # Zeigt eine Zusammenfassung der Socket-Statistiken an
  ```

---
##### **7.5 `nmap` – Netzwerk-Scanning**
`nmap` ist ein **leistungsstarkes Tool** zum **Scannen von Netzwerken**, um offene Ports, Dienste und Sicherheitslücken zu identifizieren.

**Installation:**
- **Debian/Ubuntu:**
  ```bash
  sudo apt install nmap
  ```
- **RHEL/CentOS:**
  ```bash
  sudo yum install nmap
  ```

**Wichtige Optionen:**

| **Option** | **Beschreibung** |
|------------|------------------|
| `-sS` | **TCP SYN Scan** (schnell und unauffällig). |
| `-sT` | **TCP Connect Scan** (langsamer, aber zuverlässiger). |
| `-sU` | **UDP Scan**. |
| `-p [port(s)]` | Gibt **Ports** an (z. B. `-p 80,443` oder `-p 1-1000`). |
| `-O` | **Betriebssystem-Erkennung**. |
| `-sV` | **Dienstversionen erkennen**. |
| `-A` | **Aggressives Scanning** (kombiniert `-O` und `-sV`). |
| `-T4` | **Schnelleres Scanning** (1-5, wobei 5 am schnellsten ist). |

**Beispiele:**
```bash
# Scan eines einzelnen Hosts
nmap 192.168.1.100

# Scan eines Subnetzes
nmap 192.168.1.0/24

# Scan mit Dienstversionen und Betriebssystem-Erkennung
nmap -sV -O 192.168.1.100

# Scan aller Ports (1-65535)
nmap -p- 192.168.1.100

# Aggressiver Scan
nmap -A 192.168.1.100
```

---
---
#### **8. Übungsaufgaben**
---
##### **Frage 1**
Wie können Sie mit `iptables` **alle eingehenden Pakete standardmäßig blockieren**, aber **SSH (Port 22) erlauben**?

??? success "Antwort"
    ```bash
    sudo iptables -P INPUT DROP
    sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
    ```

---
##### **Frage 2**
Wie können Sie mit `ufw` **HTTP (Port 80) und HTTPS (Port 443) erlauben**?

??? success "Antwort"
    ```bash
    sudo ufw allow 80/tcp
    sudo ufw allow 443/tcp
    ```
    oder:
    ```bash
    sudo ufw allow http
    sudo ufw allow https
    ```

---
##### **Frage 3**
Wie können Sie mit `firewalld` **SSH (Port 22) dauerhaft erlauben**?

??? success "Antwort"
    ```bash
    sudo firewall-cmd --add-service=ssh --permanent
    sudo firewall-cmd --reload
    ```

---
##### **Frage 4**
Wie können Sie eine **IP-Adresse (z. B. 192.168.1.100) mit `iptables` blockieren**?

??? success "Antwort"
    ```bash
    sudo iptables -A INPUT -s 192.168.1.100 -j DROP
    ```

---
##### **Frage 5**
Wie können Sie mit `nftables` eine **Regel erstellen, die ICMP (Ping) erlaubt**?

??? success "Antwort"
    ```bash
    sudo nft add rule inet filter input icmp type echo-request counter accept
    ```

---
##### **Frage 6**
Wie können Sie mit `fail2ban` **SSH-Login-Versuche nach 3 fehlgeschlagenen Versuchen für 1 Stunde blockieren**?

??? success "Antwort"
    Bearbeiten Sie `/etc/fail2ban/jail.local`:
    ```ini
    [sshd]
    enabled = true
    maxretry = 3
    bantime = 3600
    ```
    Dann:
    ```bash
    sudo systemctl restart fail2ban
    ```

---
##### **Frage 7**
Wie können Sie den **SSH-Port auf 2222 ändern** und **Root-Login deaktivieren**?

??? success "Antwort"
    Bearbeiten Sie `/etc/ssh/sshd_config`:
    ```ini
    Port 2222
    PermitRootLogin no
    ```
    Dann:
    ```bash
    sudo systemctl restart sshd
    ```

---
##### **Frage 8**
Wie können Sie mit `tcpdump` **alle TCP-Pakete auf Port 80 erfassen**?

??? success "Antwort"
    ```bash
    sudo tcpdump -i eth0 tcp port 80
    ```

---
##### **Frage 9**
Wie können Sie mit `nmap` **alle offenen Ports auf einem Host (192.168.1.100) scannen**?

??? success "Antwort"
    ```bash
    nmap -p- 192.168.1.100
    ```

---
##### **Frage 10**
Wie können Sie mit `firewalld` **eine benutzerdefinierte Zone namens `trusted` erstellen** und **alle eingehenden Verbindungen erlauben**?

??? success "Antwort"
    ```bash
    sudo firewall-cmd --new-zone=trusted --permanent
    sudo firewall-cmd --zone=trusted --set-target=ACCEPT --permanent
    sudo firewall-cmd --reload
    ```

---
---
#### **9. Praktische Beispiele**
---
##### **Beispiel 1: Firewall-Regeln für einen Webserver**
**Szenario:** Ein Webserver soll **HTTP (80)**, **HTTPS (443)** und **SSH (22)** erlauben, aber **alle anderen eingehenden Verbindungen blockieren**.

**Lösung mit `ufw`:**
```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow 22/tcp
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw enable
```

**Lösung mit `firewalld`:**
```bash
sudo firewall-cmd --zone=public --add-service=ssh --permanent
sudo firewall-cmd --zone=public --add-service=http --permanent
sudo firewall-cmd --zone=public --add-service=https --permanent
sudo firewall-cmd --zone=public --set-target=DROP --permanent
sudo firewall-cmd --reload
```

---
##### **Beispiel 2: Schutz vor Brute-Force-Angriffen mit `fail2ban`**
**Szenario:** Ein Server wird **häufig von unbekannten IPs angegriffen**, die versuchen, sich per SSH einzuloggen.

**Lösung:**
1. Installieren Sie `fail2ban`:
   ```bash
   sudo apt install fail2ban
   ```
2. Konfigurieren Sie `/etc/fail2ban/jail.local`:
   ```ini
   [sshd]
   enabled = true
   port = ssh
   filter = sshd
   logpath = /var/log/auth.log
   maxretry = 3
   bantime = 3600
   ```
3. Starten Sie `fail2ban`:
   ```bash
   sudo systemctl start fail2ban
   sudo systemctl enable fail2ban
   ```

---
##### **Beispiel 3: Netzwerkverkehr analysieren mit `tcpdump`**
**Szenario:** Sie möchten **verdächtigen Netzwerkverkehr** auf Port 443 (HTTPS) überwachen.

**Lösung:**
```bash
sudo tcpdump -i eth0 -n port 443 -w https_traffic.pcap
```
- **`-i eth0`**: Erfasse Verkehr auf dem Interface `eth0`.
- **`-n`**: Zeige IP-Adressen statt Hostnamen an.
- **`port 443`**: Filtere nach Port 443.
- **`-w https_traffic.pcap`**: Speichere die erfassten Pakete in einer Datei.

---
##### **Beispiel 4: Netzwerk-Scan mit `nmap`**
**Szenario:** Sie möchten **alle offenen Ports und Dienste** auf einem Server (192.168.1.100) identifizieren.

**Lösung:**
```bash
nmap -sS -sV -O -T4 192.168.1.100
```
- **`-sS`**: TCP SYN Scan (schnell und unauffällig).
- **`-sV`**: Dienstversionen erkennen.
- **`-O`**: Betriebssystem-Erkennung.
- **`-T4`**: Schnelleres Scanning.

---
##### **Beispiel 5: Port-Weiterleitung mit `iptables`**
**Szenario:** Sie möchten **Port 8080 auf dem Host auf Port 80 eines internen Servers (192.168.1.10) weiterleiten**.

**Lösung:**
```bash
# Aktiviert NAT für die Weiterleitung
sudo iptables -t nat -A PREROUTING -p tcp --dport 8080 -j DNAT --to-destination 192.168.1.10:80
sudo iptables -t nat -A POSTROUTING -j MASQUERADE

# Erlaubt die Weiterleitung in der FORWARD-Kette
sudo iptables -A FORWARD -p tcp -d 192.168.1.10 --dport 80 -j ACCEPT
```

---
---
#### **10. Zusammenfassung der wichtigsten Befehle**

| **Aktion** | **`iptables`** | **`nftables`** | **`ufw`** | **`firewalld`** |
|------------|----------------|----------------|-----------|----------------|
| **Regeln anzeigen** | `sudo iptables -L -n -v` | `sudo nft list ruleset` | `sudo ufw status` | `sudo firewall-cmd --list-all` |
| **Standardrichtlinie setzen** | `sudo iptables -P INPUT DROP` | `sudo nft add rule inet filter input counter drop` | `sudo ufw default deny incoming` | `sudo firewall-cmd --zone=public --set-target=DROP` |
| **Port erlauben (z. B. 22)** | `sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT` | `sudo nft add rule inet filter input tcp dport 22 counter accept` | `sudo ufw allow 22` | `sudo firewall-cmd --add-port=22/tcp --permanent` |
| **IP blockieren (z. B. 192.168.1.100)** | `sudo iptables -A INPUT -s 192.168.1.100 -j DROP` | `sudo nft add rule inet filter input ip saddr 192.168.1.100 counter drop` | `sudo ufw deny from 192.168.1.100` | `sudo firewall-cmd --zone=public --add-rich-rule='rule family="ipv4" source address="192.168.1.100" reject' --permanent` |
| **Regeln speichern** | `sudo iptables-save > /etc/iptables.rules` | `sudo nft -f /etc/nftables.conf` | `sudo ufw enable` | `sudo firewall-cmd --reload` |
| **Dienst erlauben (z. B. HTTP)** | `sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT` | `sudo nft add rule inet filter input tcp dport 80 counter accept` | `sudo ufw allow http` | `sudo firewall-cmd --add-service=http --permanent` |

---
---
#### **11. Häufige Fehler und Lösungen**

| **Problem** | **Ursache** | **Lösung** |
|-------------|-------------|------------|
| **`iptables: No chain/target/match by that name`** | Falsche Syntax oder nicht existierende Kette. | Überprüfen Sie die Syntax und Kettennamen. |
| **`ufw: command not found`** | `ufw` ist nicht installiert. | Installieren Sie `ufw` mit `sudo apt install ufw`. |
| **`firewalld: not running`** | `firewalld` ist nicht aktiviert. | Starten Sie `firewalld` mit `sudo systemctl start firewalld`. |
| **`fail2ban: not blocking IPs`** | Falsche Konfiguration oder Log-Pfad. | Überprüfen Sie `/etc/fail2ban/jail.local` und den Log-Pfad. |
| **`nmap: Host seems down`** | Host ist nicht erreichbar oder Firewall blockiert Scans. | Überprüfen Sie die Netzwerkverbindung und Firewall-Regeln. |
| **`tcpdump: permission denied`** | Keine Berechtigung für das Interface. | Verwenden Sie `sudo`. |
| **SSH-Verbindung wird abgelehnt** | Falscher Port oder Firewall blockiert SSH. | Überprüfen Sie den SSH-Port und Firewall-Regeln. |

---
---
#### **12. Vertiefung: Netzwerksicherheit mit `SELinux` und `AppArmor`**
##### **12.1 `SELinux` – Security-Enhanced Linux**
`SELinux` ist ein **Mandatory Access Control (MAC)**-System, das **Zugangsrichtlinien** auf Dateien, Prozesse und Ports erzwingt. Es ist standardmäßig in **RHEL/CentOS/Fedora** aktiviert.

**Wichtige Befehle:**

| **Befehl** | **Beschreibung** |
|------------|------------------|
| `getenforce` | Zeigt den **Aktuellen Modus** von SELinux an (`Enforcing`, `Permissive`, `Disabled`). |
| `setenforce 0` | Setzt SELinux in den **Permissive-Modus** (nur für die aktuelle Sitzung). |
| `setenforce 1` | Setzt SELinux in den **Enforcing-Modus** (nur für die aktuelle Sitzung). |
| `sestatus` | Zeigt den **Status von SELinux** an. |
| `chcon -t [typ] [datei]` | Ändert den **SELinux-Kontext** einer Datei. |
| `restorecon -v [datei]` | Setzt den **Standard-Kontext** für eine Datei zurück. |
| `ausearch -m avc -ts recent` | Durchsucht **Audit-Logs** nach SELinux-Zugriffsverletzungen. |

**Beispiel: SELinux-Modus ändern (dauerhaft)**
Bearbeiten Sie `/etc/selinux/config`:
```ini
SELINUX=enforcing  # oder "permissive" oder "disabled"
```
Dann:
```bash
sudo reboot
```

---
##### **12.2 `AppArmor` – Application Armor**
`AppArmor` ist ein **Mandatory Access Control (MAC)**-System für **Debian/Ubuntu**. Es beschränkt die **Aktionen von Anwendungen**.

**Wichtige Befehle:**

| **Befehl** | **Beschreibung** |
|------------|------------------|
| `sudo aa-status` | Zeigt den **Status von AppArmor** an. |
| `sudo aa-enforce [profil]` | Erzwingt ein **Profil**. |
| `sudo aa-complain [profil]` | Setzt ein Profil in den **Complain-Modus** (Logs, aber blockiert nicht). |
| `sudo aa-disable [profil]` | **Deaktiviert ein Profil**. |
| `sudo aa-genprof [pfad/zur/anwendung]` | Erstellt ein **neues Profil** für eine Anwendung. |

**Beispiel: AppArmor-Profil für `nginx` erstellen**
```bash
sudo aa-genprof /usr/sbin/nginx
```
Folgen Sie den Anweisungen, um das Profil zu erstellen.

