---
title: Configurer votre storefront
description: 'Découvrez comment exécuter l’outil de génération de modèles automatique pour configurer votre storefront [!DNL Adobe Commerce as a Cloud Service] '
feature: Storefront
role: Developer
level: Beginner
exl-id: 02928dc4-1777-483e-b0ee-b04fc813864d
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
source-git-commit: 0cd9749574460374a8fe875f1eff54f2a4a8d614
workflow-type: tm+mt
source-wordcount: '250'
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

* [Mise à jour du contenu du storefront](./use-cases.md#update-storefront-content) : gérez et affichez le contenu et les données sur le storefront.
* [Expérimentation contextuelle](./use-cases.md#contextual-experimentation) : créez et gérez des expériences sur votre storefront.
* [Générer des variations](./use-cases.md#generate-variations) : utilisez Generative AI pour automatiser la génération de contenu de haute qualité.
* [Documentation d’Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/)—Obtenez des informations détaillées sur la mise à jour du contenu du site et l’intégration aux composants frontend de Commerce et aux données principales.
* [Service de configuration](https://www.aem.live/docs/config-service-setup) : découvrez comment migrer votre configuration de storefront depuis `config.json` pour utiliser le service de configuration, qui prend en charge les cas d’utilisation avancés tels que la configuration et les recouvrements repoless.
