---
title: Filtres de recommandation
description: Découvrez comment utiliser des filtres pour contrôler quels produits apparaissent dans les recommandations  [!DNL Adobe Commerce Optimizer] .
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et  [!DNL Adobe Commerce Optimizer]  (infrastructure SaaS gérée par Adobe)."
exl-id: f6100538-23c0-4e90-9834-a895d4707282
source-git-commit: e15624322fabb89d0b618f9d6c689445a7c448df
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 0%

---

# Filtrer les produits

[!DNL Adobe Commerce Optimizer] applique automatiquement des filtres par défaut non configurables aux unités de recommandation. Si plusieurs unités de recommandation sont déployées sur une page, [!DNL Adobe Commerce Optimizer] filtre tous les produits qui se répètent dans les unités. Seule la première référence à un produit répété est utilisée, afin de laisser de la place à d’autres produits à recommander. [!DNL Adobe Commerce Optimizer] filtre également tous les produits achetés précédemment et ceux qui se trouvent dans le panier.

Lorsque vous [créez](create.md) une unité de recommandation, vous pouvez définir des filtres qui contrôlent les produits pouvant être affichés dans les recommandations. Ces filtres sont basés sur un ensemble de conditions d’inclusion ou d’exclusion que vous définissez. Seuls les produits qui correspondent à toutes les conditions d’inclusion apparaissent dans les recommandations. Les produits qui correspondent à l’une des conditions d’exclusion ne sont pas recommandés.

Vous pouvez configurer plusieurs filtres et n’activer que ceux de votre choix en cliquant sur le bouton (bascule) de chaque page de filtre. Vous pouvez ainsi créer des brouillons de filtres pour une utilisation ultérieure. Le nombre de filtres activés s’affiche sur chaque onglet.

## Conditions

Les conditions peuvent être statiques ou dynamiques.

- Une condition statique utilise des attributs de produit existants pour déterminer quels produits peuvent apparaître dans l’unité. Par exemple, vous pouvez spécifier que seuls les produits en stock dont le prix est supérieur à 25 $ apparaissent dans l’unité.

- Condition dynamique clé du contexte actuel d’un acheteur, tel que la catégorie ou le produit actuellement consulté. Par exemple, lors de la création d’une recommandation de produit à déployer sur les pages de détails du produit, vous pouvez créer une condition pour recommander uniquement des produits qui se trouvent dans une plage de prix relative du produit actuellement consulté.

### Opérateurs logiques

Les opérateurs logiques `AND` et `OR` sont utilisés pour joindre plusieurs conditions. Si vous utilisez à la fois des filtres d’inclusion et d’exclusion, les inclusions sont d’abord évaluées afin de déterminer tous les produits possibles qui peuvent être recommandés, puis les produits qui correspondent à n’importe quel filtre d’exclusion sont supprimés de la liste.

- `AND` - Rejoint deux conditions de filtrage des inclusions
- `OR` - Rejoint deux conditions de filtrage des exclusions

## Types de filtres

Chaque type de filtre cible un aspect différent du catalogue, tel que le produit et le prix, afin que vous puissiez limiter ou élargir les produits éligibles à une unité. Choisissez les types qui correspondent à vos objectifs de marchandisage, puis combinez les conditions d’inclusion et d’exclusion selon vos besoins. Les sous-sections ci-dessous décrivent le comportement de chaque type et la manière dont [!DNL Adobe Commerce Optimizer] l’applique.

>[!NOTE]
>
>Seuls les produits correspondant à vos filtres **inclusion** peuvent être recommandés et tout produit correspondant à un filtre **exclusion** est supprimé.

### Prix

>[!IMPORTANT]
>
>La fonctionnalité suivante est en version bêta.

Le filtrage des prix utilise le **prix calculé final** de chaque produit pour le **catalogue de prix actif** du storefront, c’est-à-dire le prix attribué au storefront dans lequel l’unité de recommandation est rendue. Cette valeur reflète les remises, les promotions et les prix spéciaux définis dans ce catalogue des prix, et non le prix catalogue seul. L’évaluation utilise uniquement le catalogue de prix de ce magasin ; les autres magasins ou catalogues de prix ne s’appliquent pas. La façon dont les tarifs sont associés à un storefront est configurée avec votre catalogue et [&#x200B; configuration des tarifs](../../setup/pricebooks.md).

#### Comment inclure et exclure des règles utiliser le prix

- **Règles d’inclusion** - Seuls les produits dont le prix final **correspond à toutes les conditions d’inclusion définies** restent éligibles. Cela inclut chaque filtre d’inclusion activé (par exemple, votre plage de prix ainsi que toute autre règle d’inclusion).
- **Règles d’exclusion** - Les produits dont le prix final **correspond à n’importe quelle condition d’exclusion définie** sont supprimés des recommandations.

**Prix affiché** - Le prix affiché sur les produits à l’intérieur de l’unité de recommandation est le même **prix final** du catalogue des prix de ce magasin. Par conséquent, ce que les acheteurs voient correspond à la valeur utilisée pour le filtrage.

#### Configurer un filtre de prix

1. Lors de la [création ou modification](create.md) d’une unité de recommandation, ouvrez **[!UICONTROL Filter products]** (ou accédez à l’étape _Filtres_ à partir du workflow d’unité).
1. Sélectionnez l&#39;onglet **[!UICONTROL Inclusions]** ou **[!UICONTROL Exclusions]**, selon que vous souhaitez autoriser uniquement les produits d&#39;une plage de prix ou bloquer les produits d&#39;une plage. Le badge de chaque onglet indique le nombre de filtres activés de ce type.
1. Dans la liste de gauche, sélectionnez **[!UICONTROL Price]**.
1. **[!UICONTROL Enable filter]**.

   Les valeurs de prix utilisent la **devise de base du site web**, comme indiqué sur la page.

1. Ouvrez **[!UICONTROL Include products based on]** (dans l’onglet **[!UICONTROL Inclusions]** ) ou le contrôle équivalent dans l’onglet **[!UICONTROL Exclusions]** , puis choisissez **[!UICONTROL Set price range]**.
1. Définissez une **[!UICONTROL Min price]** et/ou une **[!UICONTROL Max price]** facultative à l’aide des champs en regard du symbole de devise. Vous pouvez saisir des montants ou utiliser les commandes **-** et **+** pour ajuster les valeurs. Laissez un lien vide si vous n’avez pas besoin d’un minimum ou d’un maximum. La fourchette est comparée au prix calculé final de chaque produit pour le portefeuille de prix actif du magasin.
1. Terminez la configuration de l’unité de recommandation et enregistrez ou publiez-la comme vous le feriez normalement pour que le filtre prenne effet.

![Filtre de prix](../../assets/filter-price.png)

### Produit

Les filtres de produit ciblent des éléments de catalogue individuels par **SKU**. Vous ajoutez un ou plusieurs SKU pour autoriser uniquement ces produits (**Inclusions**) ou les bloquer (**Exclusions**), en utilisant la même page **[!UICONTROL Filter products]** que [filtres de prix](#price). Vous ne pouvez pas afficher en surface les produits désactivés ou les produits qui ne sont pas visibles individuellement dans une unité de recommandation ; ces produits n’apparaissent jamais sur le storefront, quels que soient les filtres.

#### Configurer un filtre de produit

1. Lors de la [création ou modification](create.md) d’une unité de recommandation, ouvrez **[!UICONTROL Filter products]** (ou accédez à l’étape _Filtres_ à partir du workflow d’unité).
1. Sélectionnez l’onglet **[!UICONTROL Inclusions]** ou **[!UICONTROL Exclusions]** . Le badge de chaque onglet indique le nombre de filtres activés de ce type.
1. Dans la liste de gauche, sélectionnez **[!UICONTROL Product]**.
1. **[!UICONTROL Enable filter]**.

   L’en-tête du panneau de droite reflète l’onglet, par exemple **[!UICONTROL Product inclusions]** ou l’équivalent pour les exclusions.

1. Dans **[!UICONTROL Product SKU]**, saisissez un SKU et cliquez sur **[!UICONTROL Add]**. Répétez l’opération pour ajouter d’autres SKU.

   Sous **[!UICONTROL Product SKUs]**, chaque SKU s’affiche sous la forme d’une balise amovible. Cliquez sur **X** sur une balise pour supprimer ce SKU ou cliquez sur **[!UICONTROL Clear All]** pour supprimer chaque SKU de la liste.

1. Terminez la configuration de l’unité de recommandation et enregistrez ou publiez-la comme vous le feriez normalement pour que le filtre prenne effet.

Pour les **inclusions**, seuls les produits dont les SKU sont répertoriés (et qui répondent à vos autres filtres d’inclusion activés) peuvent être recommandés. Pour les **exclusions**, tout produit dont le SKU est répertorié n’est pas recommandé, même s’il est éligible par ailleurs.

![Filtre de produit](../../assets/filter-product.png)

>[!NOTE]
>
>Les produits enfants d’un produit configurable ne sont pas affichés dans une unité de recommandation, car ces produits enfants ont la visibilité de _Non visible individuellement_.

<!--### Attribute

You can filter products based on attribute criteria, including attribute values. Selected values use OR logic to either include or exclude products when any of the specified values are found.-->
