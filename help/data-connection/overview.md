---
title: Présentation du guide
description: Découvrez comment intégrer des données Adobe Commerce à Adobe Experience Platform à l’aide de l’extension  [!DNL Data Connection] .
recommendations: noCatalog
exl-id: 660f9337-cad8-47fb-a959-0770f0fd813c
source-git-commit: 8e3e71c7de56b367a73ab048fa13ba2cdeb55f41
workflow-type: tm+mt
source-wordcount: '1762'
ht-degree: 0%

---

# [!DNL Data Connection] Introduction

>[!IMPORTANT]
>
>Le connecteur Experience Platform a été renommé [!DNL Data Connection].

L’extension [!DNL Data Connection] connecte votre instance web Adobe Commerce au Adobe Experience Platform et à l’Edge Network. Pour les développeurs d’applications mobiles, vous utilisez Adobe Experience Platform Mobile SDK avec Commerce pour capturer et envoyer des données Commerce à Experience Platform. [En savoir plus](./mobile-sdk-epc.md).

Votre boutique Commerce contient une mine de données. Les informations sur la manière dont vos clients parcourent, affichent et achètent finalement les produits sur votre site peuvent révéler des opportunités de créer une expérience d’achat plus personnalisée. Bien que ces données puissent informer les fonctionnalités Commerce natives telles que les règles de prix de panier et les blocs dynamiques, les données restent compartimentées dans votre instance Commerce.

Adobe Experience Platform fournit une suite de technologies qui, lorsqu’elles sont enrichies de données issues de votre boutique Commerce, peuvent les distribuer via Edge Network à d’autres produits Adobe DX afin de déverrouiller les informations sur le comportement d’achat de votre acheteur. Grâce à ces informations détaillées, vous pouvez créer une expérience d’achat plus personnalisée sur tous les canaux.

L’image suivante montre le flux de vos données Commerce de votre magasin vers d’autres produits Adobe DX lorsque l’extension [!DNL Data Connection] est installée et configurée.

![Flux de données vers Experience Platform Edge](assets/commerce-edge.png)

Dans l’image ci-dessus, vos données comportementales, de back-office et de profil client sont envoyées à Experience Platform Edge à l’aide d’un SDK, d’une API et d’un connecteur source. Vous n’avez pas besoin de comprendre entièrement comment ces éléments fonctionnent, car l’extension gère la complexité du partage de données pour vous. Lorsque les données d’événement sont à la périphérie, vous pouvez extraire ces données dans d’autres applications Experience Platform. Par exemple :

| Application | Objectif | Cas d’utilisation |
|---|---|---|
| [Adobe [!DNL Real-Time CDP]](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=fr) | Gestion des profils et service de segmentation | **Segmentation de l’historique des achats** : les commerçants peuvent identifier les clients qui achètent un article selon une période spécifique (mensuelle, trimestrielle, annuelle, etc.). Les commerçants peuvent ensuite créer des segments pour ces clients et les cibler pour les promotions, les campagnes et, _en haut de l’entonnoir_ les données pour les prospects des services d’abonnement<br>. **Segmentation par catégorie** : les commerçants peuvent voir quelle catégorie de produits a été achetée.<br> **Segmentation basée sur l’offre** : les commerçants peuvent identifier les clients qui renvoient régulièrement des produits. Les offres et les remises qui leur sont accordées peuvent désormais être plus intelligentes. Par exemple, la livraison gratuite peut être supprimée pour un client qui renvoie des produits en permanence.<br> **Ciblage semblable** : une _audience semblable_ est une méthodologie adoptée par un commerçant pour ses promotions afin d’atteindre de nouvelles personnes susceptibles d’être intéressées par son entreprise, car elles partagent des caractéristiques similaires à vos clients existants. Les segments semblables peuvent être créés en fonction des données comportementales et transactionnelles. <br> **Propension des clients** : les changements de comportement des clients peuvent être identifiés en raison de profils clients plus détaillés qui peuvent être créés à partir des données transactionnelles. Le degré de confiance dans le score de propension sera plus élevé, car davantage de données seront intégrées aux calculs, comme les retours de produit et les configurations de produit.<br> **Vente croisée** : un commerçant peut identifier de solides opportunités de vente croisée et de vente incitative à partir des informations granulaires capturées dans Commerce. |
| [Client [!DNL Journey Analytics]](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html) | Analyse approfondie du parcours Commerce complet | **Tendances saisonnières** : Un commerçant peut identifier les tendances saisonnières, ce qui l&#39;aide à se préparer aux changements périodiques de la demande pour des produits particuliers. En outre, les commerçants peuvent identifier les changements dans la popularité globale de n&#39;importe quel produit au fil des années.<br> **Analyse de conversion** : en sachant quand un produit a été acheté, ainsi qu’en accédant aux événements d’impression de storefront, les commerçants peuvent générer un profil riche du client pour effectuer une analyse de conversion. |
| [Adobe [!DNL Analytics]](https://experienceleague.adobe.com/docs/analytics/analyze/admin-overview/analytics-overview.html) | Analyse approfondie du comportement des clients et des performances des campagnes | **Retours de commande** : les commerçants peuvent identifier les clients et les segments de clientèle les plus importants qui ont un modèle de retours de produits. Cela aide les commerçants à améliorer leur stratégie commerciale, car ils comprennent à quoi ressemble leur comportement de base de clients.<br> **Adresse de la commande** : en fonction de l’adresse de livraison, un commerçant peut comprendre si les commandes sont passées par les clients eux-mêmes ou si elles sont pour une autre personne ou entité.<br> **Tendances saisonnières** : Un commerçant peut identifier les tendances saisonnières, ce qui l&#39;aide à se préparer aux changements périodiques de la demande pour des produits particuliers. En outre, les commerçants peuvent identifier les changements dans la popularité globale de n&#39;importe quel produit au fil des années.<br> **Analyse de conversion** : en sachant quand un produit a été acheté, ainsi qu’en accédant aux événements d’impression de storefront, les commerçants peuvent générer un profil riche du client pour effectuer une analyse de conversion. **Remarque** Adobe Analytics ne prend en charge que les données d’événement comportementales (storefront). Adobe Analytics ne prend pas en charge les données d’événement transactionnel (backoffice). |
| [Adobe [!DNL Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html) | Orchestration des campagnes sur plusieurs canaux | **parcours basés sur le comportement** : les commerçants peuvent cibler un client qui a acheté un téléphone mobile il y a deux ans en lui suggérant d’acheter le nouveau modèle. Les commerçants peuvent créer des campagnes et des promotions personnalisées pour ces clients et utiliser les fonctionnalités d’e-mail et de SMS pour les contacter. De plus, les commerçants peuvent utiliser l&#39;ordre historique et les données comportementales pour identifier les tendances. Par exemple, un client qui a acheté un article avec une configuration particulière dans le passé et qui envisage maintenant d’acheter le même produit peut voir son parcours d’achat amélioré en lui donnant une visibilité et un accès aux mêmes configurations de produit.<br> **Personalization** : avec un accès aux informations de profil client, [!DNL Journey Optimizer] pouvez déverrouiller des parcours hautement personnalisés, ce qui permet aux commerçants d’atteindre les clients sur plusieurs canaux différents.<br> **Création d’un nouveau profil** : les e-mails de bienvenue et les activités promotionnelles peuvent inciter de nouveaux clients à faire leurs achats et les influencer dans leurs parcours.<br> **Profil supprimé** : les commerçants peuvent choisir de cesser d&#39;envoyer des e-mails promotionnels aux clients qui ont fermé leur compte. Les commerçants peuvent également créer des campagnes pour reconquérir les clients perdus. |

## Extraction des données Experience Platform dans Commerce

L’envoi de vos données Commerce à Experience Platform à l’aide de l’extension [!DNL Data Connection] est un aspect des fonctionnalités de partage de données de Commerce. L’autre côté, qui est une extension facultative, est appelé [Audience Activation](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html). Cette extension vous permet de créer des audiences dans Real-Time CDP et de les déployer dans votre boutique Commerce pour informer les règles de prix de panier, les règles de produit associées et les blocs dynamiques.

À un niveau élevé, le flux de données de votre boutique Commerce vers Experience Platform et retour via l’extension Audience Activation ressemble à ce qui suit :

![[!DNL Data Connection] le flux](assets/data-connection.png)

Une fois la connexion entre Commerce et Experience Platform et Experience Platform vers Commerce configurée, les données continuent à circuler. Vous n’avez pas besoin de vous reconnecter, sauf si une mise à niveau l’exige.

## Concepts

Le partage de données entre ces deux systèmes nécessite la compréhension de plusieurs concepts.

- **Données** - Les données partagées avec Experience Platform sont des données collectées à partir des événements du navigateur sur votre storefront, des événements du back-office sur le serveur et des données d’enregistrement de profil. Les événements de storefront sont capturés à partir des interactions des acheteurs sur le site et incluent des événements tels que [`addToCart`](events.md#addtocart), [`pageView`](events.md#pageview), [`createAccount`](events.md#createaccount), [`editAccount`](events.md#editaccount), [`startCheckout`](events.md#startcheckout), [`completeCheckout`](events.md#completecheckout), [`signIn`](events.md#signin), [`signOut`](events.md#signout), etc. Voir [Événements storefront](events.md#storefront-events) pour obtenir la liste complète des événements storefront. Les événements côté serveur, ou back-office, incluent des informations [état de la commande](events-backoffice.md#order-status) telles que [`orderPlaced`](events-backoffice.md#orderplaced), [`orderReturned`](events-backoffice.md#orderitemreturncompleted), [`orderShipped`](events-backoffice.md#ordershipmentcompleted), [`orderCancelled`](events-backoffice.md#ordercancelled), etc. Voir [Événements back office](events-backoffice.md) pour obtenir la liste complète des événements back office. Les données d’enregistrement de profil contiennent des informations lorsqu’un nouveau profil est créé, mis à jour ou supprimé. Voir [Données d’enregistrement de profil](events-profilerecord.md) pour en savoir plus.

- **Experience Platform et Edge Network** - Entrepôt de données pour la plupart des produits Adobe DX. Les données envoyées à Experience Platform sont propagées aux produits Adobe DX via Experience Platform Edge Network. Par exemple, vous pouvez lancer Journey Optimizer, récupérer vos données d’événement Commerce spécifiques à partir du serveur Edge et créer un e-mail de panier abandonné dans Journey Optimizer. Journey Optimizer peut ensuite envoyer cet e-mail s’il existe des paniers abandonnés dans votre boutique Commerce. En savoir plus sur [Experience Platform et Edge Network](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/overview.html).

- **Schéma** - Le schéma décrit la structure des données envoyées. Avant qu’Experience Platform puisse ingérer vos données Commerce, vous devez composer un schéma pour décrire la structure des données et fournir des contraintes pour le type de données pouvant être contenu dans chaque champ. Les schémas se composent d’une classe de base et de zéro ou plusieurs groupes de champs. Le schéma utilise la structure XDM, que tous les produits Adobe DX peuvent lire. Le schéma garantit que les données envoyées à Experience Platform sont comprises dans tous les produits DX. En savoir plus sur les [schémas](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html).

- **Jeu de données** - Structure de stockage et de gestion pour une collection de données, généralement un tableau contenant un schéma (colonnes) et des champs (lignes). Les jeux de données contiennent également des métadonnées qui décrivent divers aspects des données stockées. Toutes les données correctement ingérées par Adobe Experience Platform sont contenues dans des jeux de données. En savoir plus sur les [ jeux de données ](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html).

- **Flux de données** - Identifiant qui permet aux données de circuler de Adobe Experience Platform vers d’autres produits Adobe DX. Cet identifiant doit être associé à un site web spécifique dans votre instance Adobe Commerce spécifique. Lorsque vous créez ce flux de données, spécifiez le schéma XDM que vous avez créé ci-dessus. En savoir plus sur les [flux de données](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html).

## Architecture prise en charge

L’extension [!DNL Data Connection] est disponible sur les architectures suivantes :

- PHP/Luma
- [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/integrations/adobe-commerce/aep/)
- [AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/integrations/aep.html)

>[!BEGINSHADEBOX]

## Conditions préalables

Pour utiliser l’extension [!DNL Data Connection], vous devez disposer des éléments suivants :

- Adobe Commerce 2.4.4 ou version ultérieure
- Adobe ID et ID d’organisation
- [ACDL (Adobe Client Data Layer)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/client-data-layer/overview.html), nécessaire pour collecter les données d’événement de storefront
- Droits sur d’autres produits Adobe DX.

>[!ENDSHADEBOX]

## Étapes d’intégration

À un niveau élevé, l’activation de l’extension [!DNL Data Connection] implique les étapes suivantes :

1. [Installez](install.md) l’extension [!DNL Data Connection].
1. [Connectez-vous](https://helpx.adobe.com/manage-account/using/access-adobe-id-account.html) à votre compte Adobe et [affichez pour confirmer](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html#concept_EA8AEE5B02CF46ACBDAD6A8508646255) votre ID d’organisation. L’ID d’organisation est l’identifiant associé à votre société Experience Cloud configurée. Cet identifiant est une chaîne alphanumérique de 24 caractères, suivie de (et qui doit inclure) `@AdobeOrg`.
1. Vérifiez que vous disposez des autorisations [autorisation pour la collecte de données dans Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html).
1. Examinez les [types de données](data-ingestion.md) que vous pouvez collecter et envoyer.
1. Créez ou mettez à jour votre [schéma d’événement de série temporelle](update-xdm.md) ou [schéma de données d’enregistrement de profil](profile-data.md) avec des groupes de champs spécifiques à Commerce.
1. [Créez un jeu de données](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html#create-a-dataset) basé sur le schéma que vous avez créé ou mis à jour. Ce jeu de données contient les données Commerce envoyées à Experience Platform Edge.
1. [Créez un flux de données](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html) puis sélectionnez le schéma XDM contenant les groupes de champs spécifiques à Commerce.
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

- [Centre d’aide](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/overview.html){target="_blank"}
- [Tickets d’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket){target="_blank"} : envoyez un ticket pour recevoir de l’aide supplémentaire.
