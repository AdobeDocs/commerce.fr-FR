---
title: Configurer votre storefront
description: 'Découvrez comment exécuter l’outil de génération de modèles automatique pour configurer votre storefront [!DNL Adobe Commerce as a Cloud Service] '
feature: Storefront
role: Developer
level: Beginner
exl-id: 02928dc4-1777-483e-b0ee-b04fc813864d
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
source-git-commit: 6eda2197fde2e88292e58b2bb4fc4759f24da558
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# Configurer votre storefront

Pour configurer votre [!DNL Adobe Commerce Storefront] optimisé par [!DNL Edge Delivery Services] for [!DNL Adobe Commerce as a Cloud Service] (SaaS), procédez comme suit.

Pour une présentation plus personnalisée et détaillée, reportez-vous à la [documentation storefront](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/).

1. Ouvrez l’[outil de création de site](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator).

1. Sélectionnez **[!UICONTROL Create New Site (Code & Content)]**.

1. Saisissez le **[!UICONTROL Github Organization/Username]** dans lequel vous souhaitez créer le référentiel de code du storefront.

1. Saisissez un **[!UICONTROL Site Name]**.

1. Dans le champ **[!UICONTROL Commerce GraphQL Endpoint (optional)]** , saisissez le point d’entrée de GraphQL [!DNL Adobe Commerce as a Cloud Service] (SaaS) auquel vous pouvez accéder dans le gestionnaire Commerce Cloud après [création de votre instance](./getting-started.md#create-an-instance).

   Si vous utilisez [[!DNL API Mesh]](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic), vous pouvez également saisir votre point d’entrée [!DNL API Mesh] GraphQL dans le champ **[!UICONTROL Commerce GraphQL Endpoint (optional)]** . Pour plus d’informations, voir [Création d’un maillage](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic/create-mesh).

1. Cliquez sur **[!UICONTROL Create Site]**. Suivez les instructions à l’écran pour autoriser l’accès à votre référentiel GitHub.

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
* Pour en savoir plus sur la mise à jour du contenu du site et l’intégration aux composants frontaux et aux données principales de Commerce, consultez la [[!DNL Adobe Commerce Storefront documentation]](https://experienceleague.adobe.com/developer/commerce/storefront/) .
