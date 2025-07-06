---
label: Boîte à Outils du Cloud Engineer Moderne
icon: ":wrench:"
order: 5
tags: [outils, productivité]
visibility: private
draft: true
---

# Boîte à Outils du Cloud Engineer Moderne

Samedi matin, 10h. Mon collègue Thomas me montre fièrement son nouvel IDE : "Regarde, j'ai installé VS Code avec 47 extensions !" J'ai regardé son écran. Télémétriques envoyées à Microsoft, suggestions d'IA basées sur GitHub Copilot, synchronisation cloud... 

"Thomas", j'ai dit, "tu viens de transformer ton éditeur en mouchard."

Cette scène m'a inspiré cet article : comment choisir ses outils quand on prône l'indépendance technologique.

## Ma Philosophie : L'Indépendance par les Outils

### Le Déclic de 2020

**Contexte :** Je développais sur VS Code, déployais sur AWS, collaborais sur Slack.
**Révélation :** J'ai réalisé que TOUS mes outils dépendaient de géants américains.
**Décision :** Migration progressive vers des alternatives européennes/open-source.

**Résultat après 4 ans :**
- Productivité identique (voire meilleure)
- Coûts divisés par 3
- Contrôle total de mes données
- Satisfaction personnelle énorme

### Mes Critères de Choix

**1. Open Source d'abord**
- Code source accessible
- Communauté active
- Pas de vendor lock-in

**2. Européen si possible**
- Données hébergées en Europe
- Entreprise européenne
- Conformité RGPD native

**3. Performance et stabilité**
- Aussi bon que l'alternative propriétaire
- Maintenance active
- Documentation complète

**4. Écosystème cohérent**
- Intégration avec mes autres outils
- Workflow fluide
- Courbe d'apprentissage raisonnable

## Développement et Édition : Mes Choix

### VS Codium : VS Code Sans Espionnage

**Pourquoi j'ai migré :**
- **Télémétrie :** VS Code envoie des données à Microsoft
- **Surveillance :** Tracking des extensions utilisées
- **Dépendance :** Écosystème Microsoft

**VS Codium :**
- Code source identique à VS Code
- Télémétrie supprimée
- Extensions compatibles
- Performance identique

**Mon setup :**
- **Extensions :** Python, Go, Docker, Kubernetes
- **Thème :** Dracula (parce que les yeux, c'est important)
- **Terminal intégré :** Zsh avec Oh My Zsh

**Temps de migration :** 2 heures. Franchement, pourquoi j'ai attendu si longtemps ?

### GitLab : Le Hub de Développement

**Pourquoi pas GitHub :**
- **Propriétaire :** Microsoft depuis 2018
- **Dépendance :** Écosystème fermé
- **Surveillance :** Données hébergées aux US

**GitLab :**
- **Open Source :** Version CE complète
- **Self-hosted :** Contrôle total
- **Intégré :** Git, CI/CD, registry, monitoring

**Mon instance GitLab :**
- **Hébergement :** OVHcloud (45€/mois)
- **Utilisateurs :** 12 développeurs
- **Projets :** 150+ repos
- **CI/CD :** 500+ pipelines/mois

**Migration depuis GitHub :** 3 jours, zéro perte de données.

## Infrastructure et Déploiement : Ma Stack

### Terraform : L'Infrastructure as Code

**Pourquoi Terraform :**
- **Multi-cloud :** Supporte tous les providers
- **Maturité :** 8 ans d'existence, stable
- **Communauté :** Énorme écosystème

**Mes providers favoris :**
- **OVHcloud :** 80% de mon infrastructure
- **Scaleway :** Tests et développement
- **Hetzner :** Projets personnels

**Mon workflow :**
```bash
# Planification
terraform plan -out=tfplan

# Validation manuelle
terraform show tfplan

# Application
terraform apply tfplan
```

**Metrics :** 200+ ressources managées, 0 dérive de configuration.

### Ansible : La Configuration Automatisée

**Pourquoi pas Puppet/Chef :**
- **Simplicité :** YAML lisible
- **Agentless :** Pas d'agent à installer
- **Polyvalence :** Système ET applications

**Mon utilisation :**
- **Configuration serveurs :** 50+ playbooks
- **Déploiement applications :** 20+ rôles
- **Maintenance :** Tasks automatisées

**Exemple playbook :**
```yaml
- name: Install Docker
  apt:
    name: docker.io
    state: present
    
- name: Start Docker service
  systemd:
    name: docker
    state: started
    enabled: yes
```

**Résultat :** Provisioning serveur en 12 minutes, configuration 100% reproductible.

### Podman : Les Containers Sans Daemon

**Pourquoi j'ai quitté Docker :**
- **Sécurité :** Daemon root obligatoire
- **Architecture :** Single point of failure
- **Entreprise :** Monétisation aggressive

**Podman :**
- **Rootless :** Sécurité par défaut
- **Daemonless :** Pas de processus central
- **Compatible :** API Docker identique

**Migration :**
```bash
# Alias pour transition douce
alias docker=podman
```

**Temps de migration :** 2 semaines, 0 régression.

## Monitoring et Observabilité : Ma Stack

### Prometheus + Grafana : Le Duo Gagnant

**Pourquoi cette stack :**
- **Open Source :** Pas de vendor lock-in
- **Scalable :** Supporte des millions de métriques
- **Intégré :** Écosystème cloud native

**Mon setup :**
- **Prometheus :** 4 instances (HA)
- **Grafana :** 1 instance avec 50+ dashboards
- **AlertManager :** Alertes intelligentes
- **Exporters :** 15+ collecteurs de métriques

**Métriques surveillées :**
- **Système :** CPU, RAM, disque, réseau
- **Applications :** Latence, erreurs, throughput
- **Business :** Utilisateurs actifs, conversions

**Rétention :** 90 jours de métriques, 2 ans d'historique.

### Loki : Les Logs Centralisés

**Pourquoi Loki :**
- **Intégration :** Grafana native
- **Performance :** Indexation intelligente
- **Coût :** Stockage optimisé

**Mon déploiement :**
- **Ingestion :** 2GB/jour de logs
- **Rétention :** 30 jours
- **Recherche :** < 2 secondes

**Exemple query :**
```logql
{job="webapp"} |= "ERROR" | json | line_format "{{.timestamp}} {{.level}} {{.message}}"
```

## Communication et Collaboration : Mes Alternatives

### Mattermost : Slack Open Source

**Pourquoi j'ai quitté Slack :**
- **Propriétaire :** Salesforce depuis 2021
- **Surveillance :** Données analysées
- **Dépendance :** Écosystème fermé

**Mattermost :**
- **Open Source :** Code source accessible
- **Self-hosted :** Contrôle total
- **Intégré :** Plugins GitLab, monitoring

**Mon instance :**
- **Hébergement :** OVHcloud (15€/mois)
- **Utilisateurs :** 25 personnes
- **Channels :** 40+ canaux
- **Integrations :** GitLab, Prometheus, Grafana

**Migration :** 1 journée, adoption immédiate.

### Element : Matrix for Business

**Pourquoi Matrix :**
- **Décentralisé :** Pas de point central
- **Chiffrement :** E2E par défaut
- **Interopérable :** Protocole ouvert

**Mon usage :**
- **Équipe technique :** Discussions privées
- **Projets sensibles :** Chiffrement end-to-end
- **Communautés :** Participation aux salons techniques

**Limite :** Interface moins polish que Slack/Teams.

## Sécurité et Confidentialité : Mes Outils

### Bitwarden : Gestionnaire de Mots de Passe

**Pourquoi pas LastPass/1Password :**
- **Propriétaire :** Logiciel fermé
- **Surveillance :** Données centralisées
- **Incidents :** Breaches régulières

**Bitwarden :**
- **Open Source :** Code auditible
- **Self-hosted :** Option disponible
- **Intégration :** Tous les navigateurs/apps

**Mon setup :**
- **Instance :** Self-hosted (Vaultwarden)
- **Mots de passe :** 200+ entrées
- **Partage :** Équipe technique
- **2FA :** Intégré

### Proton : Email et VPN

**Pourquoi j'ai quitté Gmail :**
- **Surveillance :** Emails analysés
- **Publicité :** Ciblage personnalisé
- **Dépendance :** Écosystème Google

**Proton :**
- **Chiffrement :** E2E par défaut
- **Suisse :** Lois sur la confidentialité
- **Intégré :** Email, VPN, Drive, Calendar

**Mon usage :**
- **Email :** 5GB, 3 domaines personnalisés
- **VPN :** 50+ serveurs européens
- **Drive :** 200GB stockage chiffré

## Productivité et Workflow : Mes Astuces

### Terminal : Zsh + Oh My Zsh

**Pourquoi Zsh :**
- **Fonctionnalités :** Auto-completion avancée
- **Personnalisation :** Thèmes et plugins
- **Performance :** Rapide et stable

**Mon setup :**
- **Thème :** Powerlevel10k
- **Plugins :** git, kubectl, terraform, ansible
- **Aliases :** 50+ raccourcis personnalisés

**Exemple .zshrc :**
```bash
# Aliases utiles
alias k='kubectl'
alias tf='terraform'
alias dc='docker-compose'
alias ll='ls -la'
```

### Homelab : Mon Laboratoire Personnel

**Pourquoi un homelab :**
- **Apprentissage :** Tester sans risque
- **Autonomie :** Héberger mes services
- **Économie :** Pas de facture cloud

**Mon setup :**
- **Serveur :** HP ProLiant DL380 G7 (300€ d'occasion)
- **RAM :** 32GB DDR3
- **Storage :** 2TB RAID 1
- **Réseau :** pfSense + UniFi

**Services hébergés :**
- **GitLab :** Repos personnels
- **Nextcloud :** Stockage fichiers
- **Grafana :** Monitoring maison
- **Bitwarden :** Gestionnaire mots de passe

## Migration : Mon Retour d'Expérience

### Planning de Migration (2020-2024)

**Année 1 (2020) :**
- VS Code → VS Codium
- Docker → Podman
- Slack → Mattermost

**Année 2 (2021) :**
- GitHub → GitLab
- Gmail → Proton
- AWS → OVHcloud

**Année 3 (2022) :**
- CloudWatch → Prometheus/Grafana
- Zoom → Jitsi Meet
- Notion → Obsidian

**Année 4 (2023) :**
- LastPass → Bitwarden
- Google Drive → Nextcloud
- Chrome → Firefox

### Difficultés Rencontrées

**Résistance d'équipe :**
- **Problème :** Habitudes ancrées
- **Solution :** Formation progressive, benefits démontrés

**Courbe d'apprentissage :**
- **Problème :** Nouveaux outils à maîtriser
- **Solution :** Documentation, practice, patience

**Écosystème moins mature :**
- **Problème :** Moins de plugins/intégrations
- **Solution :** Développement custom, contributions OSS

### Bénéfices Obtenus

**Économique :**
- **Coûts :** -60% sur les outils
- **Licences :** Zéro coût propriétaire
- **Hosting :** Contrôle des factures

**Sécurité :**
- **Données :** Contrôle total
- **Confidentialité :** Pas de surveillance
- **Compliance :** RGPD native

**Technique :**
- **Flexibilité :** Customisation totale
- **Performance :** Optimisation possible
- **Apprentissage :** Compréhension profonde

## Mes Recommandations par Niveau

### Débutant (0-2 ans d'expérience)

**Essentiels :**
- **Éditeur :** VS Codium
- **Terminal :** Zsh + Oh My Zsh
- **Git :** GitLab (gratuit)
- **Containers :** Podman

**Coût :** 0€
**Temps d'apprentissage :** 1 mois

### Intermédiaire (2-5 ans d'expérience)

**Ajouts :**
- **IaC :** Terraform + Ansible
- **Monitoring :** Prometheus + Grafana
- **CI/CD :** GitLab CI
- **Sécurité :** Bitwarden

**Coût :** 50€/mois (hébergement)
**Temps d'apprentissage :** 3 mois

### Expert (5+ ans d'expérience)

**Ajouts :**
- **Homelab :** Serveur personnel
- **Monitoring avancé :** Loki + Jaeger
- **Sécurité :** Vault + PKI
- **Contributions :** Open Source

**Coût :** 200€/mois (équipement + hosting)
**Temps d'apprentissage :** 6 mois

## Budget Outillage : Mes Chiffres

### Coût Mensuel (2024)

**Hébergement :**
- GitLab instance : 45€
- Monitoring stack : 25€
- Homelab (électricité) : 30€
- Services divers : 20€

**Licences :**
- Proton Suite : 12€
- Bitwarden : 3€
- Domaines : 5€

**Total mensuel : 140€**

### Comparaison avec Stack Propriétaire

**Stack propriétaire :**
- GitHub Enterprise : 50€/mois
- AWS : 200€/mois
- Office 365 : 15€/mois
- Monitoring SaaS : 100€/mois
- Slack : 25€/mois

**Total : 390€/mois**

**Économie : 250€/mois (3000€/an)**

## Conclusion : Votre Indépendance Technologique

J'ai mis 4 ans à construire ma stack d'outils indépendants. Le résultat ? Productivité identique, coûts divisés par 3, contrôle total de mes données.

**Mes 3 conseils pour commencer :**
1. **Commencez petit :** Un outil à la fois
2. **Testez d'abord :** Parallel run avant migration
3. **Documentez tout :** Workflow et configurations

**Votre plan pour les 3 prochains mois :**
- Migrez vers VS Codium
- Testez Podman en parallèle de Docker
- Créez un compte GitLab
- Installez Prometheus sur un serveur test

**Dans 1 an, vous aurez :**
- Une stack d'outils indépendants
- Des compétences valorisables
- Une facture allégée
- Un contrôle total de vos données

**Et surtout :** Vous participerez à l'écosystème open source européen. Chaque utilisateur qui migre vers des alternatives ouvertes, c'est un vote pour l'indépendance technologique.

**Parce que nos outils façonnent notre façon de travailler. Autant choisir des outils qui nous façonnent positivement.**

---

*Article écrit avec VS Codium, hébergé sur GitLab, monitoré par Prometheus, et backupé sur Nextcloud. Cohérence quand tu nous tiens !* 