---
title: Règles de marchandisage
description: '[!DNL Adobe Commerce Optimizer] règles de marchandisage associent une logique à des actions pour façonner les résultats de recherche, les listes de produits par défaut et les pages de catégories.'
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et  [!DNL Adobe Commerce Optimizer]  (infrastructure SaaS gérée par Adobe)."
exl-id: f2a9b5e8-d23d-4855-b424-ca6b40e057df
source-git-commit: 8abc0593c166a2dd861cfb78674918de1d0744de
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 0%

---

# Règles de marchandisage

Les règles de marchandisage associent une logique à des actions pour définir la façon dont les produits apparaissent dans **résultats de recherche**, sur **listes de produits par défaut** (**Toutes les listes de produits**) et sur **pages de catégorie** ([règles de catégorie](#category-rules) sont en version bêta). Vous pouvez booster, enterrer, épingler ou masquer des produits et appliquer le **classement intelligent** afin que les annonces reflètent les objectifs de votre entreprise.

Chaque **règle de recherche** comporte trois composants principaux :

- **Conditions** - Exigences basées sur des requêtes qui déclenchent une action lorsque la recherche de l’acheteur correspond.
- **Événements** - Actions qui ont lieu lorsque les conditions sont remplies (classement manuel et événements associés).
- **Détails** - Nom de la règle, période facultative et description.

**Règles de catégorie** utilisez **sélection de catégorie** au lieu des conditions de requête de recherche. Le classement intelligent et le classement manuel fonctionnent de la même manière que pour la recherche, avec les différences répertoriées dans [Créer et gérer des règles](add.md).

Vous pouvez combiner plusieurs conditions et actions pour les règles de recherche et planifier l’activation de n’importe quelle règle pour une période donnée. Vous pouvez également définir une **règle par défaut** (**Toutes les listes de produits**) qui s’applique lorsqu’aucune règle de recherche ou de catégorie plus spécifique ne s’applique.

## Règles de catégorie {#category-rules}

>[!IMPORTANT]
>
>Les règles de catégorie sont en version Beta.

**Règles de catégorie** contrôlez l’ordre des produits sur les **pages de catégorie**. Vous sélectionnez une ou plusieurs catégories, puis appliquez un classement intelligent (par exemple, les plus consultés, en tendance) et des actions manuelles telles que épingler, booster et enterrer. Ils n’utilisent pas les conditions de requête de recherche. Pour connaître les étapes de configuration, les types de règle et la manière dont le classement s’applique à la catégorie par rapport à la recherche, consultez [Création et gestion des règles](add.md).

## Conditions requises

Une simple **règle de recherche** peut avoir une seule condition et un seul événement, tandis qu’une règle complexe peut avoir jusqu’à dix conditions qui déclenchent jusqu’à 25 événements. Les **règles de catégorie** suivent les mêmes limites d’événement pour le classement manuel ; elles n’utilisent pas de conditions de requête.

Les règles peuvent avoir :

- Jusqu’à dix **conditions** (règles de recherche uniquement)
- Jusqu’à 25 **événements**

Le texte de la requête peut contenir :

- Caractères alphanumériques (lettres et chiffres)
- Caractères majuscules ou minuscules. La majuscule est ignorée.

## Opérateurs logiques

Les opérateurs logiques `AND` et `OR` joignent deux conditions et renvoient des résultats différents. Tous les opérateurs logiques utilisés dans une règle avec plusieurs conditions sont identiques. Il n’est pas possible d’utiliser à la fois `AND` et `OR` dans la même règle.

### Faire correspondre les opérateurs

Les opérateurs de correspondance `All` et `Any` déterminent l’opérateur logique utilisé pour joindre plusieurs conditions dans la règle et peuvent être utilisés pour modifier l’opérateur existant.

- `All` - Utilise l’opérateur logique `AND` pour joindre plusieurs conditions. Une règle qui utilise l’opérateur `All` correspondance ne peut avoir qu’une seule condition `Search query is`.
- `Any` - Utilise l’opérateur logique `OR` pour joindre plusieurs conditions.

Lors de la composition d’une règle complexe, il peut être utile de l’écrire avec une mise en retrait pour décrire les conditions, les événements associés, les noms de produit ou les SKU qui sont nécessaires pour renvoyer les résultats que vous souhaitez atteindre. Créez ensuite la règle et testez le résultat.

## Règle par défaut

Vous pouvez définir une règle par défaut (**Toutes les listes de produits**) qui s’applique lorsqu’aucun terme de recherche n’est fourni ou qu’aucune autre règle de recherche ne peut être appliquée. Si vous définissez la règle par défaut sur « Les plus achetés », les requêtes sont définies par défaut sur ce type de classement, sauf si elles sont remplacées par un terme de recherche plus spécifique. Aucun terme de recherche ne peut être défini pour la règle par défaut. Les **règles de catégorie** sont distinctes : elles s’appliquent uniquement aux catégories que vous sélectionnez et ne remplacent pas la règle d’énumération par défaut.

## Ordre de priorité avec plusieurs règles

Les éléments suivants s’appliquent aux **règles de recherche** et à leur interaction pour une recherche donnée. **Les règles de catégorie** s’appliquent par catégorie ; consultez [Création et gestion des règles](add.md#category-rules) pour savoir comment elles s’intègrent aux règles de recherche et aux règles par défaut.

Une seule règle de recherche est appliquée à la fois à un terme de recherche.
Si plusieurs règles s’appliquent à une expression de recherche, toutes ces règles sont appliquées. S’il existe une collision entre deux règles (`rule 1` qui augmente le SKU1 mais `rule 2` masque le même SKU), la dernière règle appliquée (`rule 2`) est prioritaire.

- Les règles sont triées selon l’horodatage « Dernière modification ». La règle la plus récemment modifiée est appliquée en premier, puis les règles plus anciennes, dans l’ordre d’horodatage.
- La condition `query is` est prioritaire sur les autres conditions. Si une règle plus récente contient une condition de `query contains`, mais qu’une règle plus ancienne comporte une condition de `query is`, la règle de `query is` est appliquée.

### Requêtes de storefront

Si une règle active contenant une condition de `query is` correspond à l’expression de recherche, elle est appliquée. S’il existe plusieurs règles de correspondance avec une condition de `query is`, la règle active la plus récemment mise à jour est appliquée.
Dans le cas contraire, la règle active la plus récemment mise à jour est appliquée.

### Prévisualisation des requêtes

La demande effectuée dans [!DNL Adobe Commerce Optimizer] fonctionne légèrement différemment. Lors de la prévisualisation des [!DNL Adobe Commerce Optimizer], toutes les règles sont appliquées, y compris celles expirées et planifiées.

- Si la règle prévisualisée comporte une condition `query is`, elle est appliquée.
- Si la règle en cours de prévisualisation ne comporte pas de condition de `query is` et qu’une règle correspondante active ultérieure avec une condition de `query is` est trouvée, la règle de `query is` est appliquée.
- Si la règle en cours de prévisualisation ne comporte pas de condition de `query is` et qu’aucune autre règle comportant une condition de `query is` n’est trouvée, la règle en cours de prévisualisation est appliquée.
