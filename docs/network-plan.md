# Network Plan

## Objectif

Mettre en place une segmentation réseau inspirée d’une architecture entreprise avec trois zones isolées :

- DMZ : exposition des services
- LAN : services internes
- ADMIN : administration et automatisation

---

## Réseaux

| Zone | Subnet | Gateway | Description |
|------|--------|--------|-------------|
| DMZ | 10.10.10.0/24 | 10.10.10.1 | Reverse proxy (Traefik) |
| LAN | 10.10.20.0/24 | 10.10.20.1 | Applications, monitoring, logs |
| ADMIN | 10.10.30.0/24 | 10.10.30.1 | Bastion, Ansible |

---

## Plan IP

| VM | Interface | IP | Zone |
|----|----------|----|------|
| fw-opnsense-01 | WAN | DHCP (libvirt NAT) | Internet |
| fw-opnsense-01 | DMZ | 10.10.10.1 | DMZ |
| fw-opnsense-01 | LAN | 10.10.20.1 | LAN |
| fw-opnsense-01 | ADMIN | 10.10.30.1 | ADMIN |
| rp-traefik-01 | eth0 | 10.10.10.10 | DMZ |
| app-docker-01 | eth0 | 10.10.20.10 | LAN |
| mon-grafana-01 | eth0 | 10.10.20.20 | LAN |
| log-loki-01 | eth0 | 10.10.20.30 | LAN |
| adm-ansible-01 | eth0 | 10.10.30.10 | ADMIN |

---

## Règles de base (à implémenter)

- ADMIN → accès complet à toutes les zones
- LAN → accès sortant vers Internet
- DMZ → accès limité (reverse proxy uniquement)
- Aucun accès direct Internet → LAN/ADMIN
- Tout passe par OPNsense

---

## Notes

- Le WAN d’OPNsense sera connecté au réseau NAT libvirt existant
- Les autres interfaces seront connectées à des réseaux internes isolés
- Les IP seront configurées en statique côté VMs (via cloud-init plus tard)
