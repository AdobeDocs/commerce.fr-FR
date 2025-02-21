---
title: Inventory management Source Transfer
description: Configurez les stocks pour le  [!DNL Store Fulfillment solution]  avec Adobe Commerce Inventory management. Configurez un nouveau stock et transférez l'inventaire en rupture de stock par défaut afin de pouvoir l'affecter à des sources configurées pour activer les fonctionnalités de prélèvement de magasin requises par la solution Store Fulfillment.
role: Admin
level: Intermediate
feature: Shipping/Delivery, Inventory, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---


# Inventory management Source Transfer

La solution [!DNL Store Fulfillment] utilise Adobe Commerce Inventory management natif. Par défaut, la configuration [!DNL Commerce] affecte tous les stocks Web au stock par défaut, auquel aucune source supplémentaire ne peut être affectée. Comme un site Web ne peut se voir attribuer qu&#39;un seul stock, un commerçant doit configurer un nouveau stock et éventuellement transférer son stock source par défaut vers une source affectée à la portée appropriée. Ensuite, la source peut être affectée au nouveau stock.

>[!IMPORTANT]
>
>Les commerçants doivent conserver la source par défaut pour tous les produits inclus dans les types de produits groupés et groupés. Ces produits ont besoin d&#39;une quantité en stock qui respecte le seuil de quantité minimale pour les articles en stock et qui inclut un statut de stock de [!UICONTROL In Stock].

Ces modifications de configuration vous permettent d’accomplir trois choses :

1. [Transférer le stock vers l&#39;origine](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/quantities/inventory-transfer) pour déplacer le stock du stock/de l&#39;origine par défaut vers le nouveau stock/la nouvelle source.

1. [Affecter des sources en bloc](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/quantities/bulk-assignment) pour ajouter de nouvelles sources pour tous vos produits.

1. [Effectuez des mises à jour en bloc des attributs de produit](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/create/bulk-product-attribute-update) pour ajouter les attributs de `Allow Store Pickup` et de `Allow Home Delivery` aux produits existants. Lorsque la solution est installée, les attributs ont les valeurs optimales *par défaut*. Toutefois, ces attributs ne sont pas appliqués aux produits existants tant que vous n’avez pas terminé le processus updateContes en bloc.

Le stock est déduit de l&#39;origine sélectionnée (magasin de vente au détail ou entrepôt de commerce électronique). Les sources utilisées comme entrepôts d&#39;e-commerce doivent être affectées au même stock que le lieu de retrait du magasin et être hiérarchisées avant les lieux de vente au détail. Pour plus d’informations, voir [Hiérarchisation des sources pour un stock](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/stocks/stocks-prioritize-sources).

Pour plus d’informations sur la gestion des stocks, des stocks et des sources, consultez la documentation destinée aux utilisateurs d’Adobe Commerce :

- [Gestion des stocks](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/introduction)

- [Gestion des quantités en stock](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/quantities/quantities-manage)

- [Gestion des stocks](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/stocks/stocks-manage)

- [Gestion des sources](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/sources/sources-manage)

- [Hiérarchisation des sources pour un stock](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/stocks/stocks-prioritize-sources)

- [ Mises à jour en bloc des attributs de produit ](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/create/bulk-product-attribute-update)


>[!IMPORTANT]
>
>La modification de la configuration des sources d&#39;inventaire et de stock peut également avoir un impact en aval sur les systèmes intégrés. Assurez-vous de comprendre l’impact des modifications apportées à la configuration de l’inventaire sur ces systèmes.
