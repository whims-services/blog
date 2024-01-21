---
icon: https://raw.githubusercontent.com/kubernetes/community/master/icons/svg/resources/labeled/ing.svg
tags:
  - kubernetes
  - ingress
---
# Kubernetes NGINX Ingress Controller optimization (Helm deployed)

The NGINX ingress controller has additional configuration options that can be customized and configured to create a more dynamic application. Basically, this can be done in two ways:

**Annotations:** this option can be used if you want a specific configuration for a particular ingress rule.
**ConfigMap:** this option can be used when you need to set global configurations for the NGINX ingress controller.

**Note:** annotations take precedence over a ConfigMap.

## Useful ingress annotations

```yaml
# Disable NGINX access logs for a particular service
nginx.ingress.kubernetes.io/enable-access-log: "false"

# Whitelist IP for a particular Ingress (CIDR or just IP)
nginx.ingress.kubernetes.io/whitelist-source-range: "X.X.X.X/24,X.X.X.X"

# Allow large file transfert
nginx.ingress.kubernetes.io/proxy-body-size: 100m

# Stick user session to the same targeted pod 
nginx.ingress.kubernetes.io/affinity: "cookie"
nginx.ingress.kubernetes.io/affinity-mode: "persistent" # change to "balanced" (default) to redistribute some sessions when scaling pods
nginx.ingress.kubernetes.io/session-cookie-name: "name-distinguishing-services"
nginx.ingress.kubernetes.io/session-cookie-max-age: "172800" # in seconds, equivalent to 48h
```

## Optimize NGINX Ingress Controller ConfigMap

You should set optimizations for the default settings of Nginx ingress controller at `values.yml`

* Autoscale the ingress controller
* Default certificate for non-configured routes
* Set as the default ingress controller
* Use professional error pages
* Access to real client IP in applications
* Set maintenance mode

```yaml
controller:
  kind: DaemonSet # <---- use DaemonSet instead of Deployment
  autoscaling:
    enabled: true
    minReplicas: 1
    maxReplicas: 3
    targetCPUUtilizationPercentage: 200
    targetMemoryUtilizationPercentage: 200
  extraArgs:
    default-ssl-certificate: "my-namespace/my-certificate" # <---- certificate, for non-configured routes
  ingressClass:
    create: true
    setAsDefaultIngress: true # (no more need of ingressClassName in ingress.yaml)
  config:
    custom-http-errors: 404,408,500,501,502,503,504,505
defaultBackend:
  enabled: true
  image:
    repository: ghcr.io/tarampampam/error-pages # <---- use professional error pages
    tag: 2.26 # https://github.com/tarampampam/error-pages/releases
  extraEnvs:
    - name: TEMPLATE_NAME
      value: connexion
    - name: SHOW_DETAILS # Optional: enables the output of additional information on error pages
      value: "false"
  service:
    externalTrafficPolicy: "Local" # <---- access to real client IP in applications
```

Sources: 
* [NGINX Ingress Controller annotations](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/)
* [Sticky session](https://kubernetes.github.io/ingress-nginx/examples/affinity/cookie/)
* [OVH Cloud - Real IPs](https://help.ovhcloud.com/csm/en-public-cloud-kubernetes-getting-source-ip-behind-loadbalancer?id=kb_article_view&sysparm_article=KB0049765)
* [Kubernetes maintenance page](https://devopsdirective.com/posts/2022/10/kubernetes-maintenance-page/)
* [LoftSh Useful configuration](https://loft.sh/blog/kubernetes-nginx-ingress-10-useful-configuration-options/)
* [Dev.to - Zenika](https://dev.to/zenika/kubernetes-nginx-ingress-controller-10-complementary-configurations-for-web-applications-ken)