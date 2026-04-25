# Infra DevOps Lab

Projet personnel réalisé dans le cadre de ma montée en compétences vers un rôle d’Ingénieur Systèmes / DevOps.

L’objectif est de concevoir et déployer une infrastructure complète, virtualisée localement, en reproduisant les bonnes pratiques d’un environnement d’entreprise : segmentation réseau, sécurité, automatisation et observabilité.

---

## Contexte technique

- Host : Arch Linux
- Virtualisation : KVM / libvirt (virt-manager)
- OS invités : Debian 12
- Approche : infrastructure reproductible + automatisation progressive

---

## Objectifs du projet

Ce projet me permet de travailler concrètement sur :

- la conception d’une architecture réseau segmentée (DMZ / LAN / ADMIN)
- le déploiement d’un firewall (OPNsense)
- l’exposition sécurisée de services via un reverse proxy (Traefik)
- la conteneurisation d’applications avec Docker
- la mise en place de supervision (Prometheus / Grafana)
- la centralisation des logs (Loki)
- l’automatisation avec Ansible
- une première approche CI/CD avec GitHub Actions

---

## Architecture cible

Trois zones réseau isolées :

| Zone | Réseau | Usage |
|------|--------|--------|
| DMZ | 10.10.10.0/24 | Services exposés (reverse proxy) |
| LAN | 10.10.20.0/24 | Applications internes + monitoring |
| ADMIN | 10.10.30.0/24 | Accès admin + automatisation |

---

## Machines prévues

| Nom | Rôle |
|-----|------|
| fw-opnsense-01 | Firewall, routage, NAT |
| rp-traefik-01 | Reverse proxy |
| app-docker-01 | Applications Docker |
| mon-grafana-01 | Monitoring |
| log-loki-01 | Logs |
| adm-ansible-01 | Bastion + Ansible + CI |

---

## Avancement

- Mise en place de l’environnement de virtualisation (KVM/libvirt)
- Configuration réseau fonctionnelle (NAT + DHCP + DNS)
- Résolution d’un problème DNS lié à libvirt / systemd-resolved
- Création d’une VM template Debian 12 prête au clonage
- Initialisation du dépôt et structuration du projet

---

## Prochaines étapes

- Création des réseaux internes (DMZ / LAN / ADMIN)
- Déploiement d’OPNsense
- Clonage et configuration des VMs
- Mise en place d’Ansible
- Déploiement des services (Docker, monitoring, logs)

---

## Objectif professionnel

Ce projet a pour but de constituer un support concret pour :

- démontrer mes compétences en systèmes et réseaux
- illustrer ma capacité à concevoir une architecture cohérente
- montrer une démarche d’automatisation et de documentation
- servir de base de discussion en entretien technique
