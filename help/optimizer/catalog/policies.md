---
title: Politiques
description: Découvrez comment utiliser des politiques pour filtrer les données au sein d’un canal afin de vous assurer que les données sont envoyées à la bonne destination.
hide: true
recommendations: noCatalog
source-git-commit: 425c801a852de566120504563e256b0351df588e
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 0%

---

# Politiques

>[!NOTE]
>
>Cette documentation décrit un produit en développement à accès anticipé et ne reflète pas toutes les fonctionnalités destinées à une disponibilité générale.

Les politiques sont des filtres d’accès aux données contenus dans les canaux qui affinent davantage les données diffusées à chaque canal. Les stratégies garantissent que le bon contenu est envoyé vers la bonne destination. Par exemple, les magasins physiques de point de vente, les places de marché, les pipelines publicitaires (Google, Facebook, Instagram).

Les stratégies sont basées sur des attributs de produit, tels que la marque, le modèle ou la catégorie de pièces, et sont utilisées pour adapter les données du catalogue aux besoins spécifiques de l’entreprise.

## Filtres

Les filtres sont le mécanisme au sein d’une politique qui applique la segmentation de catalogue. Les filtres permettent aux entreprises d&#39;adapter leurs vitrines et leurs canaux à des ensembles de produits spécifiques en fonction de leurs besoins opérationnels. Vous utilisez des critères tels que les attributs de produit, les opérateurs et les valeurs pour définir une règle ou une condition qui indique quels produits sont inclus ou exclus dans un canal ou un storefront.

### Parties d&#39;un filtre

Un filtre est composé des parties suivantes :

| Partie | Description | Exemple |
|---|---|---|
| **Attribut** | Attribut de produit utilisé pour le filtrage. | `part_category` |
| **Opérateur** | Condition appliquée à l’attribut . | `IN`, `EQUALS`, `CONTAINS` |
| **Source de la valeur** | Indique si les valeurs sont `STATIC` ou `TRIGGER`. | `STATIC` |
| **Valeur** | Valeurs spécifiques qui remplissent la condition. | `brakes, suspension` |

### Exemple

Un filtre avec l’attribut `part_category`, un opérateur de `IN` et des valeurs `brakes, suspension` garantit que seuls les produits classés comme freins et suspension sont inclus dans la politique.

### Types de source de valeur

Il existe deux types de sources de valeurs : **STATIC** et **TRIGGER**.

Les politiques avec une **Source de valeur** de **STATIC** sont considérées comme des politiques universelles. Les politiques universelles définissent l’expérience d’un site web dans son ensemble. Cela signifie que le canal exécutera toujours cette politique. En d’autres termes, l’exécution de cette politique n’est basée sur aucune interaction de l’utilisateur sur le storefront.

Les politiques avec une **Source de valeur** de **DÉCLENCHEUR** sont appelées politiques exclusives. Cela signifie que le canal n’exécutera cette politique que lorsque le déclencheur sera spécifié dans l’en-tête de l’appel API. Sur le storefront, cela signifie que les informations sont affichées en fonction de ce que l’acheteur sélectionne. Par exemple, dans l’image suivante, il y a deux menus déroulants : **Marque** et **Modèle**.

![Déclencher la source de valeur sur la vitrine](../assets/policy-trigger.png)

**La marque** et **le modèle** sont des déclencheurs définis :

- `AC-Policy-Brand`
- `AC-Policy-Model`

Si l’acheteur clique sur la **liste déroulante Marque** , l’en-tête de l’appel API contient `AC-Policy-Brand`, qui est configuré pour afficher uniquement les produits spécifiques à la `AC-Policy-Brand` stratégie.

## Créer une règle

Dans cette section, vous allez créer une nouvelle stratégie. La politique peut être **STATIQUE** ou **DÉCLENCHEUR**.

### Créer une politique STATIQUE

1. Dans le menu de gauche, ouvrez la **[!UICONTROL Catalog]** section et cliquez sur **[!UICONTROL Policies]**.

1. Cliquez sur le **[!UICONTROL Add Policy]** bouton.

   Une nouvelle page s’ouvre pour vous permettre de renseigner les détails de la stratégie.

1. Saisissez le nom de la stratégie, par exemple « Catégories de pièces Celport ».

1. Cliquez sur le bouton **[!UICONTROL Add Filter]** .

   Une boîte de dialogue s’ouvre pour vous permettre d’ajouter des détails de filtre.

1. Ajoutez les détails du filtre. Par exemple :

   1. **Attribut** - Saisissez un attribut de votre catalogue. Par exemple, « part_category ». Ce nom doit correspondre exactement au nom de l’attribut dans votre catalogue.
   1. **Opérateur** : sélectionnez l’opérateur. Par exemple, **IN.**
   1. **Source** de valeur : sélectionnez **STATIC**.
   1. **Valeur** : entrez la ou les valeurs de l’attribut que vous avez spécifié précédemment. Par exemple, « freins, suspension ».Ces noms doivent correspondre exactement aux noms des valeurs de l’attribut que vous avez spécifié précédemment.

1. Cliquez sur le **[!UICONTROL Save]** bouton dans la boîte de dialogue des détails du filtre.

1. Cliquez sur les points d’action (...) à côté du filtre que vous avez créé et sélectionnez **Activer**. À partir de là, vous pouvez également **Modifier**, **Désactiver** ou **Supprimer** le filtre.

   La colonne **Statut** affiche une icône verte et le mot « Activé ».

1. Cliquez sur le **[!UICONTROL Save]** bouton pour enregistrer la nouvelle stratégie. Si le bouton n’est pas actif, assurez-vous que le nom de la stratégie est ajouté en cliquant sur l’icône en forme de crayon en regard de **Nouvelle stratégie**.

1. Pour vérifier votre nouvelle stratégie, revenez à la liste des stratégies en cliquant sur la flèche Précédent.Votre nouvelle stratégie est répertoriée.

### Création d’une politique TRIGGER

1. Dans le menu de gauche, ouvrez la section **[!UICONTROL Catalog]** et cliquez sur **[!UICONTROL Policies]**.

1. Cliquez sur le bouton **[!UICONTROL Add Policy]** .

   Une nouvelle page s’ouvre pour que vous puissiez renseigner les détails de la politique. &#x200B;

1. Entrez le nom de la règle, par exemple, « Exporter les catégories d&#39;articles ».

1. Cliquez sur le **[!UICONTROL Add Trigger]** bouton.

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

En suivant ces étapes, la politique sera créée et prête à être liée à un canal pour contrôler la visibilité du produit.
