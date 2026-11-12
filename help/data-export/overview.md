---
title: '[!DNL SaaS Data Export Guide]'
description: Découvrez comment utiliser l’extension [!DNL data export] pour les services Adobe Commerce SaaS qui synchronisent les données entre Adobe Commerce et les services Commerce connectés.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: 8a0067ba-90a4-48a6-8276-208d09abe6fc
TQID: https://experienceleague.adobe.com/OHE1GBUEd8hHFPwFlO9fJa3Y0wK2xZ0HOYnwUn0-DSk
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
feature_v2:
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
    internal-label: Data management
source-git-commit: 672e67ef99d52c942013a880ecfec0da31e76756
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 5%
---
# Guide [!DNL SaaS Data Export]

[!DNL SaaS data export] synchronise les données entre une instance Adobe Commerce et les services Commerce connectés. Lorsque vous ajoutez Live Search, Product Recommendations, Catalog Service ou [!DNL Adobe Commerce Optimizer Connector] à une installation Adobe Commerce, l’extension [!DNL Data Export] est installée automatiquement.

>[!NOTE]
>
>Si vous installez [!DNL Adobe Commerce Optimizer Connector], la même extension [!DNL Data Export] collecte les flux de catalogue et de prix de [!DNL Adobe Commerce]. Le connecteur mappe ensuite et envoie ces flux à [!DNL Adobe Commerce Optimizer] à l’aide du modèle de données de catalogue composable (CCDM). Consultez la [[!DNL Adobe Commerce Optimizer Connector] présentation](../aco-connector/overview.md) pour la configuration et l’architecture, et le [Pipeline de synchronisation du connecteur](../aco-connector/connector-sync-pipeline.md) pour le comportement de synchronisation après l’exportation.

L&#39;exportation de données SaaS collecte et exporte divers types de données, appelés _flux_, qui regroupent des types spécifiques d&#39;informations. Selon les services Commerce installés, les flux d’exportation de données SaaS incluent :

- **Flux d’entités de catalogue** données agrégées de produits. Les données incluent les produits, les attributs de produit, les prix de produit, les variations de produit, les catégories, les autorisations de catégorie et les autorisations de produit.
- Le flux **Étendues** agrège les données pour les groupes de clients, les sites Web, les magasins et les vues de magasin.
- Le flux de **commandes client** agrège les données de commande, y compris leurs entités associées telles que les factures, les expéditions, les avoirs, etc.
- Le **flux Multi-Source Inventory** agrège les données sur les éléments de statut du stock.

L&#39;export de données SaaS est fourni sous la forme d&#39;une extension PHP qui prend en charge la synchronisation automatique et manuelle :

- **Synchronisation automatisée** : après la synchronisation complète initiale lorsque vous connectez un service Commerce, les tâches cron maintiennent les services connectés à jour à l’aide d’une synchronisation partielle et d’une reprise automatique des éléments ayant échoué, sans aucune action requise de la part de l’utilisateur administrateur ou de l’intégrateur système.

- **Synchronisation manuelle** : exécutez une resynchronisation complète ou resynchronisez les flux sélectionnés à partir de l’interface de ligne de commande Commerce Admin ou de l’[interface de ligne de commande Commerce](data-export-cli-commands.md).

- **Surveillance** : suivez l’intégrité, le statut et la diffusion des flux depuis la page [!UICONTROL Data Feed Sync Status] et le tableau de bord de la gestion des données dans l’administration Commerce. Voir [Gérer la synchronisation](data-sync-manage.md) pour les étapes de vérification et de resynchronisation.

Pour connaître le comportement de synchronisation, les modes et le diagramme de flux d&#39;exportation, consultez [Fonctionnement de la synchronisation](sync-overview.md).

L’exportation des données SaaS fournit également des outils pour planifier et résoudre les problèmes liés au processus de synchronisation :

- **Planification et performances** : estimez le temps de synchronisation pour planifier le traitement et éviter l&#39;interruption du site, et personnalisez le traitement des exportations pour améliorer les performances. Voir [Estimer le volume de données et la durée de transmission](estimate-data-volume-sync-time.md) et [Améliorer les performances d’exportation des données](customize-export-processing.md).

- **Suivi et dépannage** : consultez le statut de synchronisation et les payloads de flux à l’aide des journaux d’exportation de données et d’exportation saas. Voir [Vérification des journaux et résolution des problèmes](troubleshooting/logging.md).

>[!MORELIKETHIS]
>
> - [Étendre et personnaliser les flux d’exportation de données SaaS](extensibility-and-customizations.md) — Ajouter ou modifier des données de flux.
> - [Scénarios de dépannage](troubleshooting/troubleshooting-scenarios.md) — Diagnostiquer les erreurs de configuration et les résultats de synchronisation inattendus.
> - [Notes de mise à jour](release-notes.md) — Mises à jour d’extensions et problèmes connus.
