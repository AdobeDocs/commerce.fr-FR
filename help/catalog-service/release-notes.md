---
title: Notes de mise à jour de [!DNL Catalog Service]
description: Dernières informations de mise  [!DNL Catalog Service]  jour pour Adobe Commerce.
feature: Services, Catalog Service, Release Notes
exl-id: 74f2e46a-5592-4857-a6d7-b95b85d8b4cc
source-git-commit: fe5f864262478d1f9e205f2cd275452594cf4675
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 0%

---

# Notes de mise à jour de [!DNL Catalog Service]

Ces notes de mise à jour décrivent les dernières versions de [!DNL Catalog Service].
La prise en charge est assurée pour la version majeure publiée actuelle. Les notes de mise à jour des anciennes versions sont fournies à titre de référence.
Les mises à jour incluent :

![Nouveau](../assets/new.svg) Nouvelles fonctionnalités
![Correctifs](../assets/fix.svg) Correctifs et améliorations
![Bogue](../assets/bug.svg) Problèmes connus

## Version majeure actuelle

### Version V1.26

_2 octobre 2024_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg) le schéma GraphQL inclut désormais l’attribut `lastModifiedAt` dans les informations sur le produit. Cet horodatage précis permet aux clients de s’assurer que les plans de site reflètent avec précision les mises à jour les plus récentes de leurs produits. Il permet également aux moteurs de recherche tels que Google de déterminer quand une réindexation est nécessaire, d’optimiser le processus d’analyse et de prévenir les problèmes liés aux dates de dernière modification agressives utilisées lorsque des informations précises ne sont pas disponibles. <!--DATA-6209-->

## Versions précédentes

+++ Versions précédentes

### Version 1.23

_2 août 2024_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Correctif](../assets/fix.svg) Vous pouvez désormais récupérer des informations sur les produits sans données de remplacement de produit (prix). Dans les versions précédentes, ces requêtes renvoyaient l’erreur suivante :
`The following sku does not have product override data in the DB: <SKU value>. Make sure data is synced.` <!--DATA-6121-->

### Version V1.22

_13 août 2024_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg) Ajout de la prise en charge de la récupération de toutes les variantes par SKU de produit. Voir [Référence de l’API Catalog Service](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/). <!--DATA-6067-->

### Version V1.22

_13 août 2024_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg) Ajout de la prise en charge de la récupération de toutes les variantes par SKU de produit. Voir [Référence de l’API Catalog Service](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/). <!--DATA-6067-->

### Version 1.19

_23 mai 2024_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures


![Correctif](../assets/fix.svg) <!--DATA-5033-->L’indicateur `InStock` pour les valeurs d’option prend désormais en compte le statut de `enabled` défini de la variante de produit.

![Correctif](../assets/fix.svg) <!--DATA-5888-->Ajoutez la prise en charge des prix de produits qui nécessitent de grands nombres (jusqu’à 16 chiffres) et une plus grande précision décimale (jusqu’à 4 décimales). Pour appliquer les mises à jour de configuration des prix à votre catalogue existant, resynchronisez les données du catalogue à partir du tableau de bord [Data Management](https://experienceleague.adobe.com/fr/docs/commerce-admin/systems/data-transfer/data-dashboard) ou à l’aide de l’interface de ligne de commande [Adobe Commerce](../landing/catalog-sync.md#command-line-interface).

#### Limites connues

Les fonctionnalités suivantes ne sont pas encore prises en charge :

* La taille maximale de la payload des attributs dynamiques est de 9 Mo.
* Le prix des produits du Groupe peut être calculé avec des prix de produits simples.
* Dans un tableau d’images, seule la première image contient des rôles.

Résolvez les problèmes suivants en utilisant le maillage API et l’API Core GraphQL :

* Prix minimum annoncé
* Tarification par niveau
* Offre groupée de produits à prix fixes

Pour plus d’informations et des exemples, voir [Service de catalogue et maillage API](mesh.md)

### Version 1.18

_1 avril 2024_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg) Ajout de la prise en charge de PHP 8.3.

![Nouveau ](../assets/new.svg) les requêtes [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/) et [`refineProduct`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/) renvoient désormais des données d’options personnalisables pour les produits simples et complexes.<!--DATA-5538-->

### Version 1.17

_2 février 2024_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg) Le [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-dashboard.html?lang=fr) est maintenant disponible. Ce tableau de bord remanié fournit des informations sur les flux de données pour [!DNL Product Recommendations], [!DNL Live Search] et [!DNL Catalog Service]. La prise en charge de cette fonctionnalité a été introduite dans la version 3.1.0 du métapaquet `catalog-service`.

### Version 1.16

_13 février 2024_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Les nouvelles vidéos produit ](../assets/new.svg) sont désormais prises en charge par l’API Catalog Service.
![Correctif](../assets/fix.svg) Les options en rupture de stock s’affichent désormais dans le widget PDP.

#### Limites connues

Ces fonctionnalités ne sont pas encore prises en charge :

* La taille maximale de la payload des attributs dynamiques est de 9 Mo.
* Prix du produit du groupe. Cette valeur peut être calculée avec des prix de produit simples.
* Dans un tableau d’images, seule la première image contient des rôles.

Les limites suivantes peuvent être résolues à l’aide du maillage API et de l’API Core GraphQL :

* Prix minimum annoncé
* [Tarification par niveau](mesh.md)

### Version 1.13

_12 octobre 2023_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg) Catalog Service prend en charge l’indicateur `inStock` pour les variantes de produits.
![Nouveau](../assets/new.svg) Les champs `urlKey` et `externalId` ont été ajoutés au schéma GraphQL.
![Nouveau](../assets/new.svg) Les produits téléchargeables et les cartes-cadeaux sont désormais pris en charge.

### Version 1.12

_19 septembre 2023_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg) Catalog Service utilise désormais l’indexation des prix [SaaS](../price-index/price-indexing.md).
![Correctif](../assets/fix.svg) cette version contient des correctifs et des améliorations du côté des services.

### Version 1.11

_18 juillet 2023_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg) le service de catalogue prend désormais en charge la requête [`recommendations`](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/recommendations/) GraphQL pour les recommandations de produits.

### Version 1.10

_27 juin 2023_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg) l’API Catalog Service prend désormais en charge `related products`.

### Version 1.7

_12 avril 2023_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg) le service de catalogue nettoie désormais les variantes de produits supprimées.
![Correctif](../assets/fix.svg) Évolutivité de l’infrastructure et améliorations des performances.

### Version 1.6

_28 mars 2023_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg) Des échantillons ont été ajoutés à la requête [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/).
![Nouveau](../assets/new.svg) Ajout de la possibilité de `entityId` à l’aide du [maillage API](mesh.md).

### Version 1.5

_6 mars 2023_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg) Ajout de la fonctionnalité [`categories`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) GraphQL.
![Correctif](../assets/fix.svg) Amélioration des performances et de l’évolutivité des API.

### Version 1.4

_7 février 2023_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.x et ultérieures

![Nouveau](../assets/new.svg) métapaquet de service de catalogue publié pour simplifier les étapes d’installation.
![Correctif](../assets/fix.svg) Amélioration de l’évolutivité et des performances de l’API.

### Version 1.3

_17 janvier 2023_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.x et ultérieures

![Nouveau](../assets/new.svg) Expérience d’intégration simplifiée et améliorée.
![Nouveau ](../assets/new.svg) de nouveaux points d’entrée de sandbox client sont disponibles pour les tests de pré-production.
![Nouveau](../assets/new.svg) Ajout de la prise en charge des produits virtuels.
![Correctif](../assets/fix.svg) Amélioration de l’évolutivité et des performances de l’API.

### Version 1.1

_18 novembre 2022_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.x et ultérieures

![Nouveau](../assets/new.svg) le service de catalogue prend désormais en charge Adobe [maillage API](https://developer.adobe.com/graphql-mesh-gateway/).
![Correctif](../assets/fix.svg) Amélioration de l’évolutivité et des performances globales des API.

### Version V1.0

_4 octobre 2022_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.x et ultérieures

![Nouveau](../assets/new.svg) prend désormais en charge les produits groupés.
![Nouveau](../assets/new.svg) Ajout de remplacements de visibilité B2B. Les produits peuvent désormais faire l’objet de recherches et peuvent être ajoutés au panier pour des groupes de clients spécifiques.
Le service ![Fix](../assets/fix.svg) est désormais plus stable et offre de meilleures performances.

### Version 0.3 - Beta+

_12 septembre 2022_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.x et ultérieures

![Nouvelles](../assets/new.svg) Prise en charge des images pour les variantes : les images du produit sont renvoyées en fonction des options sélectionnées.
![Nouveau](../assets/new.svg) Rôles pour la prise en charge des prix : permettent uniquement aux membres de groupes de clients spécifiques de voir le prix des produits
![Correctif](../assets/fix.svg) Stabilité et performances améliorées du service
![Nouveau](../assets/new.svg) Des mises à jour sont reçues lorsque des produits sont supprimés du catalogue

### Version de Beta

_9 août 2022_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.x et ultérieures

![Nouveau](../assets/new.svg) Les requêtes `products` et `refineProduct` renvoient les données suivantes :

* Attributs de produit (système) prédéfinis.
* Attributs de produit dynamiques et les filtrer par rôle (page d’affichage du produit/page de liste des produits).
* Options du produit.
* Images de produit et filtrage par rôle (PDP/PLP).
* Prix spécifique pour les produits simples et plages de prix pour les produits configurables.
* Prix et fourchettes de prix du groupe de clients. Ils renvoient un prix de secours par défaut pour les acheteurs sans groupe de clients.
* Types de produits qui utilisent une tarification spécifique au client B2B.
