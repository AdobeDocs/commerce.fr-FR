---
title: Prise en main de  [!DNL Adobe Commerce Optimizer]
description: Découvrez comment commencer à utiliser  [!DNL Adobe Commerce Optimizer].
hide: true
recommendations: noCatalog
exl-id: de57d93d-e156-45c1-86aa-de29a8c34bd2
source-git-commit: 9c3f5d1d5e7fd57d2306502d654a854bc5c66c71
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---

# Prise en main

>[!NOTE]
>
>Cette documentation décrit un produit en développement à accès anticipé et ne reflète pas toutes les fonctionnalités destinées à une disponibilité générale.

Ce guide vous guide tout au long de la création et de l’utilisation d’une instance [!DNL Adobe Commerce Optimizer].

<!--Click the tabs below to see high-level workflow overviews for the following user types:

- Administrators
- Merchants
- Developers

>[!BEGINTABS]

>[!TAB Administrator and merchant workflow]

This diagram provides a high-level overview of how administrators and merchants access and manage [!DNL Adobe Commerce Optimizer] instances. See the [Adobe Admin Console Guide](https://helpx.adobe.com/enterprise/admin-guide.html) for more information about administrator workflows.

NEED DIAGRAM

>[!TAB Developer workflow]

This diagram provides a high-level overview of how developers create integrations for [!DNL Adobe Commerce Optimizer] using App Builder. See the [API documentation](https://developer.adobe.com/commerce/webapi/rest/) for more information.

NEED DIAGRAM

>[!ENDTABS]
-->

## Configuration

Une fois les instances [!DNL Adobe Commerce Optimizer] prêtes, l’équipe d’approvisionnement [!DNL Adobe Commerce Optimizer] vous fournit les points d’entrée suivants :

| Poste | Exemple d’URL | Objectif |
|---|---|---|
| Interface utilisateur [!DNL Adobe Commerce Optimizer] | `https://experience.adobe.com/#/@commerceprojectbeacon/commerce-optimizer-studio?tenant=<tenantId>` | Accédez à l’interface utilisateur de Commerce Optimizer pour gérer votre catalogue dans :<br>1. Règles de marchandisage (découverte de produit, recommandations de produit).<br>2. Gestion de catalogue (création de canaux et de politiques).3 <br>. Insights de données (afficher le statut d’ingestion des données de votre catalogue). |
| API Storefront | `https://na1-sandbox.api.commerce.adobe.com/<tenantId>/graphql` | Accédez aux API nécessaires pour configurer votre storefront Commerce optimisé par Edge Delivery Services. |
| API d’ingestion des données de catalogue | `https://na1-sandbox.api.commerce.adobe.com/<tenantId>/v1/catalog/<entity>` | Accédez aux API nécessaires pour ingérer les données de votre catalogue. |

>[!NOTE]
>
>Consultez la [documentation pour les développeurs](https://developer-stage.adobe.com/commerce/services/composable-catalog/) pour en savoir plus sur les API nécessaires à la configuration de Storefront et à l’ingestion de catalogues.

En tant que participant à l’accès anticipé, vous recevrez un e-mail contenant un lien sécurisé qui, avec votre jeton IMS, vous permettra de vous connecter à [!DNL Adobe Commerce Optimizer] ou d’effectuer des appels API.

## Configurer le storefront

Maintenant que vous disposez d’une instance [!DNL Adobe Commerce Optimizer], vous êtes prêt à poursuivre [la configuration](./storefront.md) votre storefront Commerce optimisé par Edge Delivery Services.

## Données de catalogue disponibles pour les participants bénéficiant d’un accès anticipé

En tant que participant à l’accès anticipé, l’instance de [!DNL Adobe Commerce Optimizer] contient des données de catalogue simulées basées sur le cas d’utilisation [ Carvelo](./use-case/admin-use-case.md). Les données simulées, ainsi que certains canaux et politiques préconfigurés, vous permettent de vous familiariser avec l’interface utilisateur de [!DNL Adobe Commerce Optimizer].

<!--Ingest catalog data

By default, [!DNL Adobe Commerce Optimizer] instances do not include any product data.

See the [Ingestion API](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/using-the-api/) documentation to learn how you can import your catalog data into [!DNL Adobe Commerce Optimizer].

The catalog data that you ingest is visible in the [data insights](./insights-overview.md) page. Additionally, you can use the [Catalog](./catalog-overview.md) page to define the channels and policies.-->
