---
title: '[!DNL SaaS Data Export Guide]'
description: Découvrez comment utiliser l [!DNL data export] extension pour les services SaaS Adobe Commerce qui synchronise les données entre Adobe Commerce et les services Commerce connectés.
role: Admin, Developer
exl-id: 8a0067ba-90a4-48a6-8276-208d09abe6fc
TQID: https://experienceleague.adobe.com/OHE1GBUEd8hHFPwFlO9fJa3Y0wK2xZ0HOYnwUn0-DSk
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 2a09ef51939649a12b72c45cbb8b0dc0d0a4c8ad
workflow-type: tm+mt
source-wordcount: 571
ht-degree: 0%

---

# Guide [!DNL SaaS Data Export]

[!DNL SaaS data export] synchronise les données entre une instance Adobe Commerce et les services Commerce connectés. Lorsque vous ajoutez Live Search, Product Recommendations, Catalog Service ou l’[!DNL Adobe Commerce Optimizer Connector] à une installation Adobe Commerce, l’extension [!DNL Data export] est installée automatiquement.

>[!NOTE]
>
>Si vous installez le [!DNL Adobe Commerce Optimizer Connector], la même extension [!DNL Data Export] collecte les flux de catalogue et de prix de [!DNL Adobe Commerce]. Le connecteur mappe ensuite et envoie ces flux aux [!DNL Adobe Commerce Optimizer] à l’aide du modèle de données de catalogue composable (CCDM). Consultez les sections [[!DNL Adobe Commerce Optimizer Connector] présentation](../aco-connector/overview.md) pour la configuration et l’architecture, et [Pipeline de synchronisation du connecteur](../aco-connector/connector-sync-pipeline.md) pour connaître le comportement de synchronisation après l’exportation.

L’exportation de données SaaS collecte et exporte divers types de données, appelés _flux_, qui agrègent des types spécifiques d’informations. Selon les services Commerce installés, les flux d’exportation de données SaaS incluent :

- **Flux d’entité de catalogue** agréger les données de produit. Les données incluent les produits, les attributs de produit, les prix de produit, les variations de produit, les catégories, les autorisations de catégorie et les autorisations de produit.
- Le **flux Portées** regroupe des données pour les groupes de clients, les sites web, les boutiques et les vues de boutique.
- Le **flux de commande client** regroupe les données de commande, y compris leurs entités associées telles que les factures, les expéditions, les avoirs, etc.
- Le **flux Inventaire multi-Source** regroupe des données sur les éléments de statut du stock.

L&#39;export de données en SaaS est livré sous forme d&#39;extension PHP. Il prend en charge plusieurs méthodes pour lancer et gérer le processus de synchronisation des données.

- **Synchronisation manuelle depuis l’Admin ou la ligne de commande**

   - Le [tableau de bord de gestion des données](https://experienceleague.adobe.com/fr/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard) de l’administration Commerce fournit une vue graphique de l’état de synchronisation qui indique les données de produit synchronisées avec succès avec les services Commerce. Vous pouvez utiliser le tableau de bord pour effectuer une resynchronisation complète (_synchronisation complète_) de tous les flux. Cependant, Adobe recommande de n’effectuer une synchronisation complète que la première fois que vous connectez Adobe Commerce à un service Commerce. Voir [Processus de synchronisation](data-synchronization.md).

     {{aco-data-sync-verification}}

   - La page [Statut de synchronisation des flux de données](https://experienceleague.adobe.com/fr/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) fournit des informations en temps réel sur l’intégrité et les performances des flux d’exportation de données qui transfèrent les données de produit et de catégorie de Commerce vers des services externes tels que les recommandations de produits, la recherche en direct et le service de catalogue, ou Adobe Commerce Optimizer.

   - L’outil de ligne de commande [Adobe Commerce &#x200B;](https://experienceleague.adobe.com/fr/docs/commerce-operations/configuration-guide/cli/config-cli) (CLI) fournit des commandes pour synchroniser des flux spécifiques et inclut des options supplémentaires pour personnaliser le traitement des flux.

- **Synchronisation automatisée avec les tâches cron**

   - [Synchronisation partielle des données](data-synchronization.md#partial-sync) : les tâches cron déclenchent une synchronisation partielle des données lorsqu’un utilisateur administrateur Commerce met à jour une entité. Le processus d’exportation des données envoie uniquement ces mises à jour aux services Commerce connectés. Le processus de synchronisation partielle est basé sur le mécanisme MView et ne nécessite aucune action de la part de l’utilisateur administrateur ou de l’intégrateur système.

   - [Reprise automatique en cas d&#39;erreur de synchronisation](data-synchronization.md#retry-failed-items-sync) : les traitements Cron déclenchent une reprise automatique du processus de synchronisation lorsque des erreurs se produisent au cours du processus de synchronisation des données.

- **Exporter la planification et les performances**

   - Les développeurs et les intégrateurs système peuvent estimer le temps nécessaire à l&#39;export des données SaaS pour synchroniser les données entre Adobe Commerce et les services connectés. Cette estimation peut vous aider à planifier le traitement de l’exportation des données afin d’éviter toute perturbation du site. Voir [&#x200B; Estimer le volume de données et la durée de transmission](estimate-data-volume-sync-time.md).

   - Dans les cas où la synchronisation doit se produire plus rapidement, l’exportation des données SaaS fournit des options de personnalisation pour améliorer les performances de traitement des exportations. Voir [Amélioration des performances d’exportation des données](customize-export-processing.md).

- **Suivre et résoudre les problèmes liés aux activités d’exportation de données** : utilisez les journaux data-export et saas-export pour consulter l’état de synchronisation et les payloads des flux pendant le processus de synchronisation et d’indexation. Voir [Journalisation et dépannage](troubleshooting-logging.md).
