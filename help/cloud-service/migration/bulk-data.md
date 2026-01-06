---
title: Outil de migration de données en bloc
description: Découvrez comment utiliser l’outil de migration de données en bloc pour migrer les données de votre instance Adobe Commerce on Cloud existante vers  [!DNL Adobe Commerce as a Cloud Service].
feature: Cloud
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
role: Developer
level: Intermediate
exl-id: 81522de9-df54-4651-b8ed-58956376af86
source-git-commit: 06bdcfbff5d376064b18bdab3945e7609075b8bc
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 0%

---

# Outil de migration de données en bloc

L’outil de migration de données en masse suit une architecture distribuée qui permet une migration sécurisée et efficace des données de PaaS vers des environnements SaaS. Cet outil permet aux personnes en charge de l’implémentation de la solution de migrer les données d’une instance Adobe Commerce on Cloud existante (PaaS) vers une instance [!DNL Adobe Commerce as a Cloud Service] (SaaS). Pour plus d’informations sur le processus de migration, consultez la [présentation de la migration](./overview.md).

>[!NOTE]
>
>L’outil de migration de données en bloc prend uniquement en charge la migration des données commerciales de base propriétaires. La migration de données personnalisées n’est actuellement pas prise en charge.

L’image suivante présente l’architecture et les composants clés pour l’utilisation de l’outil de migration de données en bloc.

![Diagramme d’architecture de l’outil de migration de données en bloc présentant le flux de données PaaS vers SaaS](../assets/bulk-data-diagram.png){zoomable="yes"}

## Workflow de migration

Le workflow de migration des données en masse comprend les étapes suivantes :

1. Configurez un nouvel environnement pour la migration.
1. Copiez les données de l’ancien système.
1. Déplacez vos données vers le nouveau système.
1. Rendez votre catalogue de produits disponible dans le nouveau système.
1. Vérifiez que vos données ont été correctement migrées.

Les sections suivantes décrivent ces étapes en détail.

## Accès à l’outil de migration de données en bloc

La disponibilité de l’outil de migration de données en bloc est la suivante :

- **T4 2025** (pas encore disponible) - Après la version initiale de l’outil de migration de données en masse, vous pourrez y accéder en soumettant un ticket d’assistance.
- **T4 2025** (pas encore disponible) - Après la publication publique de l’outil de migration de données en masse, il sera accessible à partir de cette page.

## Créer un environnement cible

Le programme de mise en œuvre de solutions (SI) crée un environnement cible pour la migration. Cet environnement stocke les données migrées à partir de l’instance source.

Tout d’abord, [créez une nouvelle instance  [!DNL Adobe Commerce as a Cloud Service] (SaaS)](../getting-started.md#create-an-instance).

### Configuration de l’outil d’extraction

Utilisez l’outil d’extraction pour extraire des données de l’instance source.

1. Téléchargez l’outil d’extraction à partir du lien fourni par Adobe.
1. Définissez les variables d’environnement suivantes dans l’outil d’extraction :
   - Détails de connexion à votre base de données MySQL existante
   - Identifiant client cible pour votre instance [!DNL Adobe Commerce as a Cloud Service]
   - Vos informations d’identification IMS, notamment :
      - Identifiant client
      - Secret client
      - Portées IMS
      - URL IMS : URL de base. Par exemple, `https://ims-na1.adobelogin.com/`.
      - Identifiant de l’organisation IMS

   Pour les étendues IMS et d’autres valeurs, sélectionnez votre type OAuth dans la section **Informations d’identification** au sein de votre projet dans le [Adobe Developer Console](https://developer.adobe.com/console/). Vous trouverez plus d’informations dans le fichier `.example.env` inclus avec l’outil d’extraction.

### Extraire les données

Avant d’exécuter l’outil d’extraction, le responsable de la mise en œuvre de la solution doit établir un tunnel SSH vers la base de données PaaS à l’aide de :

```bash
magento-cloud tunnel:open
```

Exécutez ensuite l’outil d’extraction qui :

1. Connectez-vous à la base de données PaaS, analysez son schéma et comparez-le aux détails du schéma du client SaaS.
1. Générer un plan d&#39;extraction et de transformation basé sur les éléments de schéma communs entre PaaS et SaaS.
1. Extrayez les données à l’aide du service de gestion des données de catalogue (CDMS).

### Charger les données

Exécutez l’outil de chargement de données fourni par Adobe. Cet outil :

1. Connectez-vous à la base de données du client SaaS à l’aide d’un compte de migration.
1. Générer un plan de chargement.
1. Exécutez le plan en déplaçant les données par lots vers la base de données cliente SaaS.
1. Traitez les supports du catalogue et transférez-les vers l’environnement cible.
1. Videz le cache Redis SaaS et invalidez les index de base de données pour le client.

### Ingestion des données de catalogue

Une fois les données chargées, elles sont automatiquement transférées de la base de données du client SaaS vers le service de catalogue.

Le service de catalogue partage ces données avec Live Search et les recommandations de produits. Aucune intervention manuelle n’est nécessaire pour ce processus. Les données sont disponibles dans tous les services une fois l’ingestion terminée.

### Vérification de l&#39;intégrité des données

Après la migration, CDMS effectue les contrôles automatiques d’intégrité des données suivants pour s’assurer de la précision et de l’exhaustivité des données migrées :

**Vérification basée sur les API**

Lors de la vérification, le système de gestion de la cohérence des données compare les réponses de l’API REST et GraphQL des requêtes précédemment exécutées aux enregistrements correspondants de l’instance cible. Toutes les incohérences sont visibles dans le statut de migration.

**Vérification au niveau de la base**

Lors de la vérification, le CDMS compte le nombre d’enregistrements extraits et compare ce nombre à la quantité d’enregistrements chargés.

**Vérification à la demande (facultatif)**

Vous pouvez également déclencher manuellement une vérification complète de tous les enregistrements système :

>[!NOTE]
>
>Ce processus nécessite de nombreuses ressources et ne doit être utilisé que dans les environnements Sandbox.

La vérification complète comprend :

- Effectuer une vérification basée sur l’API à l’aide de toutes les réponses API REST et GraphQL pré-extraites
- Rapport détaillé de toutes les incohérences détectées
