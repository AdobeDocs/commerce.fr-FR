---
title: Présentation des événements
description: Découvrez les événements que  [!DNL Adobe Commerce Optimizer]  utilise pour améliorer la recherche et les recommandations.
role: Admin, Developer
recommendations: noCatalog
source-git-commit: 356b10704c9e7c7329d3e9c0e10baa15d5142ec0
workflow-type: tm+mt
source-wordcount: '1398'
ht-degree: 0%

---

# Événements

Les événements sont un outil essentiel pour améliorer l’expérience d’achat et stimuler les conversions en exploitant les informations sur les données en temps réel.

[!DNL Adobe Commerce Optimizer] déploie automatiquement les événements storefront sur votre site. Ces événements capturent des données à partir des interactions des acheteurs sur votre site. Ces données anonymisées alimentent [recommandations](../../manage-results/recommendation-performance.md), [découverte de produits](../../manage-results/search-performance.md) et [mesures de succès](../../manage-results/success-metrics.md).

>[!NOTE]
>
>La collecte de données n’inclut pas les informations d’identification personnelle (PII). Tous les identifiants d’utilisateur, tels que les ID de cookie et les adresses IP, sont strictement anonymisés. [En savoir plus](https://www.adobe.com/privacy/experience-cloud.html).

La page **Événements** vous permet d’observer les données d’événement storefront collectées. Disposer d’une vue dans la collecte de données d’événement permet aux commerçants de vérifier qu’ils ont correctement implémenté les événements du storefront et que ceux-ci sont capturés avec succès. Les commerçants peuvent utiliser cette page pour identifier les problèmes potentiels et prendre des mesures pour résoudre les problèmes d’événement.

## Nombre d’événements

L’onglet **Nombre d’événements** effectue le suivi des interactions des acheteurs, telles que les recherches, les clics et les achats, afin de vous aider à analyser les tendances et à améliorer l’expérience d’achat.

![Nombre d’événements](../../assets/event-counts.png){zoomable="yes"}

| Champ | Description |
|---|---|
| **Période** | Spécifions la période pour afficher un sous-ensemble spécifique de données. |
| **Événements Storefront par heure** | Affiche un graphique indiquant le nombre d’événements déclenchés sur votre storefront. |
| **Total des événements storefront** | Tableau filtrable qui affiche les détails de tous les événements déclenchés sur votre storefront. |

## Vérification de l&#39;intégrité

L’onglet **Sanity Check** donne des informations sur l’intégrité de chaque événement comportemental, ce qui permet d’assurer une collecte de données et une fonctionnalité précises. &#x200B;

![Contrôle de l’intégrité](../../assets/sanity-check.png){zoomable="yes"}

| Champ | Description |
|---|---|
| **Période** | Spécifions la période pour afficher un sous-ensemble spécifique de données. |
| **Découverte de produits** | Affiche les événements requis pour personnaliser les résultats de la recherche de produit. La colonne **Status** indique si les événements ont été reçus. |
| **Recommandations** | Affiche les événements requis pour personnaliser les recommandations de produits. La colonne **Status** indique si les événements ont été reçus. |

Les sections suivantes décrivent les détails des événements pour [découverte de produit](#product-discovery) et [recommandations](#recommendations).

### Découverte de produits

La découverte de produits utilise des événements pour alimenter les algorithmes de recherche tels que « Les plus consultés » et « Affiché ceci, consulté cela ».

Ce tableau décrit les événements utilisés par la découverte de produits [stratégies de classement](../../merchandising/rules/add.md#intelligent-ranking).

| Stratégie de classement | Événements | Page |
| --- | --- | --- |
| Les plus consultés | `page-view`<br>`product-view` | Page des détails du produit |
| Les plus achetés | `page-view`<br>`place-order` | Panier/Passage en caisse |
| Les plus ajoutés au panier | `page-view`<br>`add-to-cart` | Page des détails du produit<br>page de liste des produits<br>panier<br>liste de souhaits |
| A consulté ceci, a consulté cela | `page-view`<br>`product-view` | Page des détails du produit |

### Événements de tableau de bord requis

Certains événements sont nécessaires pour renseigner le tableau de bord des performances de recherche [search](../../manage-results/search-performance.md)

| Zone du tableau de bord | Événements | Joindre le champ |
| ------------------- | ------------- | ---------- |
| Recherches uniques | `page-view`, `search-request-sent`, `search-response-received` | `searchRequestId` |
| Aucun résultat de recherche | `page-view`, `search-request-sent`, `search-response-received` | `searchRequestId` |

### Recommendations

Les recommandations utilisent deux types de données :

- **Comportemental** - Données provenant de l’engagement d’un acheteur sur votre site, telles que les consultations de produits, les articles ajoutés au panier et les achats.
- **Catalogue** - Métadonnées du produit, telles que le nom, le prix, la disponibilité, etc.

Adobe Sensei agrège les données comportementales et de catalogue, créant des recommandations pour chaque type de recommandation. Le service Recommendations déploie ensuite ces recommandations sur votre storefront sous la forme d’un widget qui contient les _éléments_ de produit recommandés.

Certains types de recommandations utilisent les données comportementales de vos clients pour entraîner des modèles de machine learning afin de créer des recommandations personnalisées. D’autres types de recommandations utilisent uniquement les données de catalogue et n’utilisent aucune donnée comportementale. Si vous souhaitez commencer rapidement à utiliser Recommendations sur votre site, vous pouvez utiliser le type de recommandation `More like this`.

#### Démarrage à froid

Quand pouvez-vous commencer à utiliser des types de recommandations qui utilisent des données comportementales ? Ça dépend. C’est ce qu’on appelle le problème _Cold Start_.

Le problème du _démarrage à froid_ fait référence au temps nécessaire pour qu’un modèle s’entraîne et devienne efficace. Pour les recommandations, cela signifie qu’il faut attendre qu’Adobe Sensei collecte suffisamment de données pour entraîner ses modèles de machine learning avant de déployer des unités de recommandation sur votre site. Plus les modèles contiennent de données, plus les recommandations sont précises et utiles. Étant donné que la collecte de données se produit sur un site en ligne, il est préférable de démarrer ce processus rapidement.

Le tableau suivant fournit des instructions générales sur le temps nécessaire à la collecte de suffisamment de données pour chaque type de recommandation :

| Type de recommandation | Durée de l’apprentissage | Remarques |
|---|---|---|
| Basé sur la popularité (`Most viewed`, `Most purchased`, `Most added to cart`) | Variable | Dépend du volume d’événements : les vues sont les plus courantes et apprennent donc plus rapidement ; ajoute ensuite au panier, puis achète. |
| `Viewed this, viewed that` | Nécessite une formation supplémentaire | Le volume des consultations de produits est récemment élevé |
| `Viewed this, bought that`, `Bought this, bought that` | Requiert le plus de formation | Les événements d’achat sont les événements les plus rares sur un site commercial, en particulier par rapport aux consultations de produits |
| `Trending` | Nécessite trois jours de données pour établir une base de popularité | Les tendances sont une mesure de l’élan récent de la popularité d’un produit par rapport à sa propre base de popularité. Le score de tendance d’un produit est calculé à l’aide d’un ensemble de premier plan (popularité récente sur 24 heures) et d’un ensemble d’arrière-plan (popularité de base sur 72 heures). Si la popularité d’un élément augmente considérablement au cours d’une période de 24 heures par rapport à sa popularité de base, il obtient un score de tendance élevé. Chaque produit a ce score, et les articles ayant le score le plus élevé à tout moment comprennent l&#39;ensemble des produits les plus en tendance. |

Autres variables pouvant avoir une incidence sur le temps nécessaire à l’entraînement :

- Un trafic plus important contribue à un apprentissage plus rapide
- Certains types de recommandations s’entraînent plus rapidement que d’autres
- [!DNL Adobe Commerce Optimizer] recalcule les données comportementales toutes les quatre heures. Les recommandations deviennent plus précises au fur et à mesure qu’elles sont utilisées sur votre site.

Pour visualiser plus facilement la progression de l’entraînement pour chaque type de recommandation, la page [Créer une recommandation](../../merchandising/recommendations/create.md#readiness-indicators) affiche des indicateurs de préparation.

Pendant que les données sont collectées sur votre site en ligne et que les modèles de machine learning sont en cours d’entraînement, vous pouvez terminer d’autres tâches de test et de configuration nécessaires à la configuration des recommandations. Lorsque vous aurez terminé ce travail, les modèles disposeront de suffisamment de données pour créer des recommandations utiles, ce qui vous permettra de les déployer sur votre storefront.

Si votre site n’obtient pas suffisamment de trafic (vues, achats, tendances) pour la plupart des SKU de produit, il se peut qu’il n’y ait pas suffisamment de données pour terminer le processus d’apprentissage. Ainsi, l’indicateur de préparation de l’espace de travail Recommendations peut sembler bloqué. Les indicateurs de préparation sont destinés à fournir aux commerçants un autre point de données pour choisir le type de recommandations le mieux adapté à leur magasin. Les chiffres sont indicatifs et peuvent ne jamais atteindre 100 %. [En savoir plus](../../merchandising/recommendations/create.md#readiness-indicators) sur les indicateurs de préparation.

#### Recommandations de sauvegarde

Si les données d’entrée sont insuffisantes pour fournir tous les éléments de recommandation demandés dans une unité, [!DNL Adobe Commerce Optimizer] fournit des recommandations de sauvegarde pour renseigner les unités de recommandation. Par exemple, si vous déployez le type de recommandation `Recommended for you` sur votre page d’accueil, un nouvel acheteur sur votre site n’a pas généré suffisamment de données comportementales pour recommander des produits personnalisés avec précision. Dans ce cas, [!DNL Adobe Commerce Optimizer] affiche les articles en fonction du type de recommandation `Most viewed` à cet acheteur.

Si la collecte des données d’entrée est insuffisante, les types de recommandation suivants reviennent à `Most viewed` type de recommandation :

- `Recommended for you`
- `Viewed this, viewed that`
- `Viewed this, bought that`
- `Bought this, bought that`
- `Trending`
- `Conversion (view to purchase)`
- `Conversion (view to cart)`

#### Événements spécifiques aux recommandations

Le tableau suivant répertorie les événements qui sont déclenchés lorsque les acheteurs interagissent avec les unités de recommandation sur le storefront. Les données d’événement collectées permettent aux [mesures](../../manage-results/recommendation-performance.md) d’analyser les performances de vos recommandations.

| Événement | Description |
| --- | --- |
| `impression-render` | Envoyé lorsque l’unité de recommandation est rendue sur la page. Si une page comporte deux unités de recommandation (achat-achat, affichage), deux événements `impression-render` sont envoyés. Cet événement est utilisé pour effectuer le suivi de la mesure pour les impressions. |
| `rec-add-to-cart-click` | L’acheteur clique sur le bouton **Ajouter au panier** pour un article dans l’unité de recommandation. |
| `rec-click` | L’acheteur clique sur un produit dans l’unité de recommandation. |
| `view` | Envoyé lorsque l’unité de recommandation devient visible à au moins 50 %, par exemple en faisant défiler la page vers le bas. Par exemple, si une unité de recommandation comporte deux lignes, un événement `view` est envoyé lorsqu’une ligne plus un pixel de la deuxième ligne devient visible pour l’acheteur. Si l’acheteur fait défiler la page de haut en bas plusieurs fois, l’événement `view` est envoyé autant de fois qu’il voit à nouveau l’ensemble de l’unité de recommandation sur la page. |

#### Événements de tableau de bord requis

Les événements suivants sont requis pour renseigner le tableau de bord [Performances Recommendations](../../manage-results/recommendation-performance.md)

| Colonne du tableau de bord | Événements | Joindre le champ |
| ---------------- | --------- | ----------- |
| Impressions | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render` | `unitId` |
| Vues | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render`, `recs-unit-view` | `unitId` |
| Clics | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-item-click`, `recs-add-to-cart-click` | `unitId` |
| Chiffre d’affaires | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-item-click`, `recs-add-to-cart-click`, `place-order` | `unitId`, `sku`, `parentSku` |
| Revenus LT | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-item-click`, `recs-add-to-cart-click`, `place-order` | `unitId`, `sku`, `parentSku` |
| CTR | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render`, `recs-item-click`, `recs-add-to-cart-click` | `unitId`, `sku`, `parentSku` |
| vCTR | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render`, `recs-unit-view`, `recs-item-click`, `recs-add-to-cart-click` | `unitId`, `sku`, `parentSku` |

Les événements suivants ne sont pas spécifiques à Recommendations, mais sont nécessaires pour qu’Adobe Sensei interprète correctement les données de l’acheteur :

- `view`
- `add-to-cart`
- `place-order`

#### Type de recommandation

Ce tableau décrit les événements utilisés par chaque type de recommandation.

| Type de recommandation | Événements | Page |
| --- | --- | --- |
| Les plus consultés | `page-view`<br>`product-view` | Page des détails du produit |
| Les plus achetés | `page-view`<br>`place-order` | Panier/Passage en caisse |
| Les plus ajoutés au panier | `page-view`<br>`add-to-cart` | Page des détails du produit<br>page de liste des produits<br>panier<br>liste de souhaits |
| A consulté ceci, a consulté cela | `page-view`<br>`product-view` | Page des détails du produit |
| A vu ceci, a acheté cela | `page-view`<br>`product-view` | Page des détails du produit<br>Panier/Passage en caisse |
| J&#39;ai acheté ça, acheté ça | `page-view`<br>`product-view` | Page des détails du produit |
| En Tendance | `page-view`<br>`product-view` | Page des détails du produit |
| Conversion : afficher pour acheter | `page-view`<br>`product-view` | Page des détails du produit |
| Conversion : afficher pour acheter | `page-view`<br>`place-order` | Panier/Passage en caisse |
| Conversion : afficher au panier | `page-view`<br>`product-view` | Page des détails du produit |
| Conversion : afficher au panier | `page-view`<br>`add-to-cart` | Page des détails du produit<br>Page de liste des produits<br>Panier<br>Liste de souhaits |

## Support technique

Si vous constatez des incohérences dans les données ou si les recommandations et les résultats de recherche ne fonctionnent pas comme prévu, [envoyez un ticket d’assistance](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide).
