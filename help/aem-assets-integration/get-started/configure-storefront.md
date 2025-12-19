---
title: Configuration de votre storefront
description: Découvrez comment connecter votre storefront Edge Delivery Services à votre intégration AEM Assets.
feature: CMS, Media, Integration
source-git-commit: d426c7878f7a66fe1047673be7c5bf65ae1949a7
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---


# Configuration de votre storefront

L’intégration AEM Assets affiche les images de produit gérées dans AEM Assets au lieu d’utiliser des images hébergées dans Adobe Commerce. L’intégration offre des fonctionnalités améliorées de gestion des images, notamment une optimisation, un recadrage et une diffusion avancés via le réseau de diffusion de contenu (CDN) d’Adobe.

Pour activer l’intégration dans les storefronts Commerce optimisés par Edge Delivery Services, mettez à jour le fichier de configuration de storefront (`config.json`) pour ajouter le paramètre `"commerce-assets-enabled": true` .

```json
{
  "public": {
    "default": {
      "commerce-assets-enabled": true
    }
  }
}
```

Les listes déroulantes Commerce détectent automatiquement la configuration `commerce-assets-enabled` et ajustent la gestion des images en conséquence.

Pour plus d’informations sur l’utilisation d’AEM Assets avec le storefront Commerce optimisé par Edge Delivery Services, effectuez la configuration du storefront décrite dans la rubrique [Intégration d’AEM Assets](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/) dans la documentation du *storefront Adobe Commerce*.
