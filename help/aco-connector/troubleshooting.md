---
title: Résolution des problèmes liés à  [!DNL Adobe Commerce Optimizer Connector]
description: Découvrez comment résoudre les problèmes d [!DNL Adobe Commerce Optimizer Connector] identification, de synchronisation des catalogues et d’exportation de portée pour les intégrations  [!DNL Adobe Commerce] .
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="PaaS uniquement" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."
autotag-review: '2026-06-09T19:00:00.000Z'
TQID: 'https://experienceleague.adobe.com/ei86QuJ3nQ2d-6NRoAeJslgDxjGlZRejD-Nx-6SAVdc'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
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
source-wordcount: 331
ht-degree: 0%

---

# Résolution des problèmes liés à [!DNL Adobe Commerce Optimizer Connector]

Utilisez ce guide pour diagnostiquer et résoudre les problèmes courants liés au [!DNL Adobe Commerce Optimizer Connector] lors de la configuration initiale, de la synchronisation des flux de catalogue et de la configuration de l’exportation de la portée. Les sections ci-dessous couvrent la validation des informations d’identification et des clients, les échecs de synchronisation des données et les diagnostics de [!DNL SaaS Data Export] associés.

## Échec de la validation des informations d’identification ou du client

Si la `aco:config:init` échoue lors de la validation des informations d’identification :

- Exécutez la commande `bin/magento aco:config:show` [!DNL Adobe Commerce] CLI pour vérifier les valeurs stockées.
- Vérifiez que l’identifiant du client appartient à l’organisation IMS utilisée pour obtenir les informations d’identification.
- Vérifiez que le client OAuth dispose des portées nécessaires pour le service d’ingestion de [!DNL Adobe Commerce Optimizer] (voir [&#x200B; Obtention des informations d’identification IMS &#x200B;](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/authentication/#obtain-ims-credentials)).

## Données non synchronisées

**Vérification des détails de l’erreur au niveau de l’élément :**

Consultez [Vérification du fonctionnement de la synchronisation des données](./data-sync-manage.md#verify-that-the-data-sync-is-working) pour connaître les étapes d’ouverture des **[!UICONTROL Data Feed Sync Status]** dans l’administration Commerce. Sélectionnez le flux qui échoue pour afficher les détails de l’erreur par élément.

Points clés concernant la gestion des erreurs :

- Les erreurs **400** ne sont pas reprises. Recherchez dans la payload des champs obligatoires incorrects ou manquants. Voir [&#x200B; Mappage de champ pour les flux du connecteur &#x200B;](reference/field-mapping.md) pour le format attendu.
- Les erreurs **5xx** sont automatiquement retentées par la tâche cron `*_resend_failed_items` (s’exécute toutes les 5 minutes).

**Vérifier la configuration de l’étendue :**

Si le problème affecte uniquement une source de catalogue spécifique (code d’affichage du magasin) ou un catalogue de prix, vérifiez si la synchronisation est désactivée pour le site web ou l’affichage du magasin correspondant. Voir [Personnalisation de la configuration d’exportation des portées de Commerce](./get-started.md#customize-the-commerce-scopes-export-configuration).

**Une fois résolu :**

Les flux du connecteur affichent un statut réussi dans **[!UICONTROL Data Feed Sync Status]**, et les produits, prix et attributs attendus apparaissent sur la page **[!UICONTROL Data Sync]** dans [!DNL Commerce Optimizer].

## Mauvaise configuration et interprétation des résultats

Pour obtenir un catalogue de comportements spécifiques causés par une mauvaise configuration ou une mauvaise interprétation des résultats de synchronisation, tels que des produits manquants, des prix incorrects ou des écarts de données au niveau de la portée, consultez la section [Dépannage des scénarios](troubleshooting/troubleshooting-scenarios.md).

## Diagnostics [!DNL SaaS Data Export]

Pour les diagnostics de [!DNL SaaS Data Export] de niveau inférieur, y compris les emplacements des journaux et les commandes de resynchronisation des flux, consultez le guide de dépannage [[!DNL SaaS Data Export] &#x200B;](https://experienceleague.adobe.com/en/docs/commerce/saas-data-export/troubleshooting/logging){target="_blank"}.
