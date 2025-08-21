---
title: Types de recommandations
description: Découvrez les recommandations que vous pouvez déployer sur différentes pages de votre site.
exl-id: bbb290b0-b50b-43d9-bf71-1813298d5f39
source-git-commit: 1548b7e11249febc2cd8682581616619f80c052f
workflow-type: tm+mt
source-wordcount: '1719'
ht-degree: 0%

---

# Types de recommandations

Adobe Commerce fournit un large ensemble de recommandations que vous pouvez déployer sur différentes pages de votre site. Tous les types de recommandations sont pilotés par les données. Elles sont optimisées par des données comportementales, des données d’attributs de produit et des mesures. Pour s’y référer facilement, les types de recommandations sont regroupés comme suit :

- [Personnalisé](#personalized)
- [Vente croisée et vente incitative](#crossup)
- [Popularité](#popularity)
- [Très performant](#highperf)

Adobe recommande d’appliquer les recommandations suivantes lors de l’utilisation de Recommendations :

- Diversifiez vos types de recommandations. Les clients commencent à ignorer les recommandations s’ils suggèrent les mêmes produits à plusieurs reprises.

- Ne déployez pas les mêmes recommandations sur la page de votre panier et sur la page de confirmation de commande. Pensez à utiliser `Most Added to Cart` pour la page Panier et `Bought This, Bought That` pour la page de confirmation de commande.

- Gardez votre site propre. Ne déployez pas plus de trois unités de recommandation sur la même page.

- Si votre boutique vend des vêtements, la recommandation `More like this` peut suggérer des produits spécifiques au genre qui ne correspondent pas au genre du produit affiché. Envisagez d’utiliser ce type de recommandation uniquement pour les catégories non vestimentaires.

>[!NOTE]
>
>Pour plus d’informations sur les événements décrits dans cet article, consultez [événements storefront](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#product-recommendations) dans la documentation destinée aux développeurs.

## Personnalisé {#personalized}

Ces types de recommandations recommandent des produits en fonction de l’historique comportemental de l’acheteur spécifique sur votre site. Par exemple, si un acheteur a déjà recherché une veste ou acheté une veste sur votre site, ces recommandations reprennent essentiellement là où il s’était arrêté et recommandent d’autres vestes ou produits similaires.

| Type | Description |
|---|---|
| Recommandé pour vous | Recommande des produits en fonction du comportement actuel et précédent de chaque acheteur sur site. Affiche des recommandations très pertinentes en fonction de l’historique de navigation et d’achat de l’acheteur. Ce type de recommandation est effectif sur la page d’accueil où la plupart des acheteurs commencent leur parcours sur un site. Pour les nouveaux acheteurs de votre site qui n’ont généré aucun signal afin de personnaliser leur expérience, Adobe Commerce affiche les produits en fonction du type de recommandation Les plus consultés . Lorsque l’acheteur commence à interagir avec les produits sur le site, cependant, les produits recommandés s’adaptent en temps réel à leur comportement.<br/><br/>**Utilisation :**<br/>- Page d’accueil<br/>- Catégorie <br/><br/>**Étiquettes suggérées :**<br/> - Uniquement pour vous<br/>- Recommandé pour vous<br/>- Inspiré par vos tendances d’achat |
| Récemment consultés | Affiche les produits consultés le plus récemment par l’acheteur, en fonction de l’historique du navigateur. Tous les produits supprimés sont supprimés par l’unité de recommandation. L’unité de recommandation ne s’affiche pas s’il n’existe aucun historique de navigateur ou un historique insuffisant lorsque des règles de filtrage sont appliquées. Si les résultats contiennent moins de produits que ceux configurés, l’unité de recommandation affiche uniquement les produits renvoyés.<br/><br/>**Utilisation :**<br/>- Page d’accueil<br/>- Catégorie<br/>- Détails du produit<br/>- Panier<br/>- Confirmation <br/><br/>**Étiquettes suggérées :**<br/>- Récemment consultés<br/>- Changez votre regard |

## Vente croisée et vente incitative {#crossup}

Ces types de recommandations sont pilotés par les réseaux sociaux pour aider les acheteurs à trouver ce que les autres ont aimé ou pilotés par les produits pour les aider à trouver d’autres produits similaires. Les produits recommandés complètent souvent le produit sélectionné.

>[!NOTE]
>
>Les types de recommandation « vu ceci, vu cela », « vu ceci, acheté cela » et « acheté ceci, acheté cela » n’utilisent pas de mesure d’occurrence simple, mais plutôt un algorithme de filtrage collaboratif plus sophistiqué qui recherche des *similitudes intéressantes* qui ne sont pas biaisées vers des produits populaires. Les données utilisées pour informer ces types de recommandations sont basées sur le comportement agrégé de l’acheteur dérivé de plusieurs sessions sur votre site. Les données ne sont pas basées sur le comportement de l’acheteur dérivé d’une seule occurrence en session sur votre site. Ces types de recommandations aident les acheteurs à trouver les produits adjacents qui ne sont pas nécessairement évidents à associer au produit actuellement consulté.

| Type | Description |
|---|---|
| A consulté ceci, a consulté cela | Recommande des produits que les acheteurs consultent plus souvent de manière disproportionnée avec le produit actuellement consulté.<br/><br/>**Utilisation :**<br/>- Détails du produit<br/>- Panier<br/>- Confirmation <br/><br/>**Étiquettes suggérées :**<br/>- Les clients qui ont consulté ce produit ont également consulté (PDP) |
| A vu ceci, a acheté cela | Recommande des produits que les acheteurs ont tendance à acheter de manière disproportionnée plus souvent après avoir consulté le produit actuel. Ce type permet aux acheteurs de découvrir des produits qu’ils n’auraient pas remarqués autrement.<br/><br/>**Où l’utiliser :**<br/>- Détails du produit<br/>- Panier<br/>- Confirmation <br/><br/>**Étiquettes suggérées :**<br/>- Clients qui ont consulté ce produit final ont acheté<br/>- Clients qui l’ont finalement acheté<br/>- Que achètent les autres après l’avoir consulté ? |
| J&#39;ai acheté ça, acheté ça | Recommande des produits que les acheteurs achètent plus souvent de manière disproportionnée par rapport au produit actuellement consulté. Ce type affiche des produits très pertinents que les acheteurs peuvent ajouter à leur panier en agrégeant ce que les autres acheteurs ont acheté avec le produit actuel.<br/><br/>**Où utilisé :**<br/>- Détails du produit<br/>- Panier<br/>- Confirmation <br/><br/>**Étiquettes suggérées :**<br/>- Obtenez tout ce dont vous avez besoin<br/>- N&#39;oubliez pas ces<br/>- Fréquemment achetés ensemble |
| Plus comme ceci | Recommande des produits en fonction de métadonnées similaires telles que le nom, la description, l’affectation de catégorie et les attributs. En évaluant les attributs des produits affichés, ce type recommande des produits similaires dans la même catégorie. Par exemple, si un acheteur navigue sur des tapis de yoga, d&#39;autres produits de la catégorie d&#39;équipement sont recommandés. Comme ce type de recommandation ne fait pas de distinction entre les sexes, il n&#39;est pas recommandé pour les vêtements, la mode ou d&#39;autres verticales spécifiques au sexe.<br/><br/>**Utilisation :**<br/>- Détails du produit<br/>- Panier<br/>- Confirmation <br/><br/>**Étiquettes suggérées :**<br/> - Plus de produits comme celui-ci<br/>- Similaire à ceci |
| [Similarité visuelle](#visualsim) | Recommande des produits d’aspect similaire au produit en cours de consultation. Ce type de recommandation est particulièrement utile si les images et les aspects visuels des produits sont importants pour l’expérience d’achat. |

## Popularité {#popularity}

Ces types de recommandations recommandent les produits les plus populaires ou les plus en vogue au cours des sept derniers jours.

| Type | Description |
|---|---|
| Les plus consultés | Recommande les produits qui ont été consultés le plus en comptant le nombre de sessions pour lesquelles une action d’affichage a eu lieu au cours des sept derniers jours.<br/><br/>**Utilisation :**<br/>- Page d’accueil<br/>- Catégorie<br/>- Détails du produit<br/>- Panier<br/>- Confirmation <br/><br/>**Étiquettes suggérées :**<br/>- Les plus populaires<br/>- Tendance<br/>- Populaire en ce moment<br/>- Récemment populaire<br/>- Produits populaires inspirés par ce produit (PDP)<br/>- Meilleures ventes |
| Les plus achetés | Recommande les produits achetés le plus souvent par les acheteurs au cours des sept derniers jours.<br/><br/>**Utilisation :**<br/>- Page d’accueil<br/>- Catégorie<br/>- Détails du produit<br/>- Panier<br/>- Confirmation <br/><br/>**Étiquettes suggérées :**<br/> - Les plus populaires<br/>- Tendance<br/>- Populaire en ce moment<br/>- Récemment populaire<br/>- Produits populaires inspirés par ce produit (PDP)<br/>- Meilleures ventes |
| Les plus ajoutés au panier | Recommande les produits les plus fréquemment ajoutés au panier par les acheteurs au cours des sept derniers jours. Ce type de recommandation peut être utilisé sur toutes les pages.<br/><br/>**Utilisation :**<br/>- Page d’accueil<br/>- Catégorie<br/>- Détails du produit<br/>- Panier<br/>- Confirmation <br/><br/>**Étiquettes suggérées :**<br/> - Les plus populaires<br/>- Tendance<br/>- Populaire en ce moment<br/>- Récemment populaire<br/>- Produits populaires inspirés par ce produit (PDP)<br/>- Meilleures ventes |
| En Tendance | Recommande des produits en fonction de l’élan récent de popularité d’un produit sur l’ensemble de votre site.<br/><br/>Adobe Sensei agrège les données de navigation et d’achat sur votre site afin de déterminer et de classer les produits les plus récemment populaires auprès de vos clientes et clients. Parce que Trending analyse l’élan récent d’un produit, il s’agit d’un type de recommandation efficace pour les catalogues qui ont un chiffre d’affaires élevé. Si votre catalogue est plus statique, il peut ne pas être aussi utile sauf si les modèles d’achat de votre audience sont très variables.<br/><br/>Lorsqu’il est utilisé sur la page d’accueil, Trending recommande des produits qui sont récemment populaires sur l’ensemble du site. La tendance n’affiche pas les produits qui sont constamment populaires, mais plutôt ceux qui sont récemment devenus populaires. Par exemple, si vous disposez d’une campagne de marketing par e-mail faisant la promotion de certains produits, l’augmentation de popularité générée par l’e-mail augmente la probabilité que les produits promus soient classés comme étant en tendance.<br/><br/>**Utilisation :**<br/>- Page d’accueil<br/>- Catégorie<br/>- Détails du produit<br/>- Panier<br/>- Confirmation <br/><br/>**Étiquettes suggérées :**<br/>- Tendance<br/>- Tendance actuelle<br/>- Tendance récente<br/>- Produits chauds<br/>- Tendance des produits associés (PDP) |

## Très performant {#highperf}

Ces types de recommandations recommandent des produits les plus performants en fonction de critères de réussite tels que les ajouts au panier ou les taux de conversion.

| Type | Description |
|---|---|
| Conversion de la vue à l’achat | Recommande les produits présentant le taux de conversion de consultation à l’achat le plus élevé. De toutes les sessions d’acheteur qui ont enregistré une consultation de produit, quelle est la proportion qui a finalement enregistré un achat par l’acheteur.<br/><br/>**Utilisation :**<br/>- Page d’accueil<br/>- Catégorie<br/>- Détails du produit<br/>- Panier<br/>- Confirmation <br/><br/>**Étiquettes suggérées :**<br/> -Meilleurs vendeurs<br/>- Produits populaires<br/>- Ce qui peut vous intéresser |
| Conversion de l’affichage au panier | Recommande les produits présentant le taux de conversion d’affichage en panier le plus élevé. De toutes les sessions d’acheteur qui ont enregistré une consultation de produit, quelle est la proportion qui a finalement enregistré un ajout au panier par l’acheteur ?<br/><br/>**Cas d’utilisation :**<br/>- Page d’accueil<br/>- Catégorie<br/>- Détails du produit<br/>- Panier<br/>- Confirmation <br/><br/>**Étiquettes suggérées :**<br/> - Meilleurs vendeurs<br/>- Produits populaires<br/>- Ce qui peut vous intéresser |
| Les plus achetés | Souvent appelé « Meilleurs vendeurs », ce type de recommandation comptabilise le nombre de sessions au cours desquelles une action de commande a eu lieu au cours des sept derniers jours. Ce type de recommandation peut être utilisé sur toutes les pages.<br/><br/>**Utilisation :**<br/>- Page d’accueil<br/>- Catégorie<br/>- Détails du produit<br/>- Panier<br/>- Confirmation <br/><br/>**Étiquettes suggérées :**<br/> - Les plus populaires<br/>- Tendance<br/>- Populaire en ce moment<br/>- Récemment populaire<br/>- Produits populaires inspirés par ce produit (PDP)<br/>- Meilleures ventes |
| Les plus ajoutés au panier | Recommande les produits les plus fréquemment ajoutés au panier par les acheteurs au cours des sept derniers jours. Ce type de recommandation peut être utilisé sur toutes les pages.<br/><br/>**Utilisation :**<br/>- Page d’accueil<br/>- Catégorie<br/>- Détails du produit<br/>- Panier<br/>- Confirmation <br/><br/>**Étiquettes suggérées :**<br/> - Les plus populaires<br/>- Tendance<br/>- Populaire en ce moment<br/>- Récemment populaire<br/>- Produits populaires inspirés par ce produit (PDP)<br/>- Meilleures ventes |

## Similarité visuelle {#visualsim}

Le type de recommandation _Similarité visuelle_ recommande des produits d’aspect similaire au produit affiché. Ce type de recommandation est particulièrement utile lorsque les images et les aspects visuels des produits constituent des parties importantes de l’expérience d’achat.

### Fonctionnement

Le type de recommandation _Similarité visuelle_ offre des recommandations pour d’autres produits de votre catalogue qui ont une similarité visuelle avec les images en cours de consultation. La similarité visuelle inclut des aspects tels que :

- Couleur
- Forme
- Taille
- Texture
- Matériau
- Style

Adobe Sensei utilise l’IA pour traiter et analyser les images de votre catalogue et créer des attributs utilisés pour déterminer les similitudes visuelles.

>[!NOTE]
>
> Si vous testez ce type de recommandation dans un environnement hors production, assurez-vous que les URL de vos images sont accessibles au public.

>[!NOTE]
>
> Actuellement, la taille des images du produit doit être inférieure ou égale à 10 Mo.

Comme ce type de recommandation ne s’applique pas à la plupart des catalogues, il n’est pas activé par défaut. Vous devez activer explicitement ce type de recommandation.

### Activer le type de recommandation de similarité visuelle

>[!NOTE]
>
> Le type de recommandation _Similarité visuelle_ est disponible lorsque vous [installez](install-configure.md) en tant que module facultatif.

1. Dans la barre latérale _Admin_, accédez à **Marketing** > _Promotions_ > **Recommandations de produit** pour afficher le tableau de bord _Recommandations de produit_.

1. Cliquez sur **Paramètres** (icône d’engrenage) pour afficher la page _Paramètres_.

1. Dans la section _Recommandations visuelles_, sélectionnez pour **Activer les recommandations visuelles**.

1. Cliquez sur **Enregistrer les modifications** lorsque vous avez terminé.

   La page [Créer une recommandation](create.md) affiche désormais **Similarité visuelle** comme un type de recommandation sélectionnable lorsque le type de page est **Détails du produit**.

Après avoir activé les recommandations visuelles, Adobe Sensei lance le traitement des images. Sa durée dépend de la taille de votre catalogue.

### Cas d’utilisation

- Détails du produit

### Étiquettes de storefront suggérées

- Tu peux aussi aimer
- Nous avons trouvé d&#39;autres produits qui pourraient vous plaire
- Inspiré par ce style

### Exemple

L’image suivante présente la page des détails du produit pour la _Clamber Watch_ :

![Montre Clamber](assets/visual-sim-pdp.png)

Vous trouverez ci-dessous l&#39;unité de recommandation _Similarité visuelle_ pour _Clamber Watch_ :

![Unité de similarité visuelle](assets/visual-sim-unit.png)
