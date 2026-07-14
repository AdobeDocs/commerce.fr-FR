---
title: '[!DNL Data Connection] Introduction'
description: Découvrez comment intégrer des données Adobe Commerce à Adobe Experience Platform à l’aide de l’extension  [!DNL Data Connection] .
recommendations: noCatalog
exl-id: 660f9337-cad8-47fb-a959-0770f0fd813c
TQID: https://experienceleague.adobe.com/-wfkGM2isTVmAaJokndxVy0-UtZ4pM9msYXmh2IE-Hc
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
  - id: fd2e3797-f2ea-4b36-a9af-52acf5e90513
source-git-commit: 5ba5dfa23580b5eefa8271277e78c6ea67879b90
workflow-type: tm+mt
source-wordcount: 1373
ht-degree: 1%

---

# [!DNL Data Connection] Introduction

>[!IMPORTANT]
>
>Le connecteur Experience Platform a été renommé [!DNL Data Connection].

L’extension [!DNL Data Connection] connecte votre instance web Adobe Commerce au Adobe Experience Platform et à l’Edge Network. Pour les développeurs d’applications mobiles, vous utilisez Adobe Experience Platform Mobile SDK avec Commerce pour capturer et envoyer des données Commerce à Experience Platform. [En savoir plus](./mobile-sdk-epc.md).

Les commerçants de plusieurs sites web peuvent configurer les paramètres de [!DNL Data Connection] applicables par site web, y compris la sélection de sandbox Experience Platform. Voir [Connexion des données Commerce à Adobe Experience Platform](connect-data.md#configuration-scope) pour connaître les champs globaux et ceux couvrant le site web.

Votre boutique Commerce contient une mine de données. Les informations sur la manière dont vos clients parcourent, affichent et achètent finalement les produits sur votre site peuvent révéler des opportunités de créer une expérience d’achat plus personnalisée. Bien que ces données puissent informer les fonctionnalités Commerce natives telles que les règles de prix de panier et les blocs dynamiques, les données restent compartimentées dans votre instance Commerce.

Adobe Experience Platform fournit une suite de technologies qui, lorsqu’elles sont enrichies de données issues de votre boutique Commerce, peuvent les distribuer via Edge Network à d’autres produits Adobe DX afin de déverrouiller les informations sur le comportement d’achat de votre acheteur. Grâce à ces informations détaillées, vous pouvez créer une expérience d’achat plus personnalisée sur tous les canaux.

L’image suivante montre le flux de vos données Commerce de votre magasin vers d’autres produits Adobe DX lorsque l’extension [!DNL Data Connection] est installée et configurée.

![Flux de données vers Experience Platform Edge](assets/commerce-edge.png)

Dans l’image ci-dessus, vos données comportementales, de back-office et de profil client sont envoyées à Experience Platform Edge à l’aide d’un SDK, d’une API et d’un connecteur source. Vous n’avez pas besoin de comprendre entièrement comment ces éléments fonctionnent, car l’extension gère la complexité du partage de données pour vous. Lorsque les données d’événement sont à la périphérie, vous pouvez les utiliser dans les produits Adobe DX en aval tels que [Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=fr), [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=fr), [Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/analyze/admin-overview/analytics-overview.html?lang=fr) et [Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=fr). Pour obtenir des exemples guidés, consultez [Utilisation de Adobe Journey Optimizer pour envoyer un e-mail de panier abandonné](using-ajo.md) et [Création d’une audience dans Real-Time CDP à l’aide des données d’événement Commerce](create-audience.md).

## Extraction des données Experience Platform dans Commerce

L’envoi de vos données Commerce à Experience Platform à l’aide de l’extension [!DNL Data Connection] est un aspect des fonctionnalités de partage de données de Commerce. L’autre côté, qui est une extension facultative, est appelé [&#128279;](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html?lang=fr). Cette extension vous permet de créer des audiences dans Real-Time CDP et de les déployer dans votre boutique Commerce pour informer les règles de prix de panier, les règles de produit associées et les blocs dynamiques.

À un niveau élevé, le flux de données de votre boutique Commerce vers Experience Platform et retour via l’extension Audience Activation ressemble à ce qui suit :

![[!DNL Data Connection] le flux](assets/data-connection.png)

Une fois la connexion entre Commerce et Experience Platform et Experience Platform vers Commerce configurée, les données continuent à circuler. Vous n’avez pas besoin de vous reconnecter, sauf si une mise à niveau l’exige.

## Concepts

Le partage de données entre ces deux systèmes nécessite la compréhension de plusieurs concepts.

- **Types de données** — [!DNL Data Connection] collecte les données **comportementales (storefront)** du navigateur, **back-office** des données des serveurs Commerce et **profile**. L’administrateur identifie la collection storefront **événements Storefront**. Voir [Types de données Commerce](data-ingestion.md) pour une taxonomie complète.

- **Données comportementales (storefront)** — Capturées à partir des interactions de l’acheteur sur le site, telles que `addToCart`, `pageView`, `startCheckout` et `completeCheckout`. Voir [événements storefront](events.md#storefront-events).

- **Données de back-office** : capturées sur les serveurs Commerce, y compris les événements [état de la commande](events-backoffice.md#order-status) tels que les [`orderPlaced`](events-backoffice.md#orderplaced) et les [`orderShipped`](events-backoffice.md#ordershipmentcompleted). Voir [Événements back office](events-backoffice.md).

- **Enregistrements de profil** — Données d’instantané envoyées lors de la création d’un profil client dans Commerce. Voir [enregistrements de profil](events-profilerecord.md) et [mettre à jour le schéma d’enregistrement de profil](profile-data.md).

- **Événements de profil** — Événements de série temporelle pour les modifications du cycle de vie des profils sur le serveur. Voir [&#x200B; Événements de profil client &#x200B;](events-backoffice.md#customer-profile-events).

- **Experience Platform et Edge Network** - Entrepôt de données pour la plupart des produits Adobe DX. Les données envoyées à Experience Platform sont propagées aux produits Adobe DX via Experience Platform Edge Network. Par exemple, vous pouvez lancer Journey Optimizer, récupérer vos données d’événement Commerce spécifiques à partir du serveur Edge et créer un e-mail de panier abandonné dans Journey Optimizer. Journey Optimizer peut ensuite envoyer cet e-mail s’il existe des paniers abandonnés dans votre boutique Commerce. En savoir plus sur [Experience Platform et Edge Network](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/overview.html?lang=fr).

- **Schéma** - Le schéma décrit la structure des données envoyées. Avant qu’Experience Platform puisse ingérer vos données Commerce, vous devez composer un schéma pour décrire la structure des données et fournir des contraintes pour le type de données pouvant être contenu dans chaque champ. Les schémas se composent d’une classe de base et de zéro ou plusieurs groupes de champs. Le schéma utilise la structure XDM, que tous les produits Adobe DX peuvent lire. Le schéma garantit que les données envoyées à Experience Platform sont comprises dans tous les produits DX. En savoir plus sur les [schémas](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=fr).

- **Jeu de données** - Structure de stockage et de gestion pour une collection de données, généralement un tableau contenant un schéma (colonnes) et des champs (lignes). Les jeux de données contiennent également des métadonnées qui décrivent divers aspects des données stockées. Toutes les données correctement ingérées par Adobe Experience Platform sont contenues dans des jeux de données. En savoir plus sur les [&#x200B; jeux de données &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html?lang=fr).

- **Flux de données** - Identifiant qui permet aux données de circuler de Adobe Experience Platform vers d’autres produits Adobe DX. Cet identifiant doit être associé à un site web spécifique dans votre instance Adobe Commerce spécifique. Lorsque vous créez ce flux de données, spécifiez le schéma XDM que vous avez créé ci-dessus. En savoir plus sur les [flux de données](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=fr).

## Architecture prise en charge

L’extension [!DNL Data Connection] est disponible sur les architectures suivantes :

- PHP/Luma
- [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/integrations/adobe-commerce/aep/)
- [AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/integrations/aep.html?lang=fr)

>[!BEGINSHADEBOX]

## Conditions préalables

Pour utiliser l’extension [!DNL Data Connection], vous devez disposer des éléments suivants :

- Adobe Commerce 2.4.4 ou version ultérieure
- Adobe ID et ID d’organisation
- [ACDL (Adobe Client Data Layer)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/client-data-layer/overview.html?lang=fr), nécessaire pour collecter les données d’événement de storefront
- Droits sur d’autres produits Adobe DX.

>[!ENDSHADEBOX]

## Activer l’extension {#enable-extension}

À un niveau élevé, l’activation de l’extension [!DNL Data Connection] implique les étapes suivantes :

1. [Installez](install.md) l’extension [!DNL Data Connection].
1. [Connectez-vous](https://helpx.adobe.com/fr/manage-account/using/access-adobe-id-account.html) à votre compte Adobe et [affichez pour confirmer](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html?lang=fr#concept_EA8AEE5B02CF46ACBDAD6A8508646255) votre ID d’organisation. L’ID d’organisation est l’identifiant associé à votre société Experience Cloud provisionnée. Cet identifiant est une chaîne alphanumérique de 24 caractères, suivie de (et qui doit inclure) `@AdobeOrg`.
1. Vérifiez que vous disposez des autorisations [autorisation pour la collecte de données dans Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=fr).
1. Examinez les [types de données](data-ingestion.md) que vous pouvez collecter et envoyer.
1. Créez ou mettez à jour votre [schéma d’événement de série temporelle](update-xdm.md) ou [schéma de données d’enregistrement de profil](profile-data.md) avec des groupes de champs spécifiques à Commerce.
1. [Créez un jeu de données](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html?lang=fr#create-a-dataset) basé sur le schéma que vous avez créé ou mis à jour. Ce jeu de données contient les données Commerce envoyées à Experience Platform Edge.
1. [Créez un flux de données](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=fr) puis sélectionnez le schéma XDM contenant les groupes de champs spécifiques à Commerce.
1. [Connexion aux services Commerce](../landing/saas.md).
1. [Connexion à Adobe Experience Platform](connect-data.md).

Le reste de ce guide vous guide tout au long de ces étapes de manière plus détaillée afin que vous puissiez vous familiariser rapidement avec les produits Adobe DX et commencer à les utiliser efficacement dans votre boutique Commerce.

>[!NOTE]
>
>Pour les développeurs mobiles, apprenez à [intégrer](./mobile-sdk-epc.md) le SDK Mobile Adobe Experience Platform avec Commerce.

## Préparation du HIPAA

L’extension [!DNL Data Connection] vous permet de partager [!DNL Commerce] données de back-office avec Experience Platform et de respecter la conformité HIPAA. [En savoir plus](hipaa-readiness.md).

## Audience

Ce guide est conçu pour les commerçants Adobe Commerce qui souhaitent enrichir et personnaliser leur boutique Commerce afin d’améliorer l’expérience d’achat de leurs clients.

## Support technique

Si vous avez besoin d’informations ou si vous avez des questions qui ne sont pas abordées dans ce guide, utilisez les ressources suivantes :

- [Centre d’aide](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/overview.html?lang=fr){target="_blank"}
- [Tickets d’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=fr#submit-ticket){target="_blank"} — Envoyez un ticket pour recevoir de l’aide supplémentaire.
