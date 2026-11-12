---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 0%
---
Les politiques définissent les filtres qui sont appliqués aux produits dans une vue de catalogue. Ils permettent de personnaliser l’assortiment de produits renvoyé à un storefront ou à un canal. Cela permet de s’assurer que le contenu approprié est diffusé à la bonne destination. Par exemple, les magasins physiques, les places de marché et les canaux publicitaires tels que Google, Facebook et Instagram.

Les politiques utilisent des attributs de produit tels que la marque, le modèle ou la catégorie d’articles pour adapter les données du catalogue aux besoins de l’entreprise. &#x200B;

## Accès à l’espace de travail Politiques

La façon dont vous ouvrez l’espace de travail *Politiques* dépend du produit que vous utilisez :

- **Administrateur Adobe Commerce** (Adobe Commerce as a Cloud Service) : Sélectionnez *Catalogue* > **Politiques**.
- **Adobe Commerce Optimizer Studio** : sélectionnez *Configuration du magasin* > **Politiques**.

## Filtres

Les filtres définissent des conditions basées sur les attributs qui déterminent quels produits correspondent à une politique. Lorsqu’elle est associée à une vue de catalogue, une politique permet de personnaliser les produits renvoyés pour cette vue. Utilisez des attributs de produit, des opérateurs et des valeurs pour définir les conditions correspondantes.

### Parties d&#39;un filtre

Un filtre est composé des parties suivantes :

| Partie | Description | Exemple |
|---|---|---|
| **Attribut** | Attribut de produit utilisé pour le filtrage. | `part_category` |
| **Opérateur** | Condition appliquée à l’attribut . | `IN`, `EQUALS`, `CONTAINS` |
| **Source de la valeur** | Indique si les valeurs sont `STATIC` ou `TRIGGER`. | `STATIC` [En savoir plus](#value-source-types) |
| **Valeur** | Valeurs spécifiques qui remplissent la condition. | `brakes, suspension` |

### Exemple

Un filtre sur `part_category` utilisant l’opérateur `IN` avec les valeurs `brakes` et `suspension` correspond aux produits dont `part_category` est l’une des valeurs.

### Types de source de valeur

Il existe deux types de sources de valeurs : **STATIC** et **TRIGGER**.

Les politiques avec une **source de valeur** sur **STATIC** sont considérées comme des politiques universelles. Les politiques universelles définissent l’expérience d’un site web dans son ensemble. Cela signifie que la vue Catalogue exécute toujours cette politique. L’exécution de la politique ne dépend pas de l’interaction de l’utilisateur storefront.

Les politiques avec une **source de valeur** sur **TRIGGER** sont appelées politiques exclusives. Cela signifie que la vue Catalogue exécute cette politique uniquement lorsque le déclencheur est spécifié dans l’en-tête de l’appel API. Sur le storefront, cela signifie que les informations sont affichées en fonction de ce que l’acheteur sélectionne. Par exemple, l’image suivante comporte deux menus déroulants : **Marque** et **Modèle**.

![Déclencher la source de valeur sur storefront](/help/assets/ccdm-shared/setup/policy-trigger.png)

**Marque** et **Modèle** sont des déclencheurs définis :

- `AC-Policy-Brand`
- `AC-Policy-Model`

Si l’acheteur clique sur la liste déroulante Modèle , l’en-tête de l’appel API contient `AC-Policy-Model`, qui est configuré pour afficher uniquement les produits spécifiques à la politique `AC-Policy-Model`.

### Déclencheurs d’en-tête HTTP à plusieurs valeurs {#multi-value-http-header-triggers}

Une politique de déclenchement utilisant le type de transport `HTTP_HEADER` peut recevoir plusieurs valeurs dans un seul en-tête. Les valeurs doivent être séparées par des virgules et l&#39;opérateur de filtre doit être `IN`. Chaque valeur est traitée comme une correspondance acceptable. Les valeurs sont évaluées avec la sémantique `OR`.

Par exemple, un filtre de politique utilisant `IN` avec l’en-tête suivant :

```
AC-Policy-Vehicle: UNIVERSAL,veh-bolt-mammoth-limited-2025
```

correspond aux produits dont l’attribut `vehicle` est `UNIVERSAL` ou `veh-bolt-mammoth-limited-2025`.

En revanche, un opérateur de filtre de `EQUALS`, `GREATER_THAN_EQUAL` ou `LESS_THAN_EQUAL` est rejeté avec une erreur de validation.

#### Notes de syntaxe

- Le nom de l’en-tête correspond au nom du déclencheur que vous configurez, par exemple `AC-Policy-Vehicle`.
- Des virgules séparent les valeurs individuelles dans l’en-tête. Lorsque le même en-tête `AC-Policy-_Name_` apparaît plusieurs fois, ses valeurs se combinent en une seule valeur d’en-tête séparée par des virgules
- L&#39;opérateur de filtre est `IN`.
- Un filtre de politique avec **Source de valeur** définie sur `TRIGGER`.
- Déclencheur dont le **type de transport** est `HTTP_HEADER`.

## Créer une politique

Dans cette section, vous allez créer une nouvelle politique. La politique peut être **STATIC** ou **TRIGGER**.

### Créer une politique STATIQUE

1. Dans l’espace de travail **[!UICONTROL Policies]**, cliquez sur le bouton **[!UICONTROL Add Policy]**.

   Une nouvelle page s’ouvre pour que vous puissiez renseigner les détails de la politique. &#x200B;

1. Entrez le nom de la règle, par exemple, « Exporter les catégories d&#39;articles ».

1. Cliquez sur le bouton **[!UICONTROL Add Filter]**.

   Une boîte de dialogue s’ouvre pour vous permettre d’ajouter des détails de filtre.

1. Ajoutez les détails du filtre. Par exemple :

   1. **Attribut** - Saisissez un attribut de votre catalogue. Par exemple, « part_category ». Ce nom doit correspondre exactement au nom de l’attribut dans votre catalogue.
   1. **Opérateur** - Sélectionnez l’opérateur. Par exemple, **IN**. &#x200B;
   1. **Valeur Source** - Sélectionnez **STATIC**. &#x200B;
   1. **Valeur** - Saisissez une valeur à partir de la définition d’attribut que vous avez précédemment spécifiée. Par exemple, entrez « freins » pour créer un filtre pour les pièces de frein.
   1. Pour enregistrer la valeur, appuyez sur **Entrée**.

      Si la politique est conçue pour filtrer selon plusieurs valeurs, saisissez chaque valeur séparément.

1. Cliquez sur le bouton **[!UICONTROL Save]** dans la boîte de dialogue Détails du filtre. &#x200B;

1. Cliquez sur l’icône de menu (...) en regard du filtre que vous avez créé, sélectionnez **Activer**. À partir de là, vous pouvez également **Modifier**, **Désactiver** ou **Supprimer** le filtre.

   La colonne **Statut** affiche une icône verte et le mot « Activé ».

1. Cliquez sur le bouton **[!UICONTROL Save]** pour enregistrer la nouvelle politique. &#x200B; Si le bouton n’est pas actif, vérifiez que le nom de la politique est ajouté en cliquant sur l’icône en forme de crayon en regard de **Nouvelle politique**.

1. Pour vérifier votre nouvelle politique, cliquez sur la flèche vers l&#39;arrière pour revenir à l&#39;espace de travail **[!UICONTROL Policies]**.

### Création d’une politique TRIGGER

1. Dans l’espace de travail **[!UICONTROL Policies]**, cliquez sur le bouton **[!UICONTROL Add Policy]**.

   Une nouvelle page s’ouvre pour que vous puissiez renseigner les détails de la politique. &#x200B;

1. Entrez le nom de la règle, par exemple, « Exporter les catégories d&#39;articles ».

1. Cliquez sur le bouton **[!UICONTROL Add Trigger]**.

   La boîte de dialogue **Détails du déclencheur** s’affiche.

1. Saisissez un nom pour le déclencheur, tel que **AC-Policy-Brand**.

1. Sélectionnez le **Type de transport**. **HTTP_HEADER** est actuellement le seul type pris en charge.

1. Cliquez sur le bouton **[!UICONTROL Save]** pour enregistrer le déclencheur.

1. Cliquez sur le bouton **[!UICONTROL Add Filter]**.

   Une boîte de dialogue s’ouvre pour vous permettre d’ajouter des détails de filtre.

1. Ajoutez les détails du filtre. Par exemple :

   1. **Attribut** - Saisissez un attribut de votre catalogue. Par exemple, « part_category ». Ce nom doit correspondre exactement au nom de l’attribut dans votre catalogue.
   1. **Opérateur** - Sélectionnez l’opérateur. Par exemple, **IN**. &#x200B;
   1. **Valeur Source** - Sélectionnez **DÉCLENCHEUR**. &#x200B;
   1. **Valeur** - Saisissez le nom du déclencheur que vous avez créé précédemment (**AC-Policy-Brand**).

   Au moment de la configuration, le filtre référence le déclencheur configuré. Au moment de l’exécution, l’en-tête de la requête API fournit la ou les valeurs évaluées par ce filtre.

1. Cliquez sur le bouton **[!UICONTROL Save]** dans la boîte de dialogue Détails du filtre. &#x200B;

1. Cliquez sur l’icône de menu (...) en regard du filtre que vous avez créé, sélectionnez **Activer**. À partir de là, vous pouvez également **Modifier**, **Désactiver** ou **Supprimer** le filtre.

   La colonne **Statut** affiche une icône verte et le mot « Activé ».

1. Cliquez sur le bouton **[!UICONTROL Save]** pour enregistrer la nouvelle politique. &#x200B; Si le bouton n’est pas actif, vérifiez que le nom de la politique est ajouté en cliquant sur l’icône en forme de crayon en regard de **Nouvelle politique**.

1. Pour vérifier votre nouvelle politique, cliquez sur la flèche vers l&#39;arrière pour revenir à l&#39;espace de travail **[!UICONTROL Policies]**.

La procédure suivante permet de créer la politique qui peut ensuite être liée à une vue de catalogue pour contrôler la visibilité du produit.
