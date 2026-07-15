---
title: Visuels de produit avec AEM Assets
description: Découvrez comment utiliser AEM Assets pour les images de produit dans  [!DNL Adobe Commerce Optimizer].
feature: CMS, Media, Configuration, Integration
role: Admin, Developer
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et  [!DNL Adobe Commerce Optimizer]  (infrastructure SaaS gérée par Adobe)."
source-git-commit: 264658bee09a22cfd55828c6960153cc1239d3fb
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---


# Visuels de produit avec AEM Assets

La fonctionnalité Visuels du produit permet aux commerçants [!DNL Adobe Commerce Optimizer] de gérer les images des produits via Adobe Experience Manager (AEM) Assets. Cette intégration fournit un workflow transparent pour synchroniser des images de produit de haute qualité d’AEM Assets avec votre catalogue [!DNL Commerce Optimizer] à l’aide des calques de catalogue.

>[!NOTE]
>
>**Visuels du produit** est le nom du lot fourni avec [!DNL Adobe Commerce as a Cloud Service] et [!DNL Adobe Commerce Optimizer]. Il associe [Dynamic Media aux fonctionnalités OpenAPI](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/dynamic-media-open-apis-overview) et [AEM Assets Prime](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/assets/assets-prime).
>
>Les clients disposant d’une licence AEM Assets différente (par exemple, **AEM Assets Ultimate**) peuvent utiliser la même intégration ; seule la version d’AEM affecte les étapes d’intégration, et non le type de licence.

## Principaux avantages

* **Gestion centralisée des ressources** : gérez toutes les images de produits dans AEM Assets, la solution de gestion des ressources numériques d’entreprise.
* **Synchronisation automatique** : les images de produit se synchronisent automatiquement lorsque des ressources sont approuvées ou mises à jour dans AEM Assets.
* **Diffusion Dynamic Media** : utilisez Dynamic Media avec les fonctionnalités OpenAPI pour une diffusion d’images optimisée.
* **Calques de catalogue** : les images de produit sont appliquées en tant que calque de catalogue, ce qui vous permet de superposer des images AEM Assets sur votre catalogue de base.

## Fonctionnement

L’intégration comporte deux flux d’événements indépendants. Les deux utilisent [&#128279;](https://developer.adobe.com/events/docs/) pour transférer des événements au service d&#39;intégration d&#39;Assets, mais chaque direction utilise son propre fournisseur d&#39;événements :

* **D’AEM Assets au service d’intégration d’Assets** : lorsqu’une ressource est approuvée, rejetée ou supprimée, l’événement est diffusé au service d’intégration d’Assets. Le service associe les ressources aux produits à l’aide d’une `match-by-SKU` ou d’une stratégie de correspondance personnalisée, puis envoie les mappages de `product-asset` à [!DNL Commerce Optimizer], où elles sont stockées en tant que couches de produit.

* **De [!DNL Commerce Optimizer] à Assets Integration Service** : lorsqu&#39;un produit est mis à jour en [!DNL Commerce Optimizer], l&#39;événement est diffusé au service d&#39;intégration d&#39;Assets. Le service resynchronise tous les mappages de ressources correspondants avec [!DNL Commerce Optimizer].

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

Pour activer l’intégration, [créez un ticket d’assistance](https://experienceleague.adobe.com/fr/docs/commerce-learn/tutorials/help-and-support/create-a-support-ticket) avec les détails de votre [!DNL Commerce Optimizer] et d’AEM Assets. L’assistance Adobe configure l’intégration et enregistre votre client auprès du service d’intégration Assets.

Voir [Configuration d’AEM Assets pour Commerce Optimizer](../../aem-assets-integration/get-started/configure-aco.md) pour obtenir des informations sur l’intégration.

### Configuration des métadonnées AEM Assets

Pour activer la correspondance automatique de produits, configurez vos ressources dans AEM Assets avec les métadonnées Commerce.

Voir [Configuration d’AEM Assets](../../aem-assets-integration/get-started/configure-aco.md#configure-aem-assets-first) pour connaître les étapes et champs de métadonnées requis.

## Restrictions

Avant d’utiliser les visuels de produit, passez en revue les [limites d’intégration](../../aem-assets-integration/get-started/configure-aco.md#limitations), les contraintes liées aux calques qui affectent la manière dont les données AEM Assets fusionnent avec votre catalogue de base.

Pour les allocations de capacité et d’utilisation (stockage des ressources, opérations Dynamic Media, licences utilisateur), consultez [Limites des visuels de produit](../boundaries-limits.md#product-visuals-limits) dans le guide _Limites et limites_.

## Utilisation des visuels de produit

Une fois l’intégration configurée, gérez vos images de produit via AEM Assets.

### Ajout d’images aux produits

1. Chargez les images dans votre référentiel AEM Assets.

1. Ajoutez des métadonnées Commerce à la ressource.

   Voir [Correspondance automatique par défaut](../../aem-assets-integration/synchronize/default-match.md) et [Correspondance automatique personnalisée](../../aem-assets-integration/synchronize/custom-match.md).

1. Valider la ressource à diffuser. La ressource doit avoir le statut **approuvé** pour déclencher la synchronisation.

1. L’image se synchronise automatiquement avec [!DNL Commerce Optimizer].

### Application du calque AEM-Assets

Pour afficher des images AEM Assets sur votre storefront, [affectez le calque `AEM-Assets` à votre vue catalogue](catalog-layer.md#assign-the-aem-assets-layer-to-a-catalog-view).

## Plus comme ceci

* [Calques de catalogue](catalog-layer.md)
* [Vues du catalogue](catalog-view.md)
* [Guide d’intégration d’AEM Assets](../../aem-assets-integration/overview.md)
