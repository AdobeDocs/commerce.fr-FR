---
title: Scénarios de dépannage pour  [!DNL Adobe Commerce Optimizer Connector]
description: Diagnostiquez et résolvez les comportements inattendus dans  [!DNL Adobe Commerce Optimizer Connector]  causés par une configuration incorrecte ou une mauvaise interprétation des résultats de synchronisation.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="PaaS uniquement" type="Informative" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."
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
source-wordcount: 516
ht-degree: 0%

---


# Scénarios de dépannage pour le [!DNL Adobe Commerce Optimizer Connector]

Cette page décrit les comportements que vous pouvez observer lors de l’utilisation des [!DNL Adobe Commerce Optimizer Connector], qui sont généralement causés par une mauvaise configuration ou une mauvaise interprétation des résultats de synchronisation. Utilisez les descriptions ci-dessous pour identifier la cause première et appliquer la résolution appropriée.

## Le statut du flux indique « Succès », mais les données ne sont pas visibles dans [!DNL Adobe Commerce Optimizer]

**Problème :** la page **[!UICONTROL Data Feed Sync Status]** signale une synchronisation réussie, mais les produits, les prix, etc. n’apparaissent pas comme prévu dans [!DNL Adobe Commerce Optimizer].

**Cause :** un statut de flux réussi signifie que les données ont été acceptées par le point d’entrée d’ingestion et non qu’elles ont fini de se propager à travers [!DNL Adobe Commerce Optimizer]. La propagation peut prendre plusieurs minutes après l’ingestion.

**Solution :**

- Patientez quelques minutes et actualisez la vue [!DNL Adobe Commerce Optimizer].
- Vérifiez que l’identifiant du client configuré dans [!DNL Adobe Commerce] correspond à l’environnement [!DNL Commerce Optimizer] que vous vérifiez.
- Vérifiez que la [source du catalogue](../../optimizer/setup/catalog-sources.md) (code vue magasin) ou le catalogue de prix approprié est sélectionné dans [!DNL Commerce Optimizer].

## Produits manquants dans le catalogue exporté

**Problème :** certains produits n’apparaissent pas dans [!DNL Adobe Commerce Optimizer] après une synchronisation complète du catalogue.

**Cause :** si la validation des produits échoue lors de l’exportation, ils sont omis de la synchronisation. Les produits désactivés ou non visibles dans le catalogue ne sont pas renvoyés par l’API de produits.

**Solution :**

- Vérifiez que les produits concernés sont affectés au site web et à la vue de magasin utilisée comme source du catalogue.
- Vérifiez que les produits sont activés et définis sur une visibilité qui inclut les listes de catalogue.
- Consultez les détails des erreurs par article pour le flux du catalogue dans **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Feed Sync Status]**.

## Les prix sont incorrects ou manquants en [!DNL Adobe Commerce Optimizer]

**Problème :** les produits apparaissent dans [!DNL Adobe Commerce Optimizer] mais n’affichent aucun prix renvoyé avec [la requête GraphQL products](https://developer.adobe.com/commerce/services/reference/graphql/#products){target="_blank"}, ou le prix ne correspond pas à ce qui est configuré dans [!DNL Adobe Commerce].

**Cause :** le flux du catalogue des prix utilise une portée qui correspond à un site web et à un groupe de clients spécifiques. Une configuration [vue catalogue](../../optimizer/setup/catalog-view.md) incorrecte peut entraîner des prix manquants ou incorrects.

**Solution :**

- Vérifiez que le site web est configuré pour la synchronisation dans la configuration d’exportation du connecteur. Voir [Personnalisation de la configuration de l’exportation des données](../get-started.md#customize-the-commerce-scopes-export-configuration).
- Vérifiez que l&#39;ID du catalogue de prix utilisé dans [!DNL Commerce Optimizer] est présent dans la configuration [vue catalogue](../../optimizer/setup/catalog-view.md){target="_blank"} utilisée pour exécuter la requête de produits.

## Les données dans [!DNL Adobe Commerce Optimizer] sont écrasées ou modifiées de manière inattendue après la synchronisation

**Problème :** les modifications de données appliquées directement dans [!DNL Adobe Commerce Optimizer] par un système externe (tel qu’un PIM ou un ERP) sont perdues ou rétablies après l’exécution d’une synchronisation par le connecteur.

**Cause :** lorsque des systèmes autres que [!DNL Adobe Commerce] écrivent directement dans [!DNL Adobe Commerce Optimizer], par exemple un PIM ou un autre système externe, des conflits de données peuvent survenir. Le connecteur synchronise les données *dans un sens*, de [!DNL Adobe Commerce] à [!DNL Adobe Commerce Optimizer], et ne resynchronise pas les modifications avec [!DNL Adobe Commerce]. Par conséquent, les données écrites directement dans [!DNL Adobe Commerce Optimizer] ne sont pas reflétées dans [!DNL Adobe Commerce] et peuvent être remplacées lors d’une synchronisation ultérieure.


**Solution :**

Au lieu d’écrire des modifications de catalogue directement dans [!DNL Adobe Commerce Optimizer], utilisez [&#x200B; calques de catalogue &#x200B;](../../optimizer/setup/catalog-layer.md){target="_blank"} pour appliquer des modifications en dehors de [!DNL Adobe Commerce]. Les couches Catalogue permettent aux systèmes externes d’enrichir ou de remplacer les données de catalogue dans [!DNL Adobe Commerce Optimizer] sans entrer en conflit avec la synchronisation du connecteur.

## Scénarios de dépannage pour les problèmes de [!DNL SaaS Data Export] courants

Pour tout problème lié au [!DNL SaaS Data Export] sous-jacent susceptible d’affecter le connecteur, consultez la section [Dépannage des scénarios pour [!DNL SaaS Data Export]](../../data-export/troubleshooting/troubleshooting-scenarios.md).
