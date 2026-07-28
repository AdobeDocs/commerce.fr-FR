---
title: Liste de contrôle de préparation du client
description: Découvrez comment préparer une migration de données en bloc vers Adobe Commerce as a Cloud Service avec une liste de contrôle de préparation couvrant l’engagement, la machine, la source et la cible.
feature: Cloud
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
role: Developer
level: Intermediate
autotag-review: '2026-07-22T19:19:18.443Z'
TQID: 'https://experienceleague.adobe.com/728hkK-dzIPzyuBhuNyOqEE9FxlVGdVc9R2wIRcXobk'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
subfeature_v2:
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 670b6214b28be93a16130552a226a8cadb487324
workflow-type: tm+mt
source-wordcount: 1171
ht-degree: 0%

---

# Liste de contrôle de préparation du client

{{bulk-data-early-access}}

Utilisez cette liste de contrôle pour préparer une migration des données d’une instance [!DNL Adobe Commerce on Cloud] ou locale vers [!DNL Adobe Commerce as a Cloud Service] à l’aide de l’outil de migration de données en bloc.

L’outil de migration est distribué dans le cadre du processus d’engagement de l’ingénierie déployée (CDE) Commerce. L’accès à l’outil est limité par un accord CDE signé et n’est pas disponible publiquement.

Cette liste de contrôle couvre ce que vous devez mettre en place avant le partage de l’outil ([Étape 1](#stage-1-before-tool-access)) et ce dont vous avez besoin pour commencer la configuration et l’exécution une fois que vous disposez de l’outil ([Étape 2](#stage-2-before-running-the-migration)). Consultez rapidement cette liste de contrôle avec votre équipe Adobe, car certains éléments nécessitent une coordination Adobe.

## Étape 1 : avant l&#39;accès à l&#39;outil

Effectuez ou confirmez les opérations suivantes avant de fournir l’outil de migration et la documentation.

- **Engagement CDE** — Un accord d’ingénierie de déploiement Commerce signé doit être en place. L’accès aux outils est accordé à l’étape de signature d’offres du cycle de vie du CDE. Coordonnez-vous avec votre équipe Adobe.
- **Questionnaire de définition de la portée terminé** — Un questionnaire de définition de la portée est rempli lors de la découverte du CDE pour vérifier que la migration est faisable avec les fonctionnalités actuelles de l’outil et pour évaluer l’empreinte et la complexité des données. Assurez-vous d’avoir terminé avec votre équipe Adobe avant de continuer.
- **Aucune donnée HIPAA confirmée** — L&#39;instance source ne doit pas contenir de données réglementées par la loi HIPAA. Confirmez-le avant de continuer.
- **Adresses IP fournies** — Fournissez à votre équipe Adobe la liste des adresses IP statiques à partir desquelles l’outil de migration s’exécutera. Cela est nécessaire pour que l’accès réseau soit configuré côté Adobe.
- **Instance cible configurée** — L&#39;instance [!DNL Adobe Commerce as a Cloud Service] cible doit être configurée avant le début de la migration. Contactez votre équipe Adobe pour confirmer que l’instance est prête.

## Étape 2 : avant d’exécuter la migration

Une fois que vous avez accès à l’outil, préparez les éléments suivants avant de commencer la configuration et l’exécution.

### Machine de migration

L’outil de migration s’exécute sur une machine que vous contrôlez, telle qu’une boîte de saut dédiée. Cette machine doit répondre aux exigences suivantes.

- **[!DNL Docker]et [!DNL Docker Compose] installés** — L&#39;outil est basé sur [!DNL Docker]. `docker` et `docker compose` (ou le `docker-compose` hérité) doivent être installés et fonctionner sur la machine de migration.
- **[!DNL Docker]d&#39;exécution** — L&#39;utilisateur exécutant la migration doit être autorisé à exécuter les commandes [!DNL Docker]. Le [!DNL Linux], l’utilisateur ou l’utilisatrice doit faire partie du groupe `docker`. Sur [!DNL macOS] et [!DNL Windows], les [!DNL Docker Desktop] doivent être en cours d’exécution et accessibles.
- **Répertoire de travail accessible en écriture** — Le répertoire dans lequel l&#39;outil de migration est extrait doit être entièrement accessible en écriture par l&#39;utilisateur de la migration. L’outil écrit des journaux, du cache, des dépendances [!DNL Composer] et des fichiers générés lors de l’exécution.
- **Espace disque suffisant** — Assurez-vous que l&#39;espace disque disponible est suffisant pour les données extraites, les images [!DNL Docker] et la sortie du journal. Les exigences d’espace varient en fonction de la taille de la base de données source.
- **Sources locales : connectivité directe de la base de données à partir de la machine de migration** — Pour les instances sources locales, la machine de migration doit avoir un accès direct au réseau à la base de données source. L’outil n’établit pas automatiquement la connectivité de la base de données locale. Vérifiez que l’hôte, le port et les informations d’identification sont accessibles à partir de la machine de migration avant d’exécuter toute commande de migration.
- **Cloud CLI installé et clé SSH enregistrée** — Pour les instances [!DNL Adobe Commerce on Cloud] source, [Cloud CLI](https://experienceleague.adobe.com/fr/docs/commerce-on-cloud/user-guide/dev-tools/cloud-cli/cloud-cli-overview) doit être installé sur la machine de migration. Votre clé publique SSH doit également être enregistrée dans votre compte. Pour obtenir des instructions, consultez le [Guide de connexions sécurisées](https://experienceleague.adobe.com/fr/docs/commerce-on-cloud/user-guide/develop/secure-connections).

### Instance Source

- **API de magasin Source accessibles** — Les API REST et GraphQL du magasin source doivent être accessibles depuis la machine de migration. Assurez-vous qu’aucune authentification HTTP de base ni restriction réseau ne bloque le trafic API vers l’URL source.
- **Informations d’identification OAuth Source** — L’outil de migration utilise OAuth pour s’authentifier auprès du magasin source. Créez ou confirmez une intégration dans la source [!UICONTROL **Admin**] ([!UICONTROL **Système**] > [!UICONTROL **Extensions**] > [!UICONTROL Integrations]) et préparez la clé du client, le secret du client, le jeton d’accès et le secret du jeton d’accès.
- **Sources PaaS : jeton API Cloud Magento** — Générez un jeton API [!DNL Cloud] à partir des [paramètres du compte Cloud](https://accounts.magento.cloud) sous [!UICONTROL **Paramètres du compte**] > [!UICONTROL **Jetons API**]. Obligatoire uniquement lorsque la source est une instance [!DNL Adobe Commerce on Cloud].
- **Informations d&#39;identification de la base de données Source** — (Sur site uniquement) Préparez les détails de connexion à la base de données source [!DNL MySQL] pour la configuration : `host`, `port`, `user`, `password` et nom de `database`.
- **Possibilité de suspendre cron** — Vous devez pouvoir arrêter cron sur l&#39;instance source pendant la durée de l&#39;extraction des données pour empêcher les écritures simultanées.
- **Possibilité de suspendre les intégrations et les tâches en arrière-plan** — Les intégrations tierces (ERP, OMS, PIM), les tâches planifiées ou les processus en arrière-plan qui écrivent dans la base de données source doivent être suspendus pour la fenêtre d’extraction.
- **Possibilité d’activer et de désactiver le mode de maintenance** — (Migration par phases uniquement) Si vous exécutez une migration par phases avec une fenêtre de maintenance, vous devez pouvoir activer et désactiver le mode de maintenance sur l’instance source.

### Instance cible

- **ID de client et ID d’organisation confirmés** — Obtenez vos `TARGET_TENANT_ID` et `TARGET_ORG_ID` auprès de votre équipe Adobe avant la configuration.
- **Informations d’identification de serveur à serveur OAuth IMS** — Requises pour que l’outil de migration s’authentifie auprès de la cible. Généré via [&#128279;](https://developer.adobe.com/console/). Vous devez disposer d’un accès [!UICONTROL Developer] ou [!UICONTROL Admin] à votre organisation Adobe, car l’accès utilisateur de base n’est pas suffisant pour créer des informations d’identification. Contactez votre équipe Adobe pour sélectionner le profil de produit approprié et préparez l’identifiant client (`ADOBE_IMS_CLIENT_ID`) et le secret client (`ADOBE_IMS_CLIENT_SECRET`).
- **URL du point d’entrée CDMS** — Fournie par votre équipe Adobe. N’essayez pas d’en déduire cette valeur. Vous avez besoin du point d’entrée de pré-production pour les migrations de sandbox et de test, ainsi que du point d’entrée de production pour les migrations de basculement en direct.
- **Configuration de base alignée entre la source et la cible** — Les données de configuration de base, telles que les paramètres de stockage et la configuration système, ne sont pas migrées par l’outil. Configurez-le manuellement sur la cible pour qu’il corresponde à la source avant la migration.
- Stockages **B2B : les fonctionnalités B2B sont configurées de manière cohérente** — Si la source est un magasin compatible B2B, assurez-vous que les paramètres de [!UICONTROL Admin] B2B appropriés sont configurés de manière cohérente à la fois sur la source et la cible avant la migration. Reportez-vous au [guide de migration](migration-guide.md) pour connaître les paramètres spécifiques requis.

### Planification de la migration

- **Approche de migration choisie** — Déterminez quelle approche correspond à votre cas d’utilisation avant de commencer.
  - Migration monophasée : aucun mode de maintenance n’est requis. Convient aux exécutions à sec, aux environnements de développement ou de sandbox, ou à toute migration où la source peut rester active pendant l’extraction.
  - Migration multiphase : le mode de maintenance est requis. Une migration en plusieurs phases est requise pour les migrations de production où la source doit être figée lors de l’extraction afin d’assurer la cohérence des données.
- **Période de maintenance prévue** — S’applique uniquement aux migrations multiphases. Planifiez et communiquez la fenêtre de maintenance à l’avance. L’instance source n’est pas disponible pour les utilisateurs finaux pendant les phases d’extraction et de chargement.
- **Code d’affichage du magasin confirmé** — Identifiez le code d’affichage du magasin (`STORE_CODE`) sur l’instance source. La valeur par défaut est `default` mais doit correspondre au code réel dans [!UICONTROL Admin] > [!UICONTROL Stores] > [!UICONTROL All Stores]. Un code de magasin incorrect peut affecter les opérations de données lors de la migration.

Après avoir confirmé tous les éléments, vous êtes prêt à vérifier l’accès au service avec le [guide d’accès au service de migration](cdms-access.md), puis à commencer les étapes de configuration et d’exécution du [guide de migration](migration-guide.md).
