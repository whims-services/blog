---
icon: https://raw.githubusercontent.com/kubernetes/community/master/icons/svg/resources/labeled/ing.svg
tags:
  - kubernetes
  - ingress
---
# Kubernetes NGINX Ingress Controller optimization

## 1. Set NGINX as the default ingress controller

**Why ? :** No more need for the ingressClassName field in ingress.yaml

**File :** `nginx.helm.values.yml`

```yaml
controller:
  ingressClass:
    create: true # default
    setAsDefaultIngress: true
```