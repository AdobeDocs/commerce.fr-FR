---
title: Présentation de  [!DNL Product Recommendations]
description: '[!DNL Product Recommendations] sont des outils marketing puissants que vous pouvez utiliser pour augmenter les conversions, augmenter le chiffre d’affaires et stimuler l’engagement des acheteurs.'
recommendations: noCatalog
badgePaas: label="PaaS uniquement" type="Informative" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."
exl-id: 72850cfd-555c-4e0e-ac3e-097e6dac2030
source-git-commit: 3821893c3df01e2e36ab0142616e52c1c92b4d51
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---

# Présentation de [!DNL Product Recommendations]

Les recommandations de produits sont un puissant outil marketing que vous pouvez utiliser pour augmenter les conversions, augmenter le chiffre d’affaires et stimuler l’engagement des acheteurs. Les recommandations de produits Adobe Commerce sont optimisées par [Adobe Sensei](https://www.adobe.com/sensei.html), qui utilise l’intelligence artificielle et des algorithmes de machine learning pour effectuer une analyse approfondie des données agrégées sur les visiteurs. Ces données, lorsqu’elles sont combinées à votre catalogue Adobe Commerce, offrent une expérience très attrayante, pertinente et personnalisée.

Les recommandations de produits sont affichées sur le storefront sous la forme d’unités avec des étiquettes, telles que « Les clients qui ont consulté ce produit ont également consulté ». Vous pouvez créer, gérer et déployer des recommandations dans les vues de votre boutique directement depuis Adobe Commerce Admin.

Si votre storefront est implémenté à l’aide de PWA Studio, consultez la documentation de [PWA](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/). Si vous utilisez une technologie frontale personnalisée telle que React ou Vue JS, apprenez à [intégrer](headless.md) [!DNL Product Recommendations] dans votre storefront découplé.

>[!NOTE]
>
>Il existe de nombreuses façons de développer une implémentation découplée ou personnalisée. Ce guide décrit une façon de le faire, en utilisant PWA Studio. Elle ne couvre pas tous les scénarios ou toutes les éventualités.

## Confidentialité

La collecte de données à des fins de [!DNL Product Recommendations] n’inclut aucune information d’identification personnelle (PII). En outre, tous les identifiants d’utilisateur tels que les ID de cookie et les adresses IP sont strictement anonymisés. Pour en savoir plus, consultez la [Politique de confidentialité d’Adobe](https://www.adobe.com/privacy/policy.html).

[!DNL Product Recommendations] utilisateurs peuvent consulter le [Tableau de bord de gestion des données](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-dashboard.html?lang=fr) pour plus d’informations sur la synchronisation des données.

## Recommandations de produits par rapport aux relations entre les produits

Étant donné la complexité en constante évolution des achats en ligne, ce qui fonctionne le mieux pour votre vitrine est souvent une combinaison de plusieurs technologies clés. L’utilisation des relations [!DNL Product Recommendations] et [produit](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/product-relationships/product-relationships.html?lang=fr) vous offre davantage de flexibilité lors de la promotion de produits. Vous pouvez tirer parti des [!DNL Product Recommendations] optimisés par Adobe Sensei pour automatiser intelligemment vos recommandations à grande échelle. Vous pouvez ensuite tirer parti des [ Règles de produits associés ](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/product-relationships/product-related-rules.html?lang=fr) lorsque vous devez intervenir manuellement pour vous assurer qu’une recommandation spécifique est envoyée à un segment d’acheteur cible ou lorsque certains objectifs commerciaux doivent être atteints.

Les recommandations de produits vous permettent d’effectuer les opérations suivantes :

- Choisissez parmi neuf types de recommandations intelligentes distincts en fonction des domaines suivants : basé sur l’acheteur, basé sur l’article, basé sur la popularité, basé sur les tendances et basé sur la similarité
- Utiliser les données comportementales pour personnaliser les recommandations dans l’ensemble du parcours de storefront de l’acheteur
- Mesurer les mesures clés pertinentes pour chaque recommandation afin de vous aider à comprendre l’impact de vos recommandations

## [!DNL Product Recommendations] de démonstration

Regardez cette vidéo pour en savoir plus sur [!DNL Product Recommendations] :

>[!VIDEO](https://video.tv.adobe.com/v/3449946?quality=12&captions=fre_fr)

## Politique de conservation des données de catalogue

Si vous n’envoyez pas de requête pour les données du catalogue dans votre environnement de test pendant 90 jours consécutifs, les données du catalogue sont définies en mode veille et aucune donnée n’est renvoyée pour une requête. Les données de catalogue de votre environnement de production ne sont pas affectées par cette politique.

Pour réactiver les données du catalogue dans votre environnement de test, [envoyez une demande d’assistance](https://experienceleague.adobe.com/fr/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#experience-league-start-page) avec le titre : « Réactiver le [!DNL Product Recommendations] » et incluez les identifiants d’environnement. Les données du catalogue de votre environnement de test doivent être restaurées dans les heures qui suivent.
