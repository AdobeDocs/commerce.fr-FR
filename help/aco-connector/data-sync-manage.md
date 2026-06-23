---
title: Gérer [!DNL Adobe Commerce Optimizer Connector] Synchroniser
description: Découvrez comment vérifier la synchronisation des données de catalogue et resynchroniser manuellement les flux du connecteur entre [!DNL Adobe Commerce] et [!DNL Adobe Commerce Optimizer].
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="PaaS uniquement" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2: id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: c32adafa-ed01-4b31-997e-2413013911b0id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
subfeature_v2: id: a40ebd6b-b542-4432-a730-1803ef74518d
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 0bfd368c50707692c7a0adda6e70e3776bd9692a
workflow-type: tm+mt
source-wordcount: 349
ht-degree: 0%

---

# Gestion de la synchronisation avec [!DNL Commerce Optimizer]

Une fois le [!DNL Adobe Commerce Optimizer Connector] configuré, la plupart des mises à jour du catalogue se synchronisent automatiquement par le biais de tâches cron planifiées. Pour plus d’informations sur le fonctionnement de la synchronisation automatisée, voir [Pipeline de synchronisation du connecteur](connector-sync-pipeline.md). Utilisez les outils de cette rubrique pour vérifier que les données atteignent [!DNL Adobe Commerce Optimizer] et resynchroniser manuellement les flux si nécessaire.

## Vérifier que la synchronisation des données fonctionne {#verify-that-the-data-sync-is-working}

{{$include /help/_includes/aco-connector/verify-optimizer-data-sync.md}}

## resynchroniser manuellement les données {#manually-resync-data}

Lorsque la synchronisation partielle et la reprise automatique ne résolvent pas les problèmes de synchronisation, vous pouvez resynchroniser manuellement les données du catalogue. L’option que vous choisissez dépend de l’origine du problème et du niveau de contrôle dont vous avez besoin.

| Tâche | Option | Remarques |
| --- | --- | --- |
| Vérifiez le statut de synchronisation et resynchronisez à partir du système en amont lorsque des produits sont manquants. | **resynchronisation du système en amont** | Dans [!DNL Commerce Optimizer], sélectionnez **[!UICONTROL Data Sync]** et vérifiez que les sources de catalogue, les produits, les prix et les attributs attendus s’affichent. Lorsque des produits sont manquants, resynchronisez à partir de l’instance de [!DNL Adobe Commerce] en amont à l’aide de la page **[!UICONTROL Data Feed Sync Status]** ou de l’interface de ligne de commande Commerce (voir les lignes suivantes). |
| Resynchroniser les éléments de flux du connecteur sélectionnés ayant échoué ou posant problème | **[!UICONTROL Data Feed Sync Status]dans Commerce Admin** | Surveillez le statut d’exportation et resynchronisez les éléments de flux du connecteur sélectionnés à partir de l’administrateur Commerce. Voir [Vérifier que la synchronisation des données fonctionne](#verify-that-the-data-sync-is-working). |
| Resynchronisation ciblée d&#39;alimentation de connecteur avec contrôle opérationnel | **Commerce CLI** | Exécutez `saas:resync` à partir de l’instance Adobe Commerce pour les flux du connecteur. Voir [Synchronisation des flux à l’aide de l’interface de ligne de commande Commerce](../data-export/data-export-cli-commands.md) et [Flux pris en charge](reference/connector-reference.md#supported-feeds). |

>[!MORELIKETHIS]
>
> - [Pipeline de synchronisation du connecteur](connector-sync-pipeline.md) — Découvrez comment fonctionnent la synchronisation automatisée, les plannings cron et la gestion des erreurs
> - [Estimer le volume des données et la durée de synchronisation](reference/estimate-data-volume-sync-time.md) — Calculer la durée de synchronisation attendue
> - [Dépannage](troubleshooting.md) — Diagnostiquer les problèmes d’exportation des informations d’identification, de synchronisation et de la portée
> - [Modules de connecteur et points d’entrée de flux](reference/connector-reference.md) — Modules de révision, points d’entrée d’API et flux pris en charge
> - [Page Statut de synchronisation des flux de données dans l’administration Commerce](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status){target="_blank"} — En savoir plus sur les champs et les fonctionnalités disponibles pour surveiller le statut des flux
> - [Tableau de bord de synchronisation des données dans [!DNL Commerce Optimizer]](https://experienceleague.adobe.com/en/docs/commerce-optimizer/data-sync/data-sync){target="_blank"} — Documentation de référence pour les champs et actions disponibles pour surveiller la synchronisation des données du catalogue
