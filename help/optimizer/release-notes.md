---
title: Notes de mise à jour
description: Dernières informations de mise à jour pour  [!DNL Adobe Commerce Optimizer].
role: Admin, Developer, User, Leader
recommendations: noCatalog
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et  [!DNL Adobe Commerce Optimizer]  (infrastructure SaaS gérée par Adobe)."
exl-id: e420d461-9ea2-4e32-aa37-230b14a297d7
source-git-commit: d0967674d05018f13dc6c8a562005d65d44e42ab
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---

# Notes de mise à jour

Les notes de mise à jour suivantes contiennent des mises à jour de [!DNL Adobe Commerce Optimizer].

## Avril 2026

**Date de publication** : 7 avril 2026

>[!BEGINSHADEBOX]

### Règles de catalogue

Les règles de marchandisage incluent désormais [règles de catégorie](./merchandising/rules/add.md), ce qui vous permet de cibler une ou plusieurs catégories et de contrôler l’ordre des produits sur les pages de catégorie à l’aide du même classement intelligent et des mêmes actions manuelles (épingler, booster, enterrer) que pour la recherche.

### Filtre de prix

Les filtres de recommandation prennent désormais en charge un [filtre de prix](./merchandising/recommendations/filters.md#price) que vous pouvez utiliser pour définir une plage de prix minimale et maximale pour les produits.

### Notes de mise à jour supplémentaires

[!DNL Adobe Commerce Optimizer] fonctionne avec les dernières versions de l’intégration AEM Assets, le connecteur Commerce Optimizer et [!DNL Adobe Commerce Storefront]. Utilisez les liens suivants pour afficher les notes de mise à jour de chaque zone :

| Extensibilité | Storefront |
| --- | --- |
| [Connecteur AEM Assets](../aem-assets-integration/release-notes.md)<br>[Commerce Optimizer](../aco-connector/release-notes.md) | [Informations de mise à jour de Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/releases/)<br>[Journal des modifications de Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/releases/changelog/) |

>[!ENDSHADEBOX]

## Février 2026

**Date de publication** : 19 février 2026

>[!BEGINSHADEBOX]

Possibilité de spécifier une vue de catalogue lorsque vous [créez des unités de recommandation](./merchandising/recommendations/create.md) ou [ des règles de marchandisage](./merchandising/rules/add.md).

### Notes de mise à jour supplémentaires

[!DNL Adobe Commerce Optimizer] fonctionne avec les dernières versions de l’intégration AEM Assets, le connecteur Commerce Optimizer et [!DNL Adobe Commerce Storefront]. Utilisez les liens suivants pour afficher les notes de mise à jour de chaque zone :

| Extensibilité | Storefront |
| --- | --- |
| [Connecteur AEM Assets](../aem-assets-integration/release-notes.md)<br>[Commerce Optimizer](../aco-connector/release-notes.md) | [Informations de mise à jour de Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/releases/)<br>[Journal des modifications de Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/releases/changelog/) |

>[!ENDSHADEBOX]

## Décembre 2025

**Date de publication** : 10 décembre 2025

>[!BEGINSHADEBOX]

### Opportunités

Les recommandations d’optimisation de site optimisées par l’IA sont désormais disponibles via l’intégration [Adobe Sites Optimizer](./manage-results/opportunities.md). Cette fonctionnalité permet aux marchandiseurs d’identifier et de résoudre les problèmes affectant les performances du site commercial grâce à la détection automatisée et aux recommandations intelligentes.

### Calques de catalogue

Ajout de [ couches de catalogue ](./setup/catalog-layer.md) afin que vous puissiez modifier les données de produit sans modifier les données sources, y compris la gestion de la priorité des couches et l’intégration aux fonctionnalités de correctif automatique d’Adobe Sites Optimizer.

### Notes de mise à jour supplémentaires

[!DNL Adobe Commerce Optimizer] fonctionne avec les dernières versions de l’intégration AEM Assets, le connecteur Commerce Optimizer et [!DNL Adobe Commerce Storefront]. Utilisez les liens suivants pour afficher les notes de mise à jour de chaque zone :

| Extensibilité | Storefront |
| --- | --- |
| [Connecteur AEM Assets](../aem-assets-integration/release-notes.md)<br>[Commerce Optimizer](../aco-connector/release-notes.md) | [Informations de mise à jour de Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/releases/)<br>[Journal des modifications de Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/releases/changelog/) |

>[!ENDSHADEBOX]

## Octobre 2025

**Date de publication** : 14 octobre 2025

>[!BEGINSHADEBOX]

### Connecteur Commerce Commerce Optimizer Salesforce

Le [!DNL Commerce Optimizer Salesforce Commerce Connector] est un nouveau kit de démarrage de l’intégration App Builder qui permet aux administrateurs et aux développeurs Commerce de connecter facilement les données du catalogue Salesforce B2C Commerce à [!DNL Commerce Optimizer].<!--COMOPT-536-->

**Pour les administrateurs :**

* Les mises à jour des catalogues dans Salesforce (produits, prix, métadonnées, tarifs) sont automatiquement synchronisées avec Commerce Optimizer, aucune intervention manuelle n’est nécessaire.
* L’intégration fonctionne indépendamment d’Adobe Commerce, ce qui réduit la complexité et les points d’échec potentiels.
* Les administrateurs peuvent compter sur des mises à jour planifiées régulières pour garantir l’exactitude des données de catalogue dans Commerce Optimizer, ce qui améliore le marchandisage et les recommandations de produits.

**Pour les développeurs :**

* Le kit de démarrage fournit un framework rationalisé et extensible pour ingérer des données de catalogue Salesforce dans les services de marchandisage SaaS.
* Des implémentations de référence, de la documentation de conception et des exemples de code sont disponibles pour accélérer les intégrations personnalisées ou le dépannage.<!--COMOPT-536-->

### Recherche en couches

* Version GA pour les fonctionnalités de recherche avancées suivantes : recherche superposée à l’aide de `startsWith` et `contains`. [En savoir plus](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#layered-search-and-expansion-of-search-types).

### API Catégories

Une nouvelle API REST Catégories est désormais disponible, ce qui permet aux administrateurs et aux développeurs de créer, mettre à jour et gérer plusieurs arborescences de catégories par programmation pour la navigation et le regroupement de produits. L’API prend en charge les configurations globales et spécifiques aux canaux. Elle est conçue pour offrir une évolutivité élevée, prenant en charge jusqu’à 10 000 arborescences de catégories et 500 catégories par arborescence. Pour plus d’informations, consultez la section [Catégories](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/#categories) du _Guide du développeur des services de marchandisage_.<!--DCAT-2649-->

### Notes de mise à jour supplémentaires

[!DNL Adobe Commerce Optimizer] fonctionne avec les dernières versions de l’intégration AEM Assets, le connecteur Commerce Optimizer et [!DNL Adobe Commerce Storefront]. Utilisez les liens suivants pour afficher les notes de mise à jour de chaque zone :

| Extensibilité | Storefront |
| --- | --- |
| [Connecteur AEM Assets](../aem-assets-integration/release-notes.md)<br>[Commerce Optimizer](../aco-connector/release-notes.md) | [Informations de mise à jour de Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/releases/)<br>[Journal des modifications de Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/releases/changelog/) |

>[!ENDSHADEBOX]

## Août 2025

**Date de publication** : 28 août 2025

>[!BEGINSHADEBOX]

### Région de l’UE désormais disponible

La prise en charge de la Région de l’Union européenne (eu1) pour les organisations IMS clientes est désormais disponible. Vous pouvez désormais sélectionner **Union européenne** en tant que **Région** lors de l’[ajout d’une instance Commerce Optimizer](./get-started.md#step-1-create-an-instance) dans le Cloud Manager. La région de l’Union européenne n’est disponible que pour les environnements de production.

Les URL de production de base pour la région de l’Union européenne sont les suivantes :

* Administrateur : `https://eu1.admin.commerce.adobe.com`
* REST et GraphQL : `https://eu1.api.commerce.adobe.com`

![créer une instance](./assets/create-instance.png){width="600" align="center" zoomable="yes"}

### Notes de mise à jour supplémentaires

[!DNL Adobe Commerce Optimizer] fonctionne avec les dernières versions de l’intégration AEM Assets, le connecteur Commerce Optimizer et [!DNL Adobe Commerce Storefront]. Utilisez les liens suivants pour afficher les notes de mise à jour de chaque zone :

| Extensibilité | Storefront |
| --- | --- |
| [Connecteur AEM Assets](../aem-assets-integration/release-notes.md)<br>[Commerce Optimizer](../aco-connector/release-notes.md) | [Informations de mise à jour de Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/releases/)<br>[Journal des modifications de Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/releases/changelog/) |

>[!ENDSHADEBOX]
