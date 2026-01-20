---
title: Types de facettes
description: '[!DNL Live Search] facettes sont dynamiques et apparaissent dans la liste Filtres, le cas échéant.'
exl-id: cd05c0c5-1028-4d66-951d-0b61c1ecc440
source-git-commit: 458f34c45406db871ec61ff408aa624f163b6ee0
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# Types de facettes

[!DNL Live Search] utilise différents types de facettes qui n’apparaissent dans la liste *Filtres* que lorsque cela est pertinent. La liste des facettes disponibles change en fonction des produits renvoyés. Les caractéristiques suivantes affectent leur présentation et leur comportement :

* Facettes épinglées - Les facettes les plus couramment utilisées peuvent être épinglées en haut de la liste. Les facettes restantes sont répertoriées dans l’ordre *Type de tri* après les facettes épinglées.
* Facettes dynamiques - Attributs de produit que [Adobe AI](https://business.adobe.com/fr/ai.html) trouve les plus pertinents pour un ensemble de produits et une requête. Le calcul prend en compte les métadonnées d’attribut de l’ensemble du catalogue et détermine au moment de la requête les facettes les plus pertinentes pour la requête.

  >[!NOTE]
  >
  >Si vous constatez que des erreurs de délai d’expiration apparaissent dans la réponse de requête de GraphQL après la création de facettes dynamiques, remplacez toutes les facettes par épinglées pour voir si cela résout les problèmes de performances.

* Facettes populaires : attributs de produit les plus souvent présents dans les résultats de recherche.
* Facettes de prix - Retourner les produits par gamme de prix. Vous pouvez indiquer le nombre de sélections et l’intervalle entre les plages de prix dans l’espace de travail [*Paramètres*](settings.md).

Au moment de la requête, [!DNL Live Search] génère les résultats de la recherche dans des groupes de facettes dynamiques et populaires.

![Facettes - Prix](assets/storefront-search-results-run-price.png)

## Storefront et options découplées

Les facettes rendues pour le storefront [!DNL Commerce] sont traitées par l’adaptateur de recherche, qui achemine les requêtes et effectue le rendu des résultats dans le storefront. Toutes les facettes de storefront [!DNL Commerce] sont triées par ordre alphabétique avec des options à sélection unique, quel que soit le type d’entrée affecté à l’attribut correspondant. Les facettes disponibles dans le storefront sont rendues en fonction du thème actuel et reflètent toutes les personnalisations apportées à la présentation de la navigation superposée.

En revanche, les implémentations [découplées](https://developer.adobe.com/commerce/php/architecture/technical-vision/web-api/) sont traitées par l’API et prennent en charge des options supplémentaires. Les facettes découplées peuvent être triées par ordre alphabétique ou par nombre et peuvent comporter des options à sélection unique ou multiple.

### Libellés de facettes

Pour les storefronts [!DNL Commerce], le libellé de la facette est déterminé par le [*Propriétés de l’attribut*](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create.html?lang=fr). Pour les magasins comportant plusieurs vues, des libellés supplémentaires peuvent être définis sous *Gérer les libellés*. Pour les implémentations découplées, les libellés sont modifiés à partir de l’espace de travail [à facettes](faceting-workspace.md).

### Type de tri

Toutes les facettes rendues pour le storefront sont triées par ordre alphabétique. Pour les implémentations découplées, les facettes peuvent être triées par ordre alphabétique ou par nombre.

| Type de tri | Description |
|--- |--- |
| Alphabétique | Dans la liste storefront *Filtres*, les facettes sont triées par ordre alphabétique. |
| Nombre | (Découplé uniquement) Pour les implémentations découplées, les facettes peuvent également être triées en fonction du nombre de valeurs trouvées par facette dans l’ensemble actuel de produits renvoyés. |
