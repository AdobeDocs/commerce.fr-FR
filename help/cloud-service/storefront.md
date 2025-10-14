---
title: Configurer votre storefront
description: 'Découvrez comment exécuter l’outil de génération de modèles automatique pour configurer votre storefront [!DNL Adobe Commerce as a Cloud Service] '
role: Developer
exl-id: 02928dc4-1777-483e-b0ee-b04fc813864d
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
source-git-commit: 408f28bdc20708022c8eca0fbfea4adb17014bf7
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# Configurer votre storefront

Pour configurer votre storefront Adobe Commerce optimisé par Edge Delivery Services pour Adobe Commerce as a Cloud Service (SaaS), procédez comme suit.

Si vous souhaitez une présentation plus personnalisée et détaillée, reportez-vous à la [documentation storefront](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/?lang=fr).

1. Ouvrez l’[outil de création de site](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator).

1. Sélectionnez **Créer un site (code et contenu)**.

1. Saisissez l’**organisation/nom d’utilisateur Github** où vous souhaitez créer le référentiel de code storefront.

1. Saisissez un **Nom du site**.

1. Dans le champ **Point d’entrée Commerce GraphQL (facultatif)** saisissez le point d’entrée Adobe Commerce as a Cloud Service (SaaS) GraphQL, auquel vous pouvez accéder dans Commerce Cloud Manager après [création de votre instance](./getting-started.md#create-an-instance).

   Si vous utilisez [maillage API](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic), vous pouvez également saisir votre point d’entrée GraphQL du maillage API dans le champ **Point d’entrée GraphQL Commerce (facultatif)**. Pour plus d’informations, voir [Création d’un maillage](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic/create-mesh).

1. Cliquez sur **Créer un site**. Suivez les instructions à l’écran pour autoriser l’accès à votre référentiel Github.

Une fois le processus terminé, vous pouvez personnaliser votre storefront à l’aide des méthodes suivantes :

* Personnalisez votre code : `https://github.com/<username or org>/<repo name>`
* Modifiez votre contenu : `https://da.live/#/<username or org>/<repo name>`
* Gérez votre configuration : `https://da.live/sheet#/<username or org>/<repo name>/configs-stage`
* Prévisualiser votre storefront : `https://main--<repo name>--<username or org>.aem.page/`

## Étapes suivantes

Consultez les articles suivants pour plus d’informations :

* Pour en savoir plus sur la gestion et l’affichage du contenu et des données dans le storefront, voir [mise à jour du contenu du storefront](./use-cases.md#update-storefront-content).
* Pour plus d’informations sur les fonctionnalités d’expérimentation contextuelle, voir [expérimentation contextuelle](./use-cases.md#contextual-experimentation).
* Pour plus d’informations sur l’utilisation de Generative AI pour automatiser la génération de contenu de haute qualité, voir [&#x200B; Générer des variations &#x200B;](./use-cases.md#generate-variations).
* Pour en savoir plus sur la mise à jour du contenu du site et l’intégration aux composants frontend de Commerce et aux données principales, consultez la [documentation du storefront d’Adobe Commerce](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=fr).
