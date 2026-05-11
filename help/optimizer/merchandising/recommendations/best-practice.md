---
title: Bonnes pratiques relatives aux recommandations
description: Découvrez où placer des recommandations sur différentes pages de votre site et obtenez des suggestions pour les libellés fréquemment utilisés pour chaque type de recommandation.
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et  [!DNL Adobe Commerce Optimizer]  (infrastructure SaaS gérée par Adobe)."
exl-id: 08d7aeff-8b86-4fa3-93e6-4b72dc1ab117
TQID: https://experienceleague.adobe.com/J4vSJ4EMfSTeL7rVEv9bTr998wvU5DR4S-hXQ3HCSGg
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
topic_v2:
  - id: bcc5edb5-84c3-4940-9f84-ed88b6c16274
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 360
ht-degree: 0%

---

# Bonnes pratiques relatives aux recommandations

Adobe recommande de suivre les instructions suivantes lors de l’utilisation de recommendations :

- Diversifiez vos types de recommandations. Les clients commencent à ignorer les recommandations s’ils suggèrent les mêmes produits à plusieurs reprises.

- Ne déployez pas les mêmes recommandations sur la page de votre panier et sur la page de confirmation de commande. Pensez à utiliser `Most Added to Cart` pour la page Panier et `Bought This, Bought That` pour la page de confirmation de commande.

- Gardez votre site propre. Ne déployez pas plus de trois unités de recommandation sur la même page.

- Si votre boutique vend des vêtements, la recommandation `More like this` peut suggérer des produits spécifiques au genre qui ne correspondent pas au genre du produit affiché. Envisagez d’utiliser ce type de recommandation uniquement pour les catégories non vestimentaires.

## Placement

Avec un si grand nombre de types de recommandations, lequel devriez-vous utiliser sur chaque page ? Si vous ne savez pas par où commencer, essayez ce qui suit :

| Page | Type de recommandation |
|---|---|
| Page d’accueil | `Recommended for you` |
| Page de produit | `Viewed this, viewed that` |
| Panier | `Bought this, bought that` |

Vous pouvez effectuer le suivi des [mesures](../../manage-results/recommendation-performance.md) et les ajuster si nécessaire. N’oubliez pas que l’expérimentation est essentielle.

## Libellés de recommandation

L’étiquette affectée à une recommandation dans le storefront affecte la manière dont les acheteurs interprètent sa pertinence pour eux. Les libellés suivants sont fréquemment utilisés pour chaque type de recommandation.

| Type de recommandation | Étiquettes recommandées |
|---|---|
| Les plus consultés<br> Les plus ajoutés au panier<br>Les plus achetés<br>Conversion (affichage au panier)<br>Conversion (affichage à l’achat) | Éléments les plus populaires<br>Popular<br>Trending<br>Popular en ce moment<br>Récemment populaires<br>Objets populaires inspirés par cet élément (PDP)<br>Meilleures ventes<br>Vous pourriez être intéressé par |
| Recommandé pour vous | Juste pour vous<br>Recommandé pour vous<br>Inspiré par vos tendances d&#39;achat |
| A Consulté Ceci, A Consulté Cela | Les clients qui ont consulté cet élément ont également consulté <br> clients ont également consulté <br> éléments connexes |
| A Consulté Ceci, A Acheté Cela | Les clients qui ont consulté cet objet ont fini par l’acheter<br>Les clients ont fini par l’acheter<br>Que font les autres après avoir consulté cet objet ? |
| J&#39;Ai Acheté Ça, J&#39;Ai Acheté Ça | Obtenez tout ce dont vous avez besoin<br>N&#39;oubliez pas ces <br> fréquemment achetés ensemble |
| Plus Comme Ceci : | Plus d&#39;éléments comme celui<br>ci similaires à ceci |
| Générique | Vous pouvez également aimer<br>Les acheteurs ont également aimé<br>Options similaires<br>Articles connexes |
| En Tendance | Tendance<br>En tendance maintenant<br>Récemment en tendance<br>Articles chauds<br>Produits liés aux tendances (PDP) |
| Récemment consultés | Récemment consultés<br>Jetez un autre coup d’œil |
