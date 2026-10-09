---
title: Surveiller la synchronisation des vues de catalogue pour les catalogues partagés B2B
last-update: 2026-09-03T00:00:00.000Z
description: Utilisez la page État de synchronisation de la vue Catalogue pour surveiller et réconcilier la vue Catalogue, la politique, la référence du catalogue et les données de configuration clés synchronisées avec Adobe Commerce Optimizer.
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="PaaS uniquement" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
subfeature_v2:
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
    internal-label: Data Transfer
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
    internal-label: Data management
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
source-git-commit: 76e77db86adecdbd3be76040970c0d0899c34cdc
workflow-type: tm+mt
source-wordcount: '1046'
ht-degree: 0%
---

# Surveiller la synchronisation des vues de catalogue pour les catalogues partagés B2B

Effectuez le suivi de la synchronisation des vues du catalogue B2B de [!DNL Adobe Commerce] à [!DNL Adobe Commerce Optimizer] à l’aide du tableau de bord [!UICONTROL Catalog View Sync Status] dans Commerce Admin.

[!UICONTROL Catalog View Sync Status] vérifie que les configurations vue catalogue, politique, référence du catalogue et clé d’accès restreint pour chaque catalogue partagé B2B existent dans [!DNL Adobe Commerce Optimizer] et correspondent à votre configuration [!DNL Adobe Commerce]. Pour effectuer plutôt le suivi de la synchronisation des flux de produits, de prix et de catégories, voir [Gérer la synchronisation des données](data-sync-status.md#verify-that-the-data-sync-is-working).

## Accès à la page du statut de synchronisation {#access-the-sync-status-page}

Dans l’administration Commerce, accédez à **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Catalog View Sync Status]**.

![Page Statut de synchronisation de l’affichage du catalogue pour surveiller le statut de synchronisation de la vue du catalogue, de la politique, du catalogue des prix et des configurations des clés d’accès dans Adobe Commerce Optimizer](assets/catalog-view-sync-status.png){width="600" zoomable="yes"}

La page comporte trois onglets : [!UICONTROL Catalog Views], [!UICONTROL Orphaned in ACO] et [!UICONTROL Deleted].

## Interprétation du statut de synchronisation pour vos catalogues partagés {#interpret-sync-status}

Sur l’onglet [!UICONTROL Catalog View] , chaque ligne représente une vue de catalogue partagée personnalisée projetée à partir d’une combinaison de vues de catalogue et de magasin partagée. La projection correspond à la vue de catalogue, à la politique, à la référence du catalogue et aux données de configuration de clé à accès restreint que [!DNL Commerce Optimizer Connector] exporte vers [!DNL Adobe Commerce Optimizer] pour le catalogue partagé. Utilisez les informations de statut pour déterminer si les données diffusées à l’expérience storefront de l’entreprise sont complètes et correctes. Le tableau suivant résume les valeurs de statut les plus courantes et leur signification pour votre catalogue partagé :

| Statut | Signification pour votre catalogue partagé |
| --- | --- |
| **Dégradé** | Quelque chose a été modifié directement en [!DNL Adobe Commerce Optimizer], par exemple, la politique ou le carnet de prix lié. Il se peut que la société ne voie pas le bon assortiment ou le mauvais prix jusqu’à ce que vous résolviez le problème. Cela peut également se produire si la clé d’accès, le nom de la vue ou la source est modifié dans Commerce Optimizer. |
| **Échec** | La vue catalogue n’existe pas dans [!DNL Adobe Commerce Optimizer] ou si le délai de grâce expire avant que la première projection ne soit effectuée. (Voir [Configurer les paramètres de synchronisation des vues du catalogue ACO](#configure-aco-catalog-view-sync-settings)). Si un statut de synchronisation de catalogue est `Failed`, l’entreprise ne peut pas accéder à l’expérience de storefront de ce catalogue partagé. |
| **Retrait** | Vous avez supprimé le catalogue partagé dans [!DNL Adobe Commerce]. La vue du catalogue reste accessible jusqu’à l’expiration du délai de grâce de suppression. La période de grâce par défaut est de sept jours. Vous pouvez modifier la valeur par défaut en mettant à jour les [paramètres de synchronisation des vues de catalogue](#configure-aco-catalog-view-sync-settings). |
| **Orphelin** | La vue ou la clé du catalogue a été créée directement dans [!DNL Adobe Commerce Optimizer] Studio, et non par le connecteur. Voir [Vérifier les entrées orphelines et supprimées](#review-orphaned-and-deleted-entries). |

[!UICONTROL Healthy], [!UICONTROL Pending] et [!UICONTROL Deleted] sont des états informatifs qui ne nécessitent aucune action. Pour obtenir la liste complète[&#128279;](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/catalog-view-sync/catalog-view-sync-status#sync-status-values){target="_blank"} consultez la section Valeurs de statut de synchronisation dans le Guide d’administration de Commerce **.

### Configurer les paramètres de synchronisation de la vue Catalogue ACO {#configure-aco-catalog-view-sync-settings}

Depuis l’administrateur [!DNL Adobe Commerce] (et non [!DNL Adobe Commerce Optimizer] Studio), accédez à **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Services]** > **[!UICONTROL ACO Catalog View Sync]** pour contrôler la manière dont le connecteur multiplie les suppressions et les créations, et s’il répare les dérives automatiquement.

![Page de configuration de la synchronisation de la vue Catalogue ACO affichant les sections Suppression, Création et Réconciliateur de dérive](assets/aco-catalog-view-sync-configuration.png){width="600" zoomable="yes"}

- **[!UICONTROL Deletion Grace Period (days)]** : nombre de jours pendant lesquels la vue de catalogue, la politique et les métadonnées d&#39;un catalogue partagé supprimé sont conservées dans [!DNL Adobe Commerce Optimizer] avant d&#39;être supprimées. La valeur par défaut est de sept jours. Définissez cette option sur `0` pour supprimer immédiatement la projection, sans délai de grâce.

- **[!UICONTROL Creation Grace Period (days)]** : nombre de jours pendant lesquels une vue de catalogue nouvellement enregistrée peut attendre que sa première projection [!DNL Adobe Commerce Optimizer] lorsqu&#39;elle est signalée comme [!UICONTROL Pending]. Si le délai de grâce expire sans projection, le statut devient [!UICONTROL Failed]. La valeur par défaut est 1.

- **[!UICONTROL Enabled]** (réconciliateur de dérive) : exécute le réconciliateur de dérive planifié qui compare les [!DNL Adobe Commerce Optimizer] à l&#39;état de projection [!DNL Adobe Commerce] et répare ou signale la divergence.

- **[!UICONTROL Automatically Repair Drift]** : lorsqu&#39;elle est définie sur **[!UICONTROL Yes]**, l&#39;exécution planifiée converge [!DNL Adobe Commerce Optimizer] vers [!DNL Adobe Commerce] pour une dérive réparable. Lorsque la valeur est définie sur **[!UICONTROL No]**, l’exécution planifiée détecte et consigne uniquement la dérive ; les entrées orphelines sont toujours signalées et ne sont jamais supprimées automatiquement. Ce paramètre affecte uniquement le réconciliateur planifié. L’action **[!UICONTROL Reconcile & Repair]** sur cette page répare toujours la dérive. Voir [&#x200B; Choisir la surveillance ou la réparation](#choose-monitoring-or-repair).

Voir [Configuration de la synchronisation des vues du catalogue ACO](https://experienceleague.adobe.com/en/docs/commerce-admin/configuration-reference/services/aco-catalog-view-sync.md) dans le guide de *[!DNL Commerce Admin]* pour plus d’informations sur chaque paramètre.

## Choisir la surveillance ou la réparation {#choose-monitoring-or-repair}

[!DNL Adobe Commerce] est toujours la source de vérité pour la vue de catalogue, la politique, le catalogue de prix et les configurations clés pour les catalogues partagés B2B. Si vous ou un autre administrateur modifiez une politique, un catalogue de prix ou un paramètre de configuration clé directement dans [!DNL Adobe Commerce Optimizer] Studio, la réconciliation signale que les différences de configuration dérivent.

- Sélectionnez **[!UICONTROL Reconcile]** pour vérifier la dérive sans rien changer, afin que vous puissiez examiner les différences avant d’agir.
- Sélectionnez **[!UICONTROL Reconcile & Repair]** pour restaurer la configuration attendue pour toute dérive réparable.

Pour examiner ce qui a changé et pourquoi, ouvrez la page détaillée d’une vue de catalogue et vérifiez son historique de dérive.

## Vérifier les entrées orphelines et supprimées {#review-orphaned-and-deleted-entries}

Les onglets **[!UICONTROL Orphaned in ACO]** et **[!UICONTROL Deleted]** couvrent deux cas que le connecteur ne peut pas réparer automatiquement, car il n’existe aucun catalogue partagé [!DNL Adobe Commerce] à réconcilier :

- **[!UICONTROL Orphaned in ACO]** : le connecteur signale les entités orphelines dans l&#39;état de synchronisation et lors de la réconciliation de dérive. Il ne les adopte pas et ne les supprime pas automatiquement même si la réconciliation s&#39;exécute avec la réparation activée.

  Une entité est orpheline lorsqu’elle existe dans [!DNL Adobe Commerce Optimizer] mais que le connecteur ne la suit pas ou ne l’associe pas à une vue de catalogue suivie. Cela peut se produire lorsqu&#39;une entité est créée manuellement, par une autre intégration, ou abandonnée après une opération de connecteur interrompue.

  - **Vues catalogue** : le connecteur ne suit pas la vue. Sélectionnez le lien Vue du catalogue pour ouvrir la page de détails Vue du catalogue dans [!DNL Adobe Commerce Optimizer] Studio. Si la vue de catalogue n’est plus nécessaire, supprimez-la.

  - **Clés d&#39;accès restreint** : aucune vue de catalogue dynamique ne fait référence à la clé. Sélectionnez le lien Vue du catalogue pour ouvrir la page de détails Vue du catalogue dans [!DNL Adobe Commerce Optimizer] Studio. Vérifiez la clé d’accès configurée et supprimez-la si elle n’est plus nécessaire.

  - **Politiques** : le connecteur ne suit pas la politique et aucune vue de catalogue en direct ne la référence. Sélectionnez le lien de la politique pour l’ouvrir dans [!DNL Adobe Commerce Optimizer] Studio.  Examinez-le et supprimez-le s’il n’est plus nécessaire.

- **[!UICONTROL Deleted]** : vous avez supprimé un catalogue partagé dans [!DNL Adobe Commerce], puis sa projection de vue de catalogue a été supprimée. Ces lignes sont conservées pendant 90 jours comme enregistrement de ce qui a été supprimé.

>[!MORELIKETHIS]
>
> - [Surveillance de l’état de synchronisation des vues du catalogue](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/catalog-view-sync-status.md){target="_blank"} — Référence complète à la documentation pour la page État de synchronisation des vues du catalogue, dans le *Guide d’administration de Commerce* —>
> - [Gérer la synchronisation des données](data-sync-status.md) — Vérifier la synchronisation des flux de produits, de prix et de catégories
> - [Vues de catalogue privé](/help/optimizer/setup/private-catalog-view.md) — Découvrez ce qu’est une vue de catalogue privé gérée par connecteur
> - [Clés d&#39;accès restreint](/help/optimizer/setup/restricted-access-keys.md) — Découvrez le fonctionnement des clés gérées par le connecteur
> - [Surveiller les modifications du catalogue partagé B2B](get-started-b2b-shared-catalogs.md#monitor-b2b-shared-catalog-changes) — Découvrez ce que le connecteur automatise pour les catalogues partagés B2B
