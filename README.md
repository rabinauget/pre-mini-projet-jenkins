# MINI PROJET JENKINS

Ce mini projet est dans le cadre du bootcamp Devops de Eazytraing

**Nom** : AUGET

**Prénom** : Rabina

**Pour la promotion 19 du Bootcamp DevOps**

**Période** : Mai - Juin - Juillet 2024

**Date de réalisation**: 30 Juin 2024

**LinkedIn** : www.linkedin.com/in/auget-rabina-61663314a

# Contexte du projet

Ce projet a pour objectif de mettre en place un pipeline CI/CD (Intégration Continue et Déploiement Continu) afin d'automatiser et d'optimiser le processus de livraison et de déploiement de l'application en utilisant Jenkins. Cela permettra de réduire les erreurs manuelles, d'accélérer les mises à jour et d'assurer une intégration fluide et homogène à chaque étape grâce à Jenkins.

Le pipeline sera déclenché à chaque push de code vers Github, assurant que les nouvelles modifications sont automatiquement compilées, testées, intégrées, puis déployées sur les serveurs de production.

# Fonctionnement du pipeline

Le pipeline CI/CD sera structuré en plusieurs étapes clés:

1. **La phase de Build :** consistera à la compilation du code source et construction des artéfacts nécessaires pour le déploiement.

2. **La phase de Test de l'artifact (Test d'acceptation) :** sera la partie où nous allons tester et confirmer que l'artéfact précédement créé est bien fonctionnel.

3. **La phase de sauvegarde de l'image (Release image) :** Après avoir confirmer que l'artéfact est fonctionnel, nous allons le sauvegarder afin de pouvoir le déployer sur les serveurs tests/prod ou le réutiliser ultérieurement.

6. **La phase de déploiment sur le serveur de production (Deploy prod & Test prod):** L'application, ayant été confirmée comme fonctionnelle à toutes les étapes, peut maintenant être déployée sur l'environnement de production pour être utilisée par les clients.

# Application

Donc le pipeline sera composé des fichiers ci-dessous:

+ **Jenkinsfile :** où nous allons énumérer toutes les étapes du pipeline CI/CD.
+ **Dockerfile :** nous servira à créer l'image docker de notre application pour pouvoir le conteneuriser.
+ **nginx.conf :** vu qu'on va utiliser nginx comme serveur web dans le container, ce fichier sera son fichier de configuration.
+ Le code source de l'application sera télécharger directement depuis le repos github dans l'image docker: https://github.com/diranetafen/static-website-example.git

# Infrastructure et techno

Nous allons utiliser les technologies ci-dessous:

+ **Hôte physique :** Windows 11 avec un CPU intel core i7-8ème 2.1GHz et 16GB RAM
+ **Hôte serveur:** Droplet 2CPU/4GB RAM/120G SSD sur DigitalOcean
+ **Jenkins :** Nous allons ensuite installer Jenkins sur le serveur de DigitalOcean via Docker
+ **Heroku :** Et pour déployer notre application, nous allons le déployer sur Heroku qui est une plateforme de déploiement d'application en ligne (https://www.heroku.com/)

# Préparation de l'environnement


