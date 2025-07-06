---
label: Nettoyage des Ressources Orphelines
icon: ":broom:"
tags:
  - cleanup
  - maintenance
  - troubleshooting
visibility: private
draft: true
---

# Nettoyage des Ressources Orphelines Kubernetes

## Introduction

Les ressources orphelines dans Kubernetes peuvent s'accumuler au fil du temps et causer des problèmes de performance et de sécurité. Cet article présente des méthodes pour identifier et nettoyer ces ressources.

## Types de Ressources Orphelines

### 1. Pods Orphelins

```bash
# Identifier les pods sans owner references
kubectl get pods --all-namespaces -o json | jq '.items[] | select(.metadata.ownerReferences == null) | {name: .metadata.name, namespace: .metadata.namespace}'
```

### 2. PersistentVolumes Non Utilisés

```bash
# Lister les PV en statut Available
kubectl get pv --all-namespaces | grep Available
```

### 3. ConfigMaps et Secrets Inutilisés

```bash
# Script pour identifier les ConfigMaps non référencés
kubectl get configmaps --all-namespaces -o json | jq -r '.items[] | "\(.metadata.namespace) \(.metadata.name)"'
```

## Scripts de Nettoyage

### Nettoyage Automatisé

```bash
#!/bin/bash
# cleanup-orphans.sh

echo "Nettoyage des ressources orphelines..."

# Supprimer les pods Failed/Succeeded
kubectl delete pods --all-namespaces --field-selector=status.phase=Succeeded
kubectl delete pods --all-namespaces --field-selector=status.phase=Failed

# Nettoyer les PV Available
kubectl get pv | grep Available | awk '{print $1}' | xargs kubectl delete pv

echo "Nettoyage terminé."
```

## Monitoring et Alerting

### Métriques Prometheus

```yaml
# Alerte pour ressources orphelines
- alert: OrphanedPods
  expr: kube_pod_owner{owner_kind=""} > 0
  for: 5m
  labels:
    severity: warning
```

## Bonnes Pratiques

### 1. Labels et Annotations

```yaml
metadata:
  labels:
    app: myapp
    version: v1.0
    managed-by: helm
  annotations:
    cleanup.policy: "delete-after-30d"
```

### 2. Finalizers

```yaml
metadata:
  finalizers:
    - cleanup.example.com/cleanup-volumes
```

## Conclusion

Un nettoyage régulier des ressources orphelines est essentiel pour maintenir un cluster Kubernetes sain et performant.
