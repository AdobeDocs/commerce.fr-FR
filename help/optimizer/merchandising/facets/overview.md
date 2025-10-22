---
title: Présentation des facettes
description: Découvrez les facettes d [!DNL Adobe Commerce Optimizer] et comment elles améliorent les résultats de recherche.
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
exl-id: cf16626e-8f85-47ca-b973-891b16c31fe3
source-git-commit: 5dd290a4e10bdbd1f6c96b67ab6c9ba1598705dc
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# Facettes

Facettes est une méthode de filtrage haute performance qui utilise plusieurs dimensions de valeurs d’attribut comme critères de recherche.

![Résultats de recherche filtrés](../../assets/storefront-search-results-run.png)

Dans une facette, les acheteurs peuvent sélectionner plusieurs options, telles que « De base » et « Doux » sous « Style », et les résultats de la recherche sont mis à jour pour afficher uniquement ces styles. De même, si un acheteur sélectionne des options sur plusieurs facettes, telles que « De base » sous « Style » et « Intérieur » sous « Climat », les résultats de la recherche sont mis à jour pour afficher le style et le climat sélectionnés.

Toute facette définie peut être utilisée comme paramètre d’URL et les résultats seront filtrés en fonction des valeurs de paramètre : `http://yourstore.com?brand=acme&color=red`.

## Agrégation de facettes

L’agrégation des facettes est effectuée comme suit : si le storefront comporte trois facettes (catégories, couleur et prix) et que les filtres de l’acheteur sont appliqués aux trois (couleur = bleu, prix compris entre 10,00 et 50,00 $, catégories = `promotions`).

- `categories` agrégation - Agrége `categories`, puis applique les filtres `color` et `price`, mais pas le filtre `categories`.
- `color` agrégation - Agrége `color`, puis applique les filtres `price` et `categories`, mais pas le filtre `color`.
- `price` agrégation - Agrége `price`, puis applique les filtres `color` et `categories`, mais pas le filtre `price`.

## Valeurs d’attribut par défaut

Les attributs de produit suivants sont utilisés par [!DNL Adobe Commerce Optimizer] et activés par défaut.

| Propriété | Description | Attribut |
|---|---|---|
| Triable | Utilisé pour le tri dans la liste de produits | `price` |
| Indexable | Utiliser dans la recherche | `price` <br />`sku`<br />`name` |

Consultez la section [API de métadonnées d’ingestion de données](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/#metadata) pour en savoir plus sur les attributs de produit et leurs propriétés.

## Propriétés d’attribut non système par défaut

Le tableau suivant présente les propriétés de recherche et de filtrage par défaut des attributs non système. Définir la propriété d’attribut *Utiliser dans la recherche* sur `Yes` rend l’attribut consultable dans [!DNL Adobe Commerce Optimizer].

| Code attribut | Indexable |
|--- |--- |
| activité | Oui |
| attributes_brand | Oui |
| marque | Oui |
| climat | Oui |
| collier | Oui |
| couleur | Oui |
| coût | Oui |
| eco_collection |  |
| sexe | Oui |
| fabricant | Oui |
| matériau | Oui |
| objectif | Oui |
| strap_bag | Oui |
| style_general | Oui |

## Propriétés d’attribut système par défaut

Le tableau suivant présente les propriétés de recherche et de filtrage par défaut des attributs système.

| Code attribut | Indexable |
|--- |--- |
| allow_open_amount | Oui |
| description | Oui |
| name | Oui |
| prix | Oui |
| short_description | Oui |
| sku | Oui |
| statut | Oui |
| tax_class_id | Oui |
| url_key | Oui |
| poids | Oui |
