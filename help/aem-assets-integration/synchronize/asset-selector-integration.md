---
title: Sélection manuelle des ressources
description: Découvrez comment le sélecteur de ressources AEM intégré à l’administration Commerce permet aux marketeurs et aux marketeurs d’ajouter facilement des images d’AEM Assets à Adobe Commerce, en rationalisant la gestion des ressources.
feature: CMS, Media, Integration
exl-id: 3c1f906f-3ec3-4eac-a47e-b21792767359
TQID: https://experienceleague.adobe.com/3fYabUvRiY8KTxQX1YiTBbLxABpQqfZLu0a6IBDsM3E
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b5f00040-57a0-4a6d-a39e-383b1936c2c9id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2: id: da3860b0-d637-47df-bef0-273751180266
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 396
ht-degree: 0%

---

# Sélection manuelle des ressources

Le **sélecteur de ressources** permet aux marketeurs et aux marketeurs d’ajouter facilement des images d’AEM Assets à Adobe Commerce, en rationalisant le processus de gestion des ressources. Cette méthode garantit la cohérence et la conformité de la marque en limitant la sélection de ressources aux ressources examinées et approuvées dans le [!DNL DAM (Digital Asset Management system)].

Le **sélecteur de ressources** est disponible lorsque l’identifiant client IMS du projet AEM Assets a été configuré dans l’administration Commerce et que les utilisateurs disposent des autorisations [autorisations et de l’authentification IMS requises](../get-started/permissions.md). Voir [ Configuration du sélecteur de ressources AEM](#configure-the-aem-asset-selector-in-adobe-commerce).

Lorsque l’intégration du sélecteur de ressources AEM **** est configurée, les marketeurs et les marketeurs peuvent :

* Gérez facilement les images de catégorie, en vous assurant qu’elles sont conformes aux directives de la marque et de la campagne.
* [!BADGE PaaS uniquement]{type=Informative tooltip="S’applique uniquement à Adobe Commerce sur les projets cloud (infrastructure PaaS gérée par Adobe)."} Attribuez des ressources directement dans Page Builder pour obtenir du contenu visuellement riche.
* [!BADGE SaaS uniquement]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."} Attribuez Assets directement dans le storefront Commerce optimisé par Edge Delivery Services pour un contenu visuellement enrichi.

>[!NOTE]
>
> Le sélecteur de ressources AEM est un composant front-end d’AEM Assets qui permet d’intégrer AEM Assets aux applications de création. Pour plus d’informations sur ce composant, consultez le [Sélecteur de ressources micro front-end](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/overview-asset-selector){target=_blank} dans le *Guide d’utilisation d’AEM as a Cloud Service*.

## Principaux avantages

L’incorporation du sélecteur de ressources AEM dans le panneau d’administration d’Adobe Commerce offre plusieurs avantages clés :

* **Cohérence de la marque**-Affiche uniquement les ressources approuvées, ce qui réduit le risque d’images obsolètes ou non conformes sur le storefront.

* **Efficacité**-Permet aux spécialistes du marketing et du marchandisage d’affecter rapidement des ressources sans passer d’une plateforme à l’autre.

* Collaboration rationalisé&#x200B;**: facilite le travail d’équipe en permettant une sélection directe des images à partir de la gestion des ressources numériques, en éliminant les téléchargements et chargements manuels.**

* **Qualité de contenu améliorée**-Garantit l’utilisation d’images optimisées et haute résolution sur les pages de produits, les catégories et le générateur de page.

![ Sélecteur de ressources ](../assets/asset-selector.png){width="600" zoomable="yes"}

## Configuration du sélecteur de ressources AEM dans Adobe Commerce

1. Dans l’Administration Commerce, accédez à **[!UICONTROL Store]** > Configuration > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

1. Renseignez le champ **[!UICONTROL IMS Client ID]** . Pour connaître les autorisations requises et la manière d’obtenir cet identifiant, voir [Autorisations utilisateur et IMS](../get-started/permissions.md).

1. **Enregistrez** la configuration.

## Étapes suivantes

* [Gestion des images de catégorie à l’aide du sélecteur de ressources](../manage-assets.md#category-images)
* [Gestion des images dans le contenu Page Builder](../manage-assets.md#using-aem-asset-selector-in-page-builder)
