---
title: Règles de marchandisage
description: '[!DNL Adobe Commerce Optimizer] règles de marchandisage combinent la logique aux actions pour façonner l’expérience d’achat.'
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
exl-id: f2a9b5e8-d23d-4855-b424-ca6b40e057df
source-git-commit: c6725fc524e9d239ccc0f16701e92ad5d2fc7729
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---

# Règles de marchandisage

Les règles de marchandisage font référence à un ensemble de règles qui combinent une logique aux actions pour façonner l’expérience de recherche d’un acheteur dans votre magasin. Vous pouvez utiliser des règles de marchandisage pour booster, enterrer, épingler ou masquer des produits afin d’étalonner les résultats de recherche en temps réel pour soutenir les objectifs de votre entreprise.

Chaque règle comporte trois composants principaux :

- Conditions - Les conditions qui déclenchent une action.
- Événements - Actions qui ont lieu lorsque les conditions sont remplies.
- Détails : nom de la règle, période facultative et description.

Vous pouvez combiner plusieurs conditions et actions et planifier l’activation d’une règle pendant une période donnée. Vous pouvez également définir une règle par défaut qui s’applique même si aucun terme de recherche n’est défini.

## Conditions requises

Une règle de recherche simple peut avoir une seule condition et un seul événement, tandis qu’une règle complexe peut avoir jusqu’à dix conditions qui déclenchent jusqu’à 25 événements.
Les règles peuvent avoir :

- Jusqu’à dix conditions
- Jusqu’à 25 événements

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

Vous pouvez définir une règle par défaut qui s’applique lorsqu’aucun terme de recherche n’est fourni ou qu’aucune autre règle de recherche ne peut être appliquée. Si vous définissez la règle par défaut sur « Les plus achetés », toutes les requêtes seront classées par défaut selon ce type de classement, sauf si elles sont super-cédées par un terme de recherche plus spécifique. Aucun terme de recherche ne peut être défini pour la règle par défaut.

## Ordre de priorité avec plusieurs règles

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
