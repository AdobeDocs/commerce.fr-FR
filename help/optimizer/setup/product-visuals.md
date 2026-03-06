---
title: Visuels de produit avec AEM Assets
description: Découvrez comment utiliser AEM Assets pour les images de produit dans  [!DNL Adobe Commerce Optimizer].
feature: CMS, Media, Configuration, Integration
role: Admin, Developer
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et  [!DNL Adobe Commerce Optimizer]  (infrastructure SaaS gérée par Adobe)."
source-git-commit: c7c21df464685783b5fae1c99d60ca91e0c334d2
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---


# Visuels de produit avec AEM Assets

La fonctionnalité Visuels du produit permet aux commerçants [!DNL Adobe Commerce Optimizer] de gérer les images des produits via Adobe Experience Manager (AEM) Assets. Cette intégration fournit un workflow transparent pour synchroniser des images de produit de haute qualité d’AEM Assets avec votre catalogue [!DNL Commerce Optimizer] à l’aide des calques de catalogue.

## Principaux avantages

* **Gestion centralisée des ressources** : gérez toutes les images de produits dans AEM Assets, la solution de gestion des ressources numériques d’entreprise.
* **Synchronisation automatique** : les images de produit se synchronisent automatiquement lorsque des ressources sont approuvées ou mises à jour dans AEM Assets.
* **Diffusion Dynamic Media** : utilisez Dynamic Media avec les fonctionnalités OpenAPI pour une diffusion d’images optimisée.
* **Calques de catalogue** : les images de produit sont appliquées en tant que calque de catalogue, ce qui vous permet de superposer des images AEM Assets sur votre catalogue de base.

## Fonctionnement

L’intégration comporte deux flux principaux :

* **Depuis AEM Assets** : lorsqu’une ressource est approuvée, rejetée ou supprimée, l’événement se propage par le pipeline Adobe vers le service d’intégration d’Assets. Le service associe les ressources aux produits à l’aide d’une `match-by-SKU` ou d’une stratégie de correspondance personnalisée, puis envoie les mappages de `product-asset` au [!DNL Commerce Optimizer], où ils sont stockés en tant que couches de produits.

* **De l’ACO** : lorsqu’un produit est mis à jour dans le [!DNL Commerce Optimizer], l’événement se propage par le pipeline Adobe vers le service d’intégration Assets. Le service resynchronise tous les mappages de ressources correspondants avec l’ACO.

Les images mises à jour sont disponibles via les API de storefront (service de catalogue, recherche en direct, recommandations de produits).

### Configuration de Source et de calque

Les images provenant d’AEM Assets sont ingérées en tant que couche de catalogue avec la configuration source suivante :

> Exemple de configuration d’une source

```json
{
  "source": {
    "locale": "en-US",
    "layer": "AEM-Assets"
  }
}
```

Cette configuration garantit que les images AEM Assets sont appliquées en tant que recouvrement sur votre catalogue de produits de base.

## Conditions préalables

Avant d’activer les visuels de produit, assurez-vous de respecter les [&#x200B; conditions préalables pour Commerce Optimizer &#x200B;](../../aem-assets-integration/get-started/configure-aco.md#prerequisites).

## Configuration

Pour activer l’intégration, [créez un ticket d’assistance](https://experienceleague.adobe.com/fr/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) avec les détails de votre [!DNL Commerce Optimizer] et d’AEM Assets. L’assistance Adobe configure l’intégration et enregistre votre client auprès du service d’intégration Assets.

Voir [Configuration d’AEM Assets pour Commerce Optimizer](../../aem-assets-integration/get-started/configure-aco.md) pour obtenir des informations sur l’intégration.

### Configuration des métadonnées AEM Assets

Pour activer la correspondance automatique de produits, configurez vos ressources dans AEM Assets avec les métadonnées Commerce.

Voir [Configuration d’AEM Assets](../../aem-assets-integration/get-started/configure-aco.md#configure-aem-assets) pour connaître les étapes et champs de métadonnées requis.

## Utilisation des visuels de produit

Une fois l’intégration configurée, gérez vos images de produit via AEM Assets.

### Ajout d’images aux produits

1. Chargez les images dans votre référentiel AEM Assets.

1. Ajoutez des métadonnées Commerce à la ressource. Voir [&#x200B; Application de métadonnées aux ressources](../../aem-assets-integration/get-started/configure-aco.md#step-3-apply-metadata-to-assets).

1. Valider la ressource à diffuser. La ressource doit avoir le statut **approuvé** pour déclencher la synchronisation.

1. L’image se synchronise automatiquement avec [!DNL Commerce Optimizer].

### Application du calque AEM-Assets

Pour afficher des images AEM Assets sur votre storefront, [affectez le calque `AEM-Assets` à votre vue catalogue](catalog-layer.md#assign-the-aem-assets-layer-to-a-catalog-view).

## Plus comme ceci

* [Calques de catalogue](catalog-layer.md)
* [Vues du catalogue](catalog-view.md)
* [Guide d’intégration d’AEM Assets](../../aem-assets-integration/overview.md)
