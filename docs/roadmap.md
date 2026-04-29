# 🗺️ Roadmap — Infra DevOps Lab

## 🎯 Objectif

Construire une infrastructure complète, automatisée et sécurisée, proche d’un environnement de production.

---

## ✅ Milestones validées

### 🧱 Infrastructure de base

- [x] Setup réseaux libvirt (DMZ / LAN / ADMIN)
- [x] Déploiement OPNsense
- [x] Configuration accès ADMIN (GUI + règles firewall)
- [x] Création template Debian 12 (cloud-init + virt-sysprep)

---

### ⚙️ Automatisation

- [x] Provisioning des VMs via cloud-init
- [x] Mise en place d’un bastion Ansible (adm-ansible-01)
- [x] Accès SSH sécurisé par clé
- [x] Inventory Ansible structuré (groupes : admin, dmz, docker_hosts)
- [x] Rôles Ansible :
  - [x] docker (installation idempotente)
  - [x] demo_app (déploiement app via docker-compose)
  - [x] traefik (reverse proxy)

---

### 🌐 Reverse Proxy

- [x] Déploiement Traefik en DMZ
- [x] Routage HTTP vers application LAN
- [x] Validation via header `Host`
- [x] HTTPS fonctionnel avec certificat self-signed
- [x] Validation via `X-Forwarded-Proto`

---

### 🔐 Sécurité

- [x] Isolation réseau (DMZ / LAN / ADMIN)
- [x] Accès aux VMs uniquement via bastion
- [x] Aucun accès direct host → DMZ
- [x] Gestion des secrets avec Ansible Vault :
  - [x] Certificat TLS chiffré
  - [x] Clé privée chiffrée
  - [x] Injection dynamique dans les conteneurs
  - [x] Aucun secret en clair dans Git

---

### ♻️ Qualité / DevOps

- [x] Playbooks Ansible idempotents (`changed=0`)
- [x] Structure Git propre (roles, inventory, playbooks)
- [x] Séparation code / secrets
- [x] Déploiement reproductible

---

## 🚧 Prochaines étapes

### 🔐 Sécurité avancée

- [X] ] Redirection HTTP → HTTPS (Traefik)
- [x] Handler Ansible pour redémarrage Traefik sur changement de configuration
- [ ] Durcissement SSH (fail2ban / config)

### 🔐 Sécurité réseau (OPNsense)

- [x] Mise en place d’un firewall stateful (OPNsense)
- [x] Segmentation réseau : DMZ / LAN / ADMIN
- [x] Règles restrictives DMZ :
  - [x] Autorisation DMZ → application (port 8081 uniquement)
  - [x] Blocage DMZ → LAN
  - [x] Blocage DMZ → ADMIN
  - [x] Autorisation DMZ → Internet

#### ✅ Tests de validation

- ✔️ Accès DMZ → app (OK)
- ❌ Accès DMZ → ADMIN (bloqué)
- ❌ ICMP DMZ → ADMIN (bloqué)

---

### 📊 Observabilité

- [X] Déploiement Prometheus
- [X] Déploiement Grafana
- [ ] Déploiement Loki (logs)
- [ ] Centralisation logs applicatifs

---

### 🚀 DevOps avancé

- [ ] CI/CD avec GitHub Actions
- [ ] Runner self-hosted (VM admin)
- [ ] Déploiement automatique via pipeline

---

### ☁️ Évolutions

- [ ] Ajout registry Docker privé
- [ ] Migration vers Kubernetes (K3s)
- [ ] Sauvegardes automatisées

---

## 🧠 Philosophie

- Infrastructure reproductible
- Automatisation maximale
- Sécurité by design
- Architecture lisible et documentée
