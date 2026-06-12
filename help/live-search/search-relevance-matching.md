---
title: Correspondance de recherche et classement
description: Découvrez comment [!DNL Live Search] priorise les correspondances exactes et proches, les correspondances de même champ et les correspondances entre champs, et comment le classement interagit avec les poids de recherche, le classement intelligent et les règles de marchandisage.
role: Admin, Developer
recommendations: noCatalog
hide: true
autotag-review: '2026-06-12T19:48:33.569Z'
TQID: 'https://experienceleague.adobe.com/v4T99FG9mFhlgbb-xDqR-C1tVvCmHDry5lxhSDaKg-4'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
subfeature_v2:
  - id: faf75e43-5608-48b8-8169-3f8a9b8a5caf
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: d378ca77-2da1-4f39-ad92-1917fe974a38
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: da5950c0f2071f48f163dd02f6c38953804ae152
workflow-type: tm+mt
source-wordcount: 914
ht-degree: 0%

---

# Correspondance de recherche et classement

>[!IMPORTANT]
>
>La fonctionnalité suivante est disponible dans [Private Beta](https://experienceleague.adobe.com/fr/docs/commerce-operations/release/beta).

[!DNL Live Search] classe les résultats afin que les acheteurs voient d’abord les produits les plus pertinents. Le service donne un coup de pouce puissant aux produits dont le texte de catalogue **correspond étroitement** à ce que l’acheteur tape, puis favorise les correspondances où les termes de requête apparaissent ensemble de manière significative et inclut enfin des correspondances plus larges (y compris un comportement qui prend en charge la correspondance de style de saisie automatique).

## Hiérarchisation des correspondances

À haut niveau, la pertinence utilise trois niveaux de force correspondante (en plus des autres facteurs de notation décrits ci-dessous) :

1. **Correspondance exacte et proche de l’expression** — L’expression de recherche complète correspond au texte du catalogue ou à une correspondance proche après une normalisation telle qu’une enchaînement (par exemple, les formulaires au singulier et au pluriel se résolvent sur la même racine). Ces correspondances bénéficient du coup de pouce de pertinence le plus élevé.

1. **Tous les mots dans le même champ** — Chaque mot de la requête apparaît dans un attribut consultable (par exemple, `red` et `pants` dans le produit **nom**). Cette couche reçoit la poussée la plus élevée suivante.

1. **Mots dans différents champs** — Les termes de requête apparaissent dans différents attributs pouvant faire l&#39;objet d&#39;une recherche (par exemple, `red` dans **color** et `pants` dans **name**). Il s’agit de la couche de correspondance la plus large et reçoit le gain de pertinence le plus faible. Elle peut également correspondre à des requêtes partielles utilisées par la saisie semi-automatique, par exemple lorsqu’un acheteur saisit du `red pan` avant de terminer la `pants`. Pour les catalogues allemands, voir [Décomposition (allemand)](#decompounding-german).

### Exemple

Pour une requête telle que `red pants` :

- Les produits avec l’expression exacte **pantalon rouge** (ou une variante proche) se classent **premiers**.
- Les produits où **rouge** et **pantalon** apparaissent dans le **même champ** (par exemple, **nom**) se classent ensuite.
- Suivent les produits dont les termes apparaissent dans **différents champs** (par exemple, **couleur** et **nom**).

### Décomposition (Allemand) {#decompounding-german}

Les catalogues allemands utilisent de nombreux mots composés. Par exemple, **spülbecken** et **spül becken** peuvent se décomposer en jetons tels que **spul** et **beck** (après endiguement), de sorte qu’un acheteur qui recherche **spul becken** peut toujours trouver **Spülbecken**. À ce niveau, les sous-mots décomposés d’un terme composé doivent apparaître dans le même champ. D’autres termes de requête peuvent correspondre dans différents champs.

Cette exigence **AND** filtre les correspondances non pertinentes lorsqu’un seul sous-mot est présent. Par exemple, une recherche de **Brauseschlauch** ne renvoie plus **Schlauchstück** lorsqu’une partie seulement du composé correspond. Une recherche pour **spülbecken** peut toujours correspondre à **spülbeckventil** car le mot plus long contient tous les jetons attendus.

>[!NOTE]
>
>La correspondance exacte et proche des expressions et la correspondance de même champ utilisent les règles décrites ci-dessus sans décomposition.

#### Exemple

Pour une expression de recherche telle que `Brauseschlauch chrom` :

- **Correspondance exacte et proche de l’expression** — Recherche l’expression complète **brauseschlauch chrom** telle qu’elle est tapée, sans décomposition (la terminaison s’applique toujours).
- **Tous les mots dans le même champ** — Recherche **brauseschlauch** et **chrom** dans le **même** attribut consultable, toujours sans décomposition (par exemple, les deux dans **name**).
- **Mots dans différents domaines** — Décompose **Brauseschlauch** en **brause** et **schlauch**. Ces jetons doivent apparaître dans le champ **same** (pas nécessairement sous la forme d’une expression adjacente). **chrom** peut correspondre dans un champ **différent** (par exemple, **brause** et **schlauch** dans **name**, **chrom** dans **color**).

Définissez **Langue** sur **Allemand** dans l’espace de travail [Paramètres](settings.md#language) afin que les règles de décomposition s’appliquent. Validez les requêtes allemandes à forte valeur ajoutée sur un storefront d’évaluation avant d’activer les modifications en production.

La décomposition est basée sur des règles et peut ajouter des cas de périphérie à ce calque. Si un sous-mot est manquant dans le dictionnaire, la segmentation en unités lexicales peut être incomplète et renvoyer des correspondances plus larges que prévu ; par exemple, **gas** manquant dans **gaszähler** peut émettre uniquement **zahl** ou **stat** manquant dans **thermostat**. Le bourgeon peut également produire des racines inattendues (par exemple, **schrauber** bourgeonnant en **schraub** ou **schelle** en **schell**). Adobe met à jour le dictionnaire et les remplacements de flux pour les cas connus à mesure que des problèmes sont identifiés.

## Autres éléments affectant le classement

La pertinence n’est pas déterminée uniquement par la correspondance d’expressions. Plusieurs signaux interagissent :

- Booster à partir de la correspondance **exacte / proche** des expressions
- Amplifier lorsque **tous les termes de la requête** apparaissent dans le champ **même**
- **Classement intelligent** (lorsqu’il est activé), qui associe la pertinence textuelle aux signaux comportementaux, consultez la section [Fonctionnement du classement intelligent](rules-add.md#how-intelligent-ranking-scoring-works)
- **[Poids de la recherche](https://experienceleague.adobe.com/fr/docs/commerce-admin/catalog/catalog/search/search-results)** sur chaque attribut et autres facteurs de pertinence textuelle (par exemple, la fréquence d’apparition des termes et la longueur du nom ou de la description). Dans [!DNL Adobe Commerce] Admin, configurez **Utiliser dans la recherche** et **Poids de la recherche** pour les attributs de produit.
- **[Rechercher des règles de marchandisage](rules.md)** telles que épingler, amplifier et enterrer

Du fait de l’interaction de ces signaux, un produit qui correspond uniquement au niveau le plus large peut parfois se classer au-dessus d’une correspondance d’expressions plus stricte, par exemple lorsque les **poids de recherche** ou la fréquence des termes dans un champ à poids élevé l’emportent sur une correspondance d’expressions plus faible ailleurs.

**Exemple :** si **pantalon rouge** apparaît comme une expression dans **description** avec **poids de recherche = 1**, mais **rouge** et **pants** apparaissent séparément dans **name** et **color** avec **poids de recherche = 10**, l’expression match dans **&#x200B;**&#x200B;peut ne pas l’emporter sur la correspondance de division, en fonction du score global.

Les règles manuelles **pin** et **bury** restent fortes ; les règles **boost** peuvent nécessiter un réglage pour surmonter les nouveaux boosts de phrase et de même champ. Validez les requêtes importantes après avoir modifié les poids ou les règles.

### Poids de recherche 1 et indexation combinée

Les attributs configurés avec le **poids minimal de la recherche** (poids **1**) et le **non** configurés pour des modes de correspondance spéciaux (tels que contains ou starts-with) peuvent être combinés dans l’index de recherche en un seul champ interne (`defaultSearchField`) afin de réduire la surcharge de mappage des champs. Traitez-la comme une surface consultable pour la correspondance **même champ** : les jetons qui arrivent uniquement dans ces champs de faible poids combinés sont évalués ensemble plutôt que comme des champs distincts par attribut. Adobe peut affiner cette optimisation au fil du temps à mesure que la correspondance évolue.

## Rubriques connexes

- [Indexation](indexing.md)
- [Bonnes pratiques](best-practice.md)
- [Ajouter des règles de recherche](rules-add.md)
- [Synonymes](synonyms.md)
