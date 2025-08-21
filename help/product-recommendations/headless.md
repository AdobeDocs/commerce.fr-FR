---
title: Découplé
description: Découvrez comment intégrer  [!DNL Product Recommendations]  dans un storefront découplé.
exl-id: c40dac31-f87e-402a-ba50-e8aa4c1d66aa
source-git-commit: 1548b7e11249febc2cd8682581616619f80c052f
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---

# Découplé

Vous pouvez intégrer [!DNL Product Recommendations] dans un storefront découplé à l’aide de [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/) ou d’une technologie frontale personnalisée, telle que React ou Vue JS.

Les intégrateurs personnalisés et découplés doivent se reporter à ces instructions Luma et PWA en tant que mise en œuvre suggérée. Il existe de nombreuses façons d’implémenter les recommandations de produits dans des solutions découplées et cette documentation ne couvre pas tous les scénarios. Les intégrateurs doivent prendre en charge les événements, la conception et les tests pour leurs implémentations.

[!DNL Product Recommendations] nécessitent des [données comportementales et de catalogue](https://experienceleague.adobe.com/docs/commerce/product-recommendations/developer/development-overview.html) pour fonctionner. Le processus de synchronisation des données de catalogue reste inchangé dans une implémentation découplée, mais des modifications sont nécessaires pour la collecte de données comportementales.

>[!NOTE]
>
>Les instances découplées doivent implémenter des événements pour alimenter le tableau de bord des recommandations de produits.

Pour intégrer [!DNL Product Recommendations] dans un storefront découplé, vous devez :

1. Envoyez des données comportementales à Adobe Sensei pour analyser et calculer les résultats des recommandations de produits. Vous pouvez également envoyer des données supplémentaires pour activer la recommandation de produit [rapport de mesures](workspace.md).

1. Récupérez les résultats des recommandations de produits et effectuez leur rendu sur la page.

Vous pouvez effectuer ces deux actions à l’aide des SDK disponibles, comme décrit dans le workflow suivant.

1. [Installez](install-configure.md) le module [!DNL Product Recommendations].

1. Installez et utilisez le [SDK d’événement de storefront d’Adobe Commerce](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/) pour déclencher les [événements comportementaux](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#product-recommendations).

   Événements minimaux requis pour renvoyer [!DNL Product Recommendations] résultats :

   | Événement | Catégorie |
   |--- | ---|
   | `view` | produit |
   | `add-to-cart` | produit |
   | `place-order` | passage en caisse |

   Pour activer le [reporting des mesures](workspace.md), les événements supplémentaires suivants sont requis :

   | Événement | Catégorie |
   |--- | ---|
   | `impression-render` | recommendation-unit |
   | `view` | recommendation-unit |
   | `rec-click` | recommendation-unit |
   | `rec-add-to-cart-click` | recommendation-unit (si un bouton « Ajouter au panier » est présent dans le modèle de recommandations) |

1. Lorsque les événements sont déclenchés, utilisez le [collecteur d’événements du storefront d’Adobe Commerce](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/) pour gérer les événements et les envoyer à Adobe Sensei.

1. Une fois les données comportementales collectées, vous pouvez [créer](create.md) [!DNL Product Recommendations] dans l’Administration.

1. Utilisez le [SDK Recommendations](https://developer.adobe.com/commerce/services/product-recommendations/) pour récupérer les unités de recommandation sur le storefront. Le SDK renvoie les données de produit nécessaires pour effectuer le rendu des unités de recommandation sur une page.

1. Découvrez comment utiliser la requête [`recommendations` GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/) pour renvoyer des informations sur les blocs de recommandation de produit pour un SKU donné, etc.
