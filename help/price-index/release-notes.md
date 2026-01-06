---
title: Notes de mise à jour de [!DNL Catalog Adapter]
description: Dernières informations de mise  [!DNL Catalog Adapter]  jour pour Adobe Commerce.
feature: Services, Release Notes
recommendations: noCatalog
roles: Admin, Developer
exl-id: d4dd0288-8853-43fe-9103-1aead8d3b56e
source-git-commit: 47419e7e19611dc4a045c195f259e2126ab77372
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# Notes de mise à jour de l’extension [!DNL Catalog Adapter]

Ces notes de mise à jour décrivent les dernières versions de l’extension [!DNL Catalog Adapter]. La prise en charge est assurée pour la version majeure publiée actuelle. Les notes de mise à jour des anciennes versions sont fournies à titre de référence.

Les mises à jour incluent :

![Nouveau](../assets/new.svg) Nouvelles fonctionnalités
![Correctifs](../assets/fix.svg) Correctifs et améliorations
![Bogue](../assets/bug.svg) Problèmes connus


>[!NOTE]
>
>L’extension [Catalog Adapter](catalog-adapter.md) désactive l’indexation des prix dans Adobe Commerce. Si vous l’avez installé, vous pouvez vérifier la version installée sur votre système à l’aide du compositeur. Dans certains cas, vous souhaiterez peut-être mettre à niveau l&#39;extension d&#39;adaptateur de catalogue sur votre système pour trouver des correctifs ou de nouvelles fonctionnalités sans mettre à jour la version du service Commerce.

## Version majeure actuelle

## Version 1.0.10

![Correction](../assets/fix.svg) Correction d’un problème où les requêtes de prix pour les produits groupés importés ou nouvellement créés pouvaient entraîner des erreurs de serveur internes, car le système tentait d’utiliser un SKU concaténé pour la recherche au lieu du SKU correct et valide. Les requêtes de prix pour les produits groupés utilisent désormais le SKU approprié et sont résolues correctement.<!--MDEE-1040-->

## Version 1.0.9

![Correctif](../assets/fix.svg) Ajout de la compatibilité pour PHP 8.4. <!--MDEE-941-->

## Version 1.0.8

![Correction](../assets/fix.svg) Correction d’un problème qui provoquait une erreur dans le journal des exceptions lors de l’ajout de variantes de produits configurables avec des SKU numériques à la liste de souhaits. <!--MDEE-876-->
