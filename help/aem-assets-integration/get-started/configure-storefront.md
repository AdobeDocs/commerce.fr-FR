---
title: Configuration de votre storefront
description: Découvrez comment connecter votre storefront Edge Delivery Services à votre intégration AEM Assets.
feature: CMS, Media, Integration
TQID: https://experienceleague.adobe.com/gl0Y2UNs3sYkXE9QYwLtAltyX1dxE699y23ey-y0KUU
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 137
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
