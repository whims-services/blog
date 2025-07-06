# Guide d'Optimisation Retype

## Fonctionnalités Avancées Implémentées

### 1. Gestion des Pages Privées/Draft

**Configuration dans `retype.yml` :**
```yaml
# Gestion des pages privées/draft
include:
  - "*.md"
  - "!**/draft-*"
  - "!**/private-*"
  - "!**/WIP-*"
```

**Utilisation dans les articles :**
```yaml
---
visibility: private
draft: true
---
```

### 2. Recherche Avancée

**Configuration :**
```yaml
search:
  enabled: true
  minChars: 2
```

**Avantages :**
- Recherche dans tous les contenus
- Indexation automatique
- Résultats pertinents

### 3. Navigation Personnalisée

**Configuration :**
```yaml
navigation:
  logo: ./static/logos/whims-bold.png
  links:
  - text: Accueil
    link: /
  - text: Fondamentaux
    link: /learn-to-cloud/
```

### 4. Personnalisation Visuelle

**Configuration :**
```yaml
colors:
  primary: "#2563eb"
  secondary: "#64748b"
```

### 5. Optimisations de Code

**Configuration :**
```yaml
codeSnippet:
  lineNumbers: true
  title: auto
```

## Fonctionnalités Retype Supplémentaires

### 1. Composants Avancés

**Alertes :**
```markdown
!!! warning "Attention"
    Contenu important à retenir
```

**Onglets :**
```markdown
=== "Linux"
    Instructions pour Linux

=== "macOS"
    Instructions pour macOS
```

**Colonnes :**
```markdown
!!! columns
    === "Colonne 1"
        Contenu de la première colonne
    
    === "Colonne 2"
        Contenu de la deuxième colonne
```

### 2. Méta-données Avancées

**Configuration par page :**
```yaml
---
title: "Titre personnalisé"
description: "Description SEO"
image: "/path/to/image.jpg"
authors: ["Maxime Dubois"]
date: 2024-01-15
tags: [devops, kubernetes]
---
```

### 3. Déploiement Automatisé

**GitHub Actions (si utilisé) :**
```yaml
name: Deploy to GitHub Pages
on:
  push:
    branches: [ main ]
jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - name: Setup Node.js
      uses: actions/setup-node@v2
      with:
        node-version: '16'
    - name: Install Retype
      run: npm install retypeapp --global
    - name: Build
      run: retype build
    - name: Deploy
      run: retype deploy
```

### 4. Intégrations Avancées

**Google Analytics :**
```yaml
integrations:
  googleAnalytics:
    id: "GA_MEASUREMENT_ID"
```

**Plausible Analytics (Alternative européenne) :**
```yaml
integrations:
  plausible:
    domain: "votredomaine.com"
```

## Workflow de Développement

### 1. Mode Développement

**Commandes :**
```bash
# Démarrer en mode développement
retype start

# Démarrer avec port personnalisé
retype start --port 5000

# Construire pour production
retype build

# Déployer
retype deploy
```

### 2. Gestion des Drafts

**Créer un draft :**
```yaml
---
visibility: private
draft: true
---
```

**Publier un draft :**
```yaml
---
# Supprimer la ligne draft: true
visibility: public
---
```

### 3. Workflow de Publication

1. **Développement :** Toutes les pages en `draft: true`
2. **Révision :** Supprimer `draft: true` pour une page
3. **Publication :** Rebuild et deploy

## Optimisations Performance

### 1. Optimisation des Images

**Configuration :**
```yaml
generator:
  directoryIndex:
    append: true
  
markdown:
  lineBreaks: soft
```

### 2. Mise en Cache

**Configuration serveur web :**
```nginx
location ~* \.(js|css|png|jpg|jpeg|gif|ico|svg)$ {
    expires 1y;
    add_header Cache-Control "public, immutable";
}
```

### 3. Compression

**Configuration :**
```yaml
server:
  compression: true
  minify: true
```

## Sécurité et Confidentialité

### 1. Exclusion de Fichiers Sensibles

**Configuration :**
```yaml
exclude:
  - "*.secret"
  - "*.env"
  - "node_modules"
  - ".git"
```

### 2. Désactivation de la Télémétrie

**Configuration :**
```yaml
telemetry: false
```

## Commandes Utiles

### 1. Développement

```bash
# Démarrer avec configuration personnalisée
retype start --config retype.dev.yml

# Construire en mode draft
retype build --include-drafts

# Nettoyer le cache
retype clean
```

### 2. Production

```bash
# Build optimisé
retype build --production

# Déployer vers GitHub Pages
retype deploy --provider github

# Déployer vers serveur personnalisé
retype deploy --provider ftp
```

## Dépannage

### 1. Pages Privées Visibles

**Problème :** Les pages draft apparaissent en production
**Solution :** Vérifier la configuration `include` dans retype.yml

### 2. Recherche Ne Fonctionne Pas

**Problème :** La recherche ne trouve pas les résultats
**Solution :** Vérifier que `search.enabled: true` est configuré

### 3. Navigation Cassée

**Problème :** Les liens de navigation ne fonctionnent pas
**Solution :** Vérifier les chemins dans la configuration `navigation.links`

## Exemple de Page Optimisée

```yaml
---
title: "Titre SEO Optimisé"
description: "Description pour les moteurs de recherche"
image: "/images/cover.jpg"
authors: ["Maxime Dubois"]
date: 2024-01-15
tags: [devops, kubernetes, tutorial]
order: 100
icon: ":gear:"
visibility: public
---

# Titre Principal

!!! tip "Conseil"
    Utilisez les composants Retype pour enrichir vos articles

=== "Exemple"
    Voici un exemple concret

=== "Explication"
    Voici l'explication détaillée
```

---

*Ce guide couvre les fonctionnalités avancées de Retype pour créer un blog technique professionnel et optimisé.* 