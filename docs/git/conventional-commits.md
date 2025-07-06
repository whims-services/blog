---
label: Conventional Commits
icon: ":memo:"
tags:
  - git
  - commits
  - standards
visibility: private
draft: true
---

# Conventional Commits

## Introduction

Les Conventional Commits sont une spécification pour ajouter une signification lisible par l'homme et les machines aux messages de commit. Cette approche facilite l'automatisation du versioning et de la génération de changelogs.

## Format des Messages

### Structure de Base

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

### Types de Commits

- **feat**: Nouvelle fonctionnalité
- **fix**: Correction de bug
- **docs**: Documentation uniquement
- **style**: Formatage, espaces, etc.
- **refactor**: Refactoring du code
- **test**: Ajout ou modification de tests
- **chore**: Maintenance, build, etc.

## Exemples Pratiques

### Commits Simples

```bash
feat: add user authentication
fix: resolve memory leak in parser
docs: update API documentation
```

### Commits avec Scope

```bash
feat(auth): implement JWT token validation
fix(database): resolve connection timeout
docs(api): add endpoint documentation
```

### Commits avec Breaking Changes

```bash
feat!: remove deprecated API endpoints

BREAKING CHANGE: The /api/v1/users endpoint has been removed.
Use /api/v2/users instead.
```

## Outils et Automation

### Commitizen

```bash
npm install -g commitizen
npm install -g cz-conventional-changelog
```

### Automated Changelog

```bash
npm install -g conventional-changelog-cli
conventional-changelog -p angular -i CHANGELOG.md -s
```

## Bonnes Pratiques

### 1. Messages Descriptifs

```bash
# Bon
feat: add password strength validation

# Mauvais
fix: bug
```

### 2. Commits Atomiques

```bash
# Séparer les fonctionnalités
feat: add user login endpoint
feat: add user registration endpoint
```

### 3. Utilisation du Body

```bash
feat: implement user caching

Add Redis-based caching for user sessions to improve
performance and reduce database load.

Cache expires after 1 hour of inactivity.
```

## Conclusion

Les Conventional Commits améliorent la lisibilité de l'historique Git et permettent l'automatisation des processus de release et de documentation. 