# ⚙️ Ansible Infrastructure-as-Code (IaC)

Dieses Repository enthält meine Ansible-Playbooks, Inventare und Konfigurationsvorlagen zur vollständigen Automatisierung, Absicherung und Bereitstellung meines Linux-Servers (Ubuntu VPS).

![Docker](https://img.shields.io/badge/Docker-Containers-blue?logo=docker)
![Grafana](https://img.shields.io/badge/Grafana-Monitoring-orange?logo=grafana)
![Prometheus](https://img.shields.io/badge/Prometheus-Metrics-orange?logo=prometheus)
![Linux](https://img.shields.io/badge/Linux-Ubuntu-black?logo=linux)
![Nginx](https://img.shields.io/badge/Nginx-Reverse_Proxy-green?logo=nginx)
![Ansible](https://img.shields.io/badge/Ansible-Automation-CC0000?logo=ansible)

---

## 📋 Übersicht der Automatisierung

Das Projekt automatisiert die Bereitstellung der Kerninfrastruktur, die Konfiguration von Sicherheitsrichtlinien und das Rollout von Docker-basierten Diensten über eine einheitliche IaC-Pipeline.

### 🛠 Kernfunktionen & Systemkonfiguration
* **System-Härtung (Security):** Automatisierte Absicherung des SSH-Daemons (`sshd_config`) und Durchsetzung restriktiver Zugriffsberechtigungen.
* **Nginx Gateway-Verwaltung:** Bereitstellung und Validierung der zentralen Reverse-Proxy-Konfigurationen zur Verteilung des HTTP/HTTPS-Traffics.
* **Automatisierte Backup-Pipeline:** Einrichtung von root-basierten Cronjobs zur täglichen, verschlüsselten Sicherung der X-UI-Datenbank (`x-ui.db.encrypted`) mit automatischem Streaming in private Telegram-Kanäle.
* **Docker Multi-Stack Deployment:** Deklaratives Rollout von Anwendungs-Infrastrukturen (Portainer, Uptime Kuma) und dem Monitoring-Stack (Prometheus, Grafana).

---

## 📂 Repository-Struktur

```text
.
├── ansible.cfg                # Globale Ansible-Konfiguration und Optimierungen
├── hosts                      # Inventardatei mit Server-Definitionen
├── site.yml                   # Haupt-Playbook für den gesamten Infrastruktur-Rollout
├── host_vars/                 # Spezifische Variablen für die Ziel-Server-IPs
├── apps_config/               # Docker-Compose-Stacks für Kernanwendungen (Portainer, Kuma)
├── monitoring_config/         # Docker-Compose-Stacks & Prometheus-Konfigurationsdateien
├── system_config/             # Systemnahe Dienste und Sicherheitsvorlagen
│   ├── cron/                  # Automatisierte Backup- und Wartungs-Cronjobs
│   ├── nginx/                 # Nginx-Hauptkonfiguration (Reverse Proxy)
│   └── ssh/                   # Abgesicherte SSH-Konfiguration (sshd_config)
└── backups/                   # Lokale Zwischenspeicherung von verschlüsselten x-ui-Backups
```

---

## 💻 Workstation-Flexibilität (Multi-Node Setup)

Das Projekt ist so konzipiert, dass es flexibel von verschiedenen Entwicklungs-Workstations ausgeführt werden kann. Die Variablen und das `hosts`-Inventar steuern dynamisch:
1. Die Verwendung unterschiedlicher SSH-Schlüssel (z. B. `id_ed25519_wsl` unter Windows/WSL2).
2. Die automatische Anpassung der Python-Interpreter-Pfade je nach Herkunftssystem (Debian GNU/Linux Laptop vs. Windows Subsystem for Linux).

---

## 🚀 Nutzung

Um das gesamte Playbook auf die Infrastruktur anzuwenden, wird folgender Befehl ausgeführt:

```bash
ansible-playbook -i hosts site.yml
```

*Hinweis: Vor der Ausführung müssen die Platzhalter im Verzeichnis  `host_vars/YOUR_SERVER_IP_HERE` durch die tatsächliche IP-Adresse des Zielservers ersetzt werden.*
