
### **Modul IV: Systemadministration und Sicherheit**
### **Thema: Softwareinstallation und -verwaltung**

---

#### **1. Einführung in die Softwareverwaltung unter Linux**
Die **Softwareverwaltung** ist ein zentraler Bestandteil der Systemadministration. Linux bietet verschiedene **Paketverwaltungssysteme**, um Software zu installieren, zu aktualisieren und zu entfernen. Die wichtigsten Systeme sind:
- **Debian/Ubuntu:** `apt` und `dpkg`
- **RHEL/CentOS/Fedora:** `yum` und `dnf` (neuer) sowie `rpm`
- **Arch Linux:** `pacman`
- **openSUSE:** `zypper`

Jedes System verwendet **Paketquellen (Repositories)**, aus denen Software heruntergeladen und installiert wird.

---

---

#### **2. Paketverwaltung unter Debian/Ubuntu (`apt` und `dpkg`)**
##### **2.1 `apt` – Advanced Package Tool**
`apt` ist das **Hauptwerkzeug** für die Paketverwaltung unter Debian und Ubuntu. Es vereinfacht die Installation, Aktualisierung und Entfernung von Paketen.

**Wichtige Befehle:**

| Befehl | Beschreibung |
|--------|--------------|
| `sudo apt update` | Aktualisiert die **Paketlisten** aus den Repositories. |
| `sudo apt upgrade` | Aktualisiert **alle installierten Pakete**. |
| `sudo apt install [paketname]` | Installiert ein **neues Paket**. |
| `sudo apt remove [paketname]` | Entfernt ein **Paket**, behält aber Konfigurationsdateien. |
| `sudo apt purge [paketname]` | Entfernt ein **Paket inklusive Konfigurationsdateien**. |
| `sudo apt autoremove` | Entfernt **nicht mehr benötigte Abhängigkeiten**. |
| `sudo apt search [suchbegriff]` | Durchsucht die **Paketdatenbank** nach einem Paket. |
| `sudo apt show [paketname]` | Zeigt **Detaillierte Informationen** zu einem Paket an. |
| `sudo apt list --installed` | Listet **alle installierten Pakete** auf. |
| `sudo apt list --upgradable` | Listet **verfügbare Updates** auf. |

**Beispiele:**
```bash
# Paketlisten aktualisieren
sudo apt update

# Ein Paket installieren (z. B. `htop`)
sudo apt install htop

# Ein Paket entfernen (z. B. `htop`)
sudo apt remove htop

# Ein Paket inklusive Konfiguration entfernen
sudo apt purge htop

# Alle Pakete aktualisieren
sudo apt upgrade

# Nicht mehr benötigte Pakete entfernen
sudo apt autoremove

# Nach einem Paket suchen (z. B. `nginx`)
sudo apt search nginx

# Informationen zu einem Paket anzeigen (z. B. `nginx`)
sudo apt show nginx
```

---
##### **2.2 `dpkg` – Debian Package Manager**
`dpkg` ist das **niedrigere Werkzeug** für die Paketverwaltung unter Debian/Ubuntu. Es arbeitet direkt mit `.deb`-Paketdateien.

**Wichtige Befehle:**

| Befehl | Beschreibung |
|--------|--------------|
| `sudo dpkg -i [paketname.deb]` | Installiert ein **lokal gespeichertes `.deb`-Paket**. |
| `sudo dpkg -r [paketname]` | Entfernt ein **Paket**. |
| `sudo dpkg -l` | Listet **alle installierten Pakete** auf. |
| `sudo dpkg -s [paketname]` | Zeigt den **Status eines Pakets** an. |
| `sudo dpkg -L [paketname]` | Listet **alle Dateien** auf, die zu einem Paket gehören. |
| `sudo dpkg --configure -a` | Behebt **unterbrochene Paketkonfigurationen**. |

**Beispiele:**
```bash
# Ein .deb-Paket installieren
sudo dpkg -i /pfad/zur/datei.deb

# Ein Paket entfernen
sudo dpkg -r htop

# Alle installierten Pakete auflisten
sudo dpkg -l

# Dateien eines Pakets auflisten (z. B. `nginx`)
sudo dpkg -L nginx
```

---
##### **2.3 Abhängigkeiten manuell auflösen**
Falls `dpkg` eine Fehlermeldung wegen **unbefriedigter Abhängigkeiten** ausgibt, können Sie diese mit `apt` beheben:
```bash
sudo apt --fix-broken install
```

---
---

#### **3. Paketverwaltung unter RHEL/CentOS/Fedora (`yum`, `dnf` und `rpm`)**
##### **3.1 `yum` – Yellowdog Updater Modified**
`yum` ist das **Hauptwerkzeug** für die Paketverwaltung unter RHEL, CentOS und älteren Fedora-Versionen.

**Wichtige Befehle:**

| Befehl | Beschreibung |
|--------|--------------|
| `sudo yum update` | Aktualisiert **alle Pakete**. |
| `sudo yum install [paketname]` | Installiert ein **neues Paket**. |
| `sudo yum remove [paketname]` | Entfernt ein **Paket**. |
| `sudo yum search [suchbegriff]` | Durchsucht die **Paketdatenbank**. |
| `sudo yum info [paketname]` | Zeigt **Informationen zu einem Paket** an. |
| `sudo yum list installed` | Listet **alle installierten Pakete** auf. |
| `sudo yum clean all` | **Bereinigt den Cache** von `yum`. |

**Beispiele:**
```bash
# Alle Pakete aktualisieren
sudo yum update

# Ein Paket installieren (z. B. `htop`)
sudo yum install htop

# Ein Paket entfernen
sudo yum remove htop

# Nach einem Paket suchen
sudo yum search nginx

# Informationen zu einem Paket anzeigen
sudo yum info nginx
```

---
##### **3.2 `dnf` – Dandified YUM**
`dnf` ist der **Nachfolger von `yum`** und wird in neueren Fedora-Versionen und RHEL 8+ verwendet. Es ist schneller und bietet bessere Abhängigkeitsauflösung.

**Wichtige Befehle:**

| Befehl | Beschreibung |
|--------|--------------|
| `sudo dnf update` | Aktualisiert **alle Pakete**. |
| `sudo dnf install [paketname]` | Installiert ein **neues Paket**. |
| `sudo dnf remove [paketname]` | Entfernt ein **Paket**. |
| `sudo dnf search [suchbegriff]` | Durchsucht die **Paketdatenbank**. |
| `sudo dnf info [paketname]` | Zeigt **Informationen zu einem Paket** an. |
| `sudo dnf list installed` | Listet **alle installierten Pakete** auf. |
| `sudo dnf autoremove` | Entfernt **nicht mehr benötigte Abhängigkeiten**. |
| `sudo dnf clean all` | **Bereinigt den Cache** von `dnf`. |

**Beispiele:**
```bash
# Alle Pakete aktualisieren
sudo dnf update

# Ein Paket installieren (z. B. `htop`)
sudo dnf install htop

# Ein Paket entfernen
sudo dnf remove htop

# Nicht mehr benötigte Pakete entfernen
sudo dnf autoremove
```

---
##### **3.3 `rpm` – Red Hat Package Manager**
`rpm` ist das **niedrigere Werkzeug** für die Paketverwaltung unter RHEL/CentOS/Fedora. Es arbeitet direkt mit `.rpm`-Paketdateien.

**Wichtige Befehle:**

| Befehl | Beschreibung |
|--------|--------------|
| `sudo rpm -i [paketname.rpm]` | Installiert ein **lokal gespeichertes `.rpm`-Paket**. |
| `sudo rpm -e [paketname]` | Entfernt ein **Paket**. |
| `rpm -qa` | Listet **alle installierten Pakete** auf. |
| `rpm -ql [paketname]` | Listet **alle Dateien** eines Pakets auf. |
| `rpm -qi [paketname]` | Zeigt **Informationen zu einem Paket** an. |

**Beispiele:**
```bash
# Ein .rpm-Paket installieren
sudo rpm -i /pfad/zur/datei.rpm

# Ein Paket entfernen
sudo rpm -e htop

# Alle installierten Pakete auflisten
rpm -qa

# Dateien eines Pakets auflisten (z. B. `nginx`)
rpm -ql nginx
```

---
---
#### **4. Paketverwaltung unter Arch Linux (`pacman`)**
##### **4.1 `pacman` – Package Manager**
`pacman` ist das **Hauptwerkzeug** für die Paketverwaltung unter Arch Linux.

**Wichtige Befehle:**

| Befehl | Beschreibung |
|--------|--------------|
| `sudo pacman -Syu` | Aktualisiert **alle Pakete und die Paketdatenbank**. |
| `sudo pacman -S [paketname]` | Installiert ein **neues Paket**. |
| `sudo pacman -R [paketname]` | Entfernt ein **Paket**. |
| `sudo pacman -Rs [paketname]` | Entfernt ein **Paket inklusive Abhängigkeiten**. |
| `sudo pacman -Q` | Listet **alle installierten Pakete** auf. |
| `sudo pacman -Qs [suchbegriff]` | Durchsucht **installierte Pakete** nach einem Suchbegriff. |
| `sudo pacman -Si [paketname]` | Zeigt **Informationen zu einem Paket** an. |
| `sudo pacman -F [dateiname]` | Sucht nach einer **Datei in allen Paketen**. |

**Beispiele:**
```bash
# Paketdatenbank aktualisieren und alle Pakete updaten
sudo pacman -Syu

# Ein Paket installieren (z. B. `htop`)
sudo pacman -S htop

# Ein Paket entfernen
sudo pacman -R htop

# Ein Paket inklusive Abhängigkeiten entfernen
sudo pacman -Rs htop

# Alle installierten Pakete auflisten
sudo pacman -Q
```

---
---
#### **5. Paketverwaltung unter openSUSE (`zypper`)**
##### **5.1 `zypper` – ZYpp Package Manager**
`zypper` ist das **Hauptwerkzeug** für die Paketverwaltung unter openSUSE.

**Wichtige Befehle:**

| Befehl | Beschreibung |
|--------|--------------|
| `sudo zypper refresh` | Aktualisiert die **Paketdatenbank**. |
| `sudo zypper update` | Aktualisiert **alle installierten Pakete**. |
| `sudo zypper install [paketname]` | Installiert ein **neues Paket**. |
| `sudo zypper remove [paketname]` | Entfernt ein **Paket**. |
| `sudo zypper search [suchbegriff]` | Durchsucht die **Paketdatenbank**. |
| `sudo zypper info [paketname]` | Zeigt **Informationen zu einem Paket** an. |
| `sudo zypper packages` | Listet **alle installierten Pakete** auf. |

**Beispiele:**
```bash
# Paketdatenbank aktualisieren
sudo zypper refresh

# Alle Pakete aktualisieren
sudo zypper update

# Ein Paket installieren (z. B. `htop`)
sudo zypper install htop

# Ein Paket entfernen
sudo zypper remove htop
```

---
---
#### **6. Paketquellen (Repositories) verwalten**
##### **6.1 Repositories unter Debian/Ubuntu**
- **Standard-Repositories** sind in `/etc/apt/sources.list` und `/etc/apt/sources.list.d/` definiert.
- **Neue Repository hinzufügen:**
  ```bash
  sudo add-apt-repository ppa:[ppa-name]
  sudo apt update
  ```
- **Repository manuell hinzufügen:**
  Bearbeiten Sie `/etc/apt/sources.list` oder erstellen Sie eine neue Datei in `/etc/apt/sources.list.d/`.

**Beispiel:**
```bash
# Ein PPA (Personal Package Archive) hinzufügen
sudo add-apt-repository ppa:ondrej/php
sudo apt update
```

---
##### **6.2 Repositories unter RHEL/CentOS/Fedora**
- **Standard-Repositories** sind in `/etc/yum.repos.d/` definiert.
- **Neues Repository hinzufügen:**
  Erstellen Sie eine `.repo`-Datei in `/etc/yum.repos.d/`.

**Beispiel:**
```bash
# Beispiel für ein EPEL-Repository unter CentOS
sudo yum install epel-release
```
oder manuell:
```bash
sudo vi /etc/yum.repos.d/epel.repo
```
Inhalt:
```ini
[epel]
name=Extra Packages for Enterprise Linux
baseurl=https://download.fedoraproject.org/pub/epel/$releasever/$basearch/
enabled=1
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL
```

---
##### **6.3 Repositories unter Arch Linux**
- **Standard-Repositories** sind in `/etc/pacman.conf` definiert.
- **Neues Repository hinzufügen:**
  Bearbeiten Sie `/etc/pacman.conf` und fügen Sie das Repository hinzu.

**Beispiel:**
```bash
# AUR (Arch User Repository) aktivieren
sudo vi /etc/pacman.conf
```
Fügen Sie folgende Zeilen hinzu:
```ini
[archlinuxfr]
SigLevel = Never
Server = http://repo.archlinux.fr/$arch
```
Dann aktualisieren:
```bash
sudo pacman -Syu
```

---
---
#### **7. Software aus dem Quellcode installieren**
Manchmal müssen Sie Software **direkt aus dem Quellcode** installieren. Dies erfordert in der Regel folgende Schritte:

1. **Abhängigkeiten installieren** (z. B. `build-essential`, `gcc`, `make`).
2. **Quellcode herunterladen** (z. B. von [GitHub](https://github.com/) oder der offiziellen Website).
3. **Quellcode entpacken**.
4. **Konfigurieren, Kompilieren und Installieren**.

**Beispiel: Installation von `nginx` aus dem Quellcode**
```bash
# 1. Abhängigkeiten installieren
sudo apt install build-essential libpcre3 libpcre3-dev zlib1g zlib1g-dev libssl-dev

# 2. Quellcode herunterladen
wget https://nginx.org/download/nginx-1.25.3.tar.gz
tar -xzvf nginx-1.25.3.tar.gz
cd nginx-1.25.3

# 3. Konfigurieren
./configure

# 4. Kompilieren
make

# 5. Installieren
sudo make install
```

---
---
#### **8. Paketabhängigkeiten verwalten**
##### **8.1 Abhängigkeiten anzeigen**
- **Debian/Ubuntu:**
  ```bash
  apt depends [paketname]
  ```
  oder
  ```bash
  apt-cache depends [paketname]
  ```

- **RHEL/CentOS/Fedora:**
  ```bash
  yum deplist [paketname]
  ```
  oder
  ```bash
  dnf deplist [paketname]
  ```

- **Arch Linux:**
  ```bash
  pacman -Si [paketname] | grep Depends
  ```

---
##### **8.2 Abhängigkeiten manuell installieren**
Falls ein Paket **fehlende Abhängigkeiten** hat, können Sie diese manuell installieren:
```bash
# Debian/Ubuntu
sudo apt install [abhängigkeit1] [abhängigkeit2]

# RHEL/CentOS/Fedora
sudo yum install [abhängigkeit1] [abhängigkeit2]
```

---
---
#### **9. Software deinstallieren und bereinigen**
##### **9.1 Vollständige Deinstallation**
- **Debian/Ubuntu:**
  ```bash
  sudo apt purge [paketname]
  sudo apt autoremove
  ```

- **RHEL/CentOS/Fedora:**
  ```bash
  sudo yum remove [paketname]
  sudo yum autoremove
  ```

- **Arch Linux:**
  ```bash
  sudo pacman -Rs [paketname]
  ```

---
##### **9.2 Konfigurationsdateien bereinigen**
Manchmal bleiben **Konfigurationsdateien** nach der Deinstallation erhalten. Um diese zu entfernen:
- **Debian/Ubuntu:**
  ```bash
  sudo apt purge [paketname]
  ```
- **RHEL/CentOS/Fedora:**
  ```bash
  sudo yum remove [paketname] --purge
  ```
  (Hinweis: `yum` entfernt standardmäßig keine Konfigurationsdateien. Verwenden Sie `rpm -e --nodeps` mit Vorsicht.)

---
---
#### **10. Übungsaufgaben**
---
##### **Frage 1**
Wie installieren Sie das Paket `htop` unter **Debian/Ubuntu**?

??? success "Antwort"
    ```bash
    sudo apt update
    sudo apt install htop
    ```

---
##### **Frage 2**
Wie aktualisieren Sie **alle Pakete** unter **RHEL/CentOS**?

??? success "Antwort"
    ```bash
    sudo yum update
    ```
    oder für neuere Versionen:
    ```bash
    sudo dnf update
    ```

---
##### **Frage 3**
Wie zeigen Sie **alle installierten Pakete** unter **Arch Linux** an?

??? success "Antwort"
    ```bash
    sudo pacman -Q
    ```

---
##### **Frage 4**
Wie entfernen Sie ein Paket **inklusive seiner Konfigurationsdateien** unter **Debian/Ubuntu**?

??? success "Antwort"
    ```bash
    sudo apt purge [paketname]
    ```

---
##### **Frage 5**
Wie fügen Sie ein **neues Repository** unter **Debian/Ubuntu** hinzu (z. B. das PPA `ondrej/php`)?

??? success "Antwort"
    ```bash
    sudo add-apt-repository ppa:ondrej/php
    sudo apt update
    ```

---
##### **Frage 6**
Wie installieren Sie ein **`.deb`-Paket** manuell unter Debian/Ubuntu?

??? success "Antwort"
    ```bash
    sudo dpkg -i /pfad/zur/datei.deb
    sudo apt --fix-broken install  # Falls Abhängigkeiten fehlen
    ```

---
##### **Frage 7**
Wie zeigen Sie **alle Dateien** an, die zu einem Paket gehören (z. B. `nginx`) unter **RHEL/CentOS**?

??? success "Antwort"
    ```bash
    rpm -ql nginx
    ```

---
##### **Frage 8**
Wie aktualisieren Sie die **Paketdatenbank** und **alle Pakete** unter **openSUSE**?

??? success "Antwort"
    ```bash
    sudo zypper refresh
    sudo zypper update
    ```

---
##### **Frage 9**
Wie installieren Sie Software **aus dem Quellcode**? Nennen Sie die 5 Schritte.

??? success "Antwort"
    1. **Abhängigkeiten installieren** (z. B. `build-essential`).
    2. **Quellcode herunterladen** (z. B. mit `wget` oder `git clone`).
    3. **Quellcode entpacken** (z. B. mit `tar -xzvf`).
    4. **Konfigurieren** (mit `./configure`).
    5. **Kompilieren und installieren** (mit `make` und `sudo make install`).

---
##### **Frage 10**
Wie entfernen Sie **nicht mehr benötigte Abhängigkeiten** unter **Debian/Ubuntu**?

??? success "Antwort"
    ```bash
    sudo apt autoremove
    ```

---
---
#### **11. Praktische Beispiele**
---
##### **Beispiel 1: Installation eines Webservers (Nginx)**
**Debian/Ubuntu:**
```bash
sudo apt update
sudo apt install nginx
sudo systemctl start nginx
sudo systemctl enable nginx
```

**RHEL/CentOS:**
```bash
sudo yum install epel-release
sudo yum install nginx
sudo systemctl start nginx
sudo systemctl enable nginx
```

---
##### **Beispiel 2: Installation von Python 3.10 unter Ubuntu 22.04**
```bash
# 1. Abhängigkeiten installieren
sudo apt update
sudo apt install software-properties-common

# 2. PPA für Python 3.10 hinzufügen
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt update

# 3. Python 3.10 installieren
sudo apt install python3.10
```

---
##### **Beispiel 3: Installation von Docker unter CentOS 7**
```bash
# 1. Altes Docker-Paket entfernen (falls vorhanden)
sudo yum remove docker docker-client docker-client-latest docker-common docker-latest docker-latest-logrotate docker-logrotate docker-engine

# 2. Abhängigkeiten installieren
sudo yum install -y yum-utils device-mapper-persistent-data lvm2

# 3. Docker-Repository hinzufügen
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

# 4. Docker installieren
sudo yum install docker-ce docker-ce-cli containerd.io

# 5. Docker starten und aktivieren
sudo systemctl start docker
sudo systemctl enable docker
```

---
##### **Beispiel 4: Installation von `htop` aus dem Quellcode**
```bash
# 1. Abhängigkeiten installieren
sudo apt install build-essential autoconf automake libncurses5-dev

# 2. Quellcode herunterladen
wget https://github.com/htop-dev/htop/archive/refs/tags/3.2.2.tar.gz
tar -xzvf 3.2.2.tar.gz
cd htop-3.2.2

# 3. Konfigurieren, kompilieren und installieren
./autogen.sh
./configure
make
sudo make install
```

---
---
#### **12. Häufige Fehler und Lösungen**

| **Problem** | **Ursache** | **Lösung** |
|-------------|-------------|------------|
| **"Package not found"** | Paket ist nicht in den Repositories verfügbar. | Repository hinzufügen oder Paket manuell installieren. |
| **"Unmet dependencies"** | Fehlende Abhängigkeiten. | `sudo apt --fix-broken install` (Debian/Ubuntu) oder `sudo yum install [abhängigkeit]` (RHEL/CentOS). |
| **"Permission denied"** | Keine Berechtigung für die Installation. | `sudo` verwenden. |
| **"Failed to fetch"** | Netzwerkprobleme oder falsche Repository-URL. | Internetverbindung prüfen oder Repository-URL korrigieren. |
| **"No space left on device"** | Nicht genug Speicherplatz. | Festplattenplatz freigeben oder `apt clean`/`yum clean all` ausführen. |
| **Kompilierungsfehler** | Fehlende Abhängigkeiten für die Kompilierung. | `build-essential` und andere Entwicklertools installieren. |

---
---
#### **13. Vertiefung: Paketverwaltung mit `snap` und `flatpak`**
##### **13.1 `snap` – Universelle Paketverwaltung**
`snap` ist ein **plattformunabhängiges Paketformat**, das von Canonical entwickelt wurde. Es ermöglicht die Installation von Software in **isolierten Containern**.

**Wichtige Befehle:**

| Befehl | Beschreibung |
|--------|--------------|
| `sudo snap install [paketname]` | Installiert ein **Snap-Paket**. |
| `sudo snap remove [paketname]` | Entfernt ein **Snap-Paket**. |
| `snap list` | Listet **alle installierten Snap-Pakete** auf. |
| `snap info [paketname]` | Zeigt **Informationen zu einem Snap-Paket** an. |
| `sudo snap refresh` | Aktualisiert **alle Snap-Pakete**. |

**Beispiel:**
```bash
# Snap installieren (falls nicht vorhanden)
sudo apt install snapd

# Ein Snap-Paket installieren (z. B. `vlc`)
sudo snap install vlc
```

---
##### **13.2 `flatpak` – Universelle Paketverwaltung**
`flatpak` ist ein **weiteres plattformunabhängiges Paketformat**, das von der **Flatpak-Community** entwickelt wurde.

**Wichtige Befehle:**

| Befehl | Beschreibung |
|--------|--------------|
| `flatpak install [paketname]` | Installiert ein **Flatpak-Paket**. |
| `flatpak remove [paketname]` | Entfernt ein **Flatpak-Paket**. |
| `flatpak list` | Listet **alle installierten Flatpak-Pakete** auf. |
| `flatpak info [paketname]` | Zeigt **Informationen zu einem Flatpak-Paket** an. |
| `flatpak update` | Aktualisiert **alle Flatpak-Pakete**. |

**Beispiel:**
```bash
# Flatpak installieren (falls nicht vorhanden)
sudo apt install flatpak

# Flathub-Repository hinzufügen
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo

# Ein Flatpak-Paket installieren (z. B. `spotify`)
flatpak install flathub com.spotify.Client
```

---
---
#### **14. Zusammenfassung der wichtigsten Befehle**

| **Aktion** | **Debian/Ubuntu (`apt`/`dpkg`)** | **RHEL/CentOS (`yum`/`dnf`/`rpm`)** | **Arch Linux (`pacman`)** | **openSUSE (`zypper`)** |
|------------|----------------------------------|--------------------------------------|----------------------------|--------------------------|
| **Paketlisten aktualisieren** | `sudo apt update` | `sudo yum makecache` / `sudo dnf makecache` | `sudo pacman -Sy` | `sudo zypper refresh` |
| **Paket installieren** | `sudo apt install [paket]` | `sudo yum install [paket]` / `sudo dnf install [paket]` | `sudo pacman -S [paket]` | `sudo zypper install [paket]` |
| **Paket entfernen** | `sudo apt remove [paket]` | `sudo yum remove [paket]` / `sudo dnf remove [paket]` | `sudo pacman -R [paket]` | `sudo zypper remove [paket]` |
| **Paket inkl. Konfig entfernen** | `sudo apt purge [paket]` | `sudo yum remove [paket]` (manuell Konfig löschen) | `sudo pacman -Rs [paket]` | `sudo zypper remove --purge [paket]` |
| **Alle Pakete aktualisieren** | `sudo apt upgrade` | `sudo yum update` / `sudo dnf update` | `sudo pacman -Syu` | `sudo zypper update` |
| **Nach Paketen suchen** | `sudo apt search [suchbegriff]` | `sudo yum search [suchbegriff]` / `sudo dnf search [suchbegriff]` | `sudo pacman -Ss [suchbegriff]` | `sudo zypper search [suchbegriff]` |
| **Installierte Pakete auflisten** | `sudo apt list --installed` | `sudo yum list installed` / `sudo dnf list installed` | `sudo pacman -Q` | `sudo zypper packages` |
| **Abhängigkeiten anzeigen** | `apt depends [paket]` | `sudo yum deplist [paket]` / `sudo dnf deplist [paket]` | `pacman -Si [paket]` | `sudo zypper info [paket]` |
| **Lokales Paket installieren** | `sudo dpkg -i [paket.deb]` | `sudo rpm -i [paket.rpm]` | `sudo pacman -U [paket.pkg.tar.zst]` | `sudo zypper install [paket.rpm]` |

