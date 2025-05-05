---
title: Collecter des données
description: Découvrez comment les événements collectent des données pour  [!DNL Product Recommendations].
feature: Services, Recommendations, Eventing
exl-id: 0d5317e3-c049-4fcd-a8e4-228668d89386
source-git-commit: 94d2a9911ab10d164d75779d1f310e5bdf2aea74
workflow-type: tm+mt
source-wordcount: '1360'
ht-degree: 0%

---

# Collecter des données

Lorsque vous installez et configurez des fonctions Adobe Commerce SaaS telles que [[!DNL Product Recommendations]](install-configure.md) ou [[!DNL Live Search]](../live-search/install.md), les modules déploient la collecte de données comportementales sur votre storefront. Ce mécanisme collecte des données comportementales anonymisées de vos clients et alimente [!DNL Product Recommendations]. Par exemple, l’événement `view` est utilisé pour calculer le type de recommandation `Viewed this, viewed that` et l’événement `place-order` est utilisé pour calculer le type de recommandation `Bought this, bought that`.

>[!NOTE]
>
>La collecte de données à des fins de [!DNL Product Recommendations] n’inclut pas les informations d’identification personnelle (PII). Tous les identifiants d’utilisateur, tels que les ID de cookie et les adresses IP, sont strictement anonymisés. En savoir [plus](https://www.adobe.com/privacy/experience-cloud.html).

## Clients du secteur de la santé

Si vous êtes un client du secteur de la santé et que vous avez installé l’extension [Data Services HIPAA](../data-connection/hipaa-readiness.md#installation), qui fait partie de l’extension [Data Connection](../data-connection/overview.md), les données d’événement de storefront utilisées par [!DNL Product Recommendations] ne sont plus capturées. En effet, les données d’événement de storefront sont générées côté client. Pour continuer à capturer et à envoyer des données d’événement de storefront, réactivez la collecte d’événements pour [!DNL Product Recommendations]. Voir [configuration générale](https://experienceleague.adobe.com/en/docs/commerce-admin/config/general/general.html#data-services) pour en savoir plus.

## Types de données et événements

Il existe deux types de données utilisées dans les recommandations de produits :

- **Comportemental** - Données provenant de l’engagement d’un acheteur sur votre site, telles que les consultations de produits, les articles ajoutés au panier et les achats.
- **Catalogue** - Métadonnées du produit, telles que le nom, le prix, la disponibilité, etc.

Lorsque vous installez le module `magento/product-recommendations`, Adobe Sensei agrège les données comportementales et de catalogue, créant des recommandations de produits pour chaque type de recommandation. Le service de recommandations de produits déploie ensuite ces recommandations sur votre storefront sous la forme d’un widget qui contient les _éléments_ de produit recommandés.

Certains types de recommandations utilisent les données comportementales de vos clients pour entraîner des modèles de machine learning afin de créer des recommandations personnalisées. D’autres types de recommandations utilisent uniquement les données de catalogue et n’utilisent aucune donnée comportementale. Si vous souhaitez commencer rapidement à utiliser les recommandations de produits sur votre site, vous pouvez utiliser les types de recommandations de catalogue uniquement suivants :

- `More like this`
- `Visual similarity`

### Démarrage à froid

Quand pouvez-vous commencer à utiliser des types de recommandations qui utilisent des données comportementales ? Ça dépend. C’est ce qu’on appelle le problème _Cold Start_.

Le problème du _démarrage à froid_ fait référence au temps nécessaire pour qu’un modèle s’entraîne et devienne efficace. Pour les recommandations de produits, cela signifie attendre qu’Adobe Sensei collecte suffisamment de données pour entraîner ses modèles de machine learning avant de déployer des unités de recommandation sur votre site. Plus les modèles contiennent de données, plus les recommandations sont précises et utiles. Comme la collecte de données se produit sur un site en ligne, il est préférable de démarrer ce processus rapidement en installant et en configurant le module `magento/production-recommendations`.

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
- Adobe Commerce recalcule les données comportementales toutes les quatre heures. Les recommandations deviennent plus précises au fur et à mesure qu’elles sont utilisées sur votre site.

Pour visualiser plus facilement la progression de l’entraînement pour chaque type de recommandation, la page [Créer une recommandation](create.md#readiness-indicators) affiche des indicateurs de préparation.

Pendant que les données sont collectées sur votre site en ligne et que les modèles de machine learning sont en cours d’entraînement, vous pouvez terminer d’autres tâches de test et de configuration nécessaires à la configuration des recommandations. Lorsque vous aurez terminé ce travail, les modèles disposeront de suffisamment de données pour créer des recommandations utiles, ce qui vous permettra de les déployer sur votre storefront.

Si votre site n’obtient pas suffisamment de trafic (vues, achats, tendances) pour la plupart des SKU de produit, il se peut qu’il n’y ait pas suffisamment de données pour terminer le processus d’apprentissage. L’indicateur de préparation dans l’administrateur peut alors sembler bloqué. Les indicateurs de préparation sont destinés à fournir aux commerçants un autre point de données pour choisir le type de recommandations le mieux adapté à leur magasin. Les chiffres sont indicatifs et peuvent ne jamais atteindre 100 %. [En savoir plus](create.md#readiness-indicators) sur les indicateurs de préparation.

### Recommandations de sauvegarde {#backuprecs}

Si les données d’entrée sont insuffisantes pour fournir tous les éléments de recommandation demandés dans une unité, Adobe Commerce fournit des recommandations de sauvegarde pour renseigner les unités de recommandation. Par exemple, si vous déployez le type de recommandation `Recommended for you` sur votre page d’accueil, un nouvel acheteur sur votre site n’a pas généré suffisamment de données comportementales pour recommander des produits personnalisés avec précision. Dans ce cas, Adobe Commerce propose à cet acheteur des articles basés sur le type de recommandation `Most viewed`.

Si la collecte des données d’entrée est insuffisante, les types de recommandation suivants reviennent à `Most viewed` type de recommandation :

- `Recommended for you`
- `Viewed this, viewed that`
- `Viewed this, bought that`
- `Bought this, bought that`
- `Trending`
- `Conversion (view to purchase)`
- `Conversion (view to cart)`

### Événements

Le [collecteur d’événements du storefront Adobe Commerce](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/#quick-start) répertorie tous les événements déployés sur votre storefront. Cette liste contient un sous-ensemble d’événements spécifiques à [!DNL Product Recommendations]. Ces événements collectent des données lorsque les acheteurs interagissent avec les unités de recommandation sur le storefront et alimentent les mesures afin d’analyser la performance de vos recommandations.

| Événement | Description |
| --- | --- |
| `impression-render` | Envoyé lorsque l’unité de recommandation est rendue sur la page. Si une page comporte deux unités de recommandation (achat-achat, affichage), deux événements `impression-render` sont envoyés. Cet événement est utilisé pour effectuer le suivi de la mesure pour les impressions. |
| `rec-add-to-cart-click` | L’acheteur clique sur le bouton **Ajouter au panier** pour un article dans l’unité de recommandation. |
| `rec-click` | L’acheteur clique sur un produit dans l’unité de recommandation. |
| `view` | Envoyé lorsque l’unité de recommandation devient visible à au moins 50 %, par exemple en faisant défiler la page vers le bas. Par exemple, si une unité de recommandation comporte deux lignes, un événement `view` est envoyé lorsqu’une ligne plus un pixel de la deuxième ligne devient visible pour l’acheteur. Si l’acheteur fait défiler la page de haut en bas plusieurs fois, l’événement `view` est envoyé autant de fois qu’il voit à nouveau l’ensemble de l’unité de recommandation sur la page. |

>[!NOTE]
>
>Les mesures de recommandations de produits sont optimisées pour les storefronts Luma. Si votre storefront est implémenté avec PWA Studio, consultez la documentation de [PWA](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/). Si vous utilisez une technologie frontale personnalisée, telle que React ou Vue JS, découvrez comment intégrer [Product Recommendations dans un environnement découplé](headless.md).

#### Événements de tableau de bord requis

Les événements suivants sont requis pour renseigner le tableau de bord [[!DNL Product Recommendations]  ](workspace.md)

| Colonne du tableau de bord | Événements | Joindre le champ |
| ---------------- | --------- | ----------- |
| Impressions | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render` | `unitId` |
| Vues | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render`, `recs-unit-view` | `unitId` |
| Clics | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-item-click`, `recs-add-to-cart-click` | `unitId` |
| Chiffre d’affaires | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-item-click`, `recs-add-to-cart-click`, `place-order` | `unitId`, `sku`, `parentSku` |
| Revenus LT | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-item-click`, `recs-add-to-cart-click`, `place-order` | `unitId`, `sku`, `parentSku` |
| CTR | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render`, `recs-item-click`, `recs-add-to-cart-click` | `unitId`, `sku`, `parentSku` |
| vCTR | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render`, `recs-unit-view`, `recs-item-click`, `recs-add-to-cart-click` | `unitId`, `sku`, `parentSku` |

Les événements suivants ne sont pas spécifiques aux recommandations de produits, mais sont nécessaires pour qu’Adobe Sensei interprète correctement les données d’acheteur :

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
| A vu ceci, a acheté cela | Rec De Produit | `page-view`<br>`product-view` | Page des détails du produit<br>Panier/Passage en caisse |
| J&#39;ai acheté ça, acheté ça | Rec De Produit | `page-view`<br>`product-view` | Page des détails du produit |
| En Tendance | `page-view`<br>`product-view` | Page des détails du produit |
| Conversion : afficher pour acheter | Rec De Produit | `page-view`<br>`product-view` | Page des détails du produit |
| Conversion : afficher pour acheter | Rec De Produit | `page-view`<br>`place-order` | Panier/Passage en caisse |
| Conversion : afficher au panier | Rec De Produit | `page-view`<br>`product-view` | Page des détails du produit |
| Conversion : afficher au panier | Rec De Produit | `page-view`<br>`add-to-cart` | Page des détails du produit<br>Page de liste des produits<br>Panier<br>Liste de souhaits |

#### Avertissements

- Les bloqueurs de publicités et les paramètres de confidentialité peuvent empêcher la capture d’événements et peuvent entraîner la sous-déclaration des mesures d’engagement et de chiffre d’affaires [mesures](workspace.md#column-descriptions). En outre, certains événements peuvent ne pas être envoyés en raison de problèmes de page ou de réseau liés aux clients qui quittent la page.
- Les [implémentations découplées](headless.md) doivent implémenter des événements pour alimenter le tableau de bord des recommandations de produits.
- Pour les produits configurables, les recommandations de produits utilisent l’image du produit parent dans l’unité de recommandation. Si aucune image n’est spécifiée pour le produit configurable, l’unité de recommandation est vide pour ce produit spécifique.

>[!NOTE]
>
>Si le [Mode de restriction des cookies](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html?lang=fr) est activé, Adobe Commerce ne collecte pas de données comportementales tant que l’acheteur n’a pas consenti à l’utilisation de cookies. Si le Mode de restriction des cookies est désactivé, Adobe Commerce collecte des données comportementales par défaut.
