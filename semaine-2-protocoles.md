# Semaine 2 — Protocoles & sécurité réseau

## Acronymes nouveaux

| Acronyme | Signification complète | Rôle |
|---|---|---|
| HTTP | HyperText Transfer Protocol | Protocole d'échange de pages web |
| HTTPS | HyperText Transfer Protocol Secure | HTTP chiffré avec TLS |
| TLS | Transport Layer Security | Chiffrement des communications |
| CA | Certificate Authority | Autorité de Certification |
| HSTS | HTTP Strict Transport Security | Force le navigateur à utiliser HTTPS |
| CSP | Content Security Policy | Contrôle les ressources chargées |
| WAF | Web Application Firewall | Pare-feu applicatif couche 7 |
| ARP | Address Resolution Protocol | Traduit IP en adresse MAC |
| DHCP | Dynamic Host Configuration Protocol | Donne automatiquement une IP |
| ICMP | Internet Control Message Protocol | Messages de contrôle réseau |
| TTL | Time To Live | Durée de vie d'un paquet |
| MITM | Man In The Middle | Attaque par interception |
| VLAN | Virtual Local Area Network | Réseau local virtuel |
| NAT | Network Address Translation | Traduit IP privée en IP publique |
| PAT | Port Address Translation | NAT avec les ports |
| VPN | Virtual Private Network | Réseau Privé Virtuel |
| LAN | Local Area Network | Réseau local |
| DoS | Denial of Service | Déni de service |

## HTTP — HyperText Transfer Protocol

### Les méthodes HTTP

| Méthode | Rôle |
|---|---|
| GET | Récupérer une ressource |
| POST | Envoyer des données |
| PUT | Remplacer une ressource |
| PATCH | Modifier partiellement une ressource |
| DELETE | Supprimer une ressource |
| HEAD | Comme GET mais sans le body |
| OPTIONS | Quelles méthodes sont autorisées |

### Les codes de statut HTTP

| Code | Signification |
|---|---|
| 200 | OK — ça marche |
| 201 | Created — ressource créée |
| 301 | Moved Permanently — redirigé définitivement |
| 302 | Found — redirigé temporairement |
| 400 | Bad Request — requête mal formée |
| 401 | Unauthorized — pas connecté |
| 403 | Forbidden — connecté mais pas le droit |
| 404 | Not Found — n'existe pas |
| 429 | Too Many Requests — trop de requêtes |
| 500 | Internal Server Error — bug serveur |
| 503 | Service Unavailable — serveur indisponible |

### HTTP vs HTTPS

| | HTTP | HTTPS |
|---|---|---|
| Chiffrement | Aucun — tout en clair | TLS — tout chiffré |
| Sécurité | Dangereux sur réseau public | Sécurisé |
| Port | 80 | 443 |
| Utilisation | Dev local uniquement | Production obligatoire |

### Ce que j'ai vu dans Wireshark en HTTP

- La requête GET complète lisible — méthode, host, headers
- User-Agent révèle l'OS et le navigateur — fuite d'information
- La version du serveur visible — Server: Apache/2.4.66
- Le code HTML de la page entièrement lisible
- En HTTPS — tout illisible sauf le certificat TLS

## ARP — Address Resolution Protocol

- Traduit une adresse IP en adresse MAC sur le réseau local
- Envoie un broadcast — "qui a cette IP ?"
- La réponse est stockée dans la table ARP
- Voir sa table ARP : `arp -a`

**Attaque : ARP Poisoning**
- L'attaquant envoie de fausses réponses ARP
- La victime envoie son trafic vers l'attaquant
- Résultat : attaque MITM — l'attaquant voit tout le trafic

## DHCP — Dynamic Host Configuration Protocol

- Donne automatiquement une IP aux machines qui se connectent
- C'est généralement le routeur qui joue ce rôle

**Processus DORA :**
1. **D — Discover** — "Y'a un serveur DHCP ?"
2. **O — Offer** — "Oui, je t'offre l'IP 192.168.1.50"
3. **R — Request** — "Ok je la prends"
4. **A — Acknowledge** — "C'est validé"

**Attaque : DHCP Starvation**
- Épuiser toutes les adresses IP disponibles
- Les nouveaux appareils ne peuvent plus se connecter

## ICMP — Internet Control Message Protocol

- Protocole de messages de contrôle réseau
- Utilisé par `ping` et `traceroute`
- TTL (Time To Live) — compteur qui diminue à chaque routeur

**Messages importants :**
- Echo Request / Echo Reply — le ping
- Destination Unreachable — machine injoignable
- Time Exceeded — TTL arrivé à 0

**Attaques :**
- Ping flood — DoS couche 3
- ICMP Tunneling — cacher des données dans des paquets ICMP

## Firewall, Routeur, Switch, Proxy

| Équipement | Rôle | Couche |
|---|---|---|
| Switch | Connecte machines sur réseau local, lit adresses MAC | 2 |
| Routeur | Connecte réseaux entre eux, lit adresses IP, fait NAT | 3 |
| Firewall | Filtre le trafic selon des règles IP et ports | 3-4 |
| Proxy | Intermédiaire entre client et internet, cache l'IP | 7 |

**Types de firewall :**
- Stateless — regarde chaque paquet indépendamment
- Stateful — suit l'état des connexions TCP
- WAF (Web Application Firewall) — couche 7, détecte SQLi, XSS

**Types de proxy :**
- Forward Proxy — proxy sortant, filtre accès internet
- Reverse Proxy — proxy entrant, protège les serveurs
- Proxy transparent — l'utilisateur ne sait pas qu'il passe par un proxy
- Burp Suite — proxy intercepteur utilisé en pentest web

## VLAN, NAT, PAT

**VLAN (Virtual Local Area Network)**
- Divise un réseau physique en réseaux logiques isolés
- Sécurité en entreprise — comptabilité isolée des développeurs
- Attaque : VLAN Hopping — sauter d'un VLAN à un autre

**NAT (Network Address Translation)**
- Traduit les IP privées en IP publique
- Permet à plusieurs appareils de partager une seule IP publique
- Fait par le routeur

**PAT (Port Address Translation)**
- Extension du NAT
- Utilise les ports pour distinguer les appareils derrière la même IP publique