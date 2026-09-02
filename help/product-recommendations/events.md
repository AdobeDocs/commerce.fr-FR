---
title: Collecter des données
description: Découvrez comment les événements collectent des données pour  [!DNL Product Recommendations].
feature: Services, Recommendations, Eventing
exl-id: 0d5317e3-c049-4fcd-a8e4-228668d89386
TQID: https://experienceleague.adobe.com/efHRMj3u3w-xvUgMnEYDpX0D-BDCUyjhhrkMaa3n-xg
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c4147b6e-073b-4d3c-9ab1-d60f2f4434efid: d3cdead0-685a-4489-9250-4bb709942f66id: eb30f47f-d87a-400f-8f78-63ce7979ff56id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 88a0b1a238090dec85e0f79082d264b720999fee
workflow-type: tm+mt
source-wordcount: 937
ht-degree: 0%

---

# Collecter des données

Lorsque vous installez et configurez [[!DNL Product Recommendations]](install-configure.md), le module déploie la collecte de données comportementales sur votre storefront. Ce mécanisme collecte des données comportementales anonymisées de vos clients et alimente [!DNL Product Recommendations]. Par exemple, l’événement `view` est utilisé pour calculer le type de recommandation `Viewed this, viewed that` et l’événement `place-order` est utilisé pour calculer le type de recommandation `Bought this, bought that`.

Pour en savoir plus sur les données comportementales collectées par les événements [!DNL Product Recommendations], consultez la [documentation destinée aux développeurs](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#product-recommendations).

>[!NOTE]
>
>La collecte de données à des fins de [!DNL Product Recommendations] n’inclut pas les informations d’identification personnelle (PII). Tous les identifiants d’utilisateur, tels que les ID de cookie et les adresses IP, sont strictement anonymisés. En savoir [plus](https://www.adobe.com/privacy/experience-cloud.html).

## Clients du secteur de la santé

Si vous êtes un client du secteur de la santé et que vous avez installé l’extension [Data Services HIPAA](../data-connection/hipaa-readiness.md#installation), incluse avec l’extension [Data Connection](../data-connection/overview.md), [!DNL Product Recommendations] cesse de collecter les données d’événement de storefront, car elles sont générées côté client.

Pour reprendre la collecte et l’envoi des données d’événement de storefront, réactivez la collecte d’événements pour [!DNL Product Recommendations]. Pour plus d’informations, voir [Configuration générale](https://experienceleague.adobe.com/en/docs/commerce-admin/config/general/general#data-services).

## Types de données et événements

Il existe deux types de données utilisées dans les recommandations de produits :

- **Comportemental** - Données provenant de l’engagement d’un acheteur sur votre site, telles que les consultations de produits, les articles ajoutés au panier et les achats.
- **Catalogue** - Métadonnées du produit, telles que le nom, le prix, la disponibilité, etc.

Lorsque vous installez le module `magento/product-recommendations`, Adobe AI agrège les données comportementales et de catalogue, créant des recommandations de produits pour chaque type de recommandation. Le service de recommandations de produits déploie ensuite ces recommandations sur votre storefront sous la forme d’un widget qui contient les _éléments_ de produit recommandés.

Certains types de recommandations utilisent les données comportementales des acheteurs pour entraîner des modèles de machine learning et générer des recommandations personnalisées. D’autres ne dépendent que des données de catalogue. Pour commencer à utiliser rapidement les recommandations de produits, choisissez l’un des types de recommandations de catalogue uniquement suivants :

- `More like this`
- `Visual similarity`

### Démarrage à froid

Quand pouvez-vous commencer à utiliser des types de recommandations qui utilisent des données comportementales ? Ça dépend. On appelle cette situation le problème _Cold Start_.

Le problème du _démarrage à froid_ est le temps nécessaire pour qu’un modèle de machine learning s’entraîne avant de pouvoir produire des recommandations efficaces. Pour les recommandations de produits, Adobe AI doit collecter suffisamment de données pour entraîner ses modèles avant de déployer les unités de recommandation. Plus de données améliorent généralement la précision et l’utilité des recommandations. Comme la collecte de données se produit sur votre site en ligne, démarrez ce processus rapidement en installant et en configurant le module `magento/product-recommendations`.

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

Pendant que votre site en ligne collecte des données et que les modèles de machine learning s’entraînent, effectuez les tâches de test et de configuration restantes. Une fois que les modèles disposent de suffisamment de données pour générer des recommandations utiles, déployez les unités de recommandation sur votre storefront.

Si votre site ne reçoit pas suffisamment de trafic (vues, achats ou tendances) pour la plupart des SKU de produit, le processus d’apprentissage peut ne pas se terminer, ce qui bloque les indicateurs de préparation dans l’administration. Les indicateurs de préparation aident les commerçants à choisir le meilleur type de recommandation pour leur magasin, mais ils ne sont qu&#39;un guide et peuvent ne jamais atteindre 100 %. En savoir plus sur les indicateurs de préparation. [En savoir plus](create.md#readiness-indicators) sur les indicateurs de préparation.

### Recommandations de sauvegarde {#backuprecs}

Lorsque des données d’entrée insuffisantes empêchent une unité de recommandation de renvoyer tous les éléments demandés, Adobe Commerce l’alimente avec des recommandations de sauvegarde. Par exemple, après le déploiement du type de recommandation `Recommended for you` sur la page d’accueil, un nouvel acheteur peut ne pas avoir généré suffisamment de données comportementales pour les recommandations personnalisées. Dans ce cas, Adobe Commerce affiche les éléments en fonction du type `Most viewed ` recommandation .

Si la collecte des données d’entrée est insuffisante, les types de recommandation suivants reviennent `Most viewed` type de recommandation :

- `Recommended for you`
- `Viewed this, viewed that`
- `Viewed this, bought that`
- `Bought this, bought that`
- `Trending`
- `Conversion (view to purchase)`
- `Conversion (view to cart)`

#### Avertissements

- Les bloqueurs de publicités et les paramètres de confidentialité peuvent empêcher la capture d’événements et peuvent entraîner la sous-déclaration des mesures d’engagement et de chiffre d’affaires [mesures](workspace.md#column-descriptions). En outre, certains événements ne sont pas envoyés car les acheteurs quittent la page ou rencontrent des problèmes réseau.
- Les [implémentations découplées](headless.md) doivent implémenter des événements pour alimenter le tableau de bord des recommandations de produits.
- Pour les produits configurables, les recommandations de produits utilisent l’image du produit parent. Si le produit parent ne comporte aucune image, ce produit n’apparaît pas dans l’unité de recommandation.

>[!NOTE]
>
>Si le [Mode de restriction des cookies](https://experienceleague.adobe.com/en/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law) est activé, Adobe Commerce ne collecte pas de données comportementales tant que l’acheteur n’a pas consenti à l’utilisation de cookies. Si le Mode de restriction des cookies est désactivé, Adobe Commerce collecte des données comportementales par défaut.
