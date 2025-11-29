# Log Archive Tool

Outil en bash pour archiver automatiquement des logs système en les compressant et en les organisant par date.

## Description

Ce script permet d'archiver des fichiers logs en :
- Compressant les logs au format `.tar.gz`
- Créant des archives nommées avec timestamp : `logs_archive_YYYYMMDD_HHMMSS.tar.gz`
- Stockant les archives dans un dossier dédié
- Permettant une exécution automatique via cron

**Cas d'usage :** Automatisation de la sauvegarde des logs pour les administrateurs système et DevOps.

## Prérequis

- Système Linux (Ubuntu, Debian, etc.)
- Bash 4.0+
- Permissions sudo pour l'installation
- Commandes système : `tar`, `date`, `mkdir`

## 📥 Installation

### 1. Cloner le repository
```bash
git clone https://github.com/AMM48/devops-lab.git
cd devops-lab/Devops-Project2_Log_Archive_Tool
```

### 2. Copier le script dans le système
```bash
sudo cp log-archive /usr/local/bin/
sudo chmod +x /usr/local/bin/log-archive
```


## Utilisation

### Syntaxe
```bash
log-archive <chemin_absolu_vers_dossier_logs>
```

### Exemples

**Archiver les logs système :**
```bash
log-archive /var/log
```

**Archiver un dossier personnalisé :**
```bash
log-archive /home/user/app/logs
```

**Résultat :**
- Création du dossier `archives_logs/` au même niveau que le dossier source
- Archive créée : `logs_archive_20241129_153045.tar.gz`

### Structure créée
```
/var/
├── log/                    # Dossier source
│   ├── syslog
│   ├── auth.log
│   └── ...
└── archives_logs/          # Nouveau dossier créé
    └── logs_archive_20241129_153045.tar.gz
```

## Configuration du Cron (Automatisation)

### Éditer le crontab
```bash
crontab -e
```

### Exemples de planification

**Archiver /var/log toutes les heures :**
```cron
0 * * * * /usr/local/bin/log-archive /var/log
```

**Tous les jours à 2h du matin :**
```cron
0 2 * * * /usr/local/bin/log-archive /var/log
```

**Tous les lundis à minuit :**
```cron
0 0 * * 1 /usr/local/bin/log-archive /var/log
```

**Toutes les 6 heures :**
```cron
0 */6 * * * /usr/local/bin/log-archive /var/log
```

### ⚠️ Important pour cron

**Toujours utiliser des chemins ABSOLUS** dans le crontab :
- ✅ `/usr/local/bin/log-archive /var/log`
- ❌ `log-archive ./logs` (ne fonctionnera pas)

### Vérifier que le cron fonctionne
```bash
# Voir les crons actifs
crontab -l
```

## Ce que j'ai appris sur ce projet

### Concepts Bash

- **Arguments de script** : Utilisation de `$1` pour récupérer l'argument utilisateur
- **Validation d'entrée** : Vérification avec `$#` (nombre d'arguments) et `-d` (test de dossier)
- **Manipulation de chemins** : `dirname` pour obtenir le dossier parent

### Commandes Linux essentielles

- `tar -czf` : Compression d'archives (c=create, z=gzip, f=file)
- `dirname` : Extraction du chemin parent
- `crontab -e` : Planification de tâches automatiques

### Système de fichiers Linux

- **Différence `/usr/bin` vs `/usr/local/bin`** :
  - `/usr/bin` → Géré par le système (packages)
  - `/usr/local/bin` → Programmes installés manuellement

### Cron

- **Syntaxe crontab** : `minute heure jour mois jour_semaine commande`
- **Contexte d'exécution** : Cron ne s'exécute pas depuis le répertoire utilisateur


## 📝 Licence

MIT License

## 👤 Auteur

**Adriusops**
- GitHub: [@Adriusops](https://github.com/Adriusops)

## 🔗 Ressources

Ce projet fait partie des [roadmap.sh DevOps Projects](https://roadmap.sh/projects/log-archive-tool).

---

⭐ Si ce projet vous aide, n'hésitez pas à lui donner une étoile sur GitHub !
