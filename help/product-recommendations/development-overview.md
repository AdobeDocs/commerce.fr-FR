---
title: Développement de l’administrateur des recommandations de produits
description: Présentation de l’architecture et des fonctionnalités de développement de Product Recommendations.
exl-id: 5967259e-c531-4fc7-9abd-cc18433fab33
TQID: https://experienceleague.adobe.com/DtPYY7DaB-A7-VyTeXkjL9Y2My-WOQx-9CD-TgrcTmk
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bbbea26f-9621-49eb-9ab8-e06fb3bbce8c
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
source-git-commit: 127067a1ef47c7d9e51c5792e03b568dd818fe8e
workflow-type: tm+mt
source-wordcount: 300
ht-degree: 0%

---

# Développement de l’administrateur des recommandations de produits

Les recommandations de produits sont un puissant outil marketing que vous pouvez utiliser pour augmenter les conversions, augmenter le chiffre d’affaires et stimuler l’engagement des acheteurs. Les recommandations de produits sont affichées sur la vitrine sous la forme d’unités telles que « Les clients qui ont consulté ce produit ont également consulté », « Les clients qui ont acheté ce produit ont également acheté », « Recommandé pour vous », etc. [&#128279;](https://business.adobe.com/fr/ai.html) alimente les recommandations de produits Adobe Commerce, qui utilisent l’intelligence artificielle et des algorithmes de machine learning pour effectuer une analyse approfondie des données agrégées d’acheteurs. Ces données, lorsqu’elles sont combinées à votre catalogue Commerce, génèrent des expériences très attrayantes, pertinentes et personnalisées pour l’acheteur.

>[!NOTE]
>
>Si votre storefront est implémenté à l’aide de PWA Studio, consultez la documentation de [PWA](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/). Découvrez comment intégrer des recommandations de produits dans un environnement [&#x200B; découplé &#x200B;](headless.md) si vous utilisez une technologie frontale personnalisée telle que React ou Vue JS. Les instances découplées doivent implémenter des événements pour alimenter l’espace de travail de recommandations de produits.

## Aperçu de l’architecture

À un niveau élevé, les recommandations de produits Commerce sont déployées en tant que SaaS. Le côté Commerce comprend le storefront, qui contient le collecteur d’événements et le modèle de disposition des recommandations, ainsi que le serveur principal, qui inclut les services de données, le module d’exportation SaaS et l’interface utilisateur d’administration. Les services Adobe AI Intelligence sont exploités côté SaaS.

![Diagramme d’architecture des recommandations de produits](assets/arch-diag-sensei.svg)

Une fois installés et configurés, les modules de recommandation permettent à votre storefront de collecter des données comportementales. Adobe AI associe ces données à vos données de catalogue pour calculer les associations de produits utilisées par le service Recommendations. Vous pouvez ensuite créer, gérer et déployer des unités de recommandation de produit directement à partir de l’interface utilisateur d’administration.

## Étapes suivantes

Lisez les rubriques suivantes pour commencer à utiliser les recommandations de produits :

- [Mise en œuvre des recommandations de produit](implementation-workflow.md)

- [Installation et configuration de Product Recommendations](install-configure.md)

- [Création de recommandations de produits](create.md)
