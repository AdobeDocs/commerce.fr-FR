---
title: Gestion des stocks de produits
description: Configurez la messagerie et les fonctionnalités de stock marchand disponibles pour les clients.
role: Admin
level: Intermediate
feature: Shipping/Delivery, Inventory, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# Gestion des stocks de produits

En tant que commerçant, vous pouvez utiliser les options Adobe Commerce [Inventory management](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/introduction) stock et source. En outre, vous pouvez utiliser la solution Store Fulfillment pour contrôler d&#39;autres options de disponibilité des stocks liées aux opérations de votre boutique.

- Option de livraison à domicile dans les magasins marchands

- Autoriser/Disponible pour le retrait de la boutique

- UPC / SKU / Autres identifiants de produit uniques

- Seuil de rupture de stock

- Décrémenter le stock à partir d’emplacements spécifiques sur commande

Configurez les options de Stock de produit à partir de l’Administration : **[!UICONTROL Catalog > Products > Select Product]**

## **Options de stock de produits**

| **Champ** | **Description** | **Portée** | **Obligatoire** |
|----------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|--------------|
| **Disponible pour la livraison à domicile** | <p>Définit la disponibilité de la livraison à domicile (expédition à partir du magasin) pour le produit. Lorsque cette option est activée, tous les emplacements de magasin commerçant affectés avec un stock disponible pour le produit sont considérés comme éligibles à l’option Livraison à domicile . Lorsque cette option est désactivée, le produit n’est jamais éligible pour la livraison à domicile.</p>En règle générale, la définition de cette option au niveau de la boutique commerçante est suffisante. Cependant, il pourrait y avoir des cas uniques pour des produits spécifiques, tels que ceux soumis à des restrictions d&#39;expédition fédérales, qui ne devraient pas être admissibles à la livraison à domicile.</p> | Site internet | Non |
| **[!UICONTROL Available for Store Pickup]** | <p>Définissez la disponibilité de la cueillette en magasin pour le produit. Lorsque cette option est activée, tous les magasins marchands affectés disposant d&#39;un stock disponible pour le produit sont considérés comme éligibles à l&#39;option de retrait en magasin. Lorsqu’il est désactivé, le produit n’est jamais éligible pour la cueillette en magasin.</p><p>Cette option peut s’avérer utile pour effectuer le suivi des stocks des commerçants dans le système que vous ne souhaitez pas vendre à partir de votre canal e-commerce.</p> | Site internet | Non |
| **[!UICONTROL UPC / SKU / Custom Scannable Identifier]** | Cet attribut doit exister en tant qu’attribut de produit et se rapporte au paramètre **[!UICONTROL Barcode Source / Barcode Type]**. Cet attribut est utilisé pour effectuer le suivi d’un code à barres scannable pour vos produits. Cette valeur peut être envoyée lorsqu’une commande est envoyée à vos magasins marchands pour prélèvement. Les associés du magasin peuvent utiliser la valeur avec la liste à servir pour faire correspondre les produits sur l’étagère à l’aide d’un lecteur de code-barres. | Affichage de la boutique | Non |

{style="table-layout:auto"}

## Sources de l’inventaire au niveau des produits

| **Champ** | **Description** | **Portée** | **Obligatoire** |
|-----------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL Out of Stock Threshold]** | <p>Définissez le seuil de stock pour l&#39;article dans chaque source. Lorsque le stock tombe sous le seuil, il est considéré comme en rupture de stock à la source.</p><p>Pour utiliser le paramètre de configuration de la boutique globale, cochez l’option **[!UICONTROL Use Default]** .</p> | Global | Non |
| **[!UICONTROL Allow Store Pickup]** | <p>Définir explicitement si l&#39;article est disponible pour le retrait en magasin, quelle que soit la configuration du stock disponible ou de l&#39;emplacement du magasin marchand.</p><p>Pour utiliser le paramètre au niveau du produit, désélectionnez l’option [!UICONTROL Use Default] et effectuez votre sélection. Sinon, ce paramètre est choisi en fonction de la configuration de **[!UICONTROL Allow In-Store Pickup]** définie sur la source du stock.</p> | Global | Non |

{style="table-layout:auto"}

