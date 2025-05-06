---
title: Intégration [!DNL Page Builder]
description: Découvrez comment utiliser  [!DNL Product Recommendations]  unités dans Page Builder.
feature: Services, Recommendations, Page Builder
exl-id: 001e8e1d-3590-4b44-b5f8-dd8b9b61f370
badgePaas: label="PaaS uniquement" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."
source-git-commit: be1c739f3821a5f1e846b3026088e3a3ff45a60f
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# Intégration [!DNL Page Builder]

Les recommandations de produits peuvent être intégrées à tout contenu Page Builder déployé sur votre site.

>[!NOTE]
>
> Vous pouvez avoir jusqu’à 25 unités de recommandation sur une page native de Page Builder. Les pages Page Builder non natives peuvent contenir jusqu’à 5 unités de recommandation. Voir [Créer une recommandation](create.md) pour plus d’informations.

## Utilisation des recommandations de produits avec du contenu Page Builder

1. Créez une unité Recommendations dans l’affichage par défaut du magasin d’un site web. Ils doivent être créés dans la vue de magasin par défaut, même si vous prévoyez de les utiliser dans différentes vues de magasin.

   >[!NOTE]
   >
   >Les mesures des unités de recommandation Page Builder n’apparaissent que dans la vue de magasin par défaut [!DNL Product Recommendations] l’espace de travail. Même si vous placez une unité de recommandation Page Builder sur une vue de magasin qui n’est pas la vue de magasin par défaut, les mesures liées à ces unités de recommandation Page Builder ne s’afficheront pas sur l’espace de travail [!DNL Product Recommendations] une vue de magasin autre que par défaut. Pour afficher les mesures Page Builder sur une vue de magasin autre que la vue par défaut [!DNL Product Recommendations] l’espace de travail, ouvrez et [modifiez](edit.md) l’unité de recommandation Page Builder dans la vue de magasin autre que la vue par défaut, puis cliquez sur [!UICONTROL **Enregistrer**]. Les mesures Page Builder apparaissent désormais dans l’espace de travail [!DNL Product Recommendations] sous l’aperçu de magasin autre que celui par défaut.

1. Dans Page Builder, sélectionnez le widget de contenu des recommandations de produits et placez-le sur votre site.

![Insérer une unité de recommandation](assets/pb-insert.png)

1. Cliquez sur **Modifier la recommandation de produit**
1. Cliquez sur **Sélectionner**
1. Sélectionnez l’unité de recommandations créée précédemment et cliquez sur **Ajouter la sélection**

![Insérer une unité de recommandation](assets/pb-select.png)

1. Apportez d’autres modifications au contenu de Page Builder et enregistrez-les.

Au moment du rendu, le contexte et la portée du contenu Page Builder sont respectés par l’unité de recommandation.
