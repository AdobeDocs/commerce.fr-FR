---
title: Politiques
description: Découvrez comment créer et gérer des politiques dans  [!DNL Adobe Commerce Optimizer].
recommendations: noCatalog
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
source-git-commit: 356b10704c9e7c7329d3e9c0e10baa15d5142ec0
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 0%

---

# Politiques

Les politiques sont des filtres d’accès aux données contenus dans les vues de catalogue qui affinent davantage les données fournies à chaque vue de catalogue. Les politiques s’assurent que le contenu approprié est envoyé à la bonne destination. Par exemple, les points de vente, les magasins physiques, les places de marché, les pipelines de publicités (Google, Facebook, Instagram).

Les politiques sont basées sur les attributs de produit, tels que la marque, le modèle ou la catégorie d’articles, et sont utilisées pour adapter les données du catalogue aux besoins spécifiques de l’entreprise. &#x200B;

## Filtres

Les filtres sont le mécanisme au sein d’une politique qui applique la segmentation de catalogue. Les filtres permettent aux entreprises d&#39;adapter les vitrines et les vues de catalogue à des ensembles de produits spécifiques en fonction des besoins opérationnels. Vous utilisez des critères tels que des attributs de produit, des opérateurs et des valeurs pour définir une règle ou une condition qui indique quels produits sont inclus ou exclus dans une vue de catalogue ou un storefront.

### Parties d&#39;un filtre

Un filtre est composé des parties suivantes :

| Partie | Description | Exemple |
|---|---|---|
| **Attribut** | Attribut de produit utilisé pour le filtrage. | `part_category` |
| **Opérateur** | Condition appliquée à l’attribut . | `IN`, `EQUALS`, `CONTAINS` |
| **Source de la valeur** | Indique si les valeurs sont `STATIC` ou `TRIGGER`. | `STATIC` [En savoir plus](#value-source-types) |
| **Valeur** | Valeurs spécifiques qui remplissent la condition. | `brakes, suspension` |

### Exemple

Un filtre avec l’attribut `part_category`, un opérateur de `IN` et des valeurs `brakes, suspension` garantit que seuls les produits avec un attribut `part_category` dont la valeur est `brake` ou `suspension` sont filtrés et affichés par la politique.

### Types de source de valeur

Il existe deux types de sources de valeurs : **STATIC** et **TRIGGER**.

Les politiques avec une **Source de valeur** de **STATIC** sont considérées comme des politiques universelles. Les politiques universelles définissent l’expérience d’un site web dans son ensemble. Cela signifie que la vue Catalogue exécutera toujours cette politique. En d’autres termes, l’exécution de cette politique n’est basée sur aucune interaction de l’utilisateur sur le storefront.

Les politiques avec une **Source de valeur** de **DÉCLENCHEUR** sont appelées politiques exclusives. Cela signifie que la vue Catalogue n’exécutera cette politique que lorsque le déclencheur sera spécifié dans l’en-tête de l’appel API. Sur le storefront, cela signifie que les informations sont affichées en fonction de ce que l’acheteur sélectionne. Par exemple, dans l’image suivante, il existe deux menus déroulants : **Marque** et **Modèle**.

![Déclencher la source de valeur sur storefront](../assets/policy-trigger.png)

**Brand** et **Model** sont des déclencheurs définis :

- `AC-Policy-Brand`
- `AC-Policy-Model`

Si l’acheteur clique sur la liste déroulante **Marque**, l’en-tête de l’appel API contient `AC-Policy-Brand`, qui est configuré pour afficher uniquement les produits spécifiques à la politique de `AC-Policy-Brand`.

## Créer une politique

Dans cette section, vous allez créer une nouvelle politique. La politique peut être **STATIQUE** ou **DÉCLENCHEUR**.

### Créer une politique STATIQUE

1. Dans le menu de gauche, ouvrez la section **[!UICONTROL Catalog]** et cliquez sur **[!UICONTROL Policies]**.

1. Cliquez sur le bouton **[!UICONTROL Add Policy]** .

   Une nouvelle page s’ouvre pour que vous puissiez renseigner les détails de la politique. &#x200B;

1. Entrez le nom de la règle, par exemple, « Exporter les catégories d&#39;articles ».

1. Cliquez sur le bouton **[!UICONTROL Add Filter]** .

   Une boîte de dialogue s’ouvre pour vous permettre d’ajouter des détails de filtre.

1. Ajoutez les détails du filtre. Par exemple :

   1. **Attribut** - Saisissez un attribut de votre catalogue. Par exemple, « part_category ». Ce nom doit correspondre exactement au nom de l’attribut dans votre catalogue.
   1. **Opérateur** - Sélectionnez l’opérateur. Par exemple, **IN**. &#x200B;
   1. **Valeur Source** - Sélectionnez **STATIQUE**. &#x200B;
   1. **Valeur** - Saisissez la ou les valeurs dans l’attribut que vous avez précédemment spécifié. Par exemple, « freins, suspension ». &#x200B;Ces noms doivent correspondre exactement aux noms des valeurs de l’attribut que vous avez précédemment spécifié.

1. Cliquez sur le bouton **[!UICONTROL Save]** dans la boîte de dialogue Détails du filtre. &#x200B;

1. Cliquez sur les points d’action (...) à côté du filtre que vous avez créé et sélectionnez **Activer**. À partir de là, vous pouvez également **Modifier**, **Désactiver** ou **Supprimer** le filtre.

   La colonne **Statut** affiche une icône verte et le mot « Activé ».

1. Cliquez sur le bouton **[!UICONTROL Save]** pour enregistrer la nouvelle politique&#x200B; Si le bouton n’est pas actif, vérifiez que le nom de la politique est ajouté en cliquant sur l’icône en forme de crayon en regard de **Nouvelle politique**.

1. Pour vérifier votre nouvelle politique, revenez à la liste des politiques en cliquant sur la flèche Précédent. &#x200B;Votre nouvelle politique est répertoriée.

### Création d’une politique TRIGGER

1. Dans le menu de gauche, ouvrez la section **[!UICONTROL Catalog]** et cliquez sur **[!UICONTROL Policies]**.

1. Cliquez sur le bouton **[!UICONTROL Add Policy]** .

   Une nouvelle page s’ouvre pour que vous puissiez renseigner les détails de la politique. &#x200B;

1. Entrez le nom de la règle, par exemple, « Exporter les catégories d&#39;articles ».

1. Cliquez sur le bouton **[!UICONTROL Add Trigger]** .

   La boîte de dialogue **Détails du déclencheur** s’affiche.

1. Saisissez un nom pour le déclencheur, tel que **AC-Policy-Brand**.

1. Sélectionnez le **Type de transport**. **HTTP_HEADER** est actuellement le seul type pris en charge.

1. Cliquez sur le bouton **[!UICONTROL Save]** pour enregistrer le déclencheur.

1. Cliquez sur le bouton **[!UICONTROL Add Filter]** .

   Une boîte de dialogue s’ouvre pour vous permettre d’ajouter des détails de filtre.

1. Ajoutez les détails du filtre. Par exemple :

   1. **Attribut** - Saisissez un attribut de votre catalogue. Par exemple, « part_category ». Ce nom doit correspondre exactement au nom de l’attribut dans votre catalogue.
   1. **Opérateur** - Sélectionnez l’opérateur. Par exemple, **IN**. &#x200B;
   1. **Valeur Source** - Sélectionnez **DÉCLENCHEUR**. &#x200B;
   1. **Valeur** - Saisissez le nom du déclencheur que vous avez créé précédemment (**AC-Policy-Brand**).

1. Cliquez sur le bouton **[!UICONTROL Save]** dans la boîte de dialogue Détails du filtre. &#x200B;

1. Cliquez sur les points d’action (...) à côté du filtre que vous avez créé et sélectionnez **Activer**. À partir de là, vous pouvez également **Modifier**, **Désactiver** ou **Supprimer** le filtre.

   La colonne **Statut** affiche une icône verte et le mot « Activé ».

1. Cliquez sur le bouton **[!UICONTROL Save]** pour enregistrer la nouvelle politique&#x200B; Si le bouton n’est pas actif, vérifiez que le nom de la politique est ajouté en cliquant sur l’icône en forme de crayon en regard de **Nouvelle politique**.

1. Pour vérifier votre nouvelle politique, revenez à la liste des politiques en cliquant sur la flèche Précédent. &#x200B;Votre nouvelle politique est répertoriée.

En suivant ces étapes, la politique sera créée et prête à être liée à une vue de catalogue pour contrôler la visibilité du produit.
