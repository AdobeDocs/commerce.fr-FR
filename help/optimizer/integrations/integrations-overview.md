---
title: Intégrations Commerce Optimizer
description: Découvrez les intégrations Adobe Commerce Optimizer pour la synchronisation des catalogues, la gestion des ressources, l’optimisation des storefront et la connectivité Salesforce Commerce Cloud.
solution: Commerce
feature: Integration, Catalog Management
role: Developer, Admin
level: Beginner
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S [!DNL Adobe Commerce Optimizer] applique uniquement aux projets (infrastructure SaaS gérée par Adobe)."
exl-id: 8f3a2c1b-9d4e-5f6a-bc7d-1e2f3a4b5c6d
source-git-commit: d8cd6f543353e1b11f3aa14b3b97b02155d23809
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---


# Intégrations [!DNL Adobe Commerce Optimizer]

[!DNL Adobe Commerce Optimizer] comprend des intégrations qui vous permettent de synchroniser les données d’Adobe Commerce sur le cloud ou sur site, de gérer les ressources, d’améliorer les expériences storefront et de connecter des systèmes externes. Les sections ci-dessous décrivent le fonctionnement de chaque intégration avec [!DNL Adobe Commerce Optimizer]. Suivez les liens pour l’installation, la configuration et l’utilisation quotidienne.

## Connecteur Adobe Commerce Optimizer {#aco-connector}

Le connecteur Adobe Commerce Optimizer est le pont qui synchronise les données de catalogue et de tarification entre Adobe Commerce (cloud ou sur site) et [!DNL Adobe Commerce Optimizer]. Lorsque vous activez le connecteur, Commerce reste le système d’enregistrement des données de produit, tandis que [!DNL Adobe Commerce Optimizer] alimente la découverte de produits, les recommandations, les règles de marchandisage, les analyses et les expériences de storefront découplé.

- Présentation du connecteur Adobe Commerce Optimizer [](../../aco-connector/overview.md){target="_blank"}
- [Prise en main du connecteur](../../aco-connector/get-started.md){target="_blank"}

## Visuels de produit avec AEM Assets {#product-visuals}

Les Visuels de produit vous permettent de gérer les images de produit via Adobe Experience Manager (AEM) Assets. Configurez AEM Assets for Commerce Optimizer pour activer les visuels de produit. Une fois la configuration terminée, vous utilisez AEM Assets comme solution centralisée de gestion des ressources numériques pour vos images de produit, avec des workflows automatisés de révision et de gestion des ressources qui maintiennent les images synchronisées avec votre catalogue Commerce Optimizer. L’intégration fait correspondre les ressources aux produits par SKU. Les mises à jour transitent par les services d’intégration d’Adobe afin que les storefronts reflètent les derniers médias sans rechargement manuel.

- [Visuels de produit avec AEM Assets](../setup/product-visuals.md)
- [Configuration d’AEM Assets pour Commerce Optimizer](../../aem-assets-integration/get-started/configure-aco.md){target="_blank"}

## Adobe Experience Manager Sites Optimizer {#aem-sites-optimizer}

Adobe Experience Manager Sites Optimizer analyse les sites web Commerce et améliore les performances en affichant des **[!UICONTROL Opportunities]** pilotées par l’IA sous forme de recommandations qui vous aident à améliorer la découverte, l’engagement et les conversions.

>[!AVAILABILITY]
>
>Cette fonctionnalité nécessite la licence **Ultima** Adobe Sites Optimizer. Vous pouvez demander une licence par l’intermédiaire de votre conseiller technique client Adobe. Une fois votre compte configuré, la fonctionnalité Opportunités est disponible dans l’interface [!DNL Adobe Commerce Optimizer] et vous pouvez commencer à utiliser des informations basées sur l’IA pour optimiser votre storefront et vos stratégies de marchandisage.

- [Opportunités](../manage-results/opportunities.md)

## Connecteur Commerce Salesforce {#commerce-salesforce-connector}

Le connecteur Commerce Salesforce (basé sur Adobe App Builder) synchronise les données de catalogue et de prix de Salesforce Commerce Cloud B2C dans [!DNL Adobe Commerce Optimizer] afin que vous puissiez utiliser les fonctionnalités de storefront et de merchandising d’Adobe sans avoir à reconfigurer votre serveur principal de commerce Salesforce. Vous pouvez planifier des synchronisations, exécuter des mises à jour à la demande et étendre l’intégration à l’aide des API Salesforce Commerce.

- [Connecteur Salesforce Commerce](../developer/salesforce-connector.md)

>[!MORELIKETHIS]
>
>- [Documentation technique de ](https://developer.adobe.com/commerce/services/optimizer/){target="_blank"}
>- [Prise en main de Adobe Commerce Optimizer](../get-started.md)
