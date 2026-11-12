---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 0%
---
>[!IMPORTANT]
>
>La fonctionnalité suivante est disponible dans [Private Beta](https://experienceleague.adobe.com/en/docs/commerce-operations/release/beta).

Les services de marchandisage avec le modèle de données de catalogue composable (CCDM) classent les résultats afin que les acheteurs voient d’abord les produits les plus pertinents. Le service booste les produits dont le texte de catalogue **correspond étroitement** à la requête de l’acheteur, puis favorise les correspondances dans lesquelles les termes apparaissent ensemble et inclut enfin des correspondances plus larges.

## Hiérarchisation des correspondances

La pertinence utilise trois niveaux de force correspondant (en plus des autres facteurs de notation décrits ci-dessous) :

1. **Correspondance exacte et proche de l&#39;expression** — L&#39;expression de recherche complète correspond au texte du catalogue, ou à une correspondance proche après normalisation, telle qu&#39;une expression de flux (par exemple, les formulaires au singulier et au pluriel sont résolus à la même racine). Ces correspondances bénéficient du coup de pouce de pertinence le plus élevé.

1. **Tous les mots dans le même champ** — Chaque mot de requête apparaît dans un attribut consultable (par exemple, `red` et `pants` dans le produit **name**). Cette couche reçoit la poussée la plus élevée suivante.

1. **Mots dans différents champs** — Les termes de requête apparaissent dans différents attributs pouvant faire l&#39;objet de recherches (par exemple, `red` dans **color** et `pants` dans **name**). Cette couche de correspondance est la plus large et reçoit le gain de pertinence le plus faible. Elle peut également correspondre à des requêtes partielles utilisées par la saisie automatique, par exemple lorsqu’un acheteur saisit `red pan` avant de terminer `pants`. Pour les catalogues allemands, voir [Décomposition (allemand)](#decompounding-german).

### Exemple

Pour une requête telle que `red pants` :

- Les produits avec l’expression exacte **pantalon rouge** (ou une variante proche) se classent **en premier**.
- Les produits pour lesquels **rouge** et **pantalons** apparaissent dans le **même champ** (par exemple, **nom**) se classent ensuite.
- Les produits où les termes apparaissent dans **différents champs** (par exemple, **color** et **name**) suivent.

### Décomposition (Allemand) {#decompounding-german}

Les catalogues allemands utilisent de nombreux mots composés. Par exemple, **spülbecken** et **spül becken** peuvent se décomposer en jetons tels que **spul** et **beck** (après la diffusion), de sorte qu’un acheteur qui recherche **spul becken** peut toujours trouver **Spülbecken**. À ce niveau, les sous-mots décomposés d’un terme composé doivent apparaître dans le même champ. D’autres termes de requête peuvent correspondre dans différents champs.

Cette exigence **AND** filtre les correspondances non pertinentes où un seul sous-mot est présent. Par exemple, une recherche sur **Brauseschlauch** ne renvoie plus **Schlauchstück** lorsqu’une partie seulement du composé correspond. Une recherche de **spülbecken** peut toujours correspondre à **spülbeckventil**, car le mot le plus long contient tous les jetons attendus.

>[!NOTE]
>
>La correspondance exacte et proche des expressions et la correspondance de même champ utilisent les règles décrites ci-dessus sans décomposition.

#### Exemple

Pour une expression de recherche telle que `Brauseschlauch chrom` :

- **Correspondance exacte et proche de l&#39;expression** — Recherche l&#39;expression complète **brauseschlauch chrom** telle qu&#39;elle est tapée, sans décomposition (la terminaison s&#39;applique toujours).
- **Tous les mots dans le même champ** — Recherche **brauseschlauch** et **chrom** dans le **même** attribut consultable, toujours sans décomposition (par exemple, les deux dans **name**).
- **Mots dans différents champs** — Décompose **Brauseschlauch** en **brause** et **schlauch**. Ces jetons doivent apparaître dans le champ **same** (pas nécessairement sous la forme d’une expression adjacente). **chrom** peut correspondre dans un champ **différent** (par exemple, **brause** et **schlauch** dans **name**, **chrom** dans **color**).

Définissez **Language** sur **Allemand** dans l’onglet [Langue](../settings.md#language) dans [Paramètres](../settings.md) afin que les règles de décomposition s’appliquent. Validez les requêtes allemandes à forte valeur ajoutée sur un storefront d’évaluation avant d’activer les modifications en production.

La décomposition est basée sur des règles et peut ajouter des cas de périphérie à ce calque. Si un sous-mot est manquant dans le dictionnaire, la segmentation en unités lexicales est incomplète et renvoie des correspondances plus larges que prévu ; par exemple, **gas** manquant dans **gaszähler** émet uniquement **zahl**, ou **stat** manquant dans **thermostat**. L&#39;écouvillon peut également produire des racines inattendues (par exemple, **schrauber** issue de **schraub** ou **schelle** à **schell**). Adobe met à jour le dictionnaire et les remplacements de flux pour les cas connus à mesure que des problèmes sont identifiés.

## Autres éléments affectant le classement

La correspondance des expressions seule ne détermine pas la pertinence. Plusieurs signaux interagissent :

- Booster à partir de **exact / proche** correspondance d&#39;expressions
- Amplifier lorsque **tous les termes de la requête** apparaissent dans le champ **même**
- **Classement intelligent** (lorsqu’il est activé), qui associe la pertinence textuelle aux signaux comportementaux ; voir [Fonctionnement du classement intelligent](../merchandising/rules/add.md#how-intelligent-ranking-scoring-works-search)
- **[Poids de la recherche](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search-results)** sur chaque attribut et autres facteurs de pertinence textuelle (par exemple, la fréquence d’apparition des termes dans le nom ou la longueur de la description). Dans *Paramètres*, configurez les attributs qui participent à la recherche par mot-clé et leurs **[poids de recherche par mot-clé](../settings.md)** relatifs.
- **[Règles de marchandisage](../merchandising/rules/overview.md)** telles que l’épinglage, l’amplification et l’enfouissement

Comme les signaux interagissent, une correspondance large se classe parfois au-dessus d&#39;une correspondance d&#39;expression plus stricte lorsque **le poids de la recherche** ou la fréquence des termes l&#39;emporte sur une correspondance d&#39;expression plus faible.

**Exemple :** Si **pantalon rouge** apparaît dans **description** avec **poids de recherche = 1**, mais que **rouge** et **pantalon** apparaissent séparément dans **name** et **color** avec **poids de recherche = 10**, la correspondance de partage l’emporte sur la correspondance d’expression.

Les règles **pin** et **bury** manuelles restent fortes ; les règles **boost** peuvent nécessiter un réglage pour surmonter les nouveaux boosts d’expression et de même champ. Validez les requêtes importantes après avoir modifié les poids ou les règles.

### Poids de recherche 1 et indexation combinée

Les attributs avec **un poids de recherche minimal** (poids **1**) et aucun mode de correspondance spécial se combinent en un seul champ interne (`defaultSearchField`) afin de réduire la surcharge de mappage. Traiter cette surface comme une surface consultable pour **correspondance de même champ** : les jetons qui arrivent uniquement dans ces champs de faible poids combinés sont évalués ensemble plutôt que comme des champs distincts par attribut. Adobe peut affiner cette optimisation au fil du temps à mesure que la correspondance évolue.

## Rubriques connexes

- [Paramètres](../settings.md)
- [Performances de recherche](search-performance.md)
- [Règles de marchandisage - Aperçu](../merchandising/rules/overview.md)
- [Ajouter des règles de recherche](../merchandising/rules/add.md)
- [Présentation des synonymes](../merchandising/synonyms/overview.md)
