---
title: Développement de l’administrateur des recommandations de produits
description: Présentation de l’architecture et des fonctionnalités de développement de Product Recommendations.
exl-id: 5967259e-c531-4fc7-9abd-cc18433fab33
source-git-commit: 458f34c45406db871ec61ff408aa624f163b6ee0
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Développement de l’administrateur des recommandations de produits

Les recommandations de produits sont un puissant outil marketing que vous pouvez utiliser pour augmenter les conversions, augmenter le chiffre d’affaires et stimuler l’engagement des acheteurs. Les recommandations de produits sont affichées sur la vitrine sous la forme d’unités telles que « Les clients qui ont consulté ce produit ont également consulté », « Les clients qui ont acheté ce produit ont également acheté », « Recommandé pour vous », etc. Les recommandations de produits Adobe Commerce sont optimisées par l’[IA d’Adobe](https://business.adobe.com/fr/ai.html), qui utilise l’intelligence artificielle et des algorithmes de machine learning pour effectuer une analyse approfondie des données agrégées sur les acheteurs. Ces données, lorsqu’elles sont combinées à votre catalogue Commerce, génèrent des expériences très attrayantes, pertinentes et personnalisées pour l’acheteur.

>[!NOTE]
>
>Si votre storefront est implémenté à l’aide de PWA Studio, consultez la documentation de [PWA](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/). Si vous utilisez une technologie frontale personnalisée, telle que React ou Vue JS, reportez-vous au guide d’utilisation pour savoir comment intégrer Product Recommendations dans un environnement [découplé](headless.md). Les instances découplées doivent implémenter des événements pour alimenter l’espace de travail de recommandations de produits.

## Aperçu de l’architecture

À un niveau élevé, les recommandations de produits Commerce sont déployées en tant que SaaS. Le côté Commerce comprend le storefront, qui contient le collecteur d’événements et le modèle de disposition des recommandations, ainsi que le serveur principal, qui inclut les services de données, le module d’exportation SaaS et l’interface utilisateur d’administration. Les services d’intelligence artificielle d’Adobe sont exploités côté SaaS.

![Diagramme d’architecture des recommandations de produits](assets/arch-diag-sensei.svg)

Une fois les modules de recommandation installés et configurés, votre storefront commencera à collecter des données comportementales. L’IA dédiée à Adobe traite ces données comportementales avec vos données de catalogue et calcule les associations de produits qui sont exploitées par le service de recommandations. À ce stade, le commerçant peut créer, gérer et déployer des unités de recommandation de produit sur son storefront directement à partir de l’interface utilisateur d’administration.

## Étapes suivantes

Lisez les rubriques suivantes pour commencer à utiliser les recommandations de produits :

- [Mise en œuvre des recommandations de produit](implementation-workflow.md)

- [Installation et configuration de Product Recommendations](install-configure.md)

- [Création de recommandations de produits](create.md)
