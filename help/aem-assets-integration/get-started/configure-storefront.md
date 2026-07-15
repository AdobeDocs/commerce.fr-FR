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
source-git-commit: 7f901cec90291e264376e3f93e6ebaaccf7c15f0
workflow-type: tm+mt
source-wordcount: 610
ht-degree: 0%

---

# Configuration de votre storefront

## Activer l’affichage des images de produits à partir d’AEM Assets {#enable-product-images}

L’intégration d’AEM Assets affiche les images de produit d’AEM Assets au lieu d’Adobe Commerce, ce qui permet une optimisation avancée, le recadrage et la diffusion sur le réseau CDN.

Pour activer l’intégration dans les storefronts Commerce optimisés par Edge Delivery Services, ajoutez le paramètre `"commerce-assets-enabled": true` au fichier de configuration de storefront (`config.json`).

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

Pour plus d’informations sur l’utilisation d’AEM Assets avec le storefront Commerce optimisé par Edge Delivery Services, consultez la rubrique sur l’[intégration d’AEM Assets](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/?lang=fr) dans la documentation du *storefront Adobe Commerce*.

>[!TIP]
>
>Pour permettre aux auteurs de parcourir et d’insérer AEM Assets dans des pages de contenu statique, consultez [Connexion d’AEM Assets à Da.live pour la création de contenu statique](#connect-aem-assets-authoring).

## Connecter AEM Assets à Da.live pour la création de contenu statique {#connect-aem-assets-authoring}

>[!NOTE]
>
>Cette configuration est distincte de l’extension d’intégration AEM Assets. Fourni par [Da.live](https://da.live){target="_blank"} il permet aux auteurs de parcourir et d’insérer AEM Assets dans des pages de contenu statiques (par exemple, des pages de destination ou des blocs de contenu) via le panneau de [!UICONTROL Library] et les [!UICONTROL Content Advisor]. Les images de produit synchronisées par le biais de l’intégration AEM Assets sont configurées séparément à l’aide du paramètre `commerce-assets-enabled`.

Suivez les étapes ci-après pour connecter AEM Assets à un storefront de création de documents (Da.live) afin que les auteurs puissent parcourir et insérer AEM Assets à partir du **[!UICONTROL Content Advisor]** tout en modifiant le contenu statique.

>[!NOTE]
>
>Pour obtenir des instructions de configuration détaillées, consultez [Configuration d’AEM Assets](https://docs.da.live/administrators/guides/setup-aem-assets){target=_blank} dans la documentation Da.live et [Intégration d’AEM Assets lors de la création de contenu pour Edge Delivery Services](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/assets/integrate-aem-assets-edge-delivery-services/integrate-aem-assets-edge-delivery-services){target=_blank} dans la documentation d’AEM Assets.

### Étape 1 : Ouvrez la configuration de votre site dans Da.live

1. À partir de [Da.live](https://da.live){target=_blank}, localisez et ouvrez votre storefront.

1. Dans la navigation du chemin de navigation, sélectionnez l’icône **[!UICONTROL Settings]** en regard du nom de votre site pour ouvrir la feuille de calcul de configuration du site.

### Étape 2 : copier l’URL de votre référentiel AEM

1. Dans un nouvel onglet, accédez à [experience.adobe.com](https://experience.adobe.com){target=_blank} et à **[!UICONTROL Experience Manager]**.

1. Ouvrez Adobe Experience Manager Assets : faites défiler l’écran jusqu’à la section **[!UICONTROL My Authoring]**, puis sélectionnez **[!UICONTROL Assets]** en regard de votre environnement de **[!UICONTROL Production]**.

1. Dans la barre d’adresse du navigateur, copiez le segment commençant par `author` jusqu’à et y compris `.com`, par exemple `author-p107634-e1009805.adobeaemcloud.com`.

### Étape 3 : ajouter l’ID de référentiel à votre configuration

1. Pour configurer votre site, revenez à Da.live et sélectionnez **[!UICONTROL data]** dans la configuration de votre site.

1. Complétez la feuille de calcul comme suit :

   | Cellule | Valeur |
   |---|---|
   | A1 | `key` |
   | B1 | `value` |
   | A2 | `aem.repositoryId` |
   | B2 | URL que vous avez copiée à l’étape 2 |

1. Sélectionnez **[!UICONTROL Save]**, puis cliquez sur la flèche vers l’arrière en regard du nom de votre site pour revenir à la racine du site.

   >[!NOTE]
   >
   > L’hôte avec préfixe `author-` parcourt les ressources à partir du niveau de création. Pour diffuser des ressources via Dynamic Media à la place, utilisez un hôte doté d’un préfixe `delivery-`. Pour toutes `aem.repositoryId` options, voir [Configuration d’AEM Assets](https://docs.da.live/administrators/guides/setup-aem-assets){target=_blank}.

### Étape 4 : connexion d’AEM Assets via la bibliothèque

1. À partir de la racine du site, sélectionnez le dossier **[!UICONTROL index]** pour l’ouvrir.

1. Dans l’éditeur, ouvrez le panneau **[!UICONTROL Library]** et sélectionnez **[!UICONTROL AEM Assets]**.

   La fenêtre contextuelle **[!UICONTROL Content Advisor]** s’ouvre et affiche vos dossiers et fichiers AEM Assets.

Votre storefront est maintenant connecté à AEM Assets. Vous pouvez parcourir et insérer des ressources directement à partir du **[!UICONTROL Content Advisor]**.

## Documentation connexe

* [Intégration d’](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/?lang=fr){target=_blank} dans la documentation *Adobe Commerce Storefront* : configuration du storefront et comportement de la gestion des images.

* [Intégrez AEM Assets lors de la création de contenu pour Edge Delivery Services](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/assets/integrate-aem-assets-edge-delivery-services/integrate-aem-assets-edge-delivery-services){target=_blank} dans la documentation *AEM Assets*.

* [Configuration d’AEM Assets](https://docs.da.live/administrators/guides/setup-aem-assets){target=_blank} et [Utilisation des médias](https://docs.da.live/authors/guides/adding-media){target=_blank} dans la documentation Da.live.
