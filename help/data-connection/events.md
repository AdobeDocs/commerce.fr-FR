---
title: Événements comportementaux
description: Découvrez les données capturées par chaque événement comportemental.
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: bcabccc9-8a2e-4045-9306-1d999bb75624
source-git-commit: 631dfacd26a333e70a70f354d191d256d90d946f
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# [!DNL Data Connection] des événements comportementaux

Vous trouverez ci-dessous la liste des événements comportementaux Commerce disponibles lorsque vous installez l’extension [!DNL Data Connection]. Les données collectées par ces événements sont envoyées au Adobe Experience Platform. Vous pouvez également créer des [événements personnalisés](custom-events.md) pour collecter des données supplémentaires non prêtes à l’emploi.

Outre les données collectées par les événements ci-après, vous obtenez également [d’autres données](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/automatic-information.html?lang=fr) fournies par le SDK Web Adobe Experience Platform.

Les événements comportementaux collectent des données comportementales anonymes auprès de vos clients lorsqu’ils parcourent votre site. Vous pouvez utiliser les données collectées par ces événements pour créer des promotions et des campagnes ciblées sur un ensemble spécifique d’acheteurs.

>[!NOTE]
>
>Tous les événements comportementaux incluent le champ [`identityMap`](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/identitymap.html?lang=fr) , qui inclut l’adresse e-mail de l’acheteur, le cas échéant, et l’ECID.

## Événements Storefront

Les événements de storefront capturent des données à partir des interactions des acheteurs sur le site et incluent des événements tels que `addToCart`, `pageView`, `createAccount`, `editAccount`, `startCheckout`, `completeCheckout`, `signIn`, `signOut`, etc. Les événements Storefront s’appliquent uniquement aux produits simples et configurables.

Consultez la [documentation pour les développeurs](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection) pour en savoir plus sur les événements de storefront.

## Événements de profil client

Les événements de profil capturés à partir du storefront incluent des informations de compte, telles que `signIn`, `signOut`, `createAccount` et `editAccount`. Ces données sont utilisées pour renseigner les détails client clés nécessaires pour mieux définir les segments ou exécuter des campagnes marketing, tels que l’envoi d’offres de remise d’inscription, de confirmations de modification de compte, etc.

Consultez la [documentation pour les développeurs](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection) pour en savoir plus sur les événements de profil client.

## Rechercher des événements

Les événements de recherche fournissent des données pertinentes par rapport à l’intention de l’acheteur. Insight dans l’intention d’un acheteur permet aux commerçants de voir comment les acheteurs recherchent des articles, ce sur quoi ils cliquent, et finalement d’acheter ou d’abandonner. Voici un exemple d’utilisation de ces données si vous souhaitez cibler les acheteurs existants qui recherchent votre meilleur produit, mais ne l’achètent jamais. Vous devez installer l’extension [[!DNL Live Search]](../live-search/install.md) pour accéder à ces événements.

Utilisez les champs `searchRequest.id` et `searchResponse.id` des événements `searchRequestSent` et `searchResponseReceived` pour faire référence de manière croisée à une requête de recherche et à la réponse de recherche correspondante.

Pour en savoir plus sur les événements de recherche, consultez la [documentation pour les développeurs](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection).

## Événements B2B

![B2B pour Adobe Commerce](../assets/b2b.svg) Pour les commerçants B2B, vous devez [installer](install.md#install-the-b2b-extension) l’extension `experience-platform-connector-b2b` pour accéder à ces événements.

Les événements B2B contiennent des informations [liste de demandes d&#39;approvisionnement](https://experienceleague.adobe.com/docs/commerce-admin/b2b/requisition-lists/requisition-lists.html?lang=fr) comme si une liste de demandes d&#39;approvisionnement avait été créée, ajoutée ou supprimée. En suivant les événements spécifiques aux listes de demandes d&#39;approvisionnement, vous pouvez voir quels produits vos clients achètent fréquemment et créer des campagnes basées sur ces données.

Consultez la [documentation pour les développeurs](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection) pour en savoir plus sur les événements B2B.
