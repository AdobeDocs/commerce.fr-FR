---
title: Paramètres
description: Découvrez comment modifier la source de vos  [!DNL Product Recommendations]  et comment activer les recommandations visuelles.
exl-id: fe37624d-c53e-40cd-b182-10f62cba74c0
source-git-commit: c11e3fbc871600f413867e0c5c0b75ad705cf115
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# Paramètres

Lorsque vous [configurez un espace de données SaaS](../landing/saas.md#saas-configuration) pour Recommendations, l’espace de données SaaS collecte des données de catalogue et stocke les données comportementales. [Adobe Sensei](https://www.adobe.com/sensei.html) analyse les données et calcule les associations de produits utilisées pour les recommandations de produits.

Les environnements hors production à des fins de test ou d&#39;évaluation ne disposent généralement pas de la quantité ou de la qualité des données comportementales du storefront pour fournir des recommandations de produits réalistes. Le comportement réel de l’acheteur à grande échelle ne peut être capturé que dans un environnement de production. Pour résoudre ce problème, Adobe Commerce vous permet d’utiliser les recommandations de produits de votre environnement de production avec d’autres espaces de données SaaS hors production. L’utilisation de données storefront réelles dans un environnement hors production vous permet de prévisualiser les recommandations que vos clients voient et d’expérimenter avec différents types de recommandations et emplacements d’emplacement. Les recommandations d’un autre espace de données SaaS peuvent être prévisualisées par les acheteurs, mais pas cliquées.

Les ordres intermédiaires sont enregistrés à l’aide de l’`environmentId` intermédiaire. Cela n’affecte pas les données de production. Les données de production sont récupérées à l’aide de l’`alternateEnvironmentId` .

>[!NOTE]
>
>Lors de l’utilisation de Product Recommendations via REST, le paramètre `alternateEnvironmentId` peut être utilisé pour spécifier d’autres espaces de données. Lors de l’utilisation de Product Recommendations via [GraphQL](https://developer.adobe.com/commerce/services/graphql/recommendations/recommendations/), ce paramètre n’est pas disponible.

## Choisir la source des recommandations

Pour modifier la source des données de vos recommandations de produits, choisissez l’espace de données SaaS avec les données comportementales que vous souhaitez utiliser. Avant de commencer, assurez-vous des points suivants :

- La collecte de données Storefront doit être [configurée et activée](install-configure.md) pour votre environnement de production et [vérifiée](verify.md) que les données comportementales sont envoyées à Adobe Commerce.
- Votre catalogue d’environnements de non-production doit être essentiellement identique à votre catalogue de production. L’utilisation de catalogues similaires garantit que les unités de recommandation de produit renvoyées ressemblent étroitement à celles de la production.

1. Connectez-vous à l’administration de votre environnement Adobe Commerce hors production.

1. Dans la barre latérale _Admin_, accédez à **Marketing** > _Promotions_ > **Recommandations de produits**.

1. Cliquez sur **Paramètres**.

   ![paramètres de recommandation de produit](assets/settings.png)
   _Paramètres_

1. Dans la section _Source de recommandations_, activez l’option **Récupérer des recommandations à partir d’un autre espace de données SaaS**. La section _Source de recommandations_ s’affiche uniquement dans un environnement hors production.

   La liste _Espaces de données SaaS disponibles_ s&#39;affiche.

   ![paramètres de recommandation de produit](assets/settings-select-saas.png)
   _Paramètres_

1. Sélectionnez l’espace de données SaaS contenant les données de l’acheteur que vous souhaitez utiliser.

1. Cliquez sur **Enregistrer les modifications**.

   Adobe Commerce récupère désormais les recommandations de l’espace de données sélectionné.

   >[!NOTE]
   >
   > Bien que vous puissiez afficher les recommandations récupérées à partir d’un autre espace de données SaaS sur le storefront hors production, vous ne pouvez pas cliquer sur les recommandations.

### Configurer un nouvel espace de données SaaS

1. Dans la section Source Recommendations , cliquez sur **Modifier la configuration**.

1. Suivez les instructions pour configurer un nouveau [[!DNL Commerce] service](/help/landing/saas.md).

## Activer les recommandations visuelles

Si le module [Recommandations visuelles de produits](install-configure.md) est installé, vous devez activer Recommandations visuelles pour utiliser le type de recommandation [Similarité visuelle](type.md#visualsim).

Dans la section _Recommandations visuelles_, définissez **Activer les recommandations visuelles** sur la position active.
