---
title: Événements Back Office
description: Découvrez les données capturées par chaque événement de back-office.
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: 65cf8150-1a14-4d4c-aa0c-1545109e4fe7
source-git-commit: 1750aee715946d3a871e021cbbee687f54d1ff09
workflow-type: tm+mt
source-wordcount: '3618'
ht-degree: 0%

---

# Événements Back Office [!DNL Data Connection]

Vous trouverez ci-dessous la liste des événements de back-office Commerce disponibles lorsque vous installez l’extension [!DNL Data Connection]. Les données collectées par ces événements sont envoyées au Adobe Experience Platform. Vous pouvez également créer des [événements personnalisés](custom-events.md) pour collecter des données supplémentaires non prêtes à l’emploi.

Outre les données collectées par les événements ci-après, vous obtenez également [d’autres données](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/automatic-information.html) fournies par le SDK Web Adobe Experience Platform.

Les événements Back Office contiennent des données côté serveur. Ces données comprennent [statut de la commande](#order-status) des informations telles que si une commande a été passée, annulée, remboursée, expédiée ou terminée. Les données côté serveur incluent également des informations [événements de profil client](#customer-profile-events) telles que si un compte a été créé, mis à jour ou supprimé.

>[!NOTE]
>
>Tous les événements de back-office incluent le champ [`identityMap`](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/identitymap.html) , qui inclut l’adresse e-mail de l’acheteur, le cas échéant, et l’ECID.

## Statut de la commande

Les données de statut de la commande affichent une vue 360 de la commande de l’acheteur. Cette vue permet aux commerçants de mieux cibler ou analyser l&#39;état complet de la commande lors du développement de campagnes marketing. Par exemple, vous pouvez repérer des tendances dans certaines catégories de produits qui s’en sortent bien à différents moments de l’année. Par exemple, les vêtements d’hiver qui se vendent mieux pendant les mois les plus froids ou certaines couleurs de produits qui intéressent les acheteurs au fil des ans. En outre, les données sur le statut de la commande peuvent vous aider à calculer la valeur client à vie en comprenant la propension d’un acheteur à effectuer une conversion en fonction de commandes précédentes.

### orderPlaced

| Description | Nom de l’événement XDM |
|---|---|
| Déclenché lorsqu’un acheteur passe une commande. | `commerce.backofficeOrderPlaced` |

#### Données collectées lors de la commande passée

Le tableau suivant décrit les données collectées pour cet événement.

| Champ | Description |
|---|---|
| `commerce.order` | Contient des informations sur la commande. |
| `commerce.order.purchaseID` | Identifiant unique attribué par le vendeur à cet achat ou ce contrat. Rien ne garantit que l’ID est unique. |
| `commerce.order.payments` | Liste des paiements pour cette commande. |
| `commerce.order.payments.paymentTransactionID` | Identifiant unique de cette transaction de paiement. |
| `commerce.order.payments.paymentAmount` | Valeur du paiement. |
| `commerce.order.payments.paymentType` | Mode de paiement de cette commande. Comptabilisé, valeurs personnalisées autorisées. |
| `commerce.order.payments.currencyCode` | Code de devise [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilisé, par exemple `USD` ou `EUR`. |
| `commerce.order.taxAmount` | Montant de la taxe payée par l&#39;acheteur dans le cadre du paiement final. |
| `commerce.order.discountAmount` | Indique le montant de la remise appliquée à l&#39;ensemble de la commande. |
| `commerce.order.createdDate` | Date et heure auxquelles une nouvelle commande est créée dans le système Commerce. Par exemple, `2022-10-15T20:20:39+00:00`. |
| `commerce.order.currencyCode` | Code de devise ISO 4217 utilisé pour les totaux des commandes. |
| `commerce.shipping` | Détails d’expédition pour un ou plusieurs produits. |
| `commerce.shipping.shippingMethod` | Méthode d’expédition choisie par le client, telle que la livraison standard, la livraison accélérée, le retrait en magasin, etc. |
| `commerce.shipping.shippingAmount` | Montant que le client a dû payer pour l’expédition. |
| `commerce.shipping.currencyCode` | Code de devise ISO 4217 utilisé pour le total d&#39;expédition. |
| `commerce.commerceScope` | Indique où un événement s’est produit (affichage du magasin, magasin, site web, etc.). |
| `commerce.commerceScope.environmentID` | Identifiant d’environnement. Identifiant alphanumérique à 32 chiffres séparé par des tirets. |
| `commerce.commerceScope.storeCode` | Code de magasin unique. Vous pouvez avoir de nombreux magasins par site web. |
| `commerce.commerceScope.storeViewCode` | Code d’affichage de magasin unique. Vous pouvez avoir plusieurs vues de magasin par magasin. |
| `commerce.commerceScope.websiteCode` | Code unique du site web. Il est possible de disposer de nombreux sites web dans un environnement. |
| `commerce.billing.address` | Adresse postale de facturation. |
| `commerce.billing.address.street1` | informations au niveau de la rue du Principal, numéro d’appartement, numéro de rue et nom de la rue |
| `commerce.billing.address.street2` | Champ supplémentaire pour les informations de niveau rue. |
| `commerce.billing.address.city` | Nom de la ville. |
| `commerce.billing.address.state` | Nom de l’état. Il s’agit d’un champ à structure libre. |
| `commerce.billing.address.postalCode` | Code postal de l’emplacement. Les codes postaux ne sont pas disponibles pour tous les pays. Dans certains pays, il ne contiendra qu&#39;une partie du code postal. |
| `commerce.billing.address.country` | Nom du territoire administré par le gouvernement. À l’exception de `xdm:countryCode`, il s’agit d’un champ à structure libre pouvant contenir le nom du pays dans n’importe quelle langue. |
| `personalEmail` | Adresse e-mail personnelle. |
| `personalEmail.address` | L’adresse technique, par exemple, `name@domain.com` telle qu’elle est généralement définie dans les normes RFC2822 et suivantes. |
| `productListItems` | Tableau de produits dans la commande. |
| `productListItems.id` | Identifiant d&#39;élément de ligne pour cette entrée de produit. |
| `productListItems.SKU` | Unité de stock. Identifiant unique du produit. |
| `productListItems.name` | Nom d’affichage ou nom lisible par l’utilisateur du produit. |
| `productListItems.priceTotal` | Prix total de l’élément de ligne du produit. |
| `productListItems.quantity` | Nombre d’unités de produit dans le panier. |
| `productListItems.discountAmount` | Indique le montant de la remise appliquée. |
| `productListItems.currencyCode` | Code de devise [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilisé, par exemple `USD` ou `EUR`. |
| `productListItems.selectedOptions` | Champ utilisé pour un produit configurable. |
| `productListItems.selectedOptions.attribute` | Identifie un attribut du produit configurable, tel que `size` ou `color`. |
| `productListItems.selectedOptions.value` | Identifie la valeur de l’attribut telle que `small` ou `black`. |
| `productListItems.categories` | Contient des informations sur la catégorie d’un produit. |
| `productListItems.categories.id` | Identifiant unique de la catégorie. |
| `productListItems.categories.name` | Nom de la catégorie. |
| `productListItems.categories.path` | Chemin d’accès à la catégorie. |
| `productListItems.productImageUrl` | URL de l’image principale du produit. |

### orderInvoiced

| Description | Nom de l’événement XDM |
|---|---|
| Déclenché lorsqu’un commerçant envoie une facture pour demander le paiement. | `commerce.backofficeOrderInvoiced` |

#### Données collectées auprès de orderInvoiced

Le tableau suivant décrit les données collectées pour cet événement.

| Champ | Description |
|---|---|
| `commerce.order` | Contient des informations sur la commande. |
| `commerce.order.purchaseID` | Identifiant unique attribué par le vendeur à cet achat ou ce contrat. Rien ne garantit que l’ID est unique. |
| `commerce.order.priceTotal` | Prix total de cette commande après application de toutes les remises et taxes. |
| `commerce.order.currencyCode` | Code de devise ISO 4217 utilisé pour les totaux des commandes. |
| `commerce.order.purchaseOrderNumber` | Identifiant unique attribué par l’acheteur à cet achat ou à ce contrat. |
| `commerce.order.payments` | Liste des paiements pour cette commande. |
| `commerce.order.payments.currencyCode` | Code de devise [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilisé, par exemple `USD` ou `EUR`. |
| `commerce.order.payments.paymentType` | Mode de paiement de cette commande. Comptabilisé, valeurs personnalisées autorisées. |
| `commerce.order.payments.paymentAmount` | Valeur du paiement. |
| `commerce.shipping` | Détails d’expédition pour un ou plusieurs produits. |
| `commerce.shipping.shippingMethod` | Méthode d’expédition choisie par le client, telle que la livraison standard, la livraison accélérée, le retrait en magasin, etc. |
| `commerce.shipping.shippingAmount` | Montant que le client a dû payer pour l’expédition. |
| `commerce.commerceScope` | Indique où un événement s’est produit (affichage du magasin, magasin, site web, etc.). |
| `commerce.commerceScope.environmentID` | Identifiant d’environnement. Identifiant alphanumérique à 32 chiffres séparé par des tirets. |
| `commerce.commerceScope.storeCode` | Code de magasin unique. Vous pouvez avoir de nombreux magasins par site web. |
| `commerce.commerceScope.storeViewCode` | Code d’affichage de magasin unique. Vous pouvez avoir plusieurs vues de magasin par magasin. |
| `commerce.commerceScope.websiteCode` | Code unique du site web. Il est possible de disposer de nombreux sites web dans un environnement. |
| `personalEmail` | Adresse e-mail personnelle. |
| `personalEmail.address` | L’adresse technique, par exemple, `name@domain.com` telle qu’elle est généralement définie dans les normes RFC2822 et suivantes. |
| `productListItems` | Tableau de produits dans la commande. |
| `productListItems.id` | Identifiant d&#39;élément de ligne pour cette entrée de produit. |
| `productListItems.SKU` | Unité de stock. Identifiant unique du produit. |
| `productListItems.name` | Nom d’affichage ou nom lisible par l’utilisateur du produit. |
| `productListItems.priceTotal` | Prix total de l’élément de ligne du produit. |
| `productListItems.quantity` | Nombre d’unités de produit dans le panier. |
| `productListItems.discountAmount` | Indique le montant de la remise appliquée. |
| `productListItems.categories` | Contient des informations sur la catégorie d’un produit. |
| `productListItems.categories.id` | Identifiant unique de la catégorie. |
| `productListItems.categories.name` | Nom de la catégorie. |
| `productListItems.categories.path` | Chemin d’accès à la catégorie. |

### orderItemsShipped

| Description | Nom de l’événement XDM |
|---|---|
| Déclenché lorsqu’une commande est expédiée. | `commerce.backofficeOrderItemsShipped` |

#### Données collectées auprès de orderItemsShipped

Le tableau suivant décrit les données collectées pour cet événement.

| Champ | Description |
|---|---|
| `commerce.order` | Contient des informations sur la commande. |
| `commerce.order.purchaseID` | Identifiant unique attribué par le vendeur à cet achat ou ce contrat. Rien ne garantit que l’ID est unique. |
| `commerce.order.payments` | Liste des paiements pour cette commande. |
| `commerce.order.payments.paymentTransactionID` | Identifiant unique de cette transaction de paiement. |
| `commerce.order.payments.paymentAmount` | Valeur du paiement. |
| `commerce.order.payments.paymentType` | Mode de paiement de cette commande. Comptabilisé, valeurs personnalisées autorisées. |
| `commerce.order.payments.currencyCode` | Code de devise [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilisé, par exemple `USD` ou `EUR`. |
| `commerce.order.priceTotal` | Prix total de cette commande après application de toutes les remises et taxes. |
| `commerce.order.purchaseOrderNumber` | Identifiant unique attribué par l’acheteur à cet achat ou à ce contrat. |
| `commerce.order.currencyCode` | Code de devise [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilisé, par exemple `USD` ou `EUR`. |
| `commerce.order.lastUpdatedDate` | Heure à laquelle un enregistrement de commande particulier est mis à jour pour la dernière fois dans le système Commerce. |
| `commerce.shipping` | Détails d’expédition pour un ou plusieurs produits. |
| `commerce.shipping.shippingMethod` | Méthode d’expédition choisie par le client, telle que la livraison standard, la livraison accélérée, le retrait en magasin, etc. |
| `commerce.shipping.shippingAmount` | Montant que le client a dû payer pour l’expédition. |
| `commerce.shipping.address` | Adresse d’expédition physique. |
| `commerce.shipping.address.street1` | Informations au niveau de la rue du Principal, numéro de l’appartement, numéro de la rue et nom de la rue. |
| `commerce.shipping.address.street2` | Deuxième ligne facultative d&#39;informations concernant la rue. |
| `commerce.shipping.address.city` | Nom de la ville. |
| `commerce.shipping.address.state` | Nom de l’État. Il s’agit d’un champ à structure libre. |
| `commerce.shipping.address.postalCode` | Code postal de l’emplacement. Les codes postaux ne sont pas disponibles pour tous les pays. Dans certains pays, il ne contiendra qu&#39;une partie du code postal. |
| `commerce.shipping.address.country` | Nom du territoire administré par le gouvernement. À l’exception de `xdm:countryCode`, il s’agit d’un champ à structure libre pouvant contenir le nom du pays dans n’importe quelle langue. |
| `commerce.shipping.currencyCode` | Code de devise [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilisé, par exemple `USD` ou `EUR`. |
| `commerce.shipping.trackingNumber` | Numéro de suivi fourni par le transporteur pour une expédition d&#39;article de commande. |
| `commerce.shipping.trackingURL` | URL permettant de suivre le statut d&#39;expédition d&#39;un article de commande. |
| `commerce.shipping.shipDate` | Date d&#39;expédition d&#39;un ou de plusieurs articles d&#39;une commande. |
| `commerce.commerceScope` | Indique où un événement s’est produit (affichage du magasin, magasin, site web, etc.). |
| `commerce.commerceScope.environmentID` | Identifiant d’environnement. Identifiant alphanumérique à 32 chiffres séparé par des tirets. |
| `commerce.commerceScope.storeCode` | Code de magasin unique. Vous pouvez avoir de nombreux magasins par site web. |
| `commerce.commerceScope.storeViewCode` | Code d’affichage de magasin unique. Vous pouvez avoir plusieurs vues de magasin par magasin. |
| `commerce.commerceScope.websiteCode` | Code unique du site web. Il est possible de disposer de nombreux sites web dans un environnement. |
| `commerce.billing.address` | Adresse postale de facturation. |
| `commerce.billing.address.street1` | informations au niveau de la rue du Principal, numéro d’appartement, numéro de rue et nom de la rue |
| `commerce.billing.address.street2` | Champ supplémentaire pour les informations de niveau rue. |
| `commerce.billing.address.city` | Nom de la ville. |
| `commerce.billing.address.state` | Nom de l’état. Il s’agit d’un champ à structure libre. |
| `commerce.billing.address.postalCode` | Code postal de l’emplacement. Les codes postaux ne sont pas disponibles pour tous les pays. Dans certains pays, il ne contiendra qu&#39;une partie du code postal. |
| `commerce.billing.address.country` | Nom du territoire administré par le gouvernement. À l’exception de `xdm:countryCode`, il s’agit d’un champ à structure libre pouvant contenir le nom du pays dans n’importe quelle langue. |
| `personalEmail` | Adresse e-mail personnelle. |
| `personalEmail.address` | L’adresse technique, par exemple, `name@domain.com` telle qu’elle est généralement définie dans les normes RFC2822 et suivantes. |
| `productListItems` | Tableau de produits dans la commande. |
| `productListItems.SKU` | Unité de stock. Identifiant unique du produit. |
| `productListItems.name` | Nom d’affichage ou nom lisible par l’utilisateur du produit. |
| `productListItems.priceTotal` | Prix total de l’élément de ligne du produit. |
| `productListItems.quantity` | Nombre d’unités de produit dans le panier. |
| `productListItems.discountAmount` | Indique le montant de la remise appliquée. |
| `productListItems.currencyCode` | Code de devise [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilisé, par exemple `USD` ou `EUR`. |
| `productListItems.selectedOptions` | Champ utilisé pour un produit configurable. |
| `productListItems.selectedOptions.attribute` | Identifie un attribut du produit configurable, tel que `size` ou `color`. |
| `productListItems.selectedOptions.value` | Identifie la valeur de l’attribut telle que `small` ou `black`. |
| `productListItems.categories` | Contient des informations sur la catégorie d’un produit. |
| `productListItems.categories.id` | Identifiant unique de la catégorie. |
| `productListItems.categories.name` | Nom de la catégorie. |
| `productListItems.categories.path` | Chemin d’accès à la catégorie. |

### orderCancelled

| Description | Nom de l’événement XDM |
|---|---|
| Déclenché lorsqu’un acheteur annule une commande. | `commerce.backofficeOrderCancelled` |

#### Données collectées auprès de orderCancelled

Le tableau suivant décrit les données collectées pour cet événement.

| Champ | Description |
|---|---|
| `commerce.order` | Contient des informations sur la commande. |
| `commerce.order.purchaseID` | Identifiant unique attribué par le vendeur à cet achat ou ce contrat. Rien ne garantit que l’ID est unique. |
| `commerce.order.purchaseOrderNumber` | Identifiant unique attribué par l’acheteur à cet achat ou à ce contrat. |
| `commerce.order.cancelDate` | Date et heure auxquelles un acheteur ou une cliente annule une commande. |
| `commerce.order.lastUpdatedDate` | Heure à laquelle un enregistrement de commande particulier est mis à jour pour la dernière fois dans le système Commerce. |
| `commerce.commerceScope` | Indique où un événement s’est produit (affichage du magasin, magasin, site web, etc.). |
| `commerce.commerceScope.environmentID` | Identifiant d’environnement. Identifiant alphanumérique à 32 chiffres séparé par des tirets. |
| `commerce.commerceScope.storeCode` | Code de magasin unique. Vous pouvez avoir de nombreux magasins par site web. |
| `commerce.commerceScope.storeViewCode` | Code d’affichage de magasin unique. Vous pouvez avoir plusieurs vues de magasin par magasin. |
| `commerce.commerceScope.websiteCode` | Code unique du site web. Il est possible de disposer de nombreux sites web dans un environnement. |
| `personalEmail` | Adresse e-mail personnelle. |
| `personalEmail.address` | L’adresse technique, par exemple, `name@domain.com` telle qu’elle est généralement définie dans les normes RFC2822 et suivantes. |

### orderLineItemRefund

| Description | Nom de l’événement XDM |
|---|---|
| Déclenché lorsqu’un acheteur est remboursé pour un article renvoyé. | `commerce.backofficeCreditMemoIssued` |

#### Données collectées auprès de orderLineItemRefund

Le tableau suivant décrit les données collectées pour cet événement.

| Champ | Description |
|---|---|
| `commerce.order` | Contient des informations sur la commande. |
| `commerce.order.purchaseID` | Identifiant unique attribué par le vendeur à cet achat ou ce contrat. Rien ne garantit que l’ID est unique. |
| `commerce.order.lastUpdatedDate` | Heure à laquelle un enregistrement de commande particulier est mis à jour pour la dernière fois dans le système Commerce. |
| `commerce.order.purchaseOrderNumber` | Identifiant unique attribué par l’acheteur à cet achat ou à ce contrat. |
| `commerce.refunds` | Liste des remboursements pour cette commande. |
| `commerce.refunds.transactionID` | Identifiant unique de ce remboursement. |
| `commerce.refunds.refundAmount` | Valeur du remboursement. |
| `commerce.refunds.refundPaymentType` | Mode de paiement de cette commande. Comptabilisé, valeurs personnalisées autorisées. |
| `commerce.refunds.currencyCode` | Code de devise [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilisé, par exemple `USD` ou `EUR`. |
| `personalEmail` | Adresse e-mail personnelle. |
| `personalEmail.address` | L’adresse technique, par exemple, `name@domain.com` telle qu’elle est généralement définie dans les normes RFC2822 et suivantes. |
| `productListItems` | Tableau de produits dans la commande. |
| `productListItems.SKU` | Unité de stock. Identifiant unique du produit. |
| `productListItems.name` | Nom d’affichage ou nom lisible par l’utilisateur du produit. |
| `productListItems.priceTotal` | Prix total de l’élément de ligne du produit. |
| `productListItems.quantity` | Nombre d’unités de produit dans le panier. |
| `productListItems.discountAmount` | Indique le montant de la remise appliquée. |
| `productListItems.currencyCode` | Code de devise [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilisé, par exemple `USD` ou `EUR`. |
| `productListItems.selectedOptions` | Champ utilisé pour un produit configurable. |
| `productListItems.selectedOptions.attribute` | Identifie un attribut du produit configurable, tel que `size` ou `color`. |
| `productListItems.selectedOptions.value` | Identifie la valeur de l’attribut telle que `small` ou `black`. |
| `productListItems.categories` | Contient des informations sur la catégorie d’un produit. |
| `productListItems.categories.id` | Identifiant unique de la catégorie. |
| `productListItems.categories.name` | Nom de la catégorie. |
| `productListItems.categories.path` | Chemin d’accès à la catégorie. |

### orderItemsReturnInitiated

| Description | Nom de l’événement XDM |
|---|---|
| Déclenché lorsqu’un acheteur demande de renvoyer un article. | `commerce.backofficeOrderItemsReturnInitiated` |

#### Données collectées auprès de orderItemsReturnInitiated

Le tableau suivant décrit les données collectées pour cet événement.

| Champ | Description |
|---|---|
| `commerce.order` | Contient des informations sur la commande. |
| `commerce.order.purchaseID` | Identifiant unique attribué par le vendeur à cet achat ou ce contrat. Rien ne garantit que l’ID est unique. |
| `commerce.order.returns` | Informations RMA (Return Merchandise Authorization) pour cette commande. |
| `commerce.order.returns.returnID` | Identifiant unique de cette autorisation de retour de marchandise (RMA). |
| `commerce.order.returns.returnStatus` | Statut de la RMA (autorisation de retour de marchandise), tel que En attente, Fermé, etc. |
| `commerce.commerceScope` | Indique où un événement s’est produit (affichage du magasin, magasin, site web, etc.). |
| `commerce.commerceScope.environmentID` | Identifiant d’environnement. Identifiant alphanumérique à 32 chiffres séparé par des tirets. |
| `commerce.commerceScope.storeCode` | Code de magasin unique. Vous pouvez avoir de nombreux magasins par site web. |
| `commerce.commerceScope.storeViewCode` | Code d’affichage de magasin unique. Vous pouvez avoir plusieurs vues de magasin par magasin. |
| `commerce.commerceScope.websiteCode` | Code unique du site web. Il est possible de disposer de nombreux sites web dans un environnement. |
| `personalEmail` | Adresse e-mail personnelle. |
| `personalEmail.address` | L’adresse technique, par exemple, `name@domain.com` telle qu’elle est généralement définie dans les normes RFC2822 et suivantes. |
| `productListItems` | Tableau de produits dans la commande. |
| `productListItems.SKU` | Unité de stock. Identifiant unique du produit. |
| `productListItems.name` | Nom d’affichage ou nom lisible par l’utilisateur du produit. |
| `productListItems.quantity` | Nombre d’unités de produit dans le panier. |
| `productListItems.selectedOptions` | Champ utilisé pour un produit configurable. |
| `productListItems.selectedOptions.attribute` | Identifie un attribut du produit configurable, tel que `size` ou `color`. |
| `productListItems.selectedOptions.value` | Identifie la valeur de l’attribut telle que `small` ou `black`. |
| `productListItems.categories` | Contient des informations sur la catégorie d’un produit. |
| `productListItems.categories.id` | Identifiant unique de la catégorie. |
| `productListItems.categories.name` | Nom de la catégorie. |
| `productListItems.categories.path` | Chemin d’accès à la catégorie. |
| `productListItems.returnItem` | Informations RMA (Return Merchandise Authorization) pour cet article. |
| `productListItems.returnItem.returnStatus` | Statut de l’élément renvoyé, tel que En attente, Approuvé, etc. |
| `productListItems.returnItem.returnReason` | Motif pour lequel un retour est demandé pour cet objet. |
| `productListItems.returnItem.returnItemCondition` | Condition de l&#39;article pour lequel le retour est demandé. |
| `productListItems.returnItem.returnResolution` | Résolution demandée de l’élément renvoyé, tel que Remboursement, Échange, etc. |
| `productListItems.returnItem.returnQuantityRequested` | Numéro de cet article que l’acheteur a demandé à renvoyer. |
| `productListItems.returnItem.returnQuantityAuthorized` | Numéro de cet élément qui peut être renvoyé. |
| `productListItems.returnItem.eturnQuantityReceived` | Nombre d’éléments renvoyés reçus. |
| `productListItems.returnItem.returnQuantityApproved` | Numéro de cet article avec retour entièrement terminé et approuvé. |

### orderItemReturnCompleted

| Description | Nom de l’événement XDM |
|---|---|
| Déclenché lorsqu’un article qu’un acheteur a demandé de renvoyer est terminé. | `commerce.backofficeOrderItemsReturnCompleted` |

#### Données collectées auprès de orderItemReturnCompleted

Le tableau suivant décrit les données collectées pour cet événement.

| Champ | Description |
|---|---|
| `commerce.order` | Contient des informations sur la commande. |
| `commerce.order.purchaseID` | Identifiant unique attribué par le vendeur à cet achat ou ce contrat. Rien ne garantit que l’ID est unique. |
| `commerce.order.returns` | Informations RMA (Return Merchandise Authorization) pour cette commande. |
| `commerce.order.returns.returnID` | Identifiant unique de cette autorisation de retour de marchandise (RMA). |
| `commerce.order.returns.returnStatus` | Statut de la RMA (autorisation de retour de marchandise), tel que En attente, Fermé, etc. |
| `commerce.commerceScope` | Indique où un événement s’est produit (affichage du magasin, magasin, site web, etc.). |
| `commerce.commerceScope.environmentID` | Identifiant d’environnement. Identifiant alphanumérique à 32 chiffres séparé par des tirets. |
| `commerce.commerceScope.storeCode` | Code de magasin unique. Vous pouvez avoir de nombreux magasins par site web. |
| `commerce.commerceScope.storeViewCode` | Code d’affichage de magasin unique. Vous pouvez avoir plusieurs vues de magasin par magasin. |
| `commerce.commerceScope.websiteCode` | Code unique du site web. Il est possible de disposer de nombreux sites web dans un environnement. |
| `personalEmail` | Adresse e-mail personnelle. |
| `personalEmail.address` | L’adresse technique, par exemple, `name@domain.com` telle qu’elle est généralement définie dans les normes RFC2822 et suivantes. |
| `productListItems` | Tableau de produits dans la commande. |
| `productListItems.SKU` | Unité de stock. Identifiant unique du produit. |
| `productListItems.name` | Nom d’affichage ou nom lisible par l’utilisateur du produit. |
| `productListItems.selectedOptions` | Champ utilisé pour un produit configurable. |
| `productListItems.selectedOptions.attribute` | Identifie un attribut du produit configurable, tel que `size` ou `color`. |
| `productListItems.selectedOptions.value` | Identifie la valeur de l’attribut telle que `small` ou `black`. |
| `productListItems.categories` | Contient des informations sur la catégorie d’un produit. |
| `productListItems.categories.id` | Identifiant unique de la catégorie. |
| `productListItems.categories.name` | Nom de la catégorie. |
| `productListItems.categories.path` | Chemin d’accès à la catégorie. |
| `productListItems.returnItem` | Informations RMA (Return Merchandise Authorization) pour cet article. |
| `productListItems.returnItem.returnStatus` | Statut de l’élément renvoyé, tel que En attente, Approuvé, etc. |
| `productListItems.returnItem.returnReason` | Motif pour lequel un retour est demandé pour cet objet. |
| `productListItems.returnItem.returnItemCondition` | Condition de l&#39;article pour lequel le retour est demandé. |
| `productListItems.returnItem.returnResolution` | Résolution demandée de l’élément renvoyé, tel que Remboursement, Échange, etc. |
| `productListItems.returnItem.returnQuantityRequested` | Numéro de cet article que l’acheteur a demandé à renvoyer. |
| `productListItems.returnItem.returnQuantityAuthorized` | Numéro de cet élément qui peut être renvoyé. |
| `productListItems.returnItem.eturnQuantityReceived` | Nombre d’éléments renvoyés reçus. |
| `productListItems.returnItem.returnQuantityApproved` | Numéro de cet article avec retour entièrement terminé et approuvé. |

### orderShipmentCompleted

| Description | Nom de l’événement XDM |
|---|---|
| Déclenché lorsqu’une expédition est terminée. | `commerce.backofficeOrderShipmentCompleted` |

#### Données collectées auprès de orderShipmentCompleted

Le tableau suivant décrit les données collectées pour cet événement.

| Champ | Description |
|---|---|
| `commerce.order` | Contient des informations sur la commande. |
| `commerce.order.purchaseID` | Identifiant unique attribué par le vendeur à cet achat ou ce contrat. Rien ne garantit que l’ID est unique. |
| `commerce.order.payments` | Liste des paiements pour cette commande. |
| `commerce.order.payments.paymentTransactionID` | Identifiant unique de cette transaction de paiement. |
| `commerce.order.payments.paymentAmount` | Valeur du paiement. |
| `commerce.order.payments.paymentType` | Mode de paiement de cette commande. Comptabilisé, valeurs personnalisées autorisées. |
| `commerce.order.payments.currencyCode` | Code de devise [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilisé, par exemple `USD` ou `EUR`. |
| `commerce.order.taxAmount` | Montant de la taxe payée par l&#39;acheteur dans le cadre du paiement final. |
| `commerce.order.createdDate` | Date et heure auxquelles une nouvelle commande est créée dans le système Commerce. Par exemple, `2022-10-15T20:20:39+00:00`. |
| `commerce.shipping` | Détails d’expédition pour un ou plusieurs produits. |
| `commerce.shipping.shippingMethod` | Méthode d’expédition choisie par le client, telle que la livraison standard, la livraison accélérée, le retrait en magasin, etc. |
| `commerce.shipping.shippingAmount` | Montant que le client a dû payer pour l’expédition. |
| `commerce.shipping.shipDate` | Date d&#39;expédition d&#39;un ou de plusieurs articles d&#39;une commande. |
| `commerce.shipping.address` | Adresse d’expédition physique. |
| `commerce.shipping.address.street1` | Informations au niveau de la rue du Principal, numéro de l’appartement, numéro de la rue et nom de la rue. |
| `commerce.shipping.address.street2` | Deuxième ligne facultative d&#39;informations concernant la rue. |
| `commerce.shipping.address.city` | Nom de la ville. |
| `commerce.shipping.address.state` | Nom de l’État. Il s’agit d’un champ à structure libre. |
| `commerce.shipping.address.postalCode` | Code postal de l’emplacement. Les codes postaux ne sont pas disponibles pour tous les pays. Dans certains pays, il ne contiendra qu&#39;une partie du code postal. |
| `commerce.shipping.address.country` | Nom du territoire administré par le gouvernement. À l’exception de `xdm:countryCode`, il s’agit d’un champ à structure libre pouvant contenir le nom du pays dans n’importe quelle langue. |
| `commerce.billing.address` | Adresse postale de facturation. |
| `commerce.billing.address.street1` | informations au niveau de la rue du Principal, numéro d’appartement, numéro de rue et nom de la rue |
| `commerce.billing.address.street2` | Champ supplémentaire pour les informations de niveau rue. |
| `commerce.billing.address.city` | Nom de la ville. |
| `commerce.billing.address.state` | Nom de l’état. Il s’agit d’un champ à structure libre. |
| `commerce.billing.address.postalCode` | Code postal de l’emplacement. Les codes postaux ne sont pas disponibles pour tous les pays. Dans certains pays, il ne contiendra qu&#39;une partie du code postal. |
| `commerce.billing.address.country` | Nom du territoire administré par le gouvernement. À l’exception de `xdm:countryCode`, il s’agit d’un champ à structure libre pouvant contenir le nom du pays dans n’importe quelle langue. |
| `personalEmail` | Adresse e-mail personnelle. |
| `personalEmail.address` | L’adresse technique, par exemple, `name@domain.com` telle qu’elle est généralement définie dans les normes RFC2822 et suivantes. |
| `productListItems` | Tableau de produits dans la commande. |
| `productListItems.SKU` | Unité de stock. Identifiant unique du produit. |
| `productListItems.name` | Nom d’affichage ou nom lisible par l’utilisateur du produit. |
| `productListItems.priceTotal` | Prix total de l’élément de ligne du produit. |
| `productListItems.quantity` | Nombre d’unités de produit dans le panier. |
| `productListItems.discountAmount` | Indique le montant de la remise appliquée. |
| `productListItems.currencyCode` | Code de devise [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilisé, par exemple `USD` ou `EUR`. |
| `productListItems.selectedOptions` | Champ utilisé pour un produit configurable. |
| `productListItems.selectedOptions.attribute` | Identifie un attribut du produit configurable, tel que `size` ou `color`. |
| `productListItems.selectedOptions.value` | Identifie la valeur de l’attribut telle que `small` ou `black`. |
| `productListItems.categories` | Contient des informations sur la catégorie d’un produit. |
| `productListItems.categories.id` | Identifiant unique de la catégorie. |
| `productListItems.categories.name` | Nom de la catégorie. |
| `productListItems.categories.path` | Chemin d’accès à la catégorie. |

## Événements de profil client

Les événements de profil capturés côté serveur incluent des informations de compte, telles que `accountCreated`, `accountUpdated` et `accountDeleted`. Ces données sont utilisées pour renseigner les détails client clés nécessaires pour mieux définir les segments ou exécuter des campagnes marketing, tels que l’envoi d’offres de remise d’inscription, de confirmations de modification de compte, etc. Il existe des événements de profil similaires capturés à partir du [storefront](events.md#customer-profile-events).

>[!NOTE]
>
>Chaque événement de profil client inclut également le champ [`identityMap`](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/identitymap.html) , qui inclut l’identifiant client Commerce généré par le système en tant qu’identifiant principal du profil et un identifiant d’e-mail utilisé en tant qu’identifiant secondaire. [Découvrez ](custom-identities.md) comment créer des attributs d’identité personnalisés pour améliorer l’identification du profil client.

### accountCreated

| Description | Nom de l’événement XDM |
|---|---|
| Déclenché lorsqu’un acheteur tente de créer un compte. | `userAccount.backofficeCreateProfile` |

#### Données collectées auprès de accountCreated

Le tableau suivant décrit les données collectées pour cet événement.

| Champ | Description |
|---|---|
| `person` | Contient des informations sur le client. |
| `person.name` | Contient des informations sur le nom du client. |
| `person.name.firstName` | Contient le prénom du client. |
| `person.name.lastName` | Contient le nom du client. |
| `personalEmail` | Adresse e-mail personnelle. |
| `personalEmail.address` | L’adresse technique, par exemple, `name@domain.com` telle qu’elle est généralement définie dans les normes RFC2822 et suivantes. |
| `commerce.commerceScope` | Indique où un événement s’est produit (affichage du magasin, magasin, site web, etc.). |
| `commerce.commerceScope.environmentID` | Identifiant d’environnement. Identifiant alphanumérique à 32 chiffres séparé par des tirets. |
| `commerce.commerceScope.storeCode` | Code de magasin unique. Vous pouvez avoir de nombreux magasins par site web. |
| `commerce.commerceScope.storeViewCode` | Code d’affichage de magasin unique. Vous pouvez avoir plusieurs vues de magasin par magasin. |
| `commerce.commerceScope.websiteCode` | Code unique du site web. Il est possible de disposer de nombreux sites web dans un environnement. |

### accountUpdated

| Description | Nom de l’événement XDM |
|---|---|
| Déclenché lorsqu’un acheteur tente de modifier un compte. | `userAccount.backofficeUpdateProfile` |

#### Données collectées auprès de accountUpdated

Le tableau suivant décrit les données collectées pour cet événement.

| Champ | Description |
|---|---|
| `person` | Contient des informations sur le client. |
| `person.name` | Contient des informations sur le nom du client. |
| `person.name.firstName` | Contient le prénom du client. |
| `person.name.lastName` | Contient le nom du client. |
| `personalEmail` | Adresse e-mail personnelle. |
| `personalEmail.address` | L’adresse technique, par exemple, `name@domain.com` telle qu’elle est généralement définie dans les normes RFC2822 et suivantes. |
| `commerce.commerceScope` | Indique où un événement s’est produit (affichage du magasin, magasin, site web, etc.). |
| `commerce.commerceScope.environmentID` | Identifiant d’environnement. Identifiant alphanumérique à 32 chiffres séparé par des tirets. |
| `commerce.commerceScope.storeCode` | Code de magasin unique. Vous pouvez avoir de nombreux magasins par site web. |
| `commerce.commerceScope.storeViewCode` | Code d’affichage de magasin unique. Vous pouvez avoir plusieurs vues de magasin par magasin. |
| `commerce.commerceScope.websiteCode` | Code unique du site web. Il est possible de disposer de nombreux sites web dans un environnement. |

### accountDeleted

| Description | Nom de l’événement XDM |
|---|---|
| Déclenché lorsqu’un acheteur tente de supprimer un compte. | `userAccount.backofficeDeleteProfile` |

#### Données collectées auprès de accountDeleted

Le tableau suivant décrit les données collectées pour cet événement.

| Champ | Description |
|---|---|
| `person` | Contient des informations sur le client. |
| `person.name` | Contient des informations sur le nom du client. |
| `person.name.firstName` | Contient le prénom du client. |
| `person.name.lastName` | Contient le nom du client. |
| `personalEmail` | Adresse e-mail personnelle. |
| `personalEmail.address` | L’adresse technique, par exemple, `name@domain.com` telle qu’elle est généralement définie dans les normes RFC2822 et suivantes. |
| `commerce.commerceScope` | Indique où un événement s’est produit (affichage du magasin, magasin, site web, etc.). |
| `commerce.commerceScope.environmentID` | Identifiant d’environnement. Identifiant alphanumérique à 32 chiffres séparé par des tirets. |
| `commerce.commerceScope.storeCode` | Code de magasin unique. Vous pouvez avoir de nombreux magasins par site web. |
| `commerce.commerceScope.storeViewCode` | Code d’affichage de magasin unique. Vous pouvez avoir plusieurs vues de magasin par magasin. |
| `commerce.commerceScope.websiteCode` | Code unique du site web. Il est possible de disposer de nombreux sites web dans un environnement. |
