---
title: Collecter des données
description: Découvrez comment les événements collectent des données pour  [!DNL Product Recommendations].
feature: Services, Recommendations, Eventing
exl-id: 0d5317e3-c049-4fcd-a8e4-228668d89386
source-git-commit: 458f34c45406db871ec61ff408aa624f163b6ee0
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 0%

---

# Collecter des données

Lorsque vous installez et configurez [[!DNL Product Recommendations]](install-configure.md), le module déploie la collecte de données comportementales sur votre storefront. Ce mécanisme collecte des données comportementales anonymisées de vos clients et alimente [!DNL Product Recommendations]. Par exemple, l’événement `view` est utilisé pour calculer le type de recommandation `Viewed this, viewed that` et l’événement `place-order` est utilisé pour calculer le type de recommandation `Bought this, bought that`.

Consultez la [documentation pour les développeurs](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#product-recommendations) pour en savoir plus sur les données comportementales collectées par les événements [!DNL Product Recommendations].

>[!NOTE]
>
>La collecte de données à des fins de [!DNL Product Recommendations] n’inclut pas les informations d’identification personnelle (PII). Tous les identifiants d’utilisateur, tels que les ID de cookie et les adresses IP, sont strictement anonymisés. En savoir [plus](https://www.adobe.com/privacy/experience-cloud.html).

## Clients du secteur de la santé

Si vous êtes un client du secteur de la santé et que vous avez installé l’extension [Data Services HIPAA](../data-connection/hipaa-readiness.md#installation), qui fait partie de l’extension [Data Connection](../data-connection/overview.md), les données d’événement de storefront utilisées par [!DNL Product Recommendations] ne sont plus capturées. En effet, les données d’événement de storefront sont générées côté client. Pour continuer à capturer et à envoyer des données d’événement de storefront, réactivez la collecte d’événements pour [!DNL Product Recommendations]. Voir [configuration générale](https://experienceleague.adobe.com/en/docs/commerce-admin/config/general/general#data-services) pour en savoir plus.

## Types de données et événements

Il existe deux types de données utilisées dans les recommandations de produits :

- **Comportemental** - Données provenant de l’engagement d’un acheteur sur votre site, telles que les consultations de produits, les articles ajoutés au panier et les achats.
- **Catalogue** - Métadonnées du produit, telles que le nom, le prix, la disponibilité, etc.

Lorsque vous installez le module `magento/product-recommendations`, l’IA d’Adobe agrège les données comportementales et de catalogue, créant des recommandations de produits pour chaque type de recommandation. Le service de recommandations de produits déploie ensuite ces recommandations sur votre storefront sous la forme d’un widget qui contient les _éléments_ de produit recommandés.

Certains types de recommandations utilisent les données comportementales de vos clients pour entraîner des modèles de machine learning afin de créer des recommandations personnalisées. D’autres types de recommandations utilisent uniquement les données de catalogue et n’utilisent aucune donnée comportementale. Si vous souhaitez commencer rapidement à utiliser les recommandations de produits sur votre site, vous pouvez utiliser les types de recommandations de catalogue uniquement suivants :

- `More like this`
- `Visual similarity`

### Démarrage à froid

Quand pouvez-vous commencer à utiliser des types de recommandations qui utilisent des données comportementales ? Ça dépend. C’est ce qu’on appelle le problème _Cold Start_.

Le problème du _démarrage à froid_ fait référence au temps nécessaire pour qu’un modèle s’entraîne et devienne efficace. Pour les recommandations de produits, cela signifie attendre que l’IA dédiée à Adobe collecte suffisamment de données pour entraîner ses modèles de machine learning avant de déployer des unités de recommandation sur votre site. Plus les modèles contiennent de données, plus les recommandations sont précises et utiles. Comme la collecte de données se produit sur un site en ligne, il est préférable de démarrer ce processus rapidement en installant et en configurant le module `magento/production-recommendations`.

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

#### Avertissements

- Les bloqueurs de publicités et les paramètres de confidentialité peuvent empêcher la capture d’événements et peuvent entraîner la sous-déclaration des mesures d’engagement et de chiffre d’affaires [mesures](workspace.md#column-descriptions). En outre, certains événements peuvent ne pas être envoyés en raison de problèmes de page ou de réseau liés aux clients qui quittent la page.
- Les [implémentations découplées](headless.md) doivent implémenter des événements pour alimenter le tableau de bord des recommandations de produits.
- Pour les produits configurables, les recommandations de produits utilisent l’image du produit parent dans l’unité de recommandation. Si aucune image n’est spécifiée pour le produit configurable, l’unité de recommandation est vide pour ce produit spécifique.

>[!NOTE]
>
>Si le [Mode de restriction des cookies](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html) est activé, Adobe Commerce ne collecte pas de données comportementales tant que l’acheteur n’a pas consenti à l’utilisation de cookies. Si le Mode de restriction des cookies est désactivé, Adobe Commerce collecte des données comportementales par défaut.
