---
title: Scénarios de dépannage pour  [!DNL SaaS Data Export]
description: Découvrez comment diagnostiquer et résoudre un comportement  [!DNL SaaS Data Export]  synchronisation inattendu provoqué par une mauvaise configuration, des paramètres de l’indexeur ou une mauvaise interprétation des résultats de synchronisation.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="PaaS uniquement" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
subfeature_v2:
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 991
ht-degree: 0%

---


# Scénarios de dépannage pour [!DNL SaaS Data Export]

Cette page décrit les comportements que vous pouvez observer lors de l’utilisation des [!DNL SaaS Data Export], qui sont généralement causés par une mauvaise configuration ou une mauvaise interprétation des résultats de synchronisation. Utilisez les descriptions ci-dessous pour identifier la cause première et appliquer la résolution appropriée.

## Produit configurable ou groupé manquant dans les services Commerce {#configurable-bundle-missing}

**Problème :** un produit configurable ou groupé a le statut *Activé* dans [!DNL Adobe Commerce] mais n’est pas renvoyé dans le storefront ou s’affiche avec un statut *Désactivé* dans les services SaaS Commerce.

**Cause :** le statut effectif des produits composites dépend du statut de leurs produits enfants, et pas seulement du statut du produit parent. Les services SaaS Commerce reflètent ce statut calculé :

- **Produits configurables** - au moins une variante de produit doit être activée.
- **Lots de produits** - au moins un produit doit être activé pour chaque option de lot requise.

Si ces conditions ne sont pas remplies, le produit parent est traité comme désactivé même si son propre statut est défini sur *Activé*.

**Solution :**

- Pour les produits configurables, vérifiez qu’au moins une variante de produit simple associée est activée et affectée à la vue de site web et de magasin appropriée.
- Pour les produits groupés, vérifiez que chaque option de bundle requise comporte au moins un produit enfant activé. Une option obligatoire avec tous les enfants désactivés entraîne le traitement de l’ensemble du lot comme désactivé.
- Après avoir activé les produits enfants appropriés, déclenchez une resynchronisation ou attendez la prochaine synchronisation planifiée, puis confirmez le statut mis à jour dans les services SaaS Commerce.

## Prix non mis à jour après l’activation de la règle de prix de catalogue {#prices-not-updated}

**Problème :** après l’activation d’une règle de prix de catalogue à l’aide de la fonction Mise à jour planifiée, les prix ne sont pas mis à jour. La `commerce-data-export.log` affiche les `synced: 0` pour `prices` flux après l’application des mises à jour planifiées.

**Cause :** une condition de concurrence peut se produire entre les groupes cron lorsque des mises à jour planifiées sont utilisées pour les règles de prix de catalogue. L’indexeur `catalog_data_exporter_product_prices` peut s’exécuter avant que sa dépendance, l’index `catalogrule_product`, ne soit complètement reconstruite. Par conséquent, l&#39;exportateur de prix lit des données obsolètes et n&#39;exporte aucune modification.

**Solution :**

La solution immédiate à ce problème est une solution : configurez les deux groupes cron pour qu’ils s’exécutent de manière séquentielle afin d’éliminer la condition de concurrence :

1. Accédez à **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Advanced]** > **[!UICONTROL System]** > **[!UICONTROL Cron (Scheduled Tasks)]**.
1. Définissez **[!UICONTROL Use Separate Process]** sur **[!UICONTROL No]** pour les deux :
   - Options de configuration cron pour le groupe : **[!UICONTROL index]**
   - Options de configuration cron pour le groupe : **[!UICONTROL staging]**
1. Videz le cache de configuration après l’enregistrement.

>[!NOTE]
>
>Avec les deux groupes s’exécutant en cours de traitement et de manière séquentielle, une réindexation complète lente bloque l’exécution de l’évaluation jusqu’à ce qu’elle se termine. Sur les catalogues volumineux, cela peut retarder l’évaluation des mises à jour.

## Incohérence des données de catalogue entre les services [!DNL Adobe Commerce] et connectés {#catalog-data-discrepancy}

**Problème :** les données de produit affichées dans les services Commerce connectés (tels que [!DNL Live Search] ou [!DNL Product Recommendations]) ne correspondent pas aux données du catalogue dans [!DNL Adobe Commerce]. Par exemple, le nom, le prix ou la description d’un produit semble obsolète ou incorrect sur le storefront.

**Cause :** lorsqu’une resynchronisation est déclenchée, la mise à jour et la prise en compte des données dans les composants de l’interface utilisateur peuvent prendre jusqu’à une heure. Si l’incohérence persiste au-delà de cette fenêtre, l’élément n’a peut-être pas été récupéré lors de la dernière synchronisation ou la synchronisation n’a pas détecté de modification, car les données de flux étaient déjà marquées comme à jour.

**Solution :**

1. Ouvrez les résultats de la recherche à partir du storefront Commerce. Sélectionnez ensuite le produit en question pour ouvrir sa vue détaillée.
1. Copiez la sortie JSON et vérifiez qu’elle correspond à ce que vous avez dans le catalogue [!DNL Commerce].
1. Si le contenu ne correspond pas, apportez une modification mineure au produit de votre catalogue, par exemple en ajoutant un espace ou un point, pour forcer la détection de la modification.
1. Attendez une resynchronisation ou déclenchez une resynchronisation manuelle à partir de l’interface de ligne de commande ou de la page [[!UICONTROL Data Feed Sync Status]](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) dans l’interface d’administration.

Pour résoudre d’autres problèmes liés aux données de catalogue dans [!DNL Product Recommendations], voir [Résolution des problèmes du module de recommandations de produits](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/troubleshoot-product-recommendations-module-in-magento-commerce) dans la base de connaissances de Commerce.

## La synchronisation des données ne s’exécute pas selon le calendrier {#sync-not-on-schedule}

**Problème :** la synchronisation des données ne s’exécute pas selon le calendrier ou aucun élément n’est synchronisé malgré les modifications du produit dans [!DNL Adobe Commerce].

**Cause :** les causes les plus courantes sont les tâches cron qui ne s’exécutent pas ou les indexeurs qui ne sont pas configurés en mode **[!UICONTROL Update by Schedule]**.

**Solution :**

- [Vérifiez que les tâches cron sont en cours d’exécution](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues).
- Vérifiez que les indexeurs des flux suivants sont définis sur **[!UICONTROL Update by Schedule]** : Attributs de catalogue, Produit, Remplacements de produit et Variante de produit. Vérifiez à partir de [[!UICONTROL Index Management]](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) dans l’administration Commerce ou à l’aide de l’interface de ligne de commande : `bin/magento indexer:show-mode | grep -i feed`.

## La synchronisation du catalogue a le statut En échec . {#catalog-sync-failed}

**Problème :** la synchronisation du catalogue affiche un statut **Échec** sur la page **[!UICONTROL Data Feed Sync Status]**.

**Cause :** une erreur irrécupérable s’est produite lors de la phase de collecte de données ou d’envoi. Les causes courantes incluent les problèmes d’authentification des API, les erreurs réseau ou les échecs de validation des données.

**Solution :**

1. Consultez les journaux d’erreurs d’exportation des données pour plus d’informations sur l’échec. Consultez la section [Vérification et dépannage des journaux](logging.md) pour connaître le format de journal et les options de journalisation étendues :
   - `var/log/commerce-data-export-errors.log` les erreurs lors de la collecte de données.
   - `var/log/saas-export-errors.log` les erreurs lors de l’envoi des données.
1. Si l’erreur n’est pas liée à la configuration ou à une extension tierce, [envoyez un ticket d’assistance](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) avec les entrées de journal appropriées.

## Le journal affiche les messages « opération ignorée - processus verrouillé » {#process-locked}

**Problème :** le fichier `commerce-data-export.log` contient des entrées similaires à celles-ci :

```json
{"feed":"products","operation":"partial sync","status":"operation skipped - process locked by \"full sync(1234)\"", ...}
```

**Cause :** il s’agit d’un comportement attendu, et non d’une erreur. Le message s’affiche lorsqu’une synchronisation partielle déclenchée par cron tente de s’exécuter alors qu’une réindexation complète ou une `saas:resync` est déjà en cours. L’extension [!DNL SaaS Data Export] utilise un mécanisme de verrouillage de flux pour empêcher les opérations de synchronisation simultanées en conflit.

**Solution :**

Aucune action n’est requise. Une fois que le processus en cours d’exécution se termine et libère le verrouillage, l’exécution cron suivante reprend et synchronise toutes les modifications en attente. Pour plus d’informations sur le fonctionnement du mécanisme de verrouillage, consultez la section [Mécanisme de verrouillage de flux pour l’exportation de données SaaS](../feed-lock-mechanism.md).

>[!MORELIKETHIS]
>
> - [Consulter les journaux et résoudre les problèmes](logging.md)
> - [Référence des codes journaux](log-codes-reference.md)
> - [Mécanisme de verrouillage de flux pour l’exportation de données SaaS](../feed-lock-mechanism.md)
