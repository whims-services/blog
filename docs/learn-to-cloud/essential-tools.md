---
icon: https://raw.githubusercontent.com/FortAwesome/Font-Awesome/6.x/svgs/solid/tools.svg
tags:
  - tools
  - cloud
  - devops
  - productivity
  - open-source
  - sovereignty
---
# Boîte à Outils du Cloud Engineer Souverain

Alors, parlons outils ! Mais pas n'importe lesquels : des outils libres, souverains et qui respectent vos données. Laissez-moi vous présenter la boîte à outils idéale pour un cloud engineer engagé.

## Terminal et Shell : Votre Cockpit de Pilotage

### Terminal Moderne et Libre
**Starship** - Prompt shell ultra-rapide et personnalisable (écrit en Rust !)
```bash
# Installation
curl -sS https://starship.rs/install.sh | sh

# Configuration ~/.config/starship.toml
[directory]
truncation_length = 3
truncate_to_repo = false

[kubernetes]
disabled = false
```

**Oh My Zsh** - Framework pour shell Zsh (100% open source)
```bash
# Installation
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# Plugins souverains recommandés
plugins=(git podman kubectl terraform ansible)
```

### Gestionnaires de Paquets Libres
- **Homebrew** (macOS/Linux) : `brew install <package>`
- **Nix** (Multi-platform) : Gestionnaire déclaratif
- **Flatpak** (Linux) : Applications sandboxées
- **APT/DNF** (Linux) : Gestionnaires système

## CLI Tools Cloud Souverains

### OVHcloud CLI
```bash
# Installation
pip install ovh

# Configuration
ovh setup

# Utilisation
ovh cloud project instance list
ovh cloud project storage list
```

### Scaleway CLI
```bash
# Installation
curl -o scw https://github.com/scaleway/scaleway-cli/releases/latest/download/scw-linux-x86_64
chmod +x scw && sudo mv scw /usr/local/bin/

# Configuration
scw init

# Utilisation
scw instance server list
scw object bucket list
```

### OpenStack CLI (Clouds Privés)
```bash
# Installation
pip install python-openstackclient

# Configuration via fichier RC
source openrc

# Utilisation
openstack server list
openstack volume list
```

## Infrastructure as Code Libre

### Terraform avec Providers Européens
```hcl
# Configuration OVHcloud
terraform {
  required_providers {
    ovh = {
      source  = "ovh/ovh"
      version = "~> 0.35"
    }
  }
}

provider "ovh" {
  endpoint = "ovh-eu"
}

resource "ovh_cloud_project_instance" "web" {
  service_name = var.service_name
  name         = "WebServer"
  flavor_name  = "s1-2"
  image_name   = "Ubuntu 22.04"
  region       = "GRA11"
}
```

### OpenTofu (Fork Libre de Terraform)
```bash
# Installation
wget https://github.com/opentofu/opentofu/releases/download/v1.6.0/tofu_1.6.0_linux_amd64.zip
unzip tofu_1.6.0_linux_amd64.zip
sudo mv tofu /usr/local/bin/
```

### Ansible - Configuration as Code
```yaml
# playbook.yml
---
- name: Configuration serveur web
  hosts: webservers
  become: yes
  
  tasks:
    - name: Installation nginx
      apt:
        name: nginx
        state: present
        update_cache: yes
    
    - name: Démarrage nginx
      systemd:
        name: nginx
        state: started
        enabled: yes
    
    - name: Configuration firewall
      ufw:
        rule: allow
        port: '80'
        proto: tcp
```

## Containerisation Souveraine

### Podman : L'Alternative Sans Daemon
```bash
# Installation (Fedora/RHEL)
sudo dnf install podman

# Installation (Ubuntu/Debian)
sudo apt install podman

# Utilisation (commandes identiques à Docker)
podman run -it registry.fedoraproject.org/fedora:latest bash
podman build -t myapp .
podman pod create --name mypod
```

### Buildah : Construction d'Images
```bash
# Installation
sudo dnf install buildah

# Construction d'image
buildah from scratch
buildah run working-container -- dnf install -y nginx
buildah config --entrypoint /usr/sbin/nginx working-container
buildah commit working-container nginx-custom
```

### Kubernetes : L'Orchestration Libre
```yaml
# deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: app
        image: myapp:latest
        ports:
        - containerPort: 8080
        resources:
          requests:
            memory: "128Mi"
            cpu: "250m"
          limits:
            memory: "256Mi"
            cpu: "500m"
```

**Outils Kubernetes essentiels :**
- **kubectl** : CLI officiel Kubernetes
- **Helm** : Gestionnaire de packages K8s
- **k9s** : Interface terminal interactive
- **kubectx/kubens** : Changement de contexte rapide

## CI/CD Open Source

### GitLab CI/CD
```yaml
# .gitlab-ci.yml
stages:
  - test
  - build
  - deploy

test:
  stage: test
  script:
    - npm test
  only:
    - merge_requests
    - main

build:
  stage: build
  script:
    - podman build -t $CI_REGISTRY_IMAGE:$CI_COMMIT_SHA .
    - podman push $CI_REGISTRY_IMAGE:$CI_COMMIT_SHA
  only:
    - main

deploy:
  stage: deploy
  script:
    - kubectl set image deployment/app app=$CI_REGISTRY_IMAGE:$CI_COMMIT_SHA
  only:
    - main
```

### Jenkins Pipeline
```groovy
pipeline {
    agent any
    
    stages {
        stage('Test') {
            steps {
                sh 'npm test'
            }
        }
        
        stage('Build') {
            steps {
                sh 'podman build -t myapp:${BUILD_NUMBER} .'
            }
        }
        
        stage('Deploy') {
            steps {
                sh 'kubectl set image deployment/app app=myapp:${BUILD_NUMBER}'
            }
        }
    }
}
```

### Tekton (Cloud Native CI/CD)
```yaml
# task.yaml
apiVersion: tekton.dev/v1beta1
kind: Task
metadata:
  name: build-and-deploy
spec:
  steps:
  - name: build
    image: quay.io/buildah/stable
    script: |
      buildah build -t $(params.image-name) .
  - name: deploy
    image: bitnami/kubectl
    script: |
      kubectl set image deployment/app app=$(params.image-name)
```

## Observabilité Communautaire

### Prometheus Stack
```yaml
# prometheus.yml
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'prometheus'
    static_configs:
      - targets: ['localhost:9090']
  
  - job_name: 'node-exporter'
    static_configs:
      - targets: ['localhost:9100']
  
  - job_name: 'app'
    static_configs:
      - targets: ['localhost:8080']
```

### Grafana - Visualisation Universelle
```bash
# Installation via Podman
podman run -d \
  -p 3000:3000 \
  --name grafana \
  -v grafana-storage:/var/lib/grafana \
  grafana/grafana

# Configuration datasource via API
curl -X POST \
  http://admin:admin@localhost:3000/api/datasources \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Prometheus",
    "type": "prometheus",
    "url": "http://prometheus:9090",
    "access": "proxy"
  }'
```

### Jaeger - Tracing Distribué
```yaml
# jaeger-all-in-one.yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: jaeger
spec:
  replicas: 1
  selector:
    matchLabels:
      app: jaeger
  template:
    metadata:
      labels:
        app: jaeger
    spec:
      containers:
      - name: jaeger
        image: jaegertracing/all-in-one:latest
        ports:
        - containerPort: 14268
        - containerPort: 16686
```

## Sécurité et Secrets Souverains

### Vault - Gestion de Secrets
```bash
# Installation
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
sudo apt-get update && sudo apt-get install vault

# Démarrage développement
vault server -dev

# Utilisation
vault kv put secret/myapp username=admin password=secret123
vault kv get secret/myapp
```

### SOPS - Secrets dans Git
```bash
# Installation
wget https://github.com/mozilla/sops/releases/download/v3.7.3/sops-v3.7.3.linux
chmod +x sops-v3.7.3.linux
sudo mv sops-v3.7.3.linux /usr/local/bin/sops

# Configuration avec age
age-keygen -o ~/.config/age/keys.txt
export SOPS_AGE_KEY_FILE=~/.config/age/keys.txt

# Chiffrement
sops -e --age age1abc123... secrets.yaml > secrets.enc.yaml
```

### Alternatives Européennes
- **Passbolt** : Gestionnaire de mots de passe collaboratif français
- **Bitwarden** : Self-hosted, code source ouvert
- **KeePass** : Gestionnaire local, formats ouverts

## Développement avec des Outils Libres

### VS Codium (VS Code sans Télémétrie)
```bash
# Installation
wget -qO - https://gitlab.com/paulcarroty/vscodium-deb-rpm-repo/raw/master/pub.gpg | gpg --dearmor | sudo dd of=/usr/share/keyrings/vscodium-archive-keyring.gpg
echo 'deb [ signed-by=/usr/share/keyrings/vscodium-archive-keyring.gpg ] https://download.vscodium.com/debs vscodium main' | sudo tee /etc/apt/sources.list.d/vscodium.list
sudo apt update && sudo apt install codium
```

### Neovim - Éditeur Modal Moderne
```bash
# Installation
sudo apt install neovim

# Configuration ~/.config/nvim/init.vim
set number
set autoindent
set tabstop=2
set shiftwidth=2
set expandtab
set mouse=a

" Plugin manager: vim-plug
call plug#begin()
Plug 'preservim/nerdtree'
Plug 'tpope/vim-fugitive'
Plug 'airblade/vim-gitgutter'
call plug#end()
```

## Networking et Diagnostic

### Outils de Diagnostic Réseau
```bash
# Installation d'outils essentiels
sudo apt install net-tools dnsutils tcpdump wireshark-cli

# Diagnostic réseau
ss -tuln                    # Ports ouverts
dig google.com             # Résolution DNS
tcpdump -i eth0 port 80    # Capture de trafic
nmap -sn 192.168.1.0/24    # Scan réseau
```

### Monitoring Réseau
```bash
# Installation iftop
sudo apt install iftop

# Utilisation
sudo iftop -i eth0          # Trafic par interface
sudo iftop -n              # Pas de résolution DNS
```

## Gestionnaires de Secrets Locaux

### Pass - Gestionnaire Unix Standard
```bash
# Installation
sudo apt install pass

# Initialisation
gpg --gen-key
pass init "votre@email.com"

# Utilisation
pass insert aws/access-key
pass show aws/access-key
pass generate aws/secret-key 32
```

### Direnv - Variables d'Environnement par Projet
```bash
# Installation
curl -sfL https://direnv.net/install.sh | bash

# Configuration ~/.bashrc
eval "$(direnv hook bash)"

# Utilisation dans un projet
echo "export API_KEY=secret123" > .envrc
direnv allow
```

## Outils de Communication Libres

### Element (Matrix)
Alternative décentralisée à Slack/Discord
```bash
# Installation
sudo apt install element-desktop

# Ou via Flatpak
flatpak install flathub im.riot.Riot
```

### Mattermost
Plateforme de collaboration auto-hébergée
```bash
# Installation via Docker
podman run -d \
  --name mattermost \
  -p 8065:8065 \
  -v mattermost-data:/mattermost/data \
  mattermost/mattermost-enterprise-edition
```

## L'Écosystème Français

### Pépites Françaises
- **Linagora** : Solutions collaboratives open source
- **Cozy Cloud** : Cloud personnel et souverain
- **Framasoft** : Promotion du logiciel libre
- **Wifirst** : Réseau et cloud français

### Distributions Linux Françaises
- **Mageia** : Distribution communautaire
- **Emmabuntüs** : Distribution solidaire
- **Primtux** : Distribution éducative

## Conseils de Productivité Souveraine

### Automatisation Quotidienne
```bash
# Script de déploiement
#!/bin/bash
set -e

echo "🚀 Déploiement en cours..."
git pull origin main
podman build -t myapp:latest .
kubectl set image deployment/app app=myapp:latest
echo "✅ Déploiement terminé !"
```

### Makefile pour Standardiser
```makefile
# Makefile
.PHONY: build deploy test

build:
	podman build -t myapp:latest .

test:
	npm test

deploy: build
	kubectl set image deployment/app app=myapp:latest

clean:
	podman rmi myapp:latest
```

### Aliases Utiles
```bash
# ~/.bashrc
alias k='kubectl'
alias kgp='kubectl get pods'
alias kgs='kubectl get services'
alias ll='ls -la'
alias tf='terraform'
alias tfa='terraform apply'
alias tfp='terraform plan'
```

## Ressources et Communautés

### Apprentissage Continu
- **LinuxFr** : Actualités et tutoriels
- **Open Source Guide** : Bonnes pratiques
- **CNCF Landscape** : Écosystème cloud native
- **Kubernetes Academy** : Formation gratuite

### Contribution
- **Documentation** de projets français
- **Issues** sur GitHub/GitLab
- **Traductions** d'outils open source
- **Modules** Terraform/Ansible

---

*Les outils que vous choisissez reflètent vos valeurs. Privilégions des solutions libres, ouvertes et respectueuses de notre souveraineté numérique ! Ensemble, construisons un écosystème technologique français fort et éthique.* 