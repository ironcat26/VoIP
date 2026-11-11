# Technical Specification: VoIP Observability Stack

## 1. Project Goal
Create a fully automated (Infrastructure-as-Code) monitoring and logging system for VoIP infrastructure (Asterisk PBX) and network equipment (MikroTik). The project must be deployed with a single command and accompanied by complete technical documentation.

## 2. Architecture
Deployed on 2 VMs under Proxmox VE (Ubuntu 22.04):
- `monitor2` (10.10.10.26): Prometheus, Alertmanager, Grafana, Loki, Ansible, Exporters.
- `app2` (10.10.10.25): Asterisk, node_exporter, asterisk_exporter, Promtail.
- `MikroTik`: SNMP (read-only).

## 3. Functional Requirements
- **Ansible:** All configuration must be automated via Ansible roles (site.yml).
- **Infrastructure Monitoring:** node_exporter (CPU, RAM, Disk), blackbox_exporter (HTTP/SIP probes).
- **VoIP Monitoring:** Asterisk (PJSIP), asterisk_exporter via AMI. Alerts: AsteriskDown, SipRegistrationLost.
- **Network Monitoring:** snmp_exporter for MikroTik. Alerts: MikroTikDown, HighInterfaceErrors.
- **Visualization:** Grafana dashboards as code (JSON provisioning).
- **Alerting:** Alertmanager + Gmail SMTP (inhibit rules, Game Day).
- **Logging:** Loki + Promtail. LogQL alerts.

## 4. Security
- SSH keys only.
- Secrets in `secrets.yml` (excluded from Git).
- Firewall (UFW, MikroTik rules).

## 5. CI/CD
GitHub Actions: yamllint, ansible-lint, promtool check, markdownlint.

## 6. Documentation
English, Markdown, Docs-as-Code. Sections: Getting Started, Architecture, Installation, Asterisk, Network, Monitoring, Metrics, Alerting, Logging, Troubleshooting, Runbooks, Glossary.
