---
title: Filtres de recommandation
description: Découvrez comment utiliser des filtres pour contrôler quels produits apparaissent dans les recommandations  [!DNL Adobe Commerce Optimizer] .
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et  [!DNL Adobe Commerce Optimizer]  (infrastructure SaaS gérée par Adobe)."
exl-id: f6100538-23c0-4e90-9834-a895d4707282
TQID: https://experienceleague.adobe.com/-pmVrAgEsSkn66K00-eaoQ4TF-7Xyxuwlniip1cR4HM
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 116d8bd804df364ddc9cb1175525f08fd32c01bf
workflow-type: tm+mt
source-wordcount: 1919
ht-degree: 0%

---

# Filtrer les produits

[!DNL Adobe Commerce Optimizer] applique automatiquement des filtres par défaut non configurables aux unités de recommandation. Si plusieurs unités de recommandation sont déployées sur une page, [!DNL Adobe Commerce Optimizer] filtre tous les produits qui se répètent dans les unités. Seule la première référence à un produit répété est utilisée, afin de laisser de la place à d’autres produits à recommander. [!DNL Adobe Commerce Optimizer] filtre également tous les produits achetés précédemment et ceux qui se trouvent dans le panier.

Lorsque vous [créez](create.md) une unité de recommandation, vous pouvez définir des filtres qui contrôlent les produits pouvant être affichés dans les recommandations. Ces filtres sont basés sur un ensemble de conditions d’inclusion ou d’exclusion que vous définissez. Seuls les produits qui correspondent à toutes les conditions d’inclusion apparaissent dans les recommandations. Les produits qui correspondent à l’une des conditions d’exclusion ne sont pas recommandés.

Vous pouvez configurer plusieurs filtres et n’activer que ceux de votre choix en cliquant sur le bouton (bascule) de chaque page de filtre. Vous pouvez ainsi créer des brouillons de filtres pour une utilisation ultérieure. Le nombre de filtres activés s’affiche sur chaque onglet.

## Conditions

Les conditions peuvent être statiques ou dynamiques.

- Une condition statique utilise des attributs de produit existants pour déterminer quels produits peuvent apparaître dans l’unité. Par exemple, vous pouvez spécifier que seuls les produits en stock dont le prix est supérieur à 25 $ apparaissent dans l’unité.

- Condition dynamique clé du contexte actuel d’un acheteur, tel que la catégorie ou le produit actuellement consulté. Par exemple, lors de la création d’une recommandation de produit à déployer sur les pages de détails du produit, vous pouvez utiliser un [filtre de prix dynamique](#dynamic-price-filters-relative-to-current-product) pour inclure ou exclure des produits d’une plage de prix relative du produit actuellement consulté.

### Opérateurs logiques

Les opérateurs logiques `AND` et `OR` sont utilisés pour joindre plusieurs conditions. Si vous utilisez des filtres d’inclusion et d’exclusion sur plusieurs types de filtre, les inclusions sont d’abord évaluées afin de déterminer tous les produits possibles qui peuvent être recommandés, puis les produits qui correspondent à n’importe quel filtre d’exclusion sont supprimés de la liste. Les filtres **Prix** utilisent un ordre différent parmi les règles de prix : les exclusions en premier, puis les inclusions. Voir [Comment inclure et exclure des règles pour utiliser le prix](#how-include-and-exclude-rules-use-price).

- `AND` - Rejoint deux conditions de filtrage des inclusions
- `OR` - Rejoint deux conditions de filtrage des exclusions

## Types de filtres

Chaque type de filtre cible un aspect différent du catalogue, tel que le produit et le prix, afin que vous puissiez limiter ou élargir les produits éligibles à une unité. Choisissez les types qui correspondent à vos objectifs de marchandisage, puis combinez les conditions d’inclusion et d’exclusion selon vos besoins. Les sous-sections ci-dessous décrivent le comportement de chaque type et la manière dont [!DNL Adobe Commerce Optimizer] l’applique.

>[!NOTE]
>
>Seuls les produits correspondant à vos filtres **inclusion** peuvent être recommandés et tout produit correspondant à un filtre **exclusion** est supprimé.

### Prix {#price}

>[!IMPORTANT]
>
>Le filtrage des prix est en version bêta.

Le filtrage des prix utilise le **prix calculé final** de chaque produit du **catalogue des prix actif** du storefront, qui est le catalogue des prix attribué au storefront dans lequel l’unité de recommandation est rendue.

Cette valeur :

- **Inclut** les remises, les promotions et les prix spéciaux définis dans ce catalogue de prix (et non le prix catalogue uniquement).
- **Exclut** l’expédition et les ajustements au niveau du panier.
- **S&#39;applique uniquement** au catalogue de prix actif pour ce storefront ; les autres storefronts ou catalogues de prix ne sont pas utilisés.

Configurez la façon dont les livres de prix sont associés à un storefront dans votre catalogue et [configuration des livres de prix](../../setup/pricebooks.md).

#### Comment inclure et exclure des règles utiliser le prix {#how-include-and-exclude-rules-use-price}

- **Règles d’exclusion** - Les produits dont le prix final **correspond à une exclusion de prix définie** sont supprimés en premier.
- **Règles d’inclusion** - Parmi les autres candidats, seuls les produits dont le prix final **correspond à toutes** les conditions d’inclusion de prix définies restent éligibles. Cela inclut chaque filtre d’inclusion activé (par exemple, votre règle de prix ainsi que toutes les autres règles d’inclusion).

Les règles de prix **filtrer** le candidat de recommandation défini ; elles ne **pas** reclassent les produits. Le moteur génère une liste avec classement, les règles d’inclusion et d’exclusion de prix suppriment les produits de cette liste et l’ordre relatif des produits restants reste le même. Si le nombre de produits admissibles est inférieur au nombre de demandes d&#39;unité, seuls les articles valides sont affichés. Si aucun n’est qualifié, l’unité n’est pas rendue (aucun espace réservé vide).

Le prix affiché sur les produits à l’intérieur de l’unité de recommandation est le même **prix final** du catalogue des prix de ce magasin, de sorte que ce que les acheteurs voient correspond à la valeur utilisée pour le filtrage. Dans la prévisualisation Admin, les produits configurables peuvent afficher une plage de prix lorsque les prix des variantes diffèrent ; voir [&#x200B; Produits configurables dans la prévisualisation &#x200B;](#configurable-products-in-preview).

#### Gamme de prix statique

Utilisez un filtre de prix **statique** lorsque vous souhaitez un minimum ou un maximum fixe dans la devise de base de votre magasin, quel que soit le produit consulté par l’acheteur.

##### Configurer un filtre de prix statique

1. Lors de la [création ou modification](create.md) d’une unité de recommandation, ouvrez **[!UICONTROL Filter products]** (ou accédez à l’étape _Filtres_ à partir du workflow d’unité).
1. Sélectionnez l&#39;onglet **[!UICONTROL Inclusions]** ou **[!UICONTROL Exclusions]**, selon que vous souhaitez autoriser uniquement les produits d&#39;une plage de prix ou bloquer les produits d&#39;une plage. Le badge de chaque onglet indique le nombre de filtres activés de ce type.
1. Dans la liste de gauche, sélectionnez **[!UICONTROL Price]**.
1. **[!UICONTROL Enable filter]**.

   Les valeurs de prix utilisent la **devise de base du site web**, comme indiqué sur la page.

1. Ouvrez **[!UICONTROL Include products based on]** (dans l’onglet **[!UICONTROL Inclusions]** ) ou le contrôle équivalent dans l’onglet **[!UICONTROL Exclusions]** , puis choisissez **[!UICONTROL Set price range]**.
1. Définissez une **[!UICONTROL Min price]** et/ou une **[!UICONTROL Max price]** facultative à l’aide des champs en regard du symbole de devise. Vous pouvez saisir des montants ou utiliser les commandes **-** et **+** pour ajuster les valeurs. Laissez un lien vide si vous n’avez pas besoin d’un minimum ou d’un maximum. La fourchette est comparée au prix calculé final de chaque produit pour le portefeuille de prix actif du magasin.
1. Terminez la configuration de l’unité de recommandation et enregistrez ou publiez-la comme vous le feriez normalement pour que le filtre prenne effet.

![Filtre de prix](../../assets/filter-price.png)

#### Filtres de prix dynamiques (par rapport au produit actuel) {#dynamic-price-filters-relative-to-current-product}

Utilisez un filtre de prix **dynamique** lorsque les recommandations doivent être limitées par rapport au **produit actuellement consulté** sur une page de détails du produit (PDP). Le filtre utilise le prix final de ce produit comme **ancre** et compare les produits recommandés aux limites que vous définissez.

Les opérateurs dynamiques sont disponibles uniquement pour les types de recommandation [liés au SKU](types.md) qui s’exécutent dans un contexte de produit, par exemple :

- A consulté ceci, a consulté cela
- A vu ceci, a acheté cela
- J&#39;ai acheté ça, acheté ça
- Plus comme ceci
- Similarité visuelle

Ils ne sont **pas** disponibles pour les types basés sur la popularité (par exemple, **Les plus consultés** ou **Les plus achetés**), car ces unités n’ont pas un seul produit actuel pour ancrer le filtre.

Sur le storefront, la liste déroulante de recommandation lit le prix du produit actuel à partir du contexte PDP et l’envoie avec la demande de recommandation. [!DNL Adobe Commerce Optimizer] utilise cette valeur comme point d’ancrage lors de l’évaluation des règles de prix dynamiques. Pour les produits configurables, l’ancre est le **variante la plus basse** prix final (`priceRange.minimum`).

##### Opérateurs

Dans **[!UICONTROL Include products based on]** (ou l’équivalent exclusions), vous pouvez choisir :

| Opérateur | Objectif |
| --- | --- |
| **Inférieur ou égal au prix actuel du produit** | Inclure ou exclure les produits au niveau ou au-dessous d&#39;une limite dérivée du prix d&#39;ancrage plus un décalage. |
| **Supérieur ou égal au prix actuel du produit** | Inclure ou exclure les produits au niveau ou au-dessus d&#39;une limite dérivée du prix d&#39;ancrage plus un décalage. |
| **Dans une plage de valeurs du produit actuel** | Inclure ou exclure les produits dont le prix final se situe dans une fourchette de devises fixes autour du prix d&#39;ancrage (les décalages par rapport au prix actuel). |
| **Dans une plage de pourcentage du produit actuel** | Inclure ou exclure les produits dont le prix final se situe dans une fourchette de pourcentage autour du point d’ancrage. |

##### Sémantique de décalage

Pour **Inférieur ou égal au prix actuel du produit** et **Supérieur ou égal au prix actuel du produit**, la valeur que vous saisissez est un **décalage numérique ajouté au prix d’ancrage** pour former la limite :

- Un décalage **négatif** déplace la limite **en dessous** du prix actuel du produit.
- Un décalage **positif** déplace la limite **au-dessus** du prix actuel du produit.
- **Vide** ou **0** signifie **aucune limite** de ce côté ; le serveur principal les traite de la même manière.
- Vous ne pouvez pas utiliser **0** pour signifier « exactement le prix actuel du produit » comme limite.

Ceci correspond à [!DNL Product Recommendations] sur PaaS. Les libellés dans l’Administration reflètent directement cette sémantique.

##### Configurer un filtre de prix dynamique

1. [Créer ou modifier](create.md) une unité de recommandation **liée au SKU** déployée sur la page **détails du produit** (ou un autre emplacement où un produit actuel est toujours en contexte).
1. Ouvrez **[!UICONTROL Filter products]** et sélectionnez l’onglet **[!UICONTROL Inclusions]** ou **[!UICONTROL Exclusions]** .
1. Sélectionnez **[!UICONTROL Price]** et activez **[!UICONTROL Enable filter]**.
1. Ouvrez **[!UICONTROL Include products based on]** (ou l’équivalent des exclusions) et choisissez un opérateur dynamique (par exemple, **Dans une plage de valeurs du produit actuel**).
1. Saisissez les décalages ou les valeurs de plage lorsque vous y êtes invité. Utilisez l’aperçu pour confirmer les résultats d’un exemple de produit.
1. Enregistrez ou publiez l’unité.

Les valeurs non valides (valeurs non numériques, combinaisons non prises en charge ou plages où le minimum est supérieur au maximum) bloquent l’enregistrement et affichent les erreurs de validation ; **[!UICONTROL Save]** reste désactivé jusqu’à ce que le filtre soit valide.

##### Lorsqu’aucun prix d’ancrage n’est disponible

Si un filtre de prix dynamique est activé mais que le storefront ne peut pas fournir un prix de produit actuel (par exemple, l’unité est rendue en dehors d’un contexte PDP), [!DNL Adobe Commerce Optimizer] ne renvoie pas de recommandations non filtrées. L’unité affiche **aucune recommandation**, car l’affichage de résultats non filtrés ne correspond pas à la règle que vous avez configurée.

##### Produits configurables dans l’aperçu {#configurable-products-in-preview}

Dans le panneau Admin **aperçu**, les prix recommandés des produits s’affichent comme suit :

- **Produits simples** - Prix final unique issu de la réponse de GraphQL.
- **Produits configurables** - Si les prix de variante minimum et maximum diffèrent, l’aperçu affiche une plage (par exemple, `$min – $max`). S’ils sont égaux, un seul prix s’affiche.

Le prix d’ancrage utilisé pour les calculs de filtre dynamique sur un produit configurable est toujours le prix final de la variante **minimum**, cohérent avec le storefront.

#### Exemples de filtres de prix

Les exemples suivants utilisent un prix de produit actuel de **$500**. Ajustez l’inclusion par rapport à l’exclusion pour correspondre à votre objectif de marchandisage.

| Opérateur | Tabulation | Objectif | Exemple de limite |
| --- | --- | --- | --- |
| Inférieur ou égal au prix actuel du produit | Exclusions | Promouvoir la montée en gamme en masquant les alternatives à bas prix | Exclure les produits ≤ 500 $ |
| Inférieur ou égal au prix actuel du produit | Inclusions | Proposer des alternatives abordables | Inclure les produits ≤ 500 $ |
| Supérieur ou égal au prix actuel du produit | Exclusions | Éviter les ventes incitatives dans un flux axé sur le budget | Exclure les produits ≥ 500 $ |
| Supérieur ou égal au prix actuel du produit | Inclusions | Options de prime de surface | Inclure les produits ≥ 500 $ |
| Dans une plage de valeurs du produit actuel | Exclusions | Diversifier à partir de points de prix similaires | Exclure 400 $-600 $ |
| Dans une plage de valeurs du produit actuel | Inclusions | Afficher des alternatives comparables dans une bande étroite | Inclure 400 $ À 600 $ |
| Dans une plage de pourcentage du produit actuel | Exclusions | Réduire les articles à prix similaires (par exemple ±20 %) | Exclure environ 400 à 600 $ |
| Dans une plage de pourcentage du produit actuel | Inclusions | Comparaison équitable au sein d&#39;une fourchette comparable | Inclure environ 400 à 600 $ |

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

<!--
### Attribute

You can filter products based on attribute criteria, including attribute values. Selected values use OR logic to either include or exclude products when any of the specified values are found.
-->
