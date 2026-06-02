### **Modul V: Zusammenführung und Zielsetzung**
### **Thema: Wichtige Open-Source-Anwendungen**

---

---

#### **1. Einführung in Open-Source-Software**
**Open-Source-Software (OSS)** ist Software, deren **Quellcode öffentlich zugänglich** ist und von der **Community weiterentwickelt, getestet und verbessert** werden kann. Open-Source-Software bietet folgende Vorteile:
- **Kostenlos**: Keine Lizenzgebühren.
- **Transparenz**: Der Quellcode kann überprüft werden (Sicherheit, Datenschutz).
- **Anpassbarkeit**: Software kann an individuelle Bedürfnisse angepasst werden.
- **Community-Unterstützung**: Große Gemeinschaft von Entwicklern und Nutzern.
- **Sicherheit**: Schnellere Fehlerbehebung durch viele Augen (Linus’s Law: *"Given enough eyeballs, all bugs are shallow"*).

---
##### **1.1 Open-Source-Lizenzen**
Open-Source-Software wird unter verschiedenen **Lizenzen** veröffentlicht, die die Nutzung, Modifikation und Weitergabe regeln. Hier sind die wichtigsten:

| **Lizenz** | **Beschreibung** | **Anforderungen** | **Beispiele** |
|------------|------------------|-------------------|---------------|
| **MIT-Lizenz** | Sehr permissiv, erlaubt fast jede Nutzung. | Beibehaltung des Lizenzhinweises. | Ruby, .NET Core, React |
| **GPL (GNU General Public License)** | Copyleft-Lizenz, erfordert, dass Modifikationen ebenfalls unter GPL veröffentlicht werden. | Quellcode muss offen bleiben. | Linux-Kernel, GIMP, Blender |
| **AGPL (Affero General Public License)** | Wie GPL, aber auch für **Netzwerkanwendungen** (z. B. SaaS). | Quellcode muss offen bleiben, auch bei Netzwerknutzung. | Nextcloud, Mastodon |
| **Apache-Lizenz 2.0** | Permissiv, aber mit **Patentschutz**. | Lizenzhinweis beibehalten, Änderungen dokumentieren. | Android, Kubernetes, Apache HTTP Server |
| **BSD-Lizenzen** (2-Clause, 3-Clause) | Sehr permissiv, ähnlich wie MIT. | Lizenzhinweis beibehalten (3-Clause: auch Werbung verbieten). | FreeBSD, OpenBSD, NetBSD |
| **LGPL (Lesser GPL)** | Erlaubt die **Verknüpfung mit proprietärer Software**. | Änderungen am LGPL-Code müssen offen bleiben. | GTK, libpng |
| **Mozilla Public License (MPL)** | Erlaubt **Modifikationen und kommerzielle Nutzung**. | Änderungen müssen offen bleiben. | Firefox, Thunderbird |

---
##### **1.2 Open-Source vs. Freie Software**
- **Open-Source-Software** (OSI-Definition): Betont **praktische Vorteile** (z. B. Qualität, Sicherheit, Kosten).
- **Freie Software** (FSF-Definition): Betont **ethische Aspekte** (Freiheit, Kontrolle über die Software).
  Die **4 Freiheiten** nach Richard Stallman:
  1. **Freiheit 0**: Die Freiheit, das Programm **für jeden Zweck** auszuführen.
  2. **Freiheit 1**: Die Freiheit, die **Funktionsweise des Programms** zu untersuchen und an die eigenen Bedürfnisse anzupassen.
  3. **Freiheit 2**: Die Freiheit, **Kopien weiterzugeben**.
  4. **Freiheit 3**: Die Freiheit, das Programm **zu verbessern und diese Verbesserungen der Öffentlichkeit zugänglich zu machen**.

---
---

#### **2. Kategorien von Open-Source-Anwendungen**
Open-Source-Software deckt **nahezu alle Bereiche** der IT ab. Hier sind die wichtigsten Kategorien mit Beispielen:

---
##### **2.1 Betriebssysteme**
| **Anwendung** | **Beschreibung** | **Website** | **Lizenz** |
|---------------|------------------|-------------|------------|
| **Linux** | Open-Source-Betriebssystemkernel, Basis für viele Distributionen. | [kernel.org](https://www.kernel.org/) | GPLv2 |
| **GNU/Linux-Distributionen** | Komplette Betriebssysteme basierend auf dem Linux-Kernel. | – | Verschieden |
| **Debian** | Eine der ältesten und stabilsten Linux-Distributionen. | [debian.org](https://www.debian.org/) | GPL, MIT, etc. |
| **Ubuntu** | Benutzerfreundliche Linux-Distribution basierend auf Debian. | [ubuntu.com](https://ubuntu.com/) | GPL, MIT, etc. |
| **Fedora** | Innovative Linux-Distribution von Red Hat. | [fedoraproject.org](https://fedoraproject.org/) | GPL, MIT, etc. |
| **Arch Linux** | Rolling-Release-Distribution für fortgeschrittene Nutzer. | [archlinux.org](https://archlinux.org/) | GPL, MIT, etc. |
| **FreeBSD** | Unix-ähnliches Betriebssystem mit Fokus auf Stabilität. | [freebsd.org](https://www.freebsd.org/) | BSD |
| **OpenBSD** | Betriebssystem mit Fokus auf Sicherheit. | [openbsd.org](https://www.openbsd.org/) | BSD |

---
##### **2.2 Büroanwendungen**
| **Anwendung** | **Beschreibung** | **Website** | **Lizenz** |
|---------------|------------------|-------------|------------|
| **LibreOffice** | Komplettes Office-Paket (Text, Tabellen, Präsentationen, Datenbanken). | [libreoffice.org](https://www.libreoffice.org/) | MPL |
| **OnlyOffice** | Office-Suite mit Kollaborationsfunktionen. | [onlyoffice.com](https://www.onlyoffice.com/) | AGPL |
| **Calligra Suite** | Office-Suite für KDE. | [calligra.org](https://calligra.org/) | LGPL |
| **Joplin** | Open-Source-Notiz-App mit Markdown-Unterstützung. | [joplinapp.org](https://joplinapp.org/) | MIT |
| **LaTeX** | Typesetting-System für wissenschaftliche Dokumente. | [latex-project.org](https://www.latex-project.org/) | LPPL |

---
##### **2.3 Grafik und Design**
| **Anwendung** | **Beschreibung** | **Website** | **Lizenz** |
|---------------|------------------|-------------|------------|
| **GIMP** | Bildbearbeitungsprogramm (Alternativ zu Photoshop). | [gimp.org](https://www.gimp.org/) | GPL |
| **Inkscape** | Vektorgrafik-Editor (Alternativ zu Adobe Illustrator). | [inkscape.org](https://inkscape.org/) | GPL |
| **Krita** | Digitales Malprogramm für Künstler. | [krita.org](https://krita.org/) | GPL |
| **Blender** | 3D-Modellierungs- und Animationssoftware. | [blender.org](https://www.blender.org/) | GPL |
| **Scribus** | Desktop-Publishing-Software. | [scribus.net](https://www.scribus.net/) | GPL |
| **Darktable** | RAW-Bildbearbeitung (Alternativ zu Lightroom). | [darktable.org](https://www.darktable.org/) | GPL |

---
##### **2.4 Multimedia**
| **Anwendung** | **Beschreibung** | **Website** | **Lizenz** |
|---------------|------------------|-------------|------------|
| **VLC Media Player** | Universeller Medienplayer. | [videolan.org](https://www.videolan.org/) | GPL |
| **Kdenlive** | Videobearbeitungssoftware. | [kdenlive.org](https://kdenlive.org/) | GPL |
| **Audacity** | Audiobearbeitungssoftware. | [audacityteam.org](https://www.audacityteam.org/) | GPL |
| **OBS Studio** | Software für Bildschirmaufnahmen und Live-Streaming. | [obsproject.com](https://obsproject.com/) | GPL |
| **HandBrake** | Videokonvertierungs-Tool. | [handbrake.fr](https://handbrake.fr/) | GPL |
| **LMMS** | Musikproduktionssoftware. | [lmms.io](https://lmms.io/) | GPL |

---
##### **2.5 Entwicklungstools**
| **Anwendung** | **Beschreibung** | **Website** | **Lizenz** |
|---------------|------------------|-------------|------------|
| **Visual Studio Code** | Code-Editor von Microsoft (Open-Source-Kern). | [code.visualstudio.com](https://code.visualstudio.com/) | MIT |
| **Eclipse** | Integrierte Entwicklungsumgebung (IDE) für Java und andere Sprachen. | [eclipse.org](https://www.eclipse.org/) | EPL |
| **IntelliJ IDEA (Community Edition)** | IDE für Java, Kotlin, Python, etc. | [jetbrains.com/idea](https://www.jetbrains.com/idea/) | Apache 2.0 |
| **Git** | Versionskontrollsystem. | [git-scm.com](https://git-scm.com/) | GPL |
| **GitLab** | Plattform für DevOps und Versionskontrolle. | [gitlab.com](https://about.gitlab.com/) | MIT |
| **GitHub** | Plattform für Hosting von Git-Repositories. | [github.com](https://github.com/) | MIT (für Open-Source-Projekte) |
| **Docker** | Container-Plattform. | [docker.com](https://www.docker.com/) | Apache 2.0 |
| **Kubernetes** | System zur Automatisierung von Container-Bereitstellung. | [kubernetes.io](https://kubernetes.io/) | Apache 2.0 |
| **Postman** | API-Test-Tool. | [postman.com](https://www.postman.com/) | Apache 2.0 (Open-Source-Version) |
| **Jupyter Notebook** | Interaktive Entwicklungsumgebung für Python, R, etc. | [jupyter.org](https://jupyter.org/) | BSD |

---
##### **2.6 Datenbanken**
| **Anwendung** | **Beschreibung** | **Website** | **Lizenz** |
|---------------|------------------|-------------|------------|
| **MySQL** | Relationales Datenbanksystem. | [mysql.com](https://www.mysql.com/) | GPL |
| **MariaDB** | Fork von MySQL. | [mariadb.org](https://mariadb.org/) | GPL |
| **PostgreSQL** | Objekt-relationales Datenbanksystem. | [postgresql.org](https://www.postgresql.org/) | PostgreSQL License |
| **SQLite** | Leichtgewichtige, serverlose Datenbank. | [sqlite.org](https://www.sqlite.org/) | Public Domain |
| **MongoDB** | NoSQL-Datenbank (Dokumentenorientiert). | [mongodb.com](https://www.mongodb.com/) | AGPL |
| **Redis** | In-Memory-Datenbank für Caching und Echtzeit-Anwendungen. | [redis.io](https://redis.io/) | BSD |
| **Elasticsearch** | Such- und Analysedatenbank. | [elastic.co](https://www.elastic.co/) | Apache 2.0 |

---
##### **2.7 Webserver und Webanwendungen**
| **Anwendung** | **Beschreibung** | **Website** | **Lizenz** |
|---------------|------------------|-------------|------------|
| **Apache HTTP Server** | Beliebter Webserver. | [apache.org](https://httpd.apache.org/) | Apache 2.0 |
| **Nginx** | Hochperformanter Webserver und Reverse Proxy. | [nginx.org](https://www.nginx.org/) | BSD |
| **WordPress** | Content-Management-System (CMS) für Blogs und Websites. | [wordpress.org](https://wordpress.org/) | GPL |
| **Joomla** | CMS für Websites. | [joomla.org](https://www.joomla.org/) | GPL |
| **Drupal** | CMS für komplexe Websites. | [drupal.org](https://www.drupal.org/) | GPL |
| **Nextcloud** | Selbstgehostete Cloud-Plattform. | [nextcloud.com](https://nextcloud.com/) | AGPL |
| **ownCloud** | Selbstgehostete Cloud-Plattform. | [owncloud.com](https://owncloud.com/) | AGPL |
| **Mastodon** | Dezentrales soziales Netzwerk. | [joinmastodon.org](https://joinmastodon.org/) | AGPL |
| **Discourse** | Forum-Software. | [discourse.org](https://www.discourse.org/) | GPL |

---
##### **2.8 Netzwerk und Sicherheit**
| **Anwendung** | **Beschreibung** | **Website** | **Lizenz** |
|---------------|------------------|-------------|------------|
| **Wireshark** | Netzwerkprotokoll-Analysator. | [wireshark.org](https://www.wireshark.org/) | GPL |
| **OpenVPN** | VPN-Software für sichere Verbindungen. | [openvpn.net](https://openvpn.net/) | GPL |
| **WireGuard** | Modernes, schnelles VPN. | [wireguard.com](https://www.wireguard.com/) | GPL |
| **Snort** | Intrusion Detection System (IDS). | [snort.org](https://www.snort.org/) | GPL |
| **Suricata** | Intrusion Detection/Prevention System (IDS/IPS). | [suricata.io](https://suricata.io/) | GPL |
| **Fail2Ban** | Schutz vor Brute-Force-Angriffen. | [fail2ban.org](https://www.fail2ban.org/) | GPL |
| **ClamAV** | Antiviren-Software. | [clamav.net](https://www.clamav.net/) | GPL |
| **Let’s Encrypt** | Kostenlose SSL/TLS-Zertifikate. | [letsencrypt.org](https://letsencrypt.org/) | Apache 2.0 |

---
##### **2.9 Virtualisierung und Container**
| **Anwendung** | **Beschreibung** | **Website** | **Lizenz** |
|---------------|------------------|-------------|------------|
| **QEMU** | Open-Source-Emulator und Virtualisierungsplattform. | [qemu.org](https://www.qemu.org/) | GPL |
| **KVM (Kernel-based Virtual Machine)** | Virtualisierungslösung für Linux. | [linux-kvm.org](https://www.linux-kvm.org/) | GPL |
| **VirtualBox** | Virtualisierungssoftware von Oracle. | [virtualbox.org](https://www.virtualbox.org/) | GPL |
| **Proxmox VE** | Enterprise-Virtualisierungsplattform. | [proxmox.com](https://www.proxmox.com/) | AGPL |
| **LXC (Linux Containers)** | Container-Plattform. | [linuxcontainers.org](https://linuxcontainers.org/) | Apache 2.0 |
| **Podman** | Container-Engine (Docker-Alternative). | [podman.io](https://podman.io/) | Apache 2.0 |
| **LXD** | Container-basierte Virtualisierungsplattform. | [linuxcontainers.org/lxd](https://linuxcontainers.org/lxd/) | Apache 2.0 |

---
##### **2.10 Wissenschaft und Bildung**
| **Anwendung** | **Beschreibung** | **Website** | **Lizenz** |
|---------------|------------------|-------------|------------|
| **Moodle** | Lernplattform (LMS). | [moodle.org](https://moodle.org/) | GPL |
| **Open edX** | Plattform für Online-Kurse. | [openedx.org](https://openedx.org/) | AGPL |
| **Kiwix** | Offline-Reader für Wikipedia und andere Inhalte. | [kiwix.org](https://www.kiwix.org/) | GPL |
| **Stellarium** | Planetarium-Software. | [stellarium.org](https://stellarium.org/) | GPL |
| **GNU Octave** | Mathematische Berechnungssoftware (Matlab-Alternative). | [octave.org](https://www.gnu.org/software/octave/) | GPL |
| **R** | Statistiksoftware. | [r-project.org](https://www.r-project.org/) | GPL |
| **JupyterLab** | Web-basierte Entwicklungsumgebung für Datenwissenschaft. | [jupyter.org](https://jupyter.org/) | BSD |

---
##### **2.11 Spiele**
| **Anwendung** | **Beschreibung** | **Website** | **Lizenz** |
|---------------|------------------|-------------|------------|
| **0 A.D.** | Echtzeit-Strategiespiel. | [play0ad.com](https://play0ad.com/) | GPL |
| **SuperTux** | 2D-Jump-and-Run-Spiel (Mario-Klon). | [supertux.org](https://www.supertux.org/) | GPL |
| **FreeCiv** | Strategiespiel (Civilization-Klon). | [freeciv.org](https://www.freeciv.org/) | GPL |
| **Wesnoth** | Rundenbasiertes Strategiespiel. | [wesnoth.org](https://www.wesnoth.org/) | GPL |
| **OpenTTD** | Transport-Simulationsspiel (Transport Tycoon Deluxe-Klon). | [openttd.org](https://www.openttd.org/) | GPL |
| **Godot Engine** | Spiel-Engine für 2D- und 3D-Spiele. | [godotengine.org](https://godotengine.org/) | MIT |

---
##### **2.12 Kommunikation und Kollaboration**
| **Anwendung** | **Beschreibung** | **Website** | **Lizenz** |
|---------------|------------------|-------------|------------|
| **Thunderbird** | E-Mail-Client von Mozilla. | [thunderbird.net](https://www.thunderbird.net/) | MPL |
| **Signal** | Verschlüsselte Messaging-App. | [signal.org](https://signal.org/) | GPL |
| **Element (Matrix)** | Dezentrale Messaging-App. | [element.io](https://element.io/) | Apache 2.0 |
| **Jitsi Meet** | Videokonferenz-Software. | [jitsi.org](https://jitsi.org/) | Apache 2.0 |
| **BigBlueButton** | Webkonferenz-System für Bildung. | [bigbluebutton.org](https://bigbluebutton.org/) | LGPL |
| **Mattermost** | Selbstgehosteter Slack-Alternative. | [mattermost.com](https://mattermost.com/) | AGPL |
| **Rocket.Chat** | Selbstgehosteter Chat-Server. | [rocket.chat](https://rocket.chat/) | MIT |

---
---
#### **3. Open-Source-Anwendungen für spezifische Anwendungsfälle**
---
##### **3.1 Open-Source für Unternehmen**
| **Anwendung** | **Beschreibung** | **Website** | **Lizenz** |
|---------------|------------------|-------------|------------|
| **ERPNext** | Enterprise Resource Planning (ERP)-System. | [erpnext.com](https://erpnext.com/) | MIT |
| **Odoo** | ERP- und CRM-System. | [odoo.com](https://www.odoo.com/) | LGPL |
| **SuiteCRM** | Customer Relationship Management (CRM). | [suitecrm.com](https://suitecrm.com/) | AGPL |
| **Nextcloud Groupware** | Kollaborationssuite (E-Mail, Kalender, Kontakte). | [nextcloud.com](https://nextcloud.com/) | AGPL |
| **Zimbra** | E-Mail- und Kollaborationsplattform. | [zimbra.com](https://www.zimbra.com/) | GPL |

---
##### **3.2 Open-Source für Entwickler**
| **Anwendung** | **Beschreibung** | **Website** | **Lizenz** |
|---------------|------------------|-------------|------------|
| **GitLab CE** | Selbstgehostete Git-Repository-Verwaltung. | [gitlab.com](https://about.gitlab.com/) | MIT |
| **Gitea** | Leichtgewichtige Git-Repository-Verwaltung. | [gitea.io](https://gitea.io/) | MIT |
| **Jenkins** | Automatisierungsserver für CI/CD. | [jenkins.io](https://www.jenkins.io/) | MIT |
| **SonarQube** | Code-Qualitätsanalyse. | [sonarqube.org](https://www.sonarqube.org/) | LGPL |
| **Sentry** | Fehlerüberwachung für Anwendungen. | [sentry.io](https://sentry.io/) | BSD |

---
##### **3.3 Open-Source für DevOps**
| **Anwendung** | **Beschreibung** | **Website** | **Lizenz** |
|---------------|------------------|-------------|------------|
| **Ansible** | Automatisierungstool für Konfiguration und Bereitstellung. | [ansible.com](https://www.ansible.com/) | GPL |
| **Terraform** | Infrastructure as Code (IaC). | [terraform.io](https://www.terraform.io/) | MPL |
| **Prometheus** | Monitoring- und Alerting-Toolkit. | [prometheus.io](https://prometheus.io/) | Apache 2.0 |
| **Grafana** | Visualisierungsplattform für Metriken. | [grafana.com](https://grafana.com/) | AGPL |
| **ELK Stack** (Elasticsearch, Logstash, Kibana) | Log-Management und Analyse. | [elastic.co](https://www.elastic.co/) | Apache 2.0 |
| **Nagios** | Monitoring-System für Server und Dienste. | [nagios.org](https://www.nagios.org/) | GPL |

---
##### **3.4 Open-Source für KI und Machine Learning**
| **Anwendung** | **Beschreibung** | **Website** | **Lizenz** |
|---------------|------------------|-------------|------------|
| **TensorFlow** | Machine-Learning-Framework von Google. | [tensorflow.org](https://www.tensorflow.org/) | Apache 2.0 |
| **PyTorch** | Machine-Learning-Framework von Facebook. | [pytorch.org](https://pytorch.org/) | BSD |
| **scikit-learn** | Machine-Learning-Bibliothek für Python. | [scikit-learn.org](https://scikit-learn.org/) | BSD |
| **Keras** | Hochlevel-Machine-Learning-API. | [keras.io](https://keras.io/) | MIT |
| **Hugging Face Transformers** | Bibliothek für NLP (Natural Language Processing). | [huggingface.co](https://huggingface.co/) | Apache 2.0 |
| **Jupyter Notebook** | Interaktive Entwicklungsumgebung für Datenwissenschaft. | [jupyter.org](https://jupyter.org/) | BSD |

---
---
#### **4. Open-Source-Alternativen zu proprietärer Software**
Viele **proprietäre Softwarelösungen** haben **Open-Source-Alternativen**, die oft **kostenlos, sicherer und anpassbarer** sind.

| **Proprietäre Software** | **Open-Source-Alternative** | **Beschreibung** |
|--------------------------|-----------------------------|------------------|
| **Microsoft Windows** | Linux (Ubuntu, Fedora, etc.) | Betriebssystem. |
| **Microsoft Office** | LibreOffice, OnlyOffice | Office-Suite. |
| **Adobe Photoshop** | GIMP, Krita | Bildbearbeitung. |
| **Adobe Illustrator** | Inkscape | Vektorgrafik. |
| **Adobe Premiere Pro** | Kdenlive, OpenShot | Videobearbeitung. |
| **Adobe After Effects** | Blender (für 3D/Animation) | 3D-Animation und Effekte. |
| **AutoCAD** | FreeCAD, LibreCAD | CAD-Software. |
| **Microsoft Visual Studio** | Visual Studio Code, Eclipse | IDE. |
| **GitHub (Enterprise)** | GitLab, Gitea | Git-Repository-Verwaltung. |
| **Slack** | Mattermost, Rocket.Chat | Team-Kollaboration. |
| **Microsoft Teams** | Jitsi Meet, Element | Videokonferenz. |
| **Zoom** | Jitsi Meet, BigBlueButton | Videokonferenz. |
| **Dropbox** | Nextcloud, ownCloud | Cloud-Speicher. |
| **Google Drive** | Nextcloud, ownCloud | Cloud-Speicher. |
| **Notion** | Joplin, AppFlowy | Notiz- und Wissensmanagement. |
| **Evernote** | Joplin, Zim | Notiz-App. |
| **Trello** | Taiga, OpenProject | Projektmanagement. |
| **Jira** | Redmine, OpenProject | Projektmanagement. |
| **Photoshop Lightroom** | Darktable, RawTherapee | RAW-Bildbearbeitung. |
| **Final Cut Pro** | Kdenlive, OpenShot | Videobearbeitung. |
| **Sublime Text** | Visual Studio Code, Kate | Texteditor. |
| **WinRAR / 7-Zip** | File Roller, PeaZip | Archivierung. |
| **Microsoft SQL Server** | PostgreSQL, MySQL | Datenbank. |
| **Oracle Database** | PostgreSQL, MariaDB | Datenbank. |
| **SAP** | ERPNext, Odoo | ERP-System. |
| **Salesforce** | SuiteCRM, Odoo | CRM-System. |
| **Matlab** | GNU Octave, Python (NumPy, SciPy) | Mathematische Berechnungen. |
| **SPSS** | R, Jamovi | Statistiksoftware. |
| **Tableau** | Metabase, Superset | Datenvisualisierung. |
| **Power BI** | Metabase, Superset | Business Intelligence. |

---
---
#### **5. Open-Source in der Praxis: Fallstudien**
---
##### **5.1 Open-Source im Unternehmen: Nextcloud**
**Szenario:** Ein Unternehmen möchte eine **selbstgehostete Cloud-Lösung** für Dateispeicherung, Kollaboration und Kommunikation nutzen.

**Lösung:**
- **Nextcloud** installieren:
  ```bash
  # Beispiel für Debian/Ubuntu
  sudo apt install nextcloud
  ```
- **Webserver (Apache/Nginx) und Datenbank (MySQL/MariaDB/PostgreSQL) konfigurieren**.
- **Apps installieren** (z. B. OnlyOffice für Dokumentenbearbeitung, Talk für Videokonferenzen).
- **Benutzer und Gruppen verwalten**.
- **Backups einrichten** (z. B. mit `rsync` oder `BorgBackup`).

**Vorteile:**
- **Datenhoheit**: Alle Daten bleiben im Unternehmen.
- **Sicherheit**: Verschlüsselung, Zertifikate (Let’s Encrypt), Firewall.
- **Kosten**: Keine Lizenzgebühren.
- **Erweiterbarkeit**: Viele Plugins und Integrationen.

---
##### **5.2 Open-Source für Entwickler: GitLab**
**Szenario:** Ein Entwicklungsteam möchte eine **selbstgehostete Git-Repository-Verwaltung** mit CI/CD-Pipelines nutzen.

**Lösung:**
- **GitLab CE (Community Edition) installieren**:
  ```bash
  # Beispiel für Debian/Ubuntu
  sudo apt install gitlab-ce
  ```
- **Konfiguration anpassen** (`/etc/gitlab/gitlab.rb`).
- **CI/CD-Pipelines einrichten** (`.gitlab-ci.yml`).
- **Runner registrieren** für die Ausführung von Jobs.

**Vorteile:**
- **Zentrale Code-Verwaltung**: Alle Projekte an einem Ort.
- **CI/CD**: Automatisierte Tests und Bereitstellungen.
- **Issue-Tracking**: Integriertes Projektmanagement.
- **Selbstgehostet**: Keine Abhängigkeit von externen Anbietern.

---
##### **5.3 Open-Source für Bildung: Moodle**
**Szenario:** Eine Schule oder Universität möchte eine **Lernplattform** für Online-Kurse einrichten.

**Lösung:**
- **Moodle installieren**:
  ```bash
  # Beispiel für Debian/Ubuntu
  sudo apt install moodle
  ```
- **Webserver (Apache/Nginx) und Datenbank (MySQL/MariaDB/PostgreSQL) konfigurieren**.
- **Kurse und Benutzer anlegen**.
- **Plugins installieren** (z. B. für Videokonferenzen mit BigBlueButton).

**Vorteile:**
- **Flexibilität**: Anpassung an individuelle Bedürfnisse.
- **Kosten**: Keine Lizenzgebühren.
- **Community**: Große Gemeinschaft mit vielen Plugins und Themen.

---
##### **5.4 Open-Source für DevOps: Docker + Kubernetes**
**Szenario:** Ein Unternehmen möchte **Container-basierte Anwendungen** bereitzustellen und zu verwalten.

**Lösung:**
1. **Docker installieren**:
   ```bash
   # Beispiel für Debian/Ubuntu
   sudo apt install docker.io
   sudo systemctl enable --now docker
   ```
2. **Kubernetes installieren** (z. B. mit `kubeadm`):
   ```bash
   sudo apt install kubeadm kubelet kubectl
   sudo kubeadm init
   ```
3. **Container-Images erstellen** (mit `Dockerfile`).
4. **Anwendungen in Kubernetes bereitzustellen** (mit `kubectl apply -f deployment.yaml`).

**Vorteile:**
- **Skalierbarkeit**: Einfaches Skalieren von Anwendungen.
- **Portabilität**: Container laufen auf jedem System mit Docker/Kubernetes.
- **Automatisierung**: CI/CD-Pipelines für Container-Images.
- **Ressourceneffizienz**: Geringerer Overhead im Vergleich zu virtuellen Maschinen.

---
---
#### **6. Open-Source-Communities und Ressourcen**
---
##### **6.1 Wichtige Open-Source-Communities**
| **Community** | **Beschreibung** | **Website** |
|---------------|------------------|-------------|
| **GitHub** | Plattform für Hosting von Open-Source-Projekten. | [github.com](https://github.com/) |
| **GitLab** | Plattform für DevOps und Open-Source-Projekte. | [gitlab.com](https://about.gitlab.com/) |
| **SourceForge** | Plattform für Open-Source-Projekte. | [sourceforge.net](https://sourceforge.net/) |
| **Open Source Initiative (OSI)** | Organisation, die Open-Source-Software fördert. | [opensource.org](https://opensource.org/) |
| **Free Software Foundation (FSF)** | Organisation, die freie Software fördert. | [fsf.org](https://www.fsf.org/) |
| **Linux Foundation** | Organisation, die Linux und Open-Source-Projekte unterstützt. | [linuxfoundation.org](https://www.linuxfoundation.org/) |
| **Apache Software Foundation** | Organisation, die Apache-Projekte unterstützt. | [apache.org](https://www.apache.org/) |
| **Eclipse Foundation** | Organisation, die Eclipse-Projekte unterstützt. | [eclipse.org](https://www.eclipse.org/) |

---
##### **6.2 Ressourcen für Open-Source-Software**
| **Ressource** | **Beschreibung** | **Website** |
|---------------|------------------|-------------|
| **GitHub Explore** | Entdecken Sie Open-Source-Projekte. | [github.com/explore](https://github.com/explore) |
| **Open Hub** | Analysiert Open-Source-Projekte. | [openhub.net](https://www.openhub.net/) |
| **AlternativeTo** | Finden Sie Open-Source-Alternativen zu proprietärer Software. | [alternativeto.net](https://alternativeto.net/) |
| **DistroWatch** | Informationen über Linux-Distributionen. | [distrowatch.com](https://distrowatch.com/) |
| **FOSS Post** | Nachrichten und Artikel über Open-Source-Software. | [fosspost.com](https://fosspost.com/) |
| **LWN.net** | Nachrichten und Artikel über Linux und Open-Source. | [lwn.net](https://lwn.net/) |
| **OpenSource.com** | Artikel und Ressourcen über Open-Source. | [opensource.com](https://opensource.com/) |

---
---
#### **7. Übungsaufgaben**
---
##### **Frage 1**
Was ist der Hauptunterschied zwischen **Open-Source-Software** und **Freier Software**?

??? success "Antwort"
    **Open-Source-Software** betont **praktische Vorteile** (z. B. Qualität, Sicherheit, Kosten), während **Freie Software** (nach der Definition der FSF) **ethische Aspekte** wie die **4 Freiheiten** (Nutzung, Anpassung, Weitergabe, Verbesserung) in den Vordergrund stellt.

---
##### **Frage 2**
Nennen Sie **drei Open-Source-Alternativen** zu Microsoft Office.

??? success "Antwort"
    1. **LibreOffice**
    2. **OnlyOffice**
    3. **Calligra Suite**

---
##### **Frage 3**
Welche **Open-Source-Lizenz** erfordert, dass Modifikationen ebenfalls unter der gleichen Lizenz veröffentlicht werden?

??? success "Antwort"
    **GPL (GNU General Public License)** und **AGPL (Affero General Public License)**.

---
##### **Frage 4**
Welche **Open-Source-Anwendung** können Sie für **Bildbearbeitung** verwenden, die eine Alternative zu Adobe Photoshop ist?

??? success "Antwort"
    **GIMP (GNU Image Manipulation Program)**.

---
##### **Frage 5**
Wie können Sie **Nextcloud** auf einem Debian/Ubuntu-System installieren?

??? success "Antwort"
    ```bash
    sudo apt install nextcloud
    ```
    Anschließend müssen Sie einen **Webserver (Apache/Nginx)** und eine **Datenbank (MySQL/MariaDB/PostgreSQL)** konfigurieren.

---
##### **Frage 6**
Welche **Open-Source-Anwendung** können Sie für **Videobearbeitung** verwenden?

??? success "Antwort"
    **Kdenlive** oder **OpenShot**.

---
##### **Frage 7**
Nennen Sie **drei Open-Source-Datenbanken**.

??? success "Antwort"
    1. **MySQL** / **MariaDB**
    2. **PostgreSQL**
    3. **MongoDB** (NoSQL)

---
##### **Frage 8**
Welche **Open-Source-Anwendung** können Sie für **Containerisierung** verwenden?

??? success "Antwort"
    **Docker** oder **Podman**.

---
##### **Frage 9**
Wie können Sie **GitLab CE** auf einem Debian/Ubuntu-System installieren?

??? success "Antwort"
    ```bash
    sudo apt install gitlab-ce
    ```
    Anschließend müssen Sie die **Konfiguration anpassen** (`/etc/gitlab/gitlab.rb`) und GitLab neu starten:
    ```bash
    sudo gitlab-ctl reconfigure
    ```

---
##### **Frage 10**
Welche **Open-Source-Anwendung** können Sie für **Monitoring und Alerting** verwenden?

??? success "Antwort"
    **Prometheus** (für Metriken) und **Grafana** (für Visualisierung).

---
---
#### **8. Praktische Beispiele**
---
##### **Beispiel 1: Installation von LibreOffice**
**Szenario:** Sie möchten **LibreOffice** auf einem Ubuntu-System installieren.

**Lösung:**
```bash
sudo apt update
sudo apt install libreoffice
```

---
##### **Beispiel 2: Installation von GIMP**
**Szenario:** Sie möchten **GIMP** für Bildbearbeitung installieren.

**Lösung:**
```bash
# Debian/Ubuntu
sudo apt install gimp

# RHEL/CentOS
sudo yum install gimp

# Arch Linux
sudo pacman -S gimp
```

---
##### **Beispiel 3: Installation von Nextcloud mit Docker**
**Szenario:** Sie möchten **Nextcloud** in einem Docker-Container ausführen.

**Lösung:**
1. **Docker installieren** (falls nicht vorhanden):
   ```bash
   sudo apt install docker.io
   sudo systemctl enable --now docker
   ```
2. **Nextcloud-Container starten**:
   ```bash
   sudo docker run -d \
     --name nextcloud \
     -p 8080:80 \
     -v /pfad/zur/daten:/var/www/html \
     --restart unless-stopped \
     nextcloud:latest
   ```
3. **Nextcloud im Browser öffnen**:
   - Öffnen Sie `http://<Ihre-IP>:8080` und folgen Sie den Installationsanweisungen.

---
##### **Beispiel 4: Installation von GitLab mit Docker**
**Szenario:** Sie möchten **GitLab CE** in Docker-Containern ausführen.

**Lösung:**
1. **Docker installieren** (falls nicht vorhanden).
2. **GitLab-Container starten**:
   ```bash
   sudo docker run -d \
     --hostname gitlab.example.com \
     --publish 443:443 --publish 80:80 --publish 22:22 \
     --name gitlab \
     --restart always \
     --volume /srv/gitlab/config:/etc/gitlab \
     --volume /srv/gitlab/logs:/var/log/gitlab \
     --volume /srv/gitlab/data:/var/opt/gitlab \
     gitlab/gitlab-ce:latest
   ```
3. **GitLab im Browser öffnen**:
   - Öffnen Sie `http://<Ihre-IP>` und folgen Sie den Installationsanweisungen.

---
##### **Beispiel 5: Installation von Moodle**
**Szenario:** Sie möchten **Moodle** für eine Lernplattform installieren.

**Lösung:**
1. **Abhängigkeiten installieren** (Apache, MySQL, PHP):
   ```bash
   sudo apt install apache2 mysql-server php php-mysql libapache2-mod-php php-gd php-curl php-mbstring php-xml php-xmlrpc php-soap php-intl php-zip
   ```
2. **Moodle herunterladen und entpacken**:
   ```bash
   wget https://download.moodle.org/stable403/moodle-4.3.0.tgz
   tar -xzvf moodle-4.3.0.tgz
   sudo mv moodle /var/www/html/
   ```
3. **Datenbank und Benutzer erstellen**:
   ```bash
   sudo mysql -u root -p
   ```
   ```sql
   CREATE DATABASE moodle;
   CREATE USER 'moodleuser'@'localhost' IDENTIFIED BY 'passwort';
   GRANT ALL PRIVILEGES ON moodle.* TO 'moodleuser'@'localhost';
   FLUSH PRIVILEGES;
   EXIT;
   ```
4. **Apache konfigurieren**:
   ```bash
   sudo chown -R www-data:www-data /var/www/html/moodle
   sudo chmod -R 755 /var/www/html/moodle
   ```
5. **Moodle im Browser öffnen**:
   - Öffnen Sie `http://<Ihre-IP>/moodle` und folgen Sie den Installationsanweisungen.

---
---
#### **9. Häufige Fehler und Lösungen**
| **Problem** | **Ursache** | **Lösung** |
|-------------|-------------|------------|
| **`E: Package not found` (Debian/Ubuntu)** | Paket ist nicht in den Repositories verfügbar. | Repository hinzufügen oder Paket manuell installieren. |
| **`Error: Unable to find a match` (RHEL/CentOS)** | Paket ist nicht in den Repositories verfügbar. | EPEL-Repository hinzufügen: `sudo yum install epel-release`. |
| **Nextcloud: "Database connection failed"** | Falsche Datenbankkonfiguration. | Überprüfen Sie die Datenbankverbindung in `/var/www/html/nextcloud/config/config.php`. |
| **GitLab: "502 Whoops, GitLab is taking too much time to respond"** | Falsche Konfiguration oder Ressourcenmangel. | Überprüfen Sie die GitLab-Logs: `sudo gitlab-ctl tail`. |
| **Moodle: "PHP extension missing"** | Fehlende PHP-Erweiterungen. | Installieren Sie die fehlenden Erweiterungen: `sudo apt install php-<erweiterung>`. |
| **Docker: "Permission denied"** | Keine Berechtigung für Docker. | Fügen Sie Ihren Benutzer zur Docker-Gruppe hinzu: `sudo usermod -aG docker $USER`. |
| **Open-Source-Software läuft nicht stabil** | Fehlende Abhängigkeiten oder veraltete Version. | Überprüfen Sie die **Systemanforderungen** und installieren Sie fehlende Abhängigkeiten. |

---
---
#### **10. Vertiefung: Open-Source in der Cloud**
---
##### **10.1 Open-Source-Cloud-Plattformen**
| **Plattform** | **Beschreibung** | **Website** | **Lizenz** |
|---------------|------------------|-------------|------------|
| **OpenStack** | Cloud-Computing-Plattform für IaaS (Infrastructure as a Service). | [openstack.org](https://www.openstack.org/) | Apache 2.0 |
| **CloudStack** | Cloud-Computing-Plattform für IaaS. | [cloudstack.apache.org](https://cloudstack.apache.org/) | Apache 2.0 |
| **Proxmox VE** | Virtualisierungsplattform mit integriertem Cloud-Management. | [proxmox.com](https://www.proxmox.com/) | AGPL |
| **OpenNebula** | Cloud-Computing-Plattform für IaaS. | [opennebula.io](https://opennebula.io/) | Apache 2.0 |

---
##### **10.2 Open-Source-Cloud-Dienste**
| **Dienst** | **Beschreibung** | **Website** | **Lizenz** |
|------------|------------------|-------------|------------|
| **Nextcloud** | Selbstgehostete Cloud-Speicherplattform. | [nextcloud.com](https://nextcloud.com/) | AGPL |
| **ownCloud** | Selbstgehostete Cloud-Speicherplattform. | [owncloud.com](https://owncloud.com/) | AGPL |
| **Seafile** | Selbstgehostete Cloud-Speicherplattform. | [seafile.com](https://www.seafile.com/) | AGPL |
| **MinIO** | Selbstgehosteter S3-kompatibler Objektspeicher. | [min.io](https://min.io/) | Apache 2.0 |
| **Ceph** | Verteilte Speicherplattform. | [ceph.io](https://ceph.io/) | LGPL |

---
---
#### **11. Zusammenfassung der wichtigsten Open-Source-Anwendungen**
| **Kategorie** | **Anwendungen** |
|---------------|------------------|
| **Betriebssysteme** | Linux, FreeBSD, OpenBSD |
| **Büroanwendungen** | LibreOffice, OnlyOffice, Joplin |
| **Grafik und Design** | GIMP, Inkscape, Krita, Blender |
| **Multimedia** | VLC, Kdenlive, Audacity, OBS Studio |
| **Entwicklungstools** | VS Code, Git, GitLab, Docker, Kubernetes |
| **Datenbanken** | MySQL, MariaDB, PostgreSQL, MongoDB, Redis |
| **Webserver** | Apache, Nginx, WordPress, Nextcloud |
| **Netzwerk und Sicherheit** | Wireshark, OpenVPN, WireGuard, Fail2Ban |
| **Virtualisierung** | QEMU, KVM, VirtualBox, Proxmox VE, LXC, Podman |
| **Wissenschaft und Bildung** | Moodle, Open edX, Kiwix, Stellarium |
| **Spiele** | 0 A.D., SuperTux, FreeCiv, Godot Engine |
| **Kommunikation** | Thunderbird, Signal, Jitsi Meet, Mattermost |

