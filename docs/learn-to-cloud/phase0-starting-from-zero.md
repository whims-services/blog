---
label: Reprendre le Contrôle de Son Parcours Tech
icon: ":rocket:"
order: 1
tags: [fondamentaux, career]
visibility: private
draft: true
---

# Reprendre le Contrôle de Son Parcours Tech

Hier, un junior de l'équipe me demandait comment j'en étais arrivé là. Assis dans mon bureau, face à mes trois écrans affichant Grafana, Kubernetes et un terminal, je me suis dit : "Merde, comment je résume 12 ans de galère et de réussites ?"

## Mon Parcours : De la Galère à la Passion

### Les Débuts Chaotiques

J'ai commencé par faire n'importe quoi. Vraiment. En 2012, j'installais Ubuntu sur tous les vieux PCs que je pouvais trouver. Ma première "infrastructure" ? Un Raspberry Pi dans ma chambre d'étudiant qui servait de serveur web. J'étais fier comme un paon, même si ça plantait deux fois par jour.

### La Révélation : Pourquoi J'ai Choisi Cette Voie

Le déclic est venu lors d'un stage en 2013. J'ai vu un ingénieur faire du déploiement automatisé avec des outils open-source. Pas de licences Microsoft à 10 000€, pas de dépendance à des solutions propriétaires. Just du code, de l'automatisation, et une liberté totale.

"C'est ça que je veux faire", je me suis dit. Et depuis, chaque choix technique que je fais est guidé par cette philosophie.

## Les Fondamentaux : Par Où Commencer Vraiment

### 1. Linux : La Base Incontournable

**Mon REX après 12 ans :** Ne perdez pas de temps avec Windows Server. Linux, c'est la base de tout dans le cloud native. J'ai perdu 6 mois à essayer de faire du Docker sur Windows en 2016. Autant dire que j'ai appris de mes erreurs.

**Ce que je recommande :**
- Installez Ubuntu ou Debian sur votre machine (dual-boot au minimum)
- Forcez-vous à utiliser le terminal pour TOUT
- Après 3 mois, vous serez à l'aise. Après 6 mois, vous ne pourrez plus vous en passer.

### 2. Programmation : L'Automatisation Avant Tout

**Mon apprentissage :** J'ai commencé par du Bash. Puis Python. Puis Go. Chaque langage avait sa logique dans mon évolution.

**Pourquoi ces langages ?**
- **Bash** : 80% de mes automatisations quotidiennes
- **Python** : Scripts, APIs, traitement de données
- **Go** : Performance, outils cloud native

**Erreur à éviter :** Ne vous dispersez pas. Maîtrisez UN langage avant de passer au suivant.

### 3. Containers : La Révolution Qui Change Tout

**Mon histoire Docker/Podman :** J'ai utilisé Docker pendant 4 ans. Puis j'ai découvert Podman. Migration terminée en 2 semaines, et je n'ai jamais regretté.

**Pourquoi Podman ?**
- Pas de daemon (sécurité++)
- Rootless par défaut
- Compatible Docker mais sans les dépendances propriétaires

**Mon conseil :** Apprenez les concepts avec Docker si vous voulez, mais migrez vers Podman dès que possible.

## La Certification : Investissement ou Perte de Temps ?

### Mon Expérience Personnelle

J'ai passé 3 certifications en 5 ans :
- **LFCS** (Linux Foundation) : 2019 - Super utile
- **CKA** (Kubernetes Administrator) : 2021 - Indispensable
- **LFCE** (Linux Foundation Engineer) : 2023 - Perfectionnement

**ROI concret :** +40% de salaire en 3 ans. Pas mal pour quelques mois d'étude.

### Les Certifications Qui Valent le Coup

**Évitez les certifications propriétaires.** Misez sur :
- **Linux Foundation** : Reconnues partout, vraiment techniques
- **Red Hat** : Excellente réputation, hands-on
- **CNCF** : L'avenir du cloud native

## Communauté : Trouvez Votre Tribu

### Ma Découverte des Communautés

En 2018, j'étais isolé. Je bossais seul, j'apprenais seul, je galérais seul. Puis j'ai découvert les communautés techniques françaises. Ça a changé ma carrière.

**Ce que ça m'a apporté :**
- Réponses à mes questions techniques
- Veille technologique collaborative
- Opportunités professionnelles
- Motivation et inspiration

### Où Aller En Priorité

**Communautés françaises actives :**
- **Discord DevOps FR** : Discussions quotidiennes, aide technique
- **Slack Cloud Native FR** : Focus sur Kubernetes et cloud native
- **Forums technique français** : Discussions approfondies

**Meetups et événements :**
- **DevOpsDays Paris** : Networking et retours d'expérience
- **Kubernetes Community Days** : Spécialisé mais excellent
- **Devoxx France** : Le plus gros événement tech français

## Mes Erreurs : Apprenez de Mes Galères

### Erreur #1 : Apprendre Sans Pratiquer

J'ai passé 6 mois à regarder des tutoriels Kubernetes sans jamais créer un cluster. **Résultat :** J'ai tout oublié.

**La solution :** Un homelab. Même basique. Même cassé. L'important c'est de mettre les mains dans le cambouis.

### Erreur #2 : Vouloir Tout Apprendre En Même Temps

En 2017, j'ai voulu apprendre Docker, Kubernetes, Terraform, Ansible et Jenkins en parallèle. **Résultat :** J'ai tout survolé, rien maîtrisé.

**La solution :** Une techno à la fois. Maîtrisez, pratiquez, puis passez à la suivante.

### Erreur #3 : Négliger la Théorie

J'étais tellement pressé de pratiquer que j'ai zappé les concepts fondamentaux. **Résultat :** J'ai mis 2 ans à comprendre pourquoi mes architectures étaient bancales.

**La solution :** Alternez théorie et pratique. Lisez, comprenez, puis implémentez.

## Votre Roadmap : Les 6 Premiers Mois

### Mois 1-2 : Les Bases
- **Linux** : Installation, terminal, commandes de base
- **Git** : Versioning, collaboration
- **Un langage** : Python ou Go selon vos préférences

### Mois 3-4 : L'Automatisation
- **Bash scripting** : Automatisez vos tâches répétitives
- **Infrastructure as Code** : Terraform ou Pulumi
- **CI/CD** : GitLab CI ou GitHub Actions

### Mois 5-6 : Le Cloud Native
- **Containers** : Podman, création d'images
- **Orchestration** : Kubernetes (les bases)
- **Monitoring** : Prometheus + Grafana

## Budget : Combien Ça Coûte Vraiment ?

### Mon Budget Annuel (2024)

**Matériel :**
- Homelab : 800€ (serveur d'occasion + stockage)
- Laptop : 1200€ (ThinkPad reconditionné)

**Formation :**
- Certifications : 400€/an
- Livres et ressources : 200€/an
- Conférences : 1000€/an

**Cloud :**
- Hébergement personnel : 50€/mois (OVHcloud)
- Tests et expérimentations : 30€/mois

**Total annuel : ~3000€**

**ROI :** Mon augmentation de salaire couvre largement ces investissements.

## Conclusion : Votre Parcours Commence Maintenant

Il y a 12 ans, j'étais un étudiant qui installait Ubuntu sur des vieux PCs. Aujourd'hui, je gère l'infrastructure cloud native d'une scale-up avec 200 développeurs. 

**Le secret ?** Pas de secret. De la curiosité, de la pratique, des erreurs assumées et une communauté qui m'a porté.

**Votre mission pour les 2 prochaines semaines :**
1. Installez Linux sur votre machine
2. Créez votre premier script Bash
3. Rejoignez une communauté technique
4. Commencez votre homelab (même basique)

**Et surtout :** Documentez votre parcours. Dans 2 ans, vous serez étonné du chemin parcouru.

---

*Article rédigé après 12 ans d'expérience, 47 projets en production, et quelques nuits blanches. Mais que de souvenirs !* 