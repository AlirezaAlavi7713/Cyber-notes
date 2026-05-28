# Semaine 2 — Linux Jour 2 — Bash scripting & réseau

## Acronymes nouveaux

| Acronyme | Signification complète | Rôle |
|---|---|---|
| sh | Shell | Extension des scripts bash |
| nc | Netcat | Outil réseau couteau suisse |
| cron | Command Run On | Planificateur de tâches Linux |
| crontab | Cron Table | Fichier des tâches planifiées |

## Bash scripting — bases

### Structure d'un script
```bash
#!/bin/bash
# Shebang — obligatoire en première ligne
# Indique quel programme exécute le script
```

### Variables
```bash
NOM="Alireza"    # Déclarer une variable
echo "$NOM"      # Utiliser une variable
echo "$(whoami)" # Command substitution — exécuter une commande
```

### Conditions
```bash
if [ $AGE -gt 18 ]; then
    echo "majeur"
else
    echo "mineur"
fi
```

### Opérateurs de comparaison
| Opérateur | Signification |
|---|---|
| -gt | Greater Than — supérieur à |
| -lt | Less Than — inférieur à |
| -eq | Equal — égal à |
| -ne | Not Equal — différent de |
| -ge | Greater or Equal — supérieur ou égal |
| -le | Less or Equal — inférieur ou égal |

### Boucles
```bash
for i in 1 2 3; do
    echo $i
done
```

### Redirections
| Symbole | Rôle |
|---|---|
| > | Redirige vers fichier — écrase |
| >> | Redirige vers fichier — ajoute |
| 2>/dev/null | Redirige les erreurs vers la poubelle |
| pipe | Chaîne les commandes |

## Commandes importantes

| Commande | Rôle |
|---|---|
| chmod +x script.sh | Rendre un script exécutable |
| ./script.sh | Exécuter un script |
| find . -type f -perm -o+w | Trouver fichiers modifiables par tous |
| nc -z -w1 IP PORT | Tester si un port est ouvert |
| netstat -an | Voir toutes les connexions réseau |
| netstat -an grep LISTEN | Voir uniquement les ports en écoute |
| crontab -l | Lister les tâches cron |
| crontab -e | Editer les tâches cron |
| crontab -r | Supprimer toutes les tâches cron |
| pkill nom | Tuer un processus par son nom |

## Syntaxe cron

--------------

Exemple : `* * * * *` = toutes les minutes

## Cron en cybersécurité

- Défensif — automatiser sauvegardes, scans, rotation logs
- Offensif — technique de persistance après compromission
- Investigation — toujours vérifier crontab sur un serveur compromis

## Éditeurs de texte terminal

| Éditeur | Quitter |
|---|---|
| nano | Ctrl+O pour sauvegarder, Ctrl+X pour quitter |
| vim | Echap puis :wq pour sauvegarder et quitter |

## Variables d'environnement

```bash
export EDITOR=nano  # Définir nano comme éditeur par défaut
```

## Ce que je retiens en cyber

- Un script bash = automatiser des commandes répétitives
- Script de scan de ports = voir quels services tournent
- netstat -an grep LISTEN = première commande sur un serveur compromis
- Cron = vecteur de persistance pour les attaquants
- Port 3306 ouvert sur ma machine = MySQL qui tourne
- Ports *.5000 et *.7000 = mes projets dev qui tournent en arrière plan