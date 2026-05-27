# Semaine 2 — Linux Jour 1

## Acronymes nouveaux

| Acronyme | Signification complète | Rôle |
|---|---|---|
| PID | Process ID | Numéro unique d'un processus |
| SIGTERM | Signal Terminate | Demande poliment d'arrêter un processus |
| SIGKILL | Signal Kill | Force l'arrêt immédiat d'un processus |

## Navigation et fichiers

| Commande | Signification | Rôle |
|---|---|---|
| pwd | Print Working Directory | Afficher le dossier actuel |
| ls | List | Lister le contenu d'un dossier |
| ls -la | List Long All | Lister avec détails et fichiers cachés |
| cd | Change Directory | Changer de dossier |
| cd .. | | Remonter d'un niveau |
| cd ~ | | Aller au home directory |
| mkdir | Make Directory | Créer un dossier |
| touch | | Créer un fichier vide |
| cat | Concatenate | Afficher le contenu d'un fichier |
| cp | Copy | Copier un fichier |
| mv | Move | Déplacer ou renommer un fichier |
| rm | Remove | Supprimer un fichier — définitif |
| echo | | Afficher du texte |
| man | Manual | Afficher le manuel d'une commande |

## Redirections

| Symbole | Rôle |
|---|---|
| > | Redirige la sortie vers un fichier — écrase |
| >> | Redirige et ajoute à la fin du fichier |
| pipe | Envoie la sortie d'une commande vers une autre |

## Commandes système

| Commande | Rôle |
|---|---|
| whoami | Afficher l'utilisateur courant |
| hostname | Afficher le nom de la machine |
| date | Afficher la date et heure |
| ifconfig | Afficher la configuration réseau |
| ps aux | Afficher tous les processus en cours |
| kill PID | Arrêter un processus — SIGTERM |
| kill -9 PID | Forcer l'arrêt d'un processus — SIGKILL |
| grep | Filtrer les lignes qui contiennent un mot |

## Différence rm vs kill

- rm = supprime un fichier sur le disque définitivement
- kill = arrête un processus en mémoire, le fichier reste sur le disque

## Permissions Linux

Format : `drwxr-xr-x`

| Caractère | Signification |
|---|---|
| d | Directory — dossier |
| - | Fichier normal |
| l | Link — lien symbolique |
| r | Read — lire = 4 |
| w | Write — écrire = 2 |
| x | Execute — exécuter = 1 |
| - | Permission absente = 0 |

Structure : `[type][propriétaire][groupe][autres]`

## chmod — valeurs importantes

| chmod | Permissions | Usage |
|---|---|---|
| 777 | rwxrwxrwx | Dangereux — tout le monde peut tout |
| 755 | rwxr-xr-x | Standard dossiers et scripts |
| 644 | rw-r--r-- | Standard fichiers |
| 600 | rw------- | Fichier privé — clés SSH, configs |
| 400 | r-------- | Lecture seule stricte |

## Fichiers importants vus

- /etc/hosts — DNS local, lu avant le vrai DNS
- ~/.ssh — clés SSH — très sensible
- ~/.bash_history — historique des commandes
- ~/.zsh_history — historique zsh

## Ce que je retiens en cyber

- whoami = première commande sur un serveur compromis
- ps aux = voir les services qui tournent et sous quel utilisateur
- chmod 777 sur un serveur = vulnérabilité
- Fichiers cachés (.) = souvent des configs sensibles avec mots de passe
- /etc/hosts modifié = redirection locale de domaines = attaque possible