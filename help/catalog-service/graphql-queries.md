---
title: '[!DNL Retrieve catalog data with GraphQL]'
description: Utilisez les requêtes GraphQL pour récupérer les données du catalogue afin d’alimenter les expériences Commerce.
role: Admin, Developer
feature: Services, API Mesh, Catalog Service
exl-id: 49bbdb3b-bbe9-4777-8ea7-3bd25ae53889
source-git-commit: ff5c717dbdd638e114bccc3f6dec26f4be269194
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# Récupération des données de catalogue avec GraphQL {#graphql-queries}

Utilisez les requêtes GraphQL pour récupérer les données sur le produit, le prix et d’autres données de l’espace de données SaaS du catalogue Adobe Commerce et utilisez-les pour effectuer le rendu des expériences Commerce plus rapidement que les requêtes GraphQL natives d’Adobe Commerce.

Le service de catalogue fournit les requêtes suivantes :

| Requête | Description | Utilisation |
|-------|-------------|-------|
| `categories` | Renvoie les données de catégorie. Si l’objet d’entrée de sous-arborescence est spécifié, la requête renvoie des détails sur les sous-catégories. | Utile pour effectuer le rendu des pages de navigation et de catégorie du storefront. [Voir exemple.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) |
| `products` | Renvoie des détails sur les SKU spécifiés en entrée. | Utilisé principalement pour effectuer le rendu du contenu sur les pages de détails du produit et de comparaison de produits. [Voir exemple.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) |
| `productSearch` | Renvoie une liste de produits correspondant aux critères de recherche. | Utile pour effectuer le rendu des résultats de recherche et des pages de liste de produits en fonction des entrées de recherche. [Voir exemple.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/) |
| `refineProduct` | Limite les résultats d’une requête de produits exécutée sur un produit complexe pour renvoyer une information spécifique sur une variante de produit. | Utile pour le rendu des pages de détails de produit mises à jour lorsque les acheteurs sélectionnent une option de produit. [Voir exemple.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/) |
| `variants` | Renvoie des détails sur toutes les variations d’un produit. | Utile pour afficher des images de variantes sur les détails du produit ou répertorier les pages sans envoyer plusieurs requêtes d’API. [Voir exemple.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/product-variants/) |

Pour plus d’informations sur l’utilisation de ces requêtes[&#128279;](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/) consultez le  Guide de l’API Catalog Service
