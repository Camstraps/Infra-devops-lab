## Reverse Proxy Traefik

La VM `rp-traefik-01`, située en DMZ, joue le rôle de reverse proxy HTTP.

- Réseau : DMZ
- IP : `10.10.10.10`
- Service exposé : Traefik
- Ports :
  - `80/tcp` : point d’entrée HTTP
  - `8080/tcp` : dashboard Traefik

Traefik est déployé via Ansible dans un conteneur Docker.

### Flux applicatif validé

Un service de test `whoami` est déployé sur `app-docker-01` dans le LAN.

- VM applicative : `app-docker-01`
- IP : `10.10.20.10`
- Port exposé : `8081/tcp`
- Conteneur : `traefik/whoami`

Le flux validé est le suivant :

```text
Client / Bastion ADMIN
    ↓
rp-traefik-01:80
    ↓
Traefik reverse proxy
    ↓
app-docker-01:8081
    ↓
demo-whoami

Test réalisé :
curl -H "Host: demo.lab.local" http://10.10.10.10

Résultat attendu :

Réponse du conteneur whoami avec les en-têtes X-Forwarded-*
