---
title: Outil de migration de données en bloc
description: Découvrez comment utiliser l’outil de migration de données en bloc pour migrer les données de votre instance Adobe Commerce on Cloud existante vers  [!DNL Adobe Commerce as a Cloud Service].
feature: Cloud
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
role: Developer
level: Intermediate
exl-id: 81522de9-df54-4651-b8ed-58956376af86
autotag-review: '2026-07-22T19:18:39.433Z'
TQID: 'https://experienceleague.adobe.com/tkCFabZpBKu-W34wsufHlVIWzCUE8FKm4kK7qZahxBU'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
subfeature_v2: id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 4c0eca0039bab7d015144dd9ac3885a0b2be0563
workflow-type: tm+mt
source-wordcount: 924
ht-degree: 0%

---

# Outil de migration de données en bloc

>[!IMPORTANT]
>
>L’outil de migration de données en masse est actuellement en accès anticipé. L’accès est fourni exclusivement par le biais du processus d’engagement de l’ingénierie déployée (CDE) Commerce.

L’outil de migration de données en masse permet aux intégrateurs système de migrer les données commerciales de base propriétaires des installations [!DNL Adobe Commerce on Cloud] ou locales vers [!DNL Adobe Commerce as a Cloud Service].

L’outil de migration de données en masse est une interface de ligne de commande Docker que les intégrateurs système exécutent sur leur propre ordinateur de migration. Il se connecte à l’instance source, extrait les données commerciales de base propriétaires, les charge dans le service de migration Adobe (service de migration de données Commerce) et surveille la progression jusqu’à la fin.

Toutes les commandes sont exécutées localement, de sorte que vous contrôlez le moment où la migration démarre, le moment où le mode de maintenance est appliqué et le moment où chaque phase s’exécute.

## Workflow de migration

L’outil gère de bout en bout les étapes suivantes :

- **Extraction de données** : extrait les données commerciales de base propriétaires de l’instance source ([!DNL Adobe Commerce on Cloud] ou locale).
- **Chargement des données** — charge les données extraites dans l&#39;instance [!DNL Adobe Commerce as a Cloud Service] cible.
- **Vérification de l&#39;intégrité des données** — effectue des contrôles post-migration automatisés, y compris la comparaison des API REST et GraphQL et la validation du nombre d&#39;enregistrements.

>[!NOTE]
>
>Actuellement, l’outil de migration de données en bloc ne prend en charge que la migration des données commerciales de base propriétaires. La migration de données personnalisées n’est actuellement pas prise en charge. Les paramètres de configuration (paramètres de magasin, configuration du système) ne sont pas migrés automatiquement et doivent être configurés indépendamment sur l’instance cible avant la migration.

## Architecture

L’outil de migration de données en masse suit une architecture distribuée qui permet une migration de données sécurisée et efficace. Cet outil permet aux intégrateurs système de migrer les données d’un [!DNL Adobe Commerce on Cloud or on-premises instance] existant vers [!DNL Adobe Commerce as a Cloud Service]. Pour plus d’informations sur le processus de migration, consultez la [présentation de la migration](../overview.md).

L’image suivante présente l’architecture et le flux de données de bout en bout à l’aide de l’outil de migration de données en bloc.

![Diagramme d’architecture de l’outil de migration de données en bloc présentant le flux de données PaaS vers SaaS](../../assets/bulk-data-diagram.png){zoomable="yes"}

### Composants

| Composant | Rôle |
| --------- | ---- |
| **Outil de migration de données en bloc** | L’interface de ligne de commande Docker que l’intégrateur système exécute sur la machine de migration, qui orchestre le pipeline complet en lisant le schéma et les données de la source, en chargeant les données extraites vers le service de migration d’Adobe et en pilotant les transitions d’état. |
| **Instance de Source (Commerce sur le cloud ou sur site)** | La source de migration. L’outil se connecte par le biais des API REST et GraphQL et d’un tunnel SSH ([!DNL Adobe Commerce on Cloud]) ou d’une connexion directe à la base de données (sur site) pour l’extraction de données. |
| **API Commerce Data Migration Service (CDMS)** | API REST gérée par Adobe qui enregistre les migrations, coordonne les transitions d’état et fournit des points d’entrée sécurisés pour le chargement des données extraites. L’outil de migration se connecte à cette API à l’aide de l’URL du point d’entrée CDMS et des informations d’identification IMS dans votre configuration `.env`. |
| **Programme de travail du service de migration des données Commerce (CDMS)** | Service en arrière-plan géré par Adobe qui charge les données extraites dans l’instance cible et exécute la vérification de l’intégrité après le chargement. |
| **[!DNL Adobe Commerce as a Cloud Service]** | La version SaaS d’Adobe Commerce et votre cible de migration. Reçoit les données chargées et expose les services de catalogue, de recherche en direct et de règles de tarification utilisés lors de la vérification de l’intégrité. |

### Flux de données

Les données se déplacent à travers les composants dans l’ordre suivant :

1. L’outil de migration de données en bloc lit le schéma et les données de la base de données à partir de l’instance source, par le biais d’un tunnel SSH pour la [!DNL Adobe Commerce on Cloud] ou d’une connexion directe à la base de données pour la connexion locale.
1. L’outil enregistre la migration et charge les données extraites via l’API CDMS.
1. Le programme de travail de CDMS charge les données dans le client de [!DNL Adobe Commerce as a Cloud Service] cible.
1. [!DNL Adobe Commerce as a Cloud Service] ingère les données de catalogue chargées et crée l’index de catalogue.
1. Le programme de travail du service de migration des données Commerce (CDMS) vérifie les données chargées par le biais de la comparaison des sommes de contrôle de la base de données, du REST et de GraphQL sur les services suivants :

   - **Catalogue** (GraphQL) — Données de produits et de catégories.
   - **Recherche en direct** (REST) : exactitude de l’index de recherche.
   - **Règles de tarification** (REST) — données de prix et de règles.

1. L’outil interroge le statut de migration tout au long de l’et récupère le rapport de migration final une fois l’opération terminée.


## Cycle de vie de l’engagement

L’accès à l’outil de migration de données en bloc est fourni exclusivement par le biais d’un engagement Commerce Deployed Engineering (CDE). L’outil n’est pas accessible au public.

Le cycle de vie type de l’engagement est le suivant :

1. **Découverte du CDE** - Effectuez l’appel de définition de la portée initial, évaluez l’empreinte et la complexité des données, puis remplissez le questionnaire de définition de la portée.
1. **Signature de l’accord** - L’accord commercial est en place et la portée de la migration est confirmée. À ce stade, vous avez accès à l’outil de migration.
1. **Co-innovation et support de CDE** - Travaillez conjointement avec Adobe pour installer l’outil dans votre environnement et exécuter des migrations de test.
1. **Mise en production** - Exécutez la migration de basculement de production et effectuez la vérification de l’intégrité des données.

## Distribution d&#39;outils

L’outil est distribué dans le cadre de l’engagement du CDE. Votre représentant Adobe fournit le package d’outils, qui comprend :

- L’interface de ligne de commande basée sur Docker et la configuration de build
- Modèle de configuration `.example.env` avec documentation pour toutes les variables d’environnement requises
- Documentation technique complète couvrant l’architecture de l’outil, la référence de configuration, les frameworks de test et de transformation personnalisés, ainsi que les guides de dépannage

Pour obtenir des instructions détaillées sur la configuration et le fonctionnement, reportez-vous à la documentation incluse dans le package de distribution d’outils.

## Guides de migration

Les pages suivantes présentent le cycle de vie complet de la migration, de la préparation à l’exécution. Pour une compréhension complète du processus de migration, examinez-les dans l’ordre suivant :

1. [Liste de contrôle de préparation du client](readiness-checklist.md) — Confirmez les conditions préalables relatives à l’engagement, à la machine de migration, à la source et à la cible avant de demander l’accès aux outils.
1. [Vérifier l’accès au service de migration](cdms-access.md) — Après avoir obtenu l’accès à l’outil, validez l’accessibilité du réseau, l’authentification IMS et l’autorisation du client par rapport à l’API Commerce Data Migration Service (CDMS).
1. [Exécution d’une migration de données en bloc](migration-guide.md) — Configurez l’outil, préparez votre réseau et vos instances, puis lancez la migration.

Pour consulter la référence complète de la configuration, les frameworks de test et de transformation personnalisés, ainsi que des conseils de dépannage, reportez-vous à la documentation incluse dans le package de distribution d’outils.
