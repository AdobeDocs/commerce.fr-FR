---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 0%
---
Les règles de marchandisage associent une logique à des actions pour déterminer comment les produits apparaissent dans les **résultats de recherche**, dans les **listes de produits par défaut** via la **règle de recherche par défaut** et sur les **pages de catégorie**. Vous pouvez booster, enterrer, épingler ou masquer des produits et appliquer un **classement intelligent** afin que les annonces reflètent les objectifs de votre entreprise.

Chaque **règle de recherche** comporte trois composants principaux :

- **Conditions** - Exigences basées sur des requêtes qui déclenchent une action lorsque la recherche de l’acheteur correspond.
- **Événements** - Actions qui ont lieu lorsque les conditions sont remplies (classement manuel et événements associés).
- **Détails** - Nom de la règle, période facultative et description.

**Les règles de catégorie** utilisent la **sélection de catégorie** au lieu des conditions de requête de recherche ; le classement intelligent et le classement manuel fonctionnent de la même manière que pour la recherche, avec des différences signalées dans [Créer et gérer des règles](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add).

Vous pouvez combiner plusieurs conditions et actions pour les règles de recherche et planifier l’activation de n’importe quelle règle pour une période donnée. Vous pouvez également définir une **règle de recherche par défaut** qui s’applique lorsqu’aucune règle de recherche ou de catégorie plus spécifique ne s’applique.

## Règles de catégorie {#category-rules}

**Les règles de catégorie** contrôlent la commande des produits sur les **pages de catégorie**. Vous sélectionnez une ou plusieurs catégories, puis appliquez un classement intelligent (par exemple, les plus consultés, en tendance) et des actions manuelles telles que épingler, booster et enterrer. Ils n’utilisent pas les conditions de requête de recherche. Pour connaître les étapes de configuration, les types de règle et la manière dont le classement s&#39;applique à la catégorie par rapport à la recherche, consultez [Créer et gérer des règles](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add).

## Conditions requises

Une simple **règle de recherche** peut avoir une seule condition et un seul événement, tandis qu’une règle complexe peut avoir jusqu’à dix conditions qui déclenchent jusqu’à 25 événements. **Les règles de catégorie** suivent les mêmes limites d&#39;événement pour le classement manuel ; elles n&#39;utilisent pas de conditions de requête.

Les règles peuvent avoir :

- Jusqu’à dix **conditions** (règles de recherche uniquement)
- Jusqu’à 25 **événements**

Le texte de la requête peut contenir :

- Caractères alphanumériques (lettres et chiffres)
- Caractères majuscules ou minuscules. La majuscule est ignorée.

## Opérateurs logiques

Les opérateurs logiques `AND` et `OR` réunissent deux conditions et renvoient des résultats différents. Tous les opérateurs logiques utilisés dans une règle avec plusieurs conditions sont identiques. Il n&#39;est pas possible d&#39;utiliser à la fois `AND` et `OR` dans la même règle.

### Faire correspondre les opérateurs

Les opérateurs Correspondance `All` et `Any` déterminent l’opérateur logique utilisé pour joindre plusieurs conditions dans la règle et peuvent être utilisés pour modifier l’opérateur existant.

- `All` : utilise l&#39;opérateur logique `AND` pour joindre plusieurs conditions. Une règle qui utilise l’opérateur de correspondance `All` ne peut avoir qu’une seule condition `Search query is`.
- `Any` : utilise l&#39;opérateur logique `OR` pour joindre plusieurs conditions.

Lors de la composition d’une règle complexe, il peut être utile de l’écrire avec une mise en retrait pour décrire les conditions, les événements associés, les noms de produit ou les SKU qui sont nécessaires pour renvoyer les résultats que vous souhaitez atteindre. Créez ensuite la règle et testez le résultat.

## Règle par défaut

Vous pouvez définir une **règle de recherche par défaut** qui s’applique lorsqu’aucun terme de recherche n’est fourni ou qu’aucune autre règle de recherche ne peut être appliquée. Si vous définissez la règle par défaut sur « Les plus achetés », les requêtes sont définies par défaut sur ce type de classement, sauf si elles sont remplacées par un terme de recherche plus spécifique. Aucun terme de recherche ne peut être défini pour la règle par défaut. **Les règles de catégorie** sont distinctes : elles s&#39;appliquent uniquement aux catégories que vous sélectionnez et ne remplacent pas la règle de liste par défaut.

## Ordre de priorité avec plusieurs règles

Les éléments suivants s’appliquent aux **règles de recherche** et à leur interaction pour une recherche donnée. **Les règles de catégorie** s’appliquent par catégorie ; consultez [Créer et gérer des règles](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add) pour savoir comment elles s’intègrent aux règles de recherche et aux règles par défaut.

Une seule règle de recherche est appliquée à la fois à un terme de recherche.
Si plusieurs règles s’appliquent à une expression de recherche, toutes ces règles sont appliquées. S’il existe une collision entre deux règles—`rule 1` qui amplifie le SKU1 mais que `rule 2` masque le même SKU—, la dernière règle appliquée (`rule 2`) est prioritaire.

- Les règles sont triées selon l’horodatage « Dernière modification ». La règle la plus récemment modifiée est appliquée en premier, puis les règles plus anciennes, dans l’ordre d’horodatage.
- La condition `query is` est prioritaire sur les autres conditions. Si une nouvelle règle contient une condition `query contains`, mais qu’une ancienne règle comporte une condition `query is`, la règle `query is` est appliquée.

### Requêtes de storefront

Si une règle active contenant une condition `query is` correspond à l’expression de recherche, elle est appliquée. S’il existe plusieurs règles correspondantes avec une condition `query is`, la règle active la plus récemment mise à jour est appliquée.
Dans le cas contraire, la règle active la plus récemment mise à jour est appliquée.

### Prévisualisation des requêtes

Les requêtes effectuées dans la prévisualisation fonctionnent légèrement différemment. Lors de la prévisualisation, toutes les règles sont appliquées, y compris celles expirées et planifiées.

- Si la règle prévisualisée comporte une condition `query is`, elle est appliquée.
- Si la règle en cours de prévisualisation ne comporte pas de condition `query is` et qu’une règle correspondante active suivante avec une condition `query is` est trouvée, la règle `query is` est appliquée.
- Si la règle en cours de prévisualisation ne comporte pas de condition `query is` et qu’aucune autre règle comportant une condition `query is` n’est trouvée, la règle en cours de prévisualisation est appliquée.
