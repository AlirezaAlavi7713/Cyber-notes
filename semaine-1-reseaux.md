# Semaine 1 — Réseaux & fondations

## Acronymes

| Acronyme | Signification complète | Rôle |
|---|---|---|
| OSI | Open Systems Interconnection | Modèle en 7 couches |
| ISO | International Organization for Standardization | Organisation qui crée les standards |
| TCP | Transmission Control Protocol | Transport fiable |
| UDP | User Datagram Protocol | Transport rapide sans garantie |
| IP | Internet Protocol | Adressage et routage réseau |
| HTTP | HyperText Transfer Protocol | Pages web |
| HTTPS | HyperText Transfer Protocol Secure | Pages web chiffrées |
| TLS | Transport Layer Security | Chiffrement moderne |
| SSL | Secure Sockets Layer | Ancien nom de TLS |
| DNS | Domain Name System | Traduit un nom de domaine en IP |
| FTP | File Transfer Protocol | Transfert de fichiers |
| SMTP | Simple Mail Transfer Protocol | Envoi d'emails |
| ARP | Address Resolution Protocol | Traduit une IP en adresse MAC |
| ICMP | Internet Control Message Protocol | Messages de contrôle réseau |
| MAC | Media Access Control | Adresse physique de la carte réseau |
| MITM | Man In The Middle | Attaque par interception |
| DoS | Denial of Service | Déni de service |
| SQL | Structured Query Language | Langage des bases de données |
| SYN | Synchronize | Flag TCP — demande de connexion |
| ACK | Acknowledgment | Flag TCP — confirmation de réception |
| FIN | Finish | Flag TCP — fermeture de connexion |
| RST | Reset | Flag TCP — réinitialisation brutale |
| PSH | Push | Flag TCP — envoie les données immédiatement |
| NAT | Network Address Translation | Traduit IP privée en IP publique |
| FAI | Fournisseur d'Accès à Internet | Orange, SFR, Free... |
| CIDR | Classless Inter-Domain Routing | Notation courte du masque réseau |
| VoIP | Voice over Internet Protocol | Téléphonie via internet |
| CDN | Content Delivery Network | Réseau de distribution de contenu |
| RDP | Remote Desktop Protocol | Bureau à distance Windows |
| SMB | Server Message Block | Partage de fichiers Windows |
| SSH | Secure Shell | Connexion distante sécurisée |
| QUIC | Quick UDP Internet Connections | Protocole rapide de Google |
| TLD | Top Level Domain | Extension du domaine (.com, .fr) |
| IANA | Internet Assigned Numbers Authority | Gère les standards internet |

## Le modèle OSI — 7 couches

Moyen mnémotechnique : **Please Do Not Throw Sausage Pizza Away**

| Couche | Nom | Protocoles | Rôle |
|---|---|---|---|
| 7 | Application | HTTP, DNS, FTP, SMTP | Interface utilisateur |
| 6 | Présentation | TLS, SSL | Chiffrement, encodage |
| 5 | Session | NetBIOS, RPC | Gestion des sessions |
| 4 | Transport | TCP, UDP | Ports, fiabilité, segmentation |
| 3 | Réseau | IP, ICMP | Adressage, routage |
| 2 | Liaison de données | Ethernet, ARP | Adresses MAC, trames |
| 1 | Physique | Câble RJ45, Wi-Fi, Fibre | Signaux physiques |

## TCP vs UDP

| | TCP | UDP |
|---|---|---|
| Connexion | Handshake SYN / SYN-ACK / ACK | Aucune |
| Fiabilité | Garantie | Aucune garantie |
| Ordre des paquets | Garanti | Non garanti |
| Vitesse | Plus lent | Plus rapide |
| Usage | HTTP, SSH, FTP | DNS, jeux, streaming, VoIP |

## Le handshake TCP

1. Client → Serveur : **SYN** — "je veux me connecter"
2. Serveur → Client : **SYN-ACK** — "ok je t'entends"
3. Client → Serveur : **ACK** — "parfait, on commence"

## Adressage IP

- **IPv4** = 4 nombres de 0 à 255 séparés par des points — ex: 192.168.1.10
- **IPv6** = 8 groupes hexadécimaux — ex: 2001:0db8:85a3::8a2e:0370:7334
- **IP privée** = adresse sur le réseau local — ex: 192.168.X.X
- **IP publique** = adresse visible sur internet — attribuée par le FAI
- **Loopback** = 127.0.0.1 = ton propre ordinateur = localhost

## CIDR — notation du masque réseau

| Notation | Masque | Nombre de machines |
|---|---|---|
| /24 | 255.255.255.0 | 254 machines |
| /16 | 255.255.0.0 | 65534 machines |
| /8 | 255.0.0.0 | 16 millions de machines |
| /32 | 255.255.255.255 | 1 seule machine |

## DNS — Domain Name System

**Rôle** : traduire un nom de domaine en adresse IP

**Types d'enregistrements :**
| Type | Rôle |
|---|---|
| A | Nom → IPv4 |
| AAAA | Nom → IPv6 |
| CNAME | Alias vers un autre nom |
| MX | Serveur mail du domaine |
| NS | Serveurs DNS autoritaires |
| PTR | IP → Nom (DNS inversé) |
| TXT | Texte libre, vérification, anti-spam |

**Port DNS** : 53 UDP (requêtes normales) / 53 TCP (transferts de zone)

## Ports importants

| Port | Protocole | Usage | Chiffré |
|---|---|---|---|
| 21 | FTP | Transfert fichiers | Non |
| 22 | SSH | Connexion distante sécurisée | Oui |
| 23 | Telnet | Connexion distante | Non |
| 25 | SMTP | Envoi emails | Non |
| 53 | DNS | Résolution noms | Non |
| 80 | HTTP | Web | Non |
| 110 | POP3 | Réception emails | Non |
| 143 | IMAP | Réception emails | Non |
| 443 | HTTPS | Web sécurisé | Oui |
| 445 | SMB | Partage fichiers Windows | Non |
| 3306 | MySQL | Base de données | Non |
| 3389 | RDP | Bureau à distance Windows | Partiel |

## Wireshark — filtres essentiels

| Filtre | Résultat |
|---|---|
| `dns` | Uniquement trafic DNS |
| `tcp` | Uniquement trafic TCP |
| `udp` | Uniquement trafic UDP |
| `http` | Uniquement trafic HTTP |
| `tcp.flags.syn == 1` | Uniquement paquets SYN |
| `ip.src == X.X.X.X` | Depuis une IP précise |
| `ip.dst == X.X.X.X` | Vers une IP précise |
| `tcp.port == 443` | Sur un port précis |

## Ce que j'ai observé dans Wireshark

- Requêtes DNS en temps réel — mon Mac contacte des dizaines de serveurs en arrière plan
- Handshake TCP — SYN puis SYN-ACK visible en direct
- Trafic QUIC — protocole UDP de Google utilisé par Chrome
- Trafic TLS chiffré — Application Data illisible car chiffré
- Mon IP locale : 192.168.1.110
- ARP Probe au démarrage — mon Mac vérifie que son IP n'est pas déjà utilisée