# Infra DevOps Lab

Ce projet est un lab personnel réalisé dans une démarche de montée en compétences autour des pratiques DevOps, de l’observabilité et de l’automatisation d’infrastructure.

Issu d’un parcours en administration systèmes et réseaux, l’objectif est ici de construire une infrastructure cohérente et proche de la réalité, tout en intégrant des outils et méthodes modernes (Docker, Ansible, monitoring, centralisation des logs).

---

## Objectifs

- Automatiser le déploiement d’une infrastructure avec Ansible
- Mettre en place une architecture réseau segmentée (DMZ / LAN / ADMIN)
- Déployer des services conteneurisés (Docker)
- Implémenter une stack d’observabilité complète (metrics + logs)
- Centraliser les logs de plusieurs machines
- Mettre en place un reverse proxy (Traefik)

---

## Architecture

### Réseau

- **DMZ** : reverse proxy
- **LAN** : applications + monitoring + logs
- **ADMIN** : bastion Ansible

---

### Machines

| Machine            | Rôle                          |
|-------------------|------------------------------|
| adm-ansible-01    | Bastion / Ansible            |
| rp-traefik-01     | Reverse proxy (DMZ)          |
| app-docker-01     | Application Docker           |
| mon-grafana-01    | Monitoring (Prometheus)      |
| log-loki-01       | Centralisation logs (Loki)   |

---

### Flux

#### Trafic web

User → Traefik → Application Docker
#### Metrics

Node Exporter → Prometheus → Grafana
#### Logs

VMs → Promtail → Loki → Grafana



---

## Stack technique

### Infrastructure
- KVM / libvirt
- Debian 12

### Automatisation
- Ansible

### Conteneurisation
- Docker
- Docker Compose

### Observabilité
- Prometheus
- Node Exporter
- Grafana
- Loki
- Promtail

### Réseau / Reverse Proxy
- Traefik

---

##  Déploiement

Le déploiement est entièrement automatisé avec Ansible.

```bash
ansible-playbook -i inventory/hosts.ini playbooks/site.yml --ask-vault-pass
```

##  Observabilité
### Logs (Loki)

Exemples de requêtes :

```bash
{job="docker"}
```

```bash
{job="system"}
```

```bash
{job="docker"} |= "error"
```

### Metrics (Prometheus)

- CPU / RAM / Disk via Node Exporter
- Visualisation via Grafana

### Exemples

---

# Ce que j’ai travaillé dans ce projet
- Mise en place d’une architecture segmentée
- Automatisation complète avec Ansible
- Déploiement de services conteneurisés
- Centralisation et exploitation des logs
- Mise en place d’une stack de monitoring
- Compréhension des flux (réseau, logs, metrics)

# Améliorations possibles

- Ajout d’alerting (Grafana / Prometheus / Loki)
- Activation et analyse des logs Traefik (HTTP access logs)
- Mise en place de TLS avec certificats valides (Let's Encrypt)
- Déploiement sur un environnement cloud (AWS / Azure)
- Ajout d’un pipeline CI/CD

# Remarques

Ce projet est avant tout un environnement d’expérimentation technique, construit pour comprendre et manipuler des briques DevOps dans un contexte cohérent.
