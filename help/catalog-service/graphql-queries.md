---
title: '[!DNL Retrieve catalog data with GraphQL]'
description: Utilisez les requêtes GraphQL pour récupérer les données du catalogue afin d’alimenter les expériences Commerce.
role: Admin, Developer
feature: Services, API Mesh, Catalog Service
exl-id: 49bbdb3b-bbe9-4777-8ea7-3bd25ae53889
TQID: https://experienceleague.adobe.com/ahutwotbB6Dxg7Tc3WMFd7S-WBMALvOYIUTmB5JKmyM
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: d842311424e76b83a131ada7a2db6e3fb868acd8
workflow-type: tm+mt
source-wordcount: 269
ht-degree: 0%

---

# Récupération des données de catalogue avec GraphQL {#graphql-queries}

Utilisez les requêtes GraphQL pour récupérer les données de produit, de prix et d’autres données de catalogue à partir de l’espace de données [!DNL Catalog Service] et effectuer [!DNL Adobe Commerce] rendu des expériences de storefront plus rapidement que les requêtes de produit natives.

{{aco-merchandising-services}}

Le [!DNL Catalog Service] fournit les requêtes suivantes :

| Requête | Description | Utilisation | Limites |
| --- | --- | --- | --- |
| `categories` | Renvoie les données de catégorie. Si l’objet d’entrée `subtree` est spécifié, la requête renvoie des détails sur les sous-catégories. | Utile pour le rendu de la navigation storefront et des pages de catégories. [Voir exemple.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/){target="_blank"} | — |
| `products` | Renvoie des détails sur les SKU spécifiés en entrée. | Utilisé principalement pour effectuer le rendu du contenu sur les pages de détails du produit et de comparaison de produits. [Voir exemple.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/){target="_blank"} | 100 SKU par demande |
| `productSearch` | Renvoie une liste de produits correspondant aux critères de recherche. | Utile pour effectuer le rendu des résultats de recherche et des pages de liste de produits en fonction des entrées de recherche. [Voir exemple.](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/){target="_blank"} | 100 SKU par demande |
| `refineProduct` | Limite les résultats de la requête `products` pour un produit complexe afin de renvoyer des informations spécifiques sur une variante de produit. | Utile pour effectuer le rendu des pages de détails de produit mises à jour lorsque les acheteurs sélectionnent une option de produit. [Voir exemple.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/){target="_blank"} | 100 SKU par demande |
| `variants` | Renvoie des détails sur toutes les variations d’un produit. | Utile pour afficher des images de variantes sur les détails du produit ou répertorier les pages sans envoyer plusieurs requêtes d’API. [Voir exemple.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/product-variants/){target="_blank"} | 100 SKU par demande |

{style="table-layout:auto"}

Voir [Storefront Services GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/){target="_blank"} pour plus d’informations sur l’utilisation de ces requêtes.
