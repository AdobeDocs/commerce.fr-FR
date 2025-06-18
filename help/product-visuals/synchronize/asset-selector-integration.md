---
title: Sélection manuelle des ressources
description: Découvrez comment le sélecteur de ressources AEM intégré à l’administration Commerce permet aux marketeurs et aux marketeurs d’ajouter facilement des images d’AEM Assets à Adobe Commerce, en rationalisant la gestion des ressources.
feature: CMS, Media, Integration
source-git-commit: d362e6e821e81f6da99c420881e1e1b1058bbd45
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Sélection manuelle des ressources

Le **sélecteur de ressources AEM** permet aux marketeurs et aux marketeurs d’ajouter facilement des images d’AEM Assets à Adobe Commerce, en rationalisant le processus de gestion des ressources. Cette méthode garantit la cohérence et la conformité de la marque en limitant la sélection de ressources aux ressources examinées et approuvées dans le [!DNL DAM (Digital Asset Management system)].

Le **sélecteur de ressources AEM** est disponible lorsque l’identifiant client IMS du projet AEM Assets a été configuré dans l’administrateur Commerce. Voir [Configuration du sélecteur de ressources AEM]&#x200B;(#configure-the-aem-asset-selector-in-adobe-commerce.

Lorsque l’intégration du sélecteur de ressources AEM **** est configurée, les marketeurs et les marketeurs peuvent :

* Gérez facilement les images de catégorie, en vous assurant qu’elles sont conformes aux directives de la marque et de la campagne.
* [!BADGE PaaS uniquement]{type=Informative tooltip="S’applique uniquement à Adobe Commerce sur les projets cloud (infrastructure PaaS gérée par Adobe)."} Attribuez des ressources directement dans Page Builder pour obtenir du contenu visuellement riche.

>[!NOTE]
>
> Le sélecteur de ressources AEM est un composant front-end d’AEM Assets qui permet d’intégrer AEM Assets aux applications de création. Pour plus d’informations sur ce composant, consultez le [Sélecteur de ressources micro front-end](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/overview-asset-selector){target=_blank} dans le *Guide d’utilisation d’AEM as a Cloud Service*.

## Principaux avantages

L’incorporation du sélecteur de ressources AEM dans le panneau d’administration d’Adobe Commerce offre plusieurs avantages clés :

* **Cohérence de la marque**-Affiche uniquement les ressources approuvées, ce qui réduit le risque d’images obsolètes ou non conformes sur le storefront.

* **Efficacité**-Permet aux spécialistes du marketing et du marchandisage d’affecter rapidement des ressources sans passer d’une plateforme à l’autre.

* **Collaboration rationalisé** : facilite le travail d’équipe en permettant une sélection directe des images à partir de la gestion des ressources numériques, en éliminant les téléchargements et chargements manuels.

* **Qualité de contenu améliorée**-Garantit l’utilisation d’images optimisées et haute résolution sur les pages de produits, les catégories et le générateur de page.

![ Sélecteur de ressources ](../assets/asset-selector.png){width="600" zoomable="yes"}

## Configuration du sélecteur de ressources AEM dans Adobe Commerce

1. Dans l’Administration Commerce, accédez à **[!UICONTROL Store]** > Configuration > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

1. Renseignez le champ **[!UICONTROL IMS Client ID]** .

1. **Enregistrez** la configuration.

## Étapes suivantes

* [Gestion des images de catégorie à l’aide du sélecteur de ressources](../manage-assets.md#category-images)
* [Gestion des images dans le contenu Page Builder](../manage-assets.md#using-aem-asset-selector-in-page-builder)
