---
title: '[!DNL SaaS Data Export Guide]'
description: Découvrez comment utiliser l [!DNL data export] extension pour les services SaaS Adobe Commerce qui synchronise les données entre Adobe Commerce et les services Commerce connectés.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: 8a0067ba-90a4-48a6-8276-208d09abe6fc
TQID: https://experienceleague.adobe.com/OHE1GBUEd8hHFPwFlO9fJa3Y0wK2xZ0HOYnwUn0-DSk
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088bid: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2: id: c1256247-af4b-46d8-9dca-0c654ecfa157id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 402
ht-degree: 0%

---

# Guide [!DNL SaaS Data Export]

[!DNL SaaS data export] synchronise les données entre une instance Adobe Commerce et les services Commerce connectés. Lorsque vous ajoutez Live Search, Product Recommendations, Catalog Service ou l’[!DNL Adobe Commerce Optimizer Connector] à une installation Adobe Commerce, l’extension [!DNL Data Export] est installée automatiquement.

>[!NOTE]
>
>Si vous installez le [!DNL Adobe Commerce Optimizer Connector], la même extension [!DNL Data Export] collecte les flux de catalogue et de prix de [!DNL Adobe Commerce]. Le connecteur mappe ensuite et envoie ces flux aux [!DNL Adobe Commerce Optimizer] à l’aide du modèle de données de catalogue composable (CCDM). Consultez les sections [[!DNL Adobe Commerce Optimizer Connector] présentation](../aco-connector/overview.md) pour la configuration et l’architecture, et [Pipeline de synchronisation du connecteur](../aco-connector/connector-sync-pipeline.md) pour connaître le comportement de synchronisation après l’exportation.

L’exportation de données SaaS collecte et exporte divers types de données, appelés _flux_, qui agrègent des types spécifiques d’informations. Selon les services Commerce installés, les flux d’exportation de données SaaS incluent :

- **Flux d’entité de catalogue** agréger les données de produit. Les données incluent les produits, les attributs de produit, les prix de produit, les variations de produit, les catégories, les autorisations de catégorie et les autorisations de produit.
- Le **flux Portées** regroupe des données pour les groupes de clients, les sites web, les boutiques et les vues de boutique.
- Le **flux de commande client** regroupe les données de commande, y compris leurs entités associées telles que les factures, les expéditions, les avoirs, etc.
- Le **flux Inventaire multi-Source** regroupe des données sur les éléments de statut du stock.

L&#39;export de données SaaS est fourni sous la forme d&#39;une extension PHP qui prend en charge la synchronisation automatique et manuelle :

- **Synchronisation automatisée** : après la synchronisation complète initiale lorsque vous connectez un service Commerce, les tâches cron maintiennent les services connectés à jour à l’aide d’une synchronisation partielle et d’une reprise automatique des éléments ayant échoué, sans aucune action requise de la part de l’utilisateur administrateur ou de l’intégrateur système.

- **Synchronisation manuelle** : exécutez une resynchronisation complète ou resynchronisez les flux sélectionnés à partir de l’interface de ligne de commande Commerce Admin ou de l’[interface de ligne de commande Commerce](data-export-cli-commands.md).

- **Surveillance** : suivez l’intégrité, le statut et la diffusion des flux depuis la page [!UICONTROL Data Feed Sync Status] et le tableau de bord de gestion des données de l’administrateur Commerce. Voir [Gérer la synchronisation](data-sync-manage.md) pour connaître les étapes de vérification et de resynchronisation.

Pour le comportement de synchronisation, les modes et le diagramme de flux d’exportation, consultez [Fonctionnement de la synchronisation](sync-overview.md).

L’exportation des données SaaS fournit également des outils pour planifier et résoudre les problèmes liés au processus de synchronisation :

- **Planification et performances**—Estimez le temps de synchronisation pour planifier le traitement et éviter les interruptions du site, et personnalisez le traitement des exportations pour améliorer les performances. Voir [ Estimer le volume et la durée de transmission des données](estimate-data-volume-sync-time.md) et [ Améliorer les performances d’exportation des données](customize-export-processing.md).

- **Suivi et dépannage** : consultez l’état de synchronisation et les payloads de flux à l’aide des journaux d’exportation de données et saas. Voir [Vérification des journaux et dépannage](troubleshooting/logging.md).

>[!MORELIKETHIS]
>
> - [Étendre et personnaliser les flux d’exportation de données SaaS](extensibility-and-customizations.md) — Ajouter ou modifier des données de flux.
> - [Scénarios de dépannage ](troubleshooting/troubleshooting-scenarios.md) — Diagnostiquez les erreurs de configuration et les résultats de synchronisation inattendus.
> - [Notes de mise à jour](release-notes.md) — Mises à jour des extensions et problèmes connus.
