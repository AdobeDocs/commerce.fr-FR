---
title: Améliorez la découverte de produits avec Adobe Commerce Live Search
description: Découvrez comment utiliser les informations sur les performances de recherche et la recherche sémantique pour aider les acheteurs à trouver des produits pertinents.
audience: Merchandisers, commerce administrators, and store owners
autotag-review: '2026-10-21T12:57:39.807Z'
TQID: 'https://experienceleague.adobe.com/vUbbKdcd7RFb3YUNNjlW4u7AgtiXJKeZeRs9uJwxYyY'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 76cfaac4-e563-56dd-8938-708bf8b84956
    internal-label: Attributes
  - id: cdfd3bc1-dc23-5cf0-b965-d3c0c55cde67
    internal-label: Best Practices
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
    internal-label: Catalog management
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: 125c1f49-aefd-5f34-a252-288937f95f6b
    internal-label: Marketing Tools
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
topic_v2:
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
    internal-label: Insights
source-git-commit: f54c816fd23786ec519d5c890bc2664c3dcf8c6f
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 0%
---

# Améliorez la découverte de produits avec Adobe Commerce Live Search

<table style="table-layout:auto">
<tr style="border: 0;">
   <td valign="middle" style="vertical-align: middle;"><img alt="Portrait de Sandra Gonzalez Mangana" src="../../assets/guidance-and-insights/live-search-author-avatar-sgonzalezmangana.png" width="96"><br><strong>Sandra Gonzalez Mangana</strong><br><em>Responsable produit senior</em></td>
</tr>
</table>

*Aidez les acheteurs à trouver les produits dont ils ont besoin grâce aux informations sur les performances de recherche et à la recherche sémantique.*

Avoir les bons produits dans votre catalogue n&#39;est qu&#39;une partie de l&#39;expérience d&#39;achat. Les acheteurs doivent également être en mesure de trouver ces produits en utilisant les mots, les expressions et les questions qu&#39;ils utilisent naturellement.

Adobe Commerce Live Search fournit des informations sur les performances de recherche qui peuvent vous aider à repérer les problèmes de découverte et à affiner l’expérience. Utilisez ces informations pour identifier les endroits où les acheteurs ont des difficultés, et pas seulement pour savoir si la recherche renvoie des résultats.

## Rechercher des signaux dans les performances de recherche

Dans l’espace de travail Performances de la recherche en direct , passez en revue des mesures telles que les recherches uniques, les recherches à zéro résultat, les résultats populaires, le taux de clic publicitaire, le taux de conversion et la position moyenne des clics. Utilisez-les pour identifier les tendances et décider quelles requêtes ou quels produits nécessitent une attention particulière. [Performances](https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-admin/performance)

Espace de travail Performances de la recherche en direct ![ présentant les recherches uniques, la position moyenne des clics, le taux de clic publicitaire, le taux de conversion et le taux de résultats nuls, avec des onglets pour les recherches uniques, les résultats nuls et les résultats populaires](../../assets/guidance-and-insights/live-search-performance-dashboard.png){width="800" zoomable="yes"}

*L’espace de travail Performances de Live Search affiche les mesures à vérifier. Les valeurs affichées sont des exemples de données.*

Tenez compte des signaux suivants :

- **Recherches sans résultat :** les requêtes sans résultat peuvent indiquer des lacunes dans votre catalogue, les informations sur les produits ou la configuration de la recherche. Visez à maintenir les recherches sans résultat en dessous de 5 %. Un taux supérieur à ce seuil est un signal qui mérite d&#39;être étudié.
- **Position de clic faible ou de clic faible :** les acheteurs peuvent voir des résultats qui ne correspondent pas à leurs besoins ou les produits pertinents peuvent ne pas être suffisamment importants. Pour garantir l’engagement, visez à ce qu’au moins 50 % des recherches génèrent un clic sur le produit.
- **Conversion faible à partir de la recherche :** vérifier si la recherche aide les acheteurs à passer d’une requête à un achat. Visez un taux de conversion supérieur à 3 %.

Traitez-les comme des signaux de référence et de diagnostic, et non comme un succès ou un échec universel. Les performances varient selon le secteur d’activité, la complexité du catalogue, le comportement des clients et la manière dont chaque mesure est mesurée. Établissez une base de référence pour votre magasin et comparez les performances au fil du temps. Les résultats peuvent varier en fonction de votre catalogue, des acheteurs et de la manière dont vous mesurez les résultats.

## Correspondre l’intention de l’acheteur, pas seulement les mots exacts

Les acheteurs ne décrivent pas toujours les produits à l’aide de la terminologie de votre catalogue. Par exemple, une personne qui cherche des « chaussures confortables pour rester debout toute la journée » peut être intéressée par des produits appelés « baskets de marche rembourrées ».

La recherche sémantique utilise le sens et le contexte ainsi que la correspondance de mots-clés, ce qui permet de connecter les requêtes en langage naturel aux produits appropriés même lorsque la requête ne correspond pas exactement à la formulation du catalogue. La recherche en direct combine la correspondance sémantique et par mot-clé dans une seule expérience de recherche. [Recherche sémantique](https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-admin/semantic-search)

La correspondance sémantique peut faciliter les recherches exploratoires, mais la pertinence dépend toujours des produits et des informations disponibles dans votre catalogue. Pour les recherches impliquant un modèle, une spécification ou une exigence de compatibilité exacts, vérifiez que les résultats restent précis.

## Vérifier la recherche sémantique pour votre déploiement

La configuration dépend du produit Adobe Commerce que vous utilisez :

- **Adobe Commerce sur les infrastructures cloud ou sur site :** la recherche sémantique Live Search est disponible pour Adobe Commerce 2.4.4 et les versions ultérieures. Dans Admin, accédez à Marketing > SEO et recherche > Recherche en direct, ouvrez les paramètres, activez la recherche sémantique et enregistrez. Il prend en charge les catalogues anglais. [Paramètres—Recherche sémantique](https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-admin/settings)
- **Adobe Commerce as a Cloud Service :** le système active par défaut la recherche sémantique. Il prend en charge les catalogues anglais. [Recherche sémantique](https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-admin/semantic-search)
- **Adobe Commerce Optimizer :** le système active la recherche sémantique par défaut. Vous pouvez éventuellement régler des commandes telles que l’amplification sémantique et le seuil de similarité. Les paramètres incluent également des options de recherche floue. [Recherche sémantique](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/semantic-search) · [Paramètres—Réglage facultatif](https://experienceleague.adobe.com/en/docs/commerce/optimizer/settings)

## Transformer les informations de recherche en action

Utilisez un cycle de révision continu pour améliorer la découverte de produits :

1. **Rechercher des requêtes à étudier.** Examinez les recherches sans résultat, les requêtes populaires et les recherches avec un faible engagement.
2. **Vérifiez ce que l’acheteur demande.** Déterminez si la requête pointe vers un produit manquant, une incohérence de libellé ou des données de produit imprécises.
3. **Améliorez les informations sur les produits.** Rendez les attributs et les descriptions des produits exacts et utiles pour les termes utilisés par les acheteurs. Pour la recherche en direct, Adobe recommande de configurer les attributs et poids recherchables appropriés et de s’assurer que les données d’attribut sont pertinentes. [Bonnes pratiques de recherche en direct](https://experienceleague.adobe.com/en/docs/commerce/live-search/best-practice)
4. **Affiner l’expérience de recherche.** Le cas échéant, utilisez des règles de recherche, des synonymes et des facettes pour aider les acheteurs à trouver et à affiner les résultats pertinents. [Bonnes pratiques de recherche en direct](https://experienceleague.adobe.com/en/docs/commerce/live-search/best-practice)
5. **Examinez les résultats et répétez l’opération.** Surveillez les mêmes requêtes et signaux de performances après avoir apporté des modifications, puis ajustez-les en fonction de ce que font les acheteurs.

## Faire en sorte que chaque recherche compte

Une requête de recherche est un signal de ce que veut un acheteur. En associant les informations sur les performances de recherche à des informations produit pertinentes et aux fonctionnalités de recherche appropriées, vous pouvez faciliter la découverte de produits répondant à leurs besoins pour les acheteurs.

### En savoir plus

- [Présentation de la recherche en direct](../../../live-search/overview.md)
- [Bonnes pratiques relatives à Live Search](../../../live-search/best-practice.md)
- [Recherche sémantique](../../../live-search/semantic-search.md) pour Adobe Commerce sur les infrastructures cloud
- [Recherche sémantique](../../../optimizer/setup/semantic-search.md) pour Adobe Commerce Optimizer
