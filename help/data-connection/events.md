---
title: Événements comportementaux
description: Découvrez les données capturées par chaque événement comportemental.
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: bcabccc9-8a2e-4045-9306-1d999bb75624
source-git-commit: 1750aee715946d3a871e021cbbee687f54d1ff09
workflow-type: tm+mt
source-wordcount: '4528'
ht-degree: 0%

---

# [!DNL Data Connection] des événements comportementaux

Vous trouverez ci-dessous la liste des événements comportementaux Commerce disponibles lorsque vous installez l’extension [!DNL Data Connection]. Les données collectées par ces événements sont envoyées au Adobe Experience Platform. Vous pouvez également créer des [événements personnalisés](custom-events.md) pour collecter des données supplémentaires non prêtes à l’emploi.

Outre les données collectées par les événements ci-après, vous obtenez également [d’autres données](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/automatic-information.html) fournies par le SDK Web Adobe Experience Platform.

Les événements comportementaux collectent des données comportementales anonymes auprès de vos clients lorsqu’ils parcourent votre site. Vous pouvez utiliser les données collectées par ces événements pour créer des promotions et des campagnes ciblées sur un ensemble spécifique d’acheteurs.

>[!NOTE]
>
>Tous les événements comportementaux incluent le champ [`identityMap`](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/identitymap.html) , qui inclut l’adresse e-mail de l’acheteur, le cas échéant, et l’ECID.

## Événements Storefront

Les événements de storefront capturent des données à partir des interactions des acheteurs sur le site et incluent des événements tels que [`addToCart`](#addtocart), [`pageView`](#pageview), [`createAccount`](#createaccount), [`editAccount`](#editaccount), [`startCheckout`](#startcheckout), [`completeCheckout`](#completecheckout), [`signIn`](#signin), [`signOut`](#signout), etc. Les événements Storefront s’appliquent uniquement aux produits simples et configurables.

### addToCart

| Description | Nom de l’événement XDM |
|---|---|
| Déclenché lorsqu’un produit est ajouté au panier ou lorsque la quantité d’un produit dans le panier est incrémentée. | `commerce.productListAdds` |

#### Données collectées depuis addToCart

Le tableau suivant décrit les données collectées pour cet événement.

| Champ | Description |
|---|---|
| `channel` | Contient des informations sur la source des données. `_id` et `_type` contiennent tous deux des [valeurs d’espace de noms](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | Identifiant unique du canal, tel que `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifie la source des données du canal, telles que les `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.productListAdds` | Indique si un produit a été ajouté à un panier. Une valeur `1` indique qu’un produit a été ajouté. |
| `commerce.cart.cartID` | ID unique qui identifie le panier du client. |
| `commerce.commerceScope` | Indique où un événement s’est produit (affichage du magasin, magasin, site web, etc.). |
| `commerce.commerceScope.environmentID` | Identifiant d’environnement. Identifiant alphanumérique à 32 chiffres séparé par des tirets. |
| `commerce.commerceScope.storeCode` | Code de magasin unique. Vous pouvez avoir de nombreux magasins par site web. |
| `commerce.commerceScope.storeViewCode` | Code d’affichage de magasin unique. Vous pouvez avoir plusieurs vues de magasin par magasin. |
| `commerce.commerceScope.websiteCode` | Code unique du site web. Il est possible de disposer de nombreux sites web dans un environnement. |
| `productListItems` | Tableau de produits qui ont été ajoutés au panier. |
| `productListItems.SKU` | Unité de stock. Identifiant unique du produit. |
| `productListItems.name` | Nom d’affichage ou nom lisible par l’utilisateur du produit. |
| `productListItems.priceTotal` | Prix total de l’élément de ligne du produit. |
| `productListItems.quantity` | Nombre d’unités de produit dans le panier. |
| `productListItems.discountAmount` | Indique le montant de la remise appliquée. |
| `productListItems.currencyCode` | Code de devise [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilisé, par exemple `USD` ou `EUR`. |
| `productListItems.productImageUrl` | URL de l’image principale du produit. |
| `productListItems.selectedOptions` | Champ utilisé pour un produit configurable. |
| `productListItems.selectedOptions.attribute` | Identifie un attribut du produit configurable, tel que `size` ou `color`. |
| `productListItems.selectedOptions.value` | Identifie la valeur de l’attribut telle que `small` ou `black`. |

### openCart

| Description | Nom de l’événement XDM |
|---|---|
| Déclenché lorsqu’un nouveau panier est créé, c’est-à-dire lorsqu’un produit est ajouté à un panier vide. | `commerce.productListOpens` |

#### Données collectées à partir d’openCart

Le tableau suivant décrit les données collectées pour cet événement.

| Champ | Description |
|---|---|
| `channel` | Contient des informations sur la source des données. `_id` et `_type` contiennent tous deux des [valeurs d’espace de noms](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | Identifiant unique du canal, tel que `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifie la source des données du canal, telles que les `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.productListOpens` | Indique si un panier a été créé. Une valeur `1` indique qu’un panier a été créé. |
| `commerce.cart.cartID` | ID unique qui identifie le panier du client. |
| `commerce.commerceScope` | Indique où un événement s’est produit (affichage du magasin, magasin, site web, etc.). |
| `commerce.commerceScope.environmentID` | Identifiant d’environnement. Identifiant alphanumérique à 32 chiffres séparé par des tirets. |
| `commerce.commerceScope.storeCode` | Code de magasin unique. Vous pouvez avoir de nombreux magasins par site web. |
| `commerce.commerceScope.storeViewCode` | Code d’affichage de magasin unique. Vous pouvez avoir plusieurs vues de magasin par magasin. |
| `commerce.commerceScope.websiteCode` | Code unique du site web. Il est possible de disposer de nombreux sites web dans un environnement. |
| `productListItems` | Tableau de produits qui ont été ajoutés au panier. |
| `productListItems.SKU` | Unité de stock. Identifiant unique du produit. |
| `productListItems.name` | Nom d’affichage ou nom lisible par l’utilisateur du produit. |
| `productListItems.priceTotal` | Prix total de l’élément de ligne du produit. |
| `productListItems.quantity` | Nombre d’unités de produit dans le panier. |
| `productListItems.discountAmount` | Indique le montant de la remise appliquée. |
| `productListItems.currencyCode` | Code de devise [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilisé, par exemple `USD` ou `EUR`. |
| `productListItems.productImageUrl` | URL de l’image principale du produit. |
| `productListItems.selectedOptions` | Champ utilisé pour un produit configurable. |
| `productListItems.selectedOptions.attribute` | Identifie un attribut du produit configurable, tel que `size` ou `color`. |
| `productListItems.selectedOptions.value` | Identifie la valeur de l’attribut telle que `small` ou `black`. |

### removeFromCart

| Description | Nom de l’événement XDM |
|---|---|
| Déclenché chaque fois qu’un produit est supprimé ou que la quantité d’un produit dans le panier est décrémentée. | `commerce.productListRemovals` |

#### Données collectées depuis removeFromCart

Le tableau suivant décrit les données collectées pour cet événement.

| Champ | Description |
|---|---|
| `channel` | Contient des informations sur la source des données. `_id` et `_type` contiennent tous deux des [valeurs d’espace de noms](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | Identifiant unique du canal, tel que `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifie la source des données du canal, telles que les `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.productListRemovals` | Indique si un produit a été supprimé du panier. Une valeur `1` indique qu’un produit a été supprimé du panier. |
| `commerce.cart.cartID` | ID unique qui identifie le panier du client. |
| `commerce.commerceScope` | Indique où un événement s’est produit (affichage du magasin, magasin, site web, etc.). |
| `commerce.commerceScope.environmentID` | Identifiant d’environnement. Identifiant alphanumérique à 32 chiffres séparé par des tirets. |
| `commerce.commerceScope.storeCode` | Code de magasin unique. Vous pouvez avoir de nombreux magasins par site web. |
| `commerce.commerceScope.storeViewCode` | Code d’affichage de magasin unique. Vous pouvez avoir plusieurs vues de magasin par magasin. |
| `commerce.commerceScope.websiteCode` | Code unique du site web. Il est possible de disposer de nombreux sites web dans un environnement. |
| `productListItems` | Tableau de produits qui ont été ajoutés au panier. |
| `productListItems.SKU` | Unité de stock. Identifiant unique du produit. |
| `productListItems.name` | Nom d’affichage ou nom lisible par l’utilisateur du produit. |
| `productListItems.priceTotal` | Prix total de l’élément de ligne du produit. |
| `productListItems.quantity` | Nombre d’unités de produit dans le panier. |
| `productListItems.discountAmount` | Indique le montant de la remise appliquée. |
| `productListItems.currencyCode` | Code de devise [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilisé, par exemple `USD` ou `EUR`. |
| `productListItems.productImageUrl` | URL de l’image principale du produit. |
| `productListItems.selectedOptions` | Champ utilisé pour un produit configurable. |
| `productListItems.selectedOptions.attribute` | Identifie un attribut du produit configurable, tel que `size` ou `color`. |
| `productListItems.selectedOptions.value` | Identifie la valeur de l’attribut telle que `small` ou `black`. |

### shoppingCartView

| Description | Nom de l’événement XDM |
|---|---|
| Déclenché lorsqu’une page du panier se charge. | `commerce.productListViews` |

#### Données collectées depuis shoppingCartView

Le tableau suivant décrit les données collectées pour cet événement.

| Champ | Description |
|---|---|
| `channel` | Contient des informations sur la source des données. `_id` et `_type` contiennent tous deux des [valeurs d’espace de noms](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | Identifiant unique du canal, tel que `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifie la source des données du canal, telles que les `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.productListViews` | Indique si une liste de produits a été consultée. |
| `commerce.cart.cartID` | ID unique qui identifie le panier du client. |
| `commerce.commerceScope` | Indique où un événement s’est produit (affichage du magasin, magasin, site web, etc.). |
| `commerce.commerceScope.environmentID` | Identifiant d’environnement. Identifiant alphanumérique à 32 chiffres séparé par des tirets. |
| `commerce.commerceScope.storeCode` | Code de magasin unique. Vous pouvez avoir de nombreux magasins par site web. |
| `commerce.commerceScope.storeViewCode` | Code d’affichage de magasin unique. Vous pouvez avoir plusieurs vues de magasin par magasin. |
| `commerce.commerceScope.websiteCode` | Code unique du site web. Il est possible de disposer de nombreux sites web dans un environnement. |
| `commerce.order` | Contient des informations sur la commande en attente pour un ou plusieurs produits. |
| `commerce.order.discountAmount` | Indique le montant de la remise appliquée à l&#39;ensemble de la commande. |
| `productListItems` | Tableau de produits qui ont été ajoutés au panier. |
| `productListItems.SKU` | Unité de stock. Identifiant unique du produit. |
| `productListItems.name` | Nom d’affichage ou nom lisible par l’utilisateur du produit. |
| `productListItems.priceTotal` | Prix total de l’élément de ligne du produit. |
| `productListItems.quantity` | Nombre d’unités de produit dans le panier. |
| `productListItems.discountAmount` | Indique le montant de la remise appliquée. |
| `productListItems.currencyCode` | Code de devise [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilisé, par exemple `USD` ou `EUR`. |
| `productListItems.productImageUrl` | URL de l’image principale du produit. |
| `productListItems.selectedOptions` | Champ utilisé pour un produit configurable. |
| `productListItems.selectedOptions.attribute` | Identifie un attribut du produit configurable, tel que `size` ou `color`. |
| `productListItems.selectedOptions.value` | Identifie la valeur de l’attribut telle que `small` ou `black`. |

### pageView

| Description | Nom de l’événement XDM |
|---|---|
| Déclenché lorsqu’une page se charge. | `web.webpagedetails.pageViews` |

#### Données collectées à partir de pageView

Le tableau suivant décrit les données collectées pour cet événement.

| Champ | Description |
|---|---|
| `channel` | Contient des informations sur la source des données. `_id` et `_type` contiennent tous deux des [valeurs d’espace de noms](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | Identifiant unique du canal, tel que `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifie la source des données du canal, telles que les `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `web.webPageDetails.pageViews` | Indique si une page a été chargée. Une `value` de `1` indique que la page a été chargée. |
| `web.webPageDetails.URL` | URL normative ou habituelle de la page web. Il peut s’agir de l’URL réelle utilisée pour accéder à la page, qui est enregistrée à l’aide de `Web Link`. |
| `web.webPageDetails.name` | Nom normatif de la page web. Il ne s’agit pas nécessairement du titre de la page ou du nom directement associé au contenu de la page. En revanche, il est utilisé pour organiser les pages d’un site à des fins de classification. |
| `web.webReferrer.URL` | URL de la page web qu’un acheteur a visitée avant de cliquer sur un lien vers votre site. |
| `commerce.commerceScope` | Indique où un événement s’est produit (affichage du magasin, magasin, site web, etc.). |
| `commerce.commerceScope.environmentID` | Identifiant d’environnement. Identifiant alphanumérique à 32 chiffres séparé par des tirets. |
| `commerce.commerceScope.storeCode` | Code de magasin unique. Vous pouvez avoir de nombreux magasins par site web. |
| `commerce.commerceScope.storeViewCode` | Code d’affichage de magasin unique. Vous pouvez avoir plusieurs vues de magasin par magasin. |
| `commerce.commerceScope.websiteCode` | Code unique du site web. Il est possible de disposer de nombreux sites web dans un environnement. |

### productPageView

| Description | Nom de l’événement XDM |
|---|---|
| Déclenché lorsqu’une page de produit se charge. | `commerce.productViews` |

#### Données collectées à partir de productPageView

Le tableau suivant décrit les données collectées pour cet événement.

| Champ | Description |
|---|---|
| `channel` | Contient des informations sur la source des données. `_id` et `_type` contiennent tous deux des [valeurs d’espace de noms](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | Identifiant unique du canal, tel que `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifie la source des données du canal, telles que les `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.productViews` | Indique si le produit a été consulté. |
| `commerce.commerceScope` | Indique où un événement s’est produit (affichage du magasin, magasin, site web, etc.). |
| `commerce.commerceScope.environmentID` | Identifiant d’environnement. Identifiant alphanumérique à 32 chiffres séparé par des tirets. |
| `commerce.commerceScope.storeCode` | Code de magasin unique. Vous pouvez avoir de nombreux magasins par site web. |
| `commerce.commerceScope.storeViewCode` | Code d’affichage de magasin unique. Vous pouvez avoir plusieurs vues de magasin par magasin. |
| `commerce.commerceScope.websiteCode` | Code unique du site web. Il est possible de disposer de nombreux sites web dans un environnement. |
| `productListItems` | Tableau de produits qui ont été ajoutés au panier. |
| `productListItems.SKU` | Unité de stock. Identifiant unique du produit. |
| `productListItems.name` | Nom d’affichage ou nom lisible par l’utilisateur du produit. |
| `productListItems.priceTotal` | Prix total de l’élément de ligne du produit. |
| `productListItems.quantity` | Nombre d’unités de produit dans le panier. |
| `productListItems.discountAmount` | Indique le montant de la remise appliquée. |
| `productListItems.currencyCode` | Code de devise [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilisé, par exemple `USD` ou `EUR`. |
| `productListItems.productImageUrl` | URL de l’image principale du produit. |
| `productListItems.selectedOptions` | Champ utilisé pour un produit configurable. |
| `productListItems.selectedOptions.attribute` | Identifie un attribut du produit configurable, tel que `size` ou `color`. |
| `productListItems.selectedOptions.value` | Identifie la valeur de l’attribut telle que `small` ou `black`. |

### startCheckout

| Description | Nom de l’événement XDM |
|---|---|
| Déclenché lorsque l’acheteur clique sur un bouton de passage en caisse. | `commerce.checkouts` |

#### Données collectées depuis startCheckout

Le tableau suivant décrit les données collectées pour cet événement.

| Champ | Description |
|---|---|
| `channel` | Contient des informations sur la source des données. `_id` et `_type` contiennent tous deux des [valeurs d’espace de noms](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | Identifiant unique du canal, tel que `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifie la source des données du canal, telles que les `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.checkouts` | Indique si une action s’est produite pendant le processus de passage en caisse. |
| `commerce.cart.cartID` | ID unique qui identifie le panier du client. |
| `commerce.commerceScope` | Indique où un événement s’est produit (affichage du magasin, magasin, site web, etc.). |
| `commerce.commerceScope.environmentID` | Identifiant d’environnement. Identifiant alphanumérique à 32 chiffres séparé par des tirets. |
| `commerce.commerceScope.storeCode` | Code de magasin unique. Vous pouvez avoir de nombreux magasins par site web. |
| `commerce.commerceScope.storeViewCode` | Code d’affichage de magasin unique. Vous pouvez avoir plusieurs vues de magasin par magasin. |
| `commerce.commerceScope.websiteCode` | Code unique du site web. Il est possible de disposer de nombreux sites web dans un environnement. |
| `productListItems` | Tableau de produits qui ont été ajoutés au panier. |
| `productListItems.SKU` | Unité de stock. Identifiant unique du produit. |
| `productListItems.name` | Nom d’affichage ou nom lisible par l’utilisateur du produit. |
| `productListItems.priceTotal` | Prix total de l’élément de ligne du produit. |
| `productListItems.quantity` | Nombre d’unités de produit dans le panier. |
| `productListItems.discountAmount` | Indique le montant de la remise appliquée. |
| `productListItems.currencyCode` | Code de devise [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilisé, par exemple `USD` ou `EUR`. |
| `productListItems.productImageUrl` | URL de l’image principale du produit. |
| `productListItems.selectedOptions` | Champ utilisé pour un produit configurable. |
| `productListItems.selectedOptions.attribute` | Identifie un attribut du produit configurable, tel que `size` ou `color`. |
| `productListItems.selectedOptions.value` | Identifie la valeur de l’attribut telle que `small` ou `black`. |

### completeCheckout

| Description | Nom de l’événement XDM |
|---|---|
| Déclenché lorsque l’acheteur passe une commande. | `commerce.purchases` |

#### Données collectées lors du passage en caisse complet

Le tableau suivant décrit les données collectées pour cet événement.

| Champ | Description |
|---|---|
| `channel` | Contient des informations sur la source des données. `_id` et `_type` contiennent tous deux des [valeurs d’espace de noms](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | Identifiant unique du canal, tel que `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifie la source des données du canal, telles que les `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.purchases` | Indique si une commande a été acceptée. |
| `commerce.order` | Contient des informations sur la commande passée pour un ou plusieurs produits. |
| `commerce.order.purchaseID` | Identifiant unique attribué par le vendeur à cet achat ou ce contrat. Rien ne garantit que l’ID est unique. |
| `commerce.order.payments` | Liste des paiements pour cette commande. |
| `commerce.order.payments.paymentTransactionID` | Identifiant unique de cette transaction de paiement. |
| `commerce.order.payments.paymentAmount` | Valeur du paiement. |
| `commerce.order.payments.paymentType` | Mode de paiement de cette commande. Les options sont les suivantes : `cash`, `credit_card`, `debit_card`, `gift_card`, `check`, `paypal`, `wire_transfer`, `credit_card_reference` et `other`. |
| `commerce.order.payments.currencyCode` | Code de devise [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilisé, par exemple `USD` ou `EUR`. |
| `commerce.order.taxAmount` | Montant de la taxe payée par l&#39;acheteur dans le cadre du paiement final. |
| `commerce.order.discountAmount` | Indique le montant de la remise appliquée à l&#39;ensemble de la commande. |
| `commerce.order.createdDate` | Date et heure auxquelles une nouvelle commande est créée dans le système Commerce. Par exemple, `2022-10-15T20:20:39+00:00`. |
| `commerce.shipping` | Détails d’expédition pour un ou plusieurs produits. |
| `commerce.shipping.shippingMethod` | Méthode d’expédition choisie par le client, telle que la livraison standard, la livraison accélérée, le retrait en magasin, etc. |
| `commerce.shipping.shippingAmount` | Montant que le client a dû payer pour l’expédition. |  | `shipping` | Détails d’expédition pour un ou plusieurs produits. |
| `commerce.shipping.currencyCode` | Code de devise [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilisé, par exemple `USD` ou `EUR`. |
| `commerce.commerceScope` | Indique où un événement s’est produit (affichage du magasin, magasin, site web, etc.). |
| `commerce.commerceScope.environmentID` | Identifiant d’environnement. Identifiant alphanumérique à 32 chiffres séparé par des tirets. |
| `commerce.commerceScope.storeCode` | Code de magasin unique. Vous pouvez avoir de nombreux magasins par site web. |
| `commerce.commerceScope.storeViewCode` | Code d’affichage de magasin unique. Vous pouvez avoir plusieurs vues de magasin par magasin. |
| `commerce.commerceScope.websiteCode` | Code unique du site web. Il est possible de disposer de nombreux sites web dans un environnement. |
| `personalEmail` | Adresse e-mail personnelle. |
| `personalEmail.address` | L’adresse technique, par exemple, `name@domain.com` telle qu’elle est généralement définie dans les normes RFC2822 et suivantes. |
| `productListItems` | Tableau de produits qui ont été ajoutés au panier. |
| `productListItems.SKU` | Unité de stock. Identifiant unique du produit. |
| `productListItems.name` | Nom d’affichage ou nom lisible par l’utilisateur du produit. |
| `productListItems.priceTotal` | Prix total de l’élément de ligne du produit. |
| `productListItems.quantity` | Nombre d’unités de produit dans le panier. |
| `productListItems.discountAmount` | Indique le montant de la remise appliquée. |
| `productListItems.productImageUrl` | URL de l’image principale du produit. |
| `productListItems.selectedOptions` | Champ utilisé pour un produit configurable. |
| `productListItems.selectedOptions.attribute` | Identifie un attribut du produit configurable, tel que `size` ou `color`. |
| `productListItems.selectedOptions.value` | Identifie la valeur de l’attribut telle que `small` ou `black`. |

## Événements de profil client

Les événements de profil capturés à partir du storefront incluent des informations de compte, telles que `signIn`, `signOut`, `createAccount` et `editAccount`. Ces données sont utilisées pour renseigner les détails client clés nécessaires pour mieux définir les segments ou exécuter des campagnes marketing, tels que l’envoi d’offres de remise d’inscription, de confirmations de modification de compte, etc. Il existe des événements de profil similaires capturés à partir du [côté serveur](events-backoffice.md#customer-profile-events).

>[!NOTE]
>
>[Découvrez ](custom-identities.md) comment créer des attributs d’identité personnalisés pour améliorer l’identification du profil client.

### SignIn

| Description | Nom de l’événement XDM |
|---|---|
| Déclenché lorsqu’un acheteur tente de se connecter. | `userAccount.login` |

>[!NOTE]
>
> Cet événement est déclenché lorsque l’action spécifique est tentée. Cela n’indique pas que l’action a réussi.

#### Données collectées lors de la connexion

Le tableau suivant décrit les données collectées pour cet événement.

| Champ | Description |
|---|---|
| `channel` | Contient des informations sur la source des données. `_id` et `_type` contiennent tous deux des [valeurs d’espace de noms](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | Identifiant unique du canal, tel que `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifie la source des données du canal, telles que les `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `person` | Acteur, contact ou propriétaire. |
| `person.accountID` | Capture l’ID du compte utilisateur. |
| `person.accountType` | Capture le type de compte utilisateur, tel que `Personal` ou `Company`, le cas échéant. |
| `person.personalEmailID` | L’adresse technique, par exemple, `name@domain.com` telle qu’elle est généralement définie dans les normes RFC2822 et suivantes. |
| `personalEmail` | Capture les coordonnées : un e-mail et les informations associées. |
| `personalEmail.address` | L’adresse technique, par exemple, `name@domain.com` telle qu’elle est généralement définie dans les normes RFC2822 et suivantes. |
| `userAccount` | Indique les détails de fidélité, les préférences, les processus de connexion et d’autres préférences du compte. |
| `userAccount.login` | Indique si un visiteur a tenté de se connecter. |
| `commerce.commerceScope` | Indique où un événement s’est produit (affichage du magasin, magasin, site web, etc.). |
| `commerce.commerceScope.environmentID` | Identifiant d’environnement. Identifiant alphanumérique à 32 chiffres séparé par des tirets. |
| `commerce.commerceScope.storeCode` | Code de magasin unique. Vous pouvez avoir de nombreux magasins par site web. |
| `commerce.commerceScope.storeViewCode` | Code d’affichage de magasin unique. Vous pouvez avoir plusieurs vues de magasin par magasin. |
| `commerce.commerceScope.websiteCode` | Code unique du site web. Il est possible de disposer de nombreux sites web dans un environnement. |

### SignOut

| Description | Nom de l’événement XDM |
|---|---|
| Déclenché lorsqu’un acheteur tente de se déconnecter. | `userAccount.logout` |

>[!NOTE]
>
> Cet événement est déclenché lorsque l’action spécifique est tentée. Cela n’indique pas que l’action a réussi.

#### Données collectées lors de la déconnexion

Le tableau suivant décrit les données collectées pour cet événement.

| Champ | Description |
|---|---|
| `channel` | Contient des informations sur la source des données. `_id` et `_type` contiennent tous deux des [valeurs d’espace de noms](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | Identifiant unique du canal, tel que `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifie la source des données du canal, telles que les `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `userAccount` | Indique les détails de fidélité, les préférences, les processus de connexion et d’autres préférences du compte. |
| `userAccount.logout` | Indique si un visiteur a tenté de se déconnecter. |
| `commerce.commerceScope` | Indique où un événement s’est produit (affichage du magasin, magasin, site web, etc.). |
| `commerce.commerceScope.environmentID` | Identifiant d’environnement. Identifiant alphanumérique à 32 chiffres séparé par des tirets. |
| `commerce.commerceScope.storeCode` | Code de magasin unique. Vous pouvez avoir de nombreux magasins par site web. |
| `commerce.commerceScope.storeViewCode` | Code d’affichage de magasin unique. Vous pouvez avoir plusieurs vues de magasin par magasin. |
| `commerce.commerceScope.websiteCode` | Code unique du site web. Il est possible de disposer de nombreux sites web dans un environnement. |

### createAccount

| Description | Nom de l’événement XDM |
|---|---|
| Déclenché lorsqu’un acheteur tente de créer un compte. | `userAccount.createProfile` |

>[!NOTE]
>
> Cet événement est déclenché lorsque l’action spécifique est tentée. Cela n’indique pas que l’action a réussi.

#### Données collectées à partir de createAccount

Le tableau suivant décrit les données collectées pour cet événement.

| Champ | Description |
|---|---|
| `channel` | Contient des informations sur la source des données. `_id` et `_type` contiennent tous deux des [valeurs d’espace de noms](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | Identifiant unique du canal, tel que `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifie la source des données du canal, telles que les `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `person` | Acteur, contact ou propriétaire. |
| `person.accountID` | Capture l’ID du compte utilisateur. |
| `person.accountType` | Capture le type de compte utilisateur, tel que `Personal` ou `Company`, le cas échéant. |
| `person.personalEmailID` | L’adresse technique, par exemple, `name@domain.com` telle qu’elle est généralement définie dans les normes RFC2822 et suivantes. |
| `personalEmail` | Capture les coordonnées : un e-mail et les informations associées. |
| `personalEmail.address` | L’adresse technique, par exemple, `name@domain.com` telle qu’elle est généralement définie dans les normes RFC2822 et suivantes. |
| `userAccount` | Indique les détails de fidélité, les préférences, les processus de connexion et d’autres préférences du compte. |
| `userAccount.updateProfile` | Indique si un utilisateur a mis à jour le profil de son compte. |
| `commerce.commerceScope` | Indique où un événement s’est produit (affichage du magasin, magasin, site web, etc.). |
| `commerce.commerceScope.environmentID` | Identifiant d’environnement. Identifiant alphanumérique à 32 chiffres séparé par des tirets. |
| `commerce.commerceScope.storeCode` | Code de magasin unique. Vous pouvez avoir de nombreux magasins par site web. |
| `commerce.commerceScope.storeViewCode` | Code d’affichage de magasin unique. Vous pouvez avoir plusieurs vues de magasin par magasin. |
| `commerce.commerceScope.websiteCode` | Code unique du site web. Il est possible de disposer de nombreux sites web dans un environnement. |

### editAccount

| Description | Nom de l’événement XDM |
|---|---|
| Déclenché lorsqu’un acheteur tente de modifier un compte. | `userAccount.updateProfile` |

>[!NOTE]
>
> Cet événement est déclenché lorsque l’action spécifique est tentée. Cela n’indique pas que l’action a réussi.

#### Données collectées à partir de editAccount

Le tableau suivant décrit les données collectées pour cet événement.

| Champ | Description |
|---|---|
| `channel` | Contient des informations sur la source des données. `_id` et `_type` contiennent tous deux des [valeurs d’espace de noms](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | Identifiant unique du canal, tel que `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifie la source des données du canal, telles que les `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `person` | Acteur, contact ou propriétaire. |
| `person.accountID` | Capture l’ID du compte utilisateur. |
| `person.accountType` | Capture le type de compte utilisateur, tel que `Personal` ou `Company`, le cas échéant. |
| `person.personalEmailID` | L’adresse technique, par exemple, `name@domain.com` telle qu’elle est généralement définie dans les normes RFC2822 et suivantes. |
| `personalEmail` | Capture les coordonnées : un e-mail et les informations associées. |
| `personalEmail.address` | L’adresse technique, par exemple, `name@domain.com` telle qu’elle est généralement définie dans les normes RFC2822 et suivantes. |
| `userAccount` | Indique les détails de fidélité, les préférences, les processus de connexion et d’autres préférences du compte. |
| `userAccount.updateProfile` | Indique si un utilisateur a mis à jour le profil de son compte. |
| `commerce.commerceScope` | Indique où un événement s’est produit (affichage du magasin, magasin, site web, etc.). |
| `commerce.commerceScope.environmentID` | Identifiant d’environnement. Identifiant alphanumérique à 32 chiffres séparé par des tirets. |
| `commerce.commerceScope.storeCode` | Code de magasin unique. Vous pouvez avoir de nombreux magasins par site web. |
| `commerce.commerceScope.storeViewCode` | Code d’affichage de magasin unique. Vous pouvez avoir plusieurs vues de magasin par magasin. |
| `commerce.commerceScope.websiteCode` | Code unique du site web. Il est possible de disposer de nombreux sites web dans un environnement. |

## Rechercher des événements

Les événements de recherche fournissent des données pertinentes par rapport à l’intention de l’acheteur. Insight dans l’intention d’un acheteur permet aux commerçants de voir comment les acheteurs recherchent des articles, ce sur quoi ils cliquent, et finalement d’acheter ou d’abandonner. Voici un exemple d’utilisation de ces données si vous souhaitez cibler les acheteurs existants qui recherchent votre meilleur produit, mais ne l’achètent jamais. Vous devez installer l’extension [[!DNL Live Search]](../live-search/install.md) pour accéder à ces événements.

Utilisez les champs `searchRequest.id` et `searchResponse.id` des événements `searchRequestSent` et `searchResponseReceived` pour faire référence de manière croisée à une requête de recherche et à la réponse de recherche correspondante.

### searchRequestSent

| Description | Nom de l’événement XDM |
|---|---|
| Déclenché par les événements suivants dans la fenêtre contextuelle « Recherche en cours de frappe » :<br><br>Appuyez sur Entrée, Cliquez sur _Afficher tout_<br><br> Déclenché par les événements suivants dans les pages de résultats de recherche :<br><br>Sélectionnez un filtre, modifiez l’ordre de tri (_Trier par_), modifiez le sens du tri (croissant ou décroissant), modifiez le nombre de résultats par page (_Afficher le # par page_), accédez à la page suivante, accédez à la page précédente, accédez à une autre page | `searchRequest` |

>[!NOTE]
>
>Les événements de recherche ne sont pas pris en charge sur une édition d’Adobe Commerce Enterprise avec l’extension B2B installée.

#### Données collectées à partir de searchRequestSent

Le tableau suivant décrit les données collectées pour cet événement.

| Champ | Description |
|---|---|
| `channel` | Contient des informations sur la source des données. `_id` et `_type` contiennent tous deux des [valeurs d’espace de noms](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | Identifiant unique du canal, tel que `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifie la source des données du canal, telles que les `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `searchRequest` | Indique si une requête de recherche a été envoyée. |
| `searchRequest.id` | ID unique de cette requête de recherche spécifique. |
| `searchRequest.value` | Valeur quantifiable de la requête. |
| `siteSearch` | Contient des informations sur la recherche. |
| `siteSearch.filter` | Indique si des filtres ont été appliqués pour limiter les résultats de la recherche. |
| `siteSearch.filter.attribute` (filtre) | Facette d’un élément utilisée pour déterminer s’il faut l’inclure dans les résultats de recherche. |
| `siteSearch.filter.isRange` | Lorsque la valeur est true, les valeurs indiquent des points d’entrée d’une plage de valeurs acceptable. |
| `siteSearch.filter.value` | Valeur d’attribut utilisée pour déterminer les éléments inclus dans les résultats de recherche. |
| `siteSearch.sort` | Indique comment les résultats de recherche doivent être triés. |
| `siteSearch.sort.attribute` (sort) | Attribut utilisé pour trier les éléments dans les résultats de recherche. |
| `siteSearch.sort.order` | Ordre dans lequel renvoyer les résultats de la recherche. |
| `siteSearch.query` | Termes recherchés. |
| `commerce.commerceScope` | Indique où un événement s’est produit (affichage du magasin, magasin, site web, etc.). |
| `commerce.commerceScope.environmentID` | Identifiant d’environnement. Identifiant alphanumérique à 32 chiffres séparé par des tirets. |
| `commerce.commerceScope.storeCode` | Code de magasin unique. Vous pouvez avoir de nombreux magasins par site web. |
| `commerce.commerceScope.storeViewCode` | Code d’affichage de magasin unique. Vous pouvez avoir plusieurs vues de magasin par magasin. |
| `commerce.commerceScope.websiteCode` | Code unique du site web. Il est possible de disposer de nombreux sites web dans un environnement. |

### searchResponseReceived

| Description | Nom de l’événement XDM |
|---|---|
| Déclenché lorsque la recherche en direct renvoie des résultats pour la fenêtre contextuelle ou la page de résultats de recherche « en cours de saisie ». | `searchResponse` |

>[!NOTE]
>
>Les événements de recherche ne sont pas pris en charge sur une édition d’Adobe Commerce Enterprise avec l’extension B2B installée.

#### Données collectées à partir de searchResponseReceived

Le tableau suivant décrit les données collectées pour cet événement.

| Champ | Description |
|---|---|
| `channel` | Contient des informations sur la source des données. `_id` et `_type` contiennent tous deux des [valeurs d’espace de noms](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | Identifiant unique du canal, tel que `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifie la source des données du canal, telles que les `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `searchResponse` | Indique si une réponse de recherche a été reçue. |
| `searchResponse.id` | ID unique de cette réponse de recherche spécifique. |
| `searchResponse.value` | Valeur quantifiable de la réponse. |
| `siteSearch.numberOfResults` | Nombre de produits renvoyés. |
| `siteSearch.suggestions` | Tableau de chaînes contenant les noms des produits et des catégories existant dans le catalogue et similaires à la requête de recherche. |
| `productListItems` | Tableau de produits qui ont été ajoutés au panier. |
| `productListItems.SKU` | Unité de stock. Identifiant unique du produit. |
| `productListItems.name` | Nom d’affichage ou nom lisible par l’utilisateur du produit. |
| `productListItems.productImageUrl` | URL de l’image principale du produit. |
| `commerce.commerceScope` | Indique où un événement s’est produit (affichage du magasin, magasin, site web, etc.). |
| `commerce.commerceScope.environmentID` | Identifiant d’environnement. Identifiant alphanumérique à 32 chiffres séparé par des tirets. |
| `commerce.commerceScope.storeCode` | Code de magasin unique. Vous pouvez avoir de nombreux magasins par site web. |
| `commerce.commerceScope.storeViewCode` | Code d’affichage de magasin unique. Vous pouvez avoir plusieurs vues de magasin par magasin. |
| `commerce.commerceScope.websiteCode` | Code unique du site web. Il est possible de disposer de nombreux sites web dans un environnement. |

## Événements B2B

![B2B pour Adobe Commerce](../assets/b2b.svg) Pour les commerçants B2B, vous devez [installer](install.md#install-the-b2b-extension) l’extension `experience-platform-connector-b2b` pour accéder à ces événements.

Les événements B2B contiennent des informations [liste de demandes d&#39;approvisionnement](https://experienceleague.adobe.com/docs/commerce-admin/b2b/requisition-lists/requisition-lists.html) comme si une liste de demandes d&#39;approvisionnement avait été créée, ajoutée ou supprimée. En suivant les événements spécifiques aux listes de demandes d&#39;approvisionnement, vous pouvez voir quels produits vos clients achètent fréquemment et créer des campagnes basées sur ces données.

### createRequisitionList

| Description | Nom de l’événement XDM |
|---|---|
| Déclenché lorsqu&#39;un acheteur crée une liste de demandes d&#39;approvisionnement. | `commerce.requisitionListOpens` |

#### Données collectées à partir de createRequisitionList

Le tableau suivant décrit les données collectées pour cet événement.

| Champ | Description |
|---|---|
| `channel` | Contient des informations sur la source des données. `_id` et `_type` contiennent tous deux des [valeurs d’espace de noms](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | Identifiant unique du canal, tel que `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifie la source des données du canal, telles que les `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.requisitionListOpens` | Indique l&#39;initialisation d&#39;une nouvelle liste de demandes d&#39;approvisionnement. |
| `commerce.requisitionList` | Propriétés de la liste de demandes d&#39;approvisionnement créée par le client. |
| `commerce.requisitionList.ID` | Identifiant unique de la liste des demandes d&#39;approvisionnement. |
| `commerce.requisitionList.name` | Nom de la liste de demandes d&#39;approvisionnement spécifiée par le client. |
| `commerce.requisitionList.description` | Description de la liste de demandes d&#39;approvisionnement spécifiée par le client. |
| `commerce.commerceScope` | Indique où un événement s’est produit (affichage du magasin, magasin, site web, etc.). |
| `commerce.commerceScope.environmentID` | Identifiant d’environnement. Identifiant alphanumérique à 32 chiffres séparé par des tirets. |
| `commerce.commerceScope.storeCode` | Code de magasin unique. Vous pouvez avoir de nombreux magasins par site web. |
| `commerce.commerceScope.storeViewCode` | Code d’affichage de magasin unique. Vous pouvez avoir plusieurs vues de magasin par magasin. |
| `commerce.commerceScope.websiteCode` | Code unique du site web. Il est possible de disposer de nombreux sites web dans un environnement. |

### addToRequisitionList

| Description | Nom de l’événement XDM |
|---|---|
| Déclenché lorsqu’un acheteur ajoute un produit à une liste de demandes d’approvisionnement existante ou lors de la création d’une liste. | `commerce.requisitionListAdds` |

#### Données collectées depuis addToRequisitionList

Le tableau suivant décrit les données collectées pour cet événement.

| Champ | Description |
|---|---|
| `channel` | Contient des informations sur la source des données. `_id` et `_type` contiennent tous deux des [valeurs d’espace de noms](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | Identifiant unique du canal, tel que `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifie la source des données du canal, telles que les `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.requisitionListAdds` | Indique l&#39;ajout d&#39;un ou plusieurs produits à une liste de demandes d&#39;approvisionnement. |
| `commerce.requisitionList` | Propriétés de la liste de demandes d&#39;approvisionnement créée par le client. |
| `commerce.requisitionList.ID` | Identifiant unique de la liste des demandes d&#39;approvisionnement. |
| `commerce.requisitionList.name` | Nom de la liste de demandes d&#39;approvisionnement spécifiée par le client. |
| `commerce.requisitionList.description` | Description de la liste de demandes d&#39;approvisionnement spécifiée par le client. |
| `commerce.commerceScope` | Indique où un événement s’est produit (affichage du magasin, magasin, site web, etc.). |
| `commerce.commerceScope.environmentID` | Identifiant d’environnement. Identifiant alphanumérique à 32 chiffres séparé par des tirets. |
| `commerce.commerceScope.storeCode` | Code de magasin unique. Vous pouvez avoir de nombreux magasins par site web. |
| `commerce.commerceScope.storeViewCode` | Code d’affichage de magasin unique. Vous pouvez avoir plusieurs vues de magasin par magasin. |
| `commerce.commerceScope.websiteCode` | Code unique du site web. Il est possible de disposer de nombreux sites web dans un environnement. |
| `productListItems` | Tableau de produits ajoutés à la liste des demandes d&#39;approvisionnement. |
| `productListItems.SKU` | Unité de stock. Identifiant unique du produit. |
| `productListItems.name` | Nom d’affichage ou nom lisible par l’utilisateur du produit. |
| `productListItems.priceTotal` | Prix total de l’élément de ligne du produit. |
| `productListItems.quantity` | Nombre d’unités de produit dans le panier. |
| `productListItems.discountAmount` | Indique le montant de la remise appliquée. |
| `productListItems.currencyCode` | Code de devise [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilisé, par exemple `USD` ou `EUR`. |
| `productListItems.selectedOptions` | Champ utilisé pour un produit configurable. |
| `productListItems.selectedOptions.attribute` | Identifie un attribut du produit configurable, tel que `size` ou `color`. |
| `productListItems.selectedOptions.value` | Identifie la valeur de l’attribut telle que `small` ou `black`. |

### removeFromRequisitionList

| Description | Nom de l’événement XDM |
|---|---|
| Déclenché lorsqu’un acheteur supprime un produit d’une liste de demandes d’approvisionnement. | `commerce.requisitionListRemovals` |

#### Données collectées depuis removeFromRequisitionList

Le tableau suivant décrit les données collectées pour cet événement.

| Champ | Description |
|---|---|
| `channel` | Contient des informations sur la source des données. `_id` et `_type` contiennent tous deux des [valeurs d’espace de noms](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | Identifiant unique du canal, tel que `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifie la source des données du canal, telles que les `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.requsitionListRemovals` | Indique la suppression d&#39;un ou de plusieurs produits d&#39;une liste de demandes d&#39;approvisionnement. |
| `commerce.requisitionList` | Propriétés de la liste de demandes d&#39;approvisionnement créée par le client. |
| `commerce.requisitionList.ID` | Identifiant unique de la liste des demandes d&#39;approvisionnement. |
| `commerce.requisitionList.name` | Nom de la liste de demandes d&#39;approvisionnement spécifiée par le client. |
| `commerce.requisitionList.description` | Description de la liste de demandes d&#39;approvisionnement spécifiée par le client. |
| `commerce.commerceScope` | Indique où un événement s’est produit (affichage du magasin, magasin, site web, etc.). |
| `commerce.commerceScope.environmentID` | Identifiant d’environnement. Identifiant alphanumérique à 32 chiffres séparé par des tirets. |
| `commerce.commerceScope.storeCode` | Code de magasin unique. Vous pouvez avoir de nombreux magasins par site web. |
| `commerce.commerceScope.storeViewCode` | Code d’affichage de magasin unique. Vous pouvez avoir plusieurs vues de magasin par magasin. |
| `commerce.commerceScope.websiteCode` | Code unique du site web. Il est possible de disposer de nombreux sites web dans un environnement. |
| `productListItems` | Tableau de produits ajoutés à la liste des demandes d&#39;approvisionnement. |
| `productListItems.SKU` | Unité de stock. Identifiant unique du produit. |
| `productListItems.name` | Nom d’affichage ou nom lisible par l’utilisateur du produit. |
| `productListItems.priceTotal` | Prix total de l’élément de ligne du produit. |
| `productListItems.quantity` | Nombre d’unités de produit dans le panier. |
| `productListItems.discountAmount` | Indique le montant de la remise appliquée. |
| `productListItems.currencyCode` | Code de devise [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilisé, par exemple `USD` ou `EUR`. |
| `productListItems.selectedOptions` | Champ utilisé pour un produit configurable. |
| `productListItems.selectedOptions.attribute` | Identifie un attribut du produit configurable, tel que `size` ou `color`. |
| `productListItems.selectedOptions.value` | Identifie la valeur de l’attribut telle que `small` ou `black`. |

### deleteRequisitionList

| Description | Nom de l’événement XDM |
|---|---|
| Déclenché lorsqu&#39;un acheteur supprime une liste de demandes d&#39;approvisionnement. | `commerce.requisitionListDeletes` |

#### Données collectées à partir de deleteRequisitionList

Le tableau suivant décrit les données collectées pour cet événement.

| Champ | Description |
|---|---|
| `channel` | Contient des informations sur la source des données. `_id` et `_type` contiennent tous deux des [valeurs d’espace de noms](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | Identifiant unique du canal, tel que `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifie la source des données du canal, telles que les `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.requisitionListDeletes` | Indique qu&#39;une liste de demandes d&#39;approvisionnement a été supprimée. |
| `commerce.requisitionList` | Propriétés de la liste de demandes d&#39;approvisionnement créée par le client. |
| `commerce.requisitionList.ID` | Identifiant unique de la liste des demandes d&#39;approvisionnement. |
| `commerce.requisitionList.name` | Nom de la liste de demandes d&#39;approvisionnement spécifiée par le client. |
| `commerce.requisitionList.description` | Description de la liste de demandes d&#39;approvisionnement spécifiée par le client. |
| `commerce.commerceScope` | Indique où un événement s’est produit (affichage du magasin, magasin, site web, etc.). |
| `commerce.commerceScope.environmentID` | Identifiant d’environnement. Identifiant alphanumérique à 32 chiffres séparé par des tirets. |
| `commerce.commerceScope.storeCode` | Code de magasin unique. Vous pouvez avoir de nombreux magasins par site web. |
| `commerce.commerceScope.storeViewCode` | Code d’affichage de magasin unique. Vous pouvez avoir plusieurs vues de magasin par magasin. |
| `commerce.commerceScope.websiteCode` | Code unique du site web. Il est possible de disposer de nombreux sites web dans un environnement. |
