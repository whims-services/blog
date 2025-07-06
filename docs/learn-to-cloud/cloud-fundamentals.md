---
label: Cloud Maîtrisé - Reprendre le Contrôle
icon: ":cloud:"
order: 2
tags: [fondamentaux, infrastructure]
visibility: private
draft: true
---

# Cloud Maîtrisé : Reprendre le Contrôle de Nos Infrastructures

Lundi matin, 8h30. Réunion d'équipe. Le CTO nous annonce : "On va migrer vers le cloud, c'est plus moderne." Silence dans la salle. Paul, notre lead dev, demande timidement : "Quel cloud ?" Réponse du CTO : "Bah, AWS comme tout le monde, non ?"

J'ai failli m'étrangler avec mon café. "Comme tout le monde" ? Laissez-moi vous expliquer pourquoi cette phrase me hérisse les poils.

## Ma Définition du Cloud (Après 8 Ans de Bataille)

### Le Cloud, C'est Quoi Vraiment ?

Le cloud computing, c'est simple : utiliser des ressources informatiques (serveurs, stockage, réseau) via internet au lieu de les posséder physiquement. Point.

**Mais attention :** cloud ne signifie pas "forcément chez Amazon". C'est là que ça devient intéressant.

### Mon Parcours Cloud : De l'Émerveillé au Critique

**2016 :** J'ai créé ma première instance AWS. Magique ! Un serveur en 2 clics.
**2017 :** Premier incident. 6 heures de downtime à cause d'un problème chez AWS.
**2018 :** Première facture surprise. 1200€ pour un test de charge mal configuré.
**2019 :** J'ai découvert OVHcloud. Même services, 60% moins cher, data en Europe.
**2020 :** Migration complète. 3 semaines de galère, mais libération totale.

**La leçon :** Le cloud, c'est fantastique. Mais pas n'importe lequel.

## Les Modèles Cloud : Ce Qu'On Ne Vous Dit Pas

### Infrastructure as a Service (IaaS)

**Définition simple :** Vous louez des serveurs virtuels.

**Mon expérience :** J'ai testé 5 providers IaaS en 3 ans. Voici ce que j'ai appris :

**OVHcloud :**
- **Pros :** Prix imbattables, data en Europe, support français
- **Cons :** Interface parfois rustique, moins de services que les géants
- **Mon usage :** 80% de notre infrastructure

**Scaleway :**
- **Pros :** Innovation française, serveurs ARM, prix compétitifs
- **Cons :** Moins mature, quelques bugs sur les services récents
- **Mon usage :** Tests et développement

**Hetzner :**
- **Pros :** Qualité allemande, excellent rapport qualité/prix
- **Cons :** Moins de datacenters, pas de services managés
- **Mon usage :** Homelab et projets personnels

### Platform as a Service (PaaS)

**Définition simple :** Vous déployez votre code, la plateforme gère l'infrastructure.

**Mon REX :** J'ai utilisé 3 solutions PaaS différentes :

**Clever Cloud (français) :**
- Migration d'une app Node.js en 2 heures
- Scaling automatique qui fonctionne
- Prix raisonnable, support réactif

**Scalingo (français) :**
- Excellent pour les apps Rails/Django
- Addons bien intégrés
- Monitoring inclus

### Software as a Service (SaaS)

**Définition simple :** Vous utilisez des logiciels hébergés.

**Mon approche :** J'évite les SaaS américains quand c'est possible. Alternatives européennes :

**Remplacements concrets :**
- Gmail → Proton Mail (Suisse)
- Slack → Mattermost (self-hosted)
- Zoom → Jitsi Meet (open-source)
- Notion → Notion (bon, là j'ai pas trouvé d'alternative convaincante)

## Pourquoi J'Évite les Géants Américains

### L'Incident de 2019 : Ma Prise de Conscience

Décembre 2019. Notre application crash à 14h un mardi. Cause : une panne AWS dans la région eu-west-1. Notre SLA client ? 99.9%. Notre compensation ? Zéro.

**La réalité :** Quand AWS tombe, vous tombez avec. Et vous n'avez aucun recours.

### Le Vendor Lock-in : Mon Cauchemar de 2020

J'ai passé 6 mois à sortir notre infrastructure de AWS. **Pourquoi ?**

**Services propriétaires :**
- RDS (base de données) → Migration vers PostgreSQL standard
- Lambda → Réécriture pour du containerisé
- CloudWatch → Migration vers Prometheus/Grafana
- ELB → Migration vers nginx

**Coût total :** 3 semaines de travail, 2 nuits blanches, 1 quasi-burnout.

**Économie annuelle :** 40% de la facture cloud.

### La Souveraineté des Données : Plus Qu'un Buzzword

**2018 :** RGPD entre en vigueur. Notre DPO découvre que nos données client transitent par des serveurs américains.

**Problème :** Le Cloud Act américain permet aux autorités US d'accéder aux données hébergées chez AWS/Azure/GCP, même en Europe.

**Solution :** Migration vers des hébergeurs européens. Compliance RGPD native.

## Les Hébergeurs Européens : Mes Retours d'Expérience

### OVHcloud : Le Champion Français

**3 ans d'utilisation, 47 projets déployés**

**Points forts :**
- **Prix :** 60% moins cher qu'AWS pour des configs équivalentes
- **Performance :** Latence excellent depuis la France
- **Support :** Français, réactif, compétent
- **Compliance :** RGPD by design

**Points faibles :**
- **Écosystème :** Moins d'outils tiers intégrés
- **Services managés :** Catalogue moins fourni
- **Documentation :** Parfois incomplète

**Métriques concrètes :**
- Uptime : 99.97% (meilleur qu'AWS sur nos apps)
- Latence : 12ms depuis Lyon (vs 28ms avec AWS)
- Coût : 2800€/mois (vs 4600€ avec AWS)

### Scaleway : L'Innovation Française

**1 an d'utilisation, projets R&D**

**Points forts :**
- **Innovation :** Premiers sur les serveurs ARM
- **Tarifs :** Très compétitifs
- **Vision :** Vraiment européenne

**Points faibles :**
- **Maturité :** Quelques bugs sur les nouveaux services
- **Documentation :** En cours d'amélioration
- **Écosystème :** Encore limité

**Cas d'usage :** Tests, développement, projets expérimentaux.

## Architecture Cloud : Mes Bonnes Pratiques

### Multi-Cloud : La Vraie Résilience

**Mon setup actuel :**
- **Production :** OVHcloud (France)
- **Staging :** Scaleway (France)
- **Backup :** Hetzner (Allemagne)
- **Monitoring :** VPS dédié (indépendant)

**Pourquoi cette architecture ?**
- Aucune dépendance à un seul provider
- Résilience géographique
- Optimisation coût/performance
- Souveraineté assurée

### Infrastructure as Code : Mon Workflow

**Stack technique :**
- **Terraform :** Provisioning infrastructure
- **Ansible :** Configuration des serveurs
- **GitLab CI :** Déploiement automatisé
- **Monitoring :** Prometheus + Grafana + AlertManager

**Exemple concret :** Notre infrastructure de prod se déploie en 12 minutes via GitLab CI. Rollback en 3 minutes.

### Monitoring : Ce Que J'Ai Appris

**Erreur classique :** Faire confiance au monitoring du provider.

**Ma solution :** Monitoring externe indépendant.

**Stack :**
- **Prometheus :** Collecte des métriques
- **Grafana :** Visualisation
- **AlertManager :** Alertes intelligentes
- **Uptime Robot :** Monitoring externe

**Métriques que je surveille :**
- Latence des APIs (< 200ms)
- Taux d'erreur (< 0.1%)
- Utilisation CPU/RAM
- Espace disque
- Certificats SSL (expiration)

## Sécurité : Mes Leçons Apprises

### L'Incident de 2021 : Ma Leçon de Cybersécurité

**Contexte :** Tentative d'intrusion sur notre infrastructure.
**Vecteur :** Brute force SSH depuis la Chine.
**Résultat :** Aucun impact grâce à nos mesures.

**Mesures de sécurité :**
- **Authentification :** Clés SSH uniquement, pas de mot de passe
- **Firewall :** Règles strictes, whitelisting
- **Monitoring :** Alertes sur les tentatives de connexion
- **Fail2ban :** Bannissement automatique des IPs suspectes

### Chiffrement : Ce Qui Marche Vraiment

**Transport :** TLS 1.3 partout, certificats Let's Encrypt
**Storage :** Chiffrement des disques avec LUKS
**Backup :** Chiffrement avec GPG avant envoi

**Mon principe :** Si c'est pas chiffré, c'est pas sécurisé.

## Coûts : La Réalité des Chiffres

### Ma Facture Cloud (2024)

**Infrastructure de prod :**
- 3 serveurs web (8GB RAM) : 90€/mois
- 1 serveur base de données (16GB RAM) : 45€/mois
- Load balancer : 15€/mois
- Stockage (500GB) : 25€/mois
- Bande passante : 10€/mois

**Total mensuel : 185€/mois**

**Équivalent AWS : 340€/mois**

**Économie annuelle : 1860€**

### ROI de la Migration

**Coût de migration :** 3 semaines de travail (≈ 12 000€)
**Économie annuelle :** 1860€ + gain en autonomie
**ROI :** Positive au bout de 7 ans

**Mais surtout :** Contrôle total de nos données et infrastructure.

## Conseils Pratiques : Par Où Commencer

### Votre Premier Serveur Cloud

**Ma recommandation :** Commencez petit avec Hetzner.
- **Serveur :** 4GB RAM, 40GB SSD (3€/mois)
- **OS :** Ubuntu 22.04 LTS
- **Accès :** SSH avec clés uniquement

**Première mission :** Déployez nginx et affichez "Hello World".

### Votre Première Application

**Stack recommandée :**
- **Frontend :** nginx + certificat Let's Encrypt
- **Backend :** Node.js ou Python (selon vos préférences)
- **Base de données :** PostgreSQL
- **Monitoring :** Prometheus + Grafana

**Objectif :** Une app simple mais production-ready.

### Votre Premier Déploiement Automatisé

**Outils :**
- **Code :** GitLab ou GitHub
- **CI/CD :** GitLab CI ou GitHub Actions
- **Déploiement :** Script bash + rsync (simple mais efficace)

**Temps nécessaire :** 2 weekends pour tout mettre en place.

## Conclusion : Votre Indépendance Cloud

J'ai mis 4 ans à comprendre que le cloud n'est pas synonyme de dépendance. Au contraire, bien utilisé, le cloud peut être un formidable outil d'indépendance technologique.

**Mes 3 principes :**
1. **Choisir des providers européens** pour la souveraineté
2. **Éviter le vendor lock-in** avec des solutions standard
3. **Maîtriser son infrastructure** avec du code et du monitoring

**Votre prochaine étape :**
1. Créez un compte chez un hébergeur européen
2. Déployez votre premier serveur
3. Automatisez avec Terraform
4. Surveillez avec Prometheus

**Dans 6 mois, vous aurez :**
- Une infrastructure cloud maîtrisée
- Des coûts optimisés
- Une souveraineté technologique
- De l'expérience valorisable

**Et surtout :** Vous ne direz plus jamais "AWS comme tout le monde". Vous direz "J'ai choisi en conscience".

---

*Article rédigé après 8 ans de cloud, 5 migrations, 2 incidents majeurs, et une conviction : l'indépendance technologique n'est pas un luxe, c'est une nécessité.* 