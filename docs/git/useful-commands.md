---
label: Commandes Git Utiles
icon: ":computer:"
tags:
  - git
  - commands
  - productivity
visibility: private
draft: true
---

# Commandes Git Utiles

## Gestion des Commits

### Modification du Dernier Commit

```bash
# Modifier le message du dernier commit
git commit --amend -m "nouveau message"

# Ajouter des fichiers au dernier commit
git add file.txt
git commit --amend --no-edit
```

### Squash de Commits

```bash
# Squash des 3 derniers commits
git rebase -i HEAD~3

# Dans l'éditeur, remplacer 'pick' par 'squash' pour les commits à fusionner
```

## Gestion des Branches

### Nettoyage des Branches

```bash
# Supprimer les branches mergées
git branch --merged | grep -v "\*\|main\|master" | xargs -n 1 git branch -d

# Supprimer les branches distantes qui n'existent plus
git remote prune origin
```

### Renommage de Branches

```bash
# Renommer la branche courante
git branch -m nouveau-nom

# Renommer une branche spécifique
git branch -m ancien-nom nouveau-nom
```

## Recherche et Historique

### Recherche dans l'Historique

```bash
# Rechercher un terme dans l'historique
git log --grep="terme"

# Rechercher dans les différences
git log -S "terme" --oneline

# Voir les modifications d'un fichier
git log -p -- chemin/vers/fichier
```

### Blame et Annotations

```bash
# Voir qui a modifié chaque ligne
git blame fichier.txt

# Voir les modifications ligne par ligne
git blame -L 10,20 fichier.txt
```

## Gestion des Fichiers

### Récupération de Fichiers

```bash
# Récupérer un fichier depuis un commit
git checkout commit-hash -- fichier.txt

# Récupérer un fichier depuis une branche
git checkout nom-branche -- fichier.txt
```

### Suppression de Fichiers

```bash
# Supprimer un fichier du tracking Git
git rm --cached fichier.txt

# Supprimer un dossier du tracking
git rm -r --cached dossier/
```

## Stash et Travail Temporaire

### Gestion du Stash

```bash
# Sauvegarder les modifications en cours
git stash save "message descriptif"

# Lister les stash
git stash list

# Appliquer un stash spécifique
git stash apply stash@{0}

# Appliquer et supprimer un stash
git stash pop
```

## Résolution de Conflits

### Outils de Merge

```bash
# Utiliser un outil de merge graphique
git mergetool

# Annuler un merge en cours
git merge --abort

# Continuer après résolution de conflit
git add fichier-résolu.txt
git commit
```

## Aliases Utiles

### Configuration des Aliases

```bash
# Aliases pour les commandes courantes
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status

# Alias pour un log plus lisible
git config --global alias.lg "log --oneline --graph --decorate --all"

# Alias pour voir les modifications
git config --global alias.unstage "reset HEAD --"
```

## Bonnes Pratiques

### 1. Commits Atomiques

```bash
# Ajouter seulement les modifications liées
git add -p  # Permet de sélectionner les hunks
```

### 2. Vérifications Avant Commit

```bash
# Voir les modifications avant commit
git diff --cached

# Voir le statut complet
git status --porcelain
```

### 3. Configuration Globale

```bash
# Configuration de base
git config --global user.name "Votre Nom"
git config --global user.email "email@example.com"

# Configuration de l'éditeur
git config --global core.editor "code --wait"

# Configuration des fins de ligne
git config --global core.autocrlf input
```

## Conclusion

Ces commandes Git permettent une gestion plus efficace des projets et une meilleure productivité au quotidien. 