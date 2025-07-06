# Tech Blog - Workflow de Publication

## 📋 Vue d'ensemble

Ce blog tech utilise [Retype](https://retype.com/) avec un système de gestion de contenu privé/public intégré. Tous les articles sont **privés par défaut** et doivent être activés manuellement pour publication.

## 🚀 Démarrage Rapide

### Installation

```bash
# Installer Retype
npm install retypeapp --global

# Démarrer en mode développement
retype start

# Ou avec port personnalisé
retype start --port 5000
```

### Première utilisation

```bash
# Construire le site
retype build

# Déployer
retype deploy
```

## 📝 Système de Publication

### États des Articles

- **🔒 Privé** : `draft: true` + `visibility: private`
- **🌐 Public** : `draft: false` + `visibility: public`

### Publier un Article

1. **Localiser l'article** dans `docs/`
2. **Éditer le frontmatter** :
   ```yaml
   ---
   label: Titre de l'article
   icon: ":rocket:"
   tags: [devops, kubernetes]
   visibility: public  # Changer de private à public
   draft: false        # Supprimer ou passer à false
   ---
   ```
3. **Rebuild et deploy** :
   ```bash
   retype build
   retype deploy
   ```

### Workflow de Révision

#### Étape 1 : Révision du Contenu
```bash
# Activer un article pour révision locale
# Éditer le frontmatter : draft: false (garder visibility: private)
retype start
```

#### Étape 2 : Publication
```bash
# Activer pour publication
# Éditer le frontmatter : visibility: public
retype build
retype deploy
```

## 📂 Structure des Articles

### Sections Disponibles

- **🎯 Fondamentaux** (`/learn-to-cloud/`) : Guides pour débuter
- **☸️ Kubernetes** (`/kubernetes/`) : Orchestration et containers
- **🔧 Git** (`/git/`) : Gestion de versions

### Articles Actuels

#### Learn to Cloud (Tous privés)
- `phase0-starting-from-zero.md` - Reprendre le Contrôle de Son Parcours Tech
- `cloud-fundamentals.md` - Cloud Maîtrisé - Reprendre le Contrôle
- `devops-fundamentals.md` - DevOps Pragmatique - La Collaboration Qui Marche
- `career-guide.md` - Carrière Cloud Native - Construire l'Avenir
- `essential-tools.md` - Boîte à Outils du Cloud Engineer Moderne

#### Kubernetes (Tous privés)
- `ingress-optimization.md` - Optimisation des Ingress Controllers
- `orphan-resources.md` - Nettoyage des Ressources Orphelines

#### Git (Tous privés)
- `conventional-commits.md` - Conventional Commits
- `useful-commands.md` - Commandes Git Utiles

## 🛠️ Commandes Retype

### Développement

```bash
# Démarrer le serveur de développement
retype start

# Avec configuration personnalisée
retype start --config retype.dev.yml

# Avec port spécifique
retype start --port 5000
```

### Build et Déploiement

```bash
# Build pour production
retype build

# Build avec drafts (développement)
retype build --include-drafts

# Nettoyer le cache
retype clean

# Déployer
retype deploy
```

### Gestion des Drafts

```bash
# Voir tous les fichiers (y compris drafts)
retype build --include-drafts

# Build production (exclut les drafts)
retype build --production
```

## 🔧 Configuration Avancée

### Personnalisation Visuelle

Le fichier `retype.yml` contient les optimisations :

- **Recherche avancée** : Activée avec indexation automatique
- **Navigation personnalisée** : Avec logos et liens
- **Thèmes et couleurs** : Cohérence visuelle
- **Composants Retype** : Alertes, onglets, colonnes

### Fonctionnalités Utilisées

- **Recherche** : Indexation complète du contenu
- **Navigation** : Structure logique avec icônes
- **Métadonnées** : SEO optimisé
- **Composants** : Enrichissement du contenu

## 📊 Persona Éditorial

Le persona **Maxime "Cloud Native" Dubois** guide l'écriture :

- **Expertise** : 12 ans d'expérience SRE
- **Philosophie** : Indépendance technologique européenne
- **Style** : REX authentiques avec métriques réelles
- **Ton** : Professionnel mais accessible

## 🚦 Processus de Publication

### Étape 1 : Rédaction
1. Créer l'article avec `draft: true`
2. Suivre le persona éditorial
3. Inclure des exemples concrets et métriques

### Étape 2 : Révision
1. Passer `draft: false` (garder `visibility: private`)
2. Relire avec `retype start`
3. Vérifier la cohérence avec le persona

### Étape 3 : Publication
1. Passer `visibility: public`
2. `retype build && retype deploy`
3. Vérifier la publication

## 🔒 Sécurité et Confidentialité

### Fichiers Exclus

- `draft-*` : Drafts en cours
- `private-*` : Contenu privé
- `WIP-*` : Work in progress
- `*.secret` : Fichiers sensibles

### Bonnes Pratiques

- Jamais de références externes non autorisées
- Pas de noms de personnes réelles
- Anonymisation des métriques sensibles
- Validation avant publication

## 🎯 Objectifs du Blog

1. **Promouvoir** l'indépendance technologique européenne
2. **Partager** des retours d'expérience authentiques
3. **Former** aux alternatives open-source
4. **Construire** une communauté tech française

## 📈 Métriques de Succès

- **Engagement** : Temps de lecture, partages
- **Technique** : Adoption des outils recommandés
- **Communauté** : Discussions et feedback
- **Impact** : Influence sur les choix technologiques

---

*Dernière mise à jour : Janvier 2025* 