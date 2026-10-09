---
title: Notes de mise à jour de [!DNL Catalog Adapter]
description: Dernières informations de mise à jour de [!DNL Catalog Adapter] pour Adobe Commerce.
feature: Services, Release Notes
recommendations: noCatalog
roles: Admin, Developer
exl-id: d4dd0288-8853-43fe-9103-1aead8d3b56e
TQID: 'https://experienceleague.adobe.com/btPlBYpdRdf-gMfqSv2px6iMfiI3FfXJSN40j61HXOU'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: adedf70c-c1e1-5734-acdc-c5c43b114964
    internal-label: Release Notes
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 76e77db86adecdbd3be76040970c0d0899c34cdc
workflow-type: tm+mt
source-wordcount: '219'
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

## Version 1.0.11

_18 juin 2026_

![Correctif](../assets/fix.svg) **Compatibilité PHP 8.5** - L’adaptateur de catalogue Adobe Commerce prend désormais en charge PHP 8.5 pour une compatibilité avec la version 2.4.9 ou ultérieure d’Adobe Commerce. <!--MDEE-1368-->

## Version 1.0.10

![Correction](../assets/fix.svg) Correction d’un problème où les requêtes de prix pour les produits groupés importés ou nouvellement créés pouvaient entraîner des erreurs de serveur internes, car le système tentait d’utiliser un SKU concaténé pour la recherche au lieu du SKU correct et valide. Les requêtes de prix pour les produits groupés utilisent désormais le SKU approprié et sont résolues correctement.<!--MDEE-1040-->

## Version 1.0.9

![Correctif](../assets/fix.svg) Ajout de la compatibilité pour PHP 8.4. <!--MDEE-941-->

## Version 1.0.8

![Correction](../assets/fix.svg) Correction d’un problème qui provoquait une erreur dans le journal des exceptions lors de l’ajout de variantes de produits configurables avec des SKU numériques à la liste de souhaits. <!--MDEE-876-->
