---
title: '[!DNL Catalog Service]'
description: 'Accélérez votre storefront Adobe Commerce avec  [!DNL Catalog Service]  : une API GraphQL haute performance qui réduit les temps de chargement des pages pour les pages de produits, les pages de catégories et les résultats de recherche.'
role: Admin, Developer
recommendations: noCatalog
exl-id: 525e3ff0-efa6-48c7-9111-d0b00f42957a
source-git-commit: e582bff6ee8ee7c4213f04bdab984efa94333fb6
workflow-type: tm+mt
source-wordcount: '1323'
ht-degree: 0%

---

# [!DNL Catalog Service] pour Adobe Commerce

L’extension [!DNL Catalog Service] for Adobe Commerce améliore les temps de chargement du storefront en fournissant des données de catalogue optimisées et en lecture seule via une API GraphQL dédiée. Ce service est spécialement conçu pour améliorer les expériences de page liées au produit, ce qui permet d’accélérer le chargement des pages et d’améliorer les taux de conversion.

Les données de modèle d’affichage riches fournies par le [!DNL Catalog Service] comprennent les détails du produit, les attributs, l’inventaire et les prix, ce qui permet un rendu rapide des expériences de storefront liées au produit, telles que :

- Pages de détails du produit
- Pages de liste de produits et de catégories
- Pages de résultats de recherche
- Carrousels de produit
- Pages de comparaison de produits
- Toute autre page qui effectue le rendu des données de produit, comme les pages de panier, de commande et de liste de souhaits


## Principaux avantages et fonctionnalités

- **Chargement de page plus rapide** : requêtes optimisées pour une récupération des données de catalogue jusqu’à 10 fois plus rapide par rapport au système GraphQL principal
- **Taux de conversion améliorés** : des temps de chargement plus rapides améliorent l’expérience utilisateur
- **Types de produits simplifiés** : le schéma unifié basé sur des types de produits simples et complexes réduit la complexité pour les développeurs
- **Précision des prix améliorée** : prise en charge des valeurs à 16 chiffres avec 4 décimales
- **Architecture découplée** : un système GraphQL distinct pour les données de catalogue assure des performances élevées sans affecter les opérations Commerce principales
- **Synchronisation des données en temps réel** : le service de catalogue est synchronisé avec l’application Adobe Commerce par le biais de l’extension d’exportation de données SaaS, ce qui garantit que les requêtes renvoient les données de catalogue les plus récentes
- **Tableau de bord de gestion des données** : surveillez et gérez les opérations de synchronisation des données à partir de l’interface d’administration d’Adobe Commerce
- **Intégration du maillage API** : vous pouvez éventuellement intégrer le [maillage API pour Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/) pour combiner les systèmes Adobe Commerce GraphQL avec d’autres API internes et tierces afin d’étendre le schéma GraphQL du service de catalogue et d’ajouter des données ou des fonctionnalités personnalisées


## Aperçu de l’architecture

L’[!DNL Catalog Service] utilise [GraphQL](https://graphql.org/) pour demander et recevoir des données de catalogue, y compris les produits, les attributs de produit, l’inventaire et les prix. GraphQL est un langage de requête qu’un client front-end utilise pour communiquer avec l’interface de programmation d’applications (API) définie sur un serveur principal tel qu’Adobe Commerce. GraphQL est une méthode de communication populaire, car elle est légère et permet à un intégrateur système de spécifier le contenu et l’ordre de chaque réponse.

Adobe Commerce fournit deux systèmes GraphQL qui servent des objectifs différents :

### Système GraphQL principal

- **Objectif** : API complète pour toutes les opérations de Commerce
- **Fonctionnalités** : requêtes (lecture) et mutations (écriture) pour les produits, les clients, le panier, le passage en caisse, etc
- **Limitation** : les requêtes de produit ne sont pas optimisées pour la vitesse.
- **Cas pratique** : opérations générales de Commerce et opérations d’écriture

### Système GraphQL du service de catalogue

- **Objectif** : requêtes de catalogue de produits hautes performances uniquement
- **Fonctionnalités** : requêtes en lecture seule pour les produits, les attributs, l’inventaire et les prix
- **Avantage** : beaucoup plus rapide que le système principal pour les données de produit
- **Cas d’utilisation** : expériences de produit Storefront pour lesquelles la vitesse est essentielle

Les données disponibles pour le service de catalogue sont fournies par l’extension d’exportation de données SaaS. Cette extension synchronise les données entre l’application Commerce et les services Commerce connectés pour s’assurer que les requêtes envoyées aux points d’entrée de l’API GraphQL des services renvoient les données de catalogue les plus récentes. Pour plus d&#39;informations sur la gestion et le dépannage des opérations d&#39;exportation de données SaaS, consultez le [Guide d&#39;exportation de données SaaS](../data-export/overview.md).

[!DNL Catalog Service] clients peuvent utiliser l&#39;indexeur de prix [SaaS](../price-index/price-indexing.md), qui offre des mises à jour de prix et des temps de synchronisation plus rapides.

## Détails de l’architecture

Le diagramme suivant illustre les différences architecturales entre le système GraphQL principal et le système GraphQL du service de catalogue, montrant comment ils fonctionnent ensemble pour optimiser les performances du storefront :

![Diagramme d’architecture de catalogue](assets/catalog-service-architecture.png)

### Fonctionnement des systèmes

**Système Core GraphQL (Approche Traditionnelle) :**
L’application web progressive (PWA) envoie les requêtes directement à l’application Commerce, qui traite chaque requête par le biais de plusieurs sous-systèmes avant de renvoyer une réponse. Ce voyage aller-retour en plusieurs étapes peut ralentir les temps de chargement des pages, ce qui peut entraîner une réduction des taux de conversion.

**Service de catalogue (approche optimisée) :**
Le service de catalogue agit comme une passerelle des services Storefront qui accède à une base de données optimisée et dédiée contenant des détails sur les produits, des attributs, des variantes, des prix et des catégories. Le service maintient la synchronisation avec Adobe Commerce par le biais d’une indexation automatisée, en contournant le cycle traditionnel de requête-réponse pour réduire considérablement la latence.

Les systèmes GraphQL principaux et de service ne communiquent pas directement entre eux. Vous accédez à chaque système à partir d’une URL différente et les appels nécessitent des informations d’en-tête différentes. Les deux systèmes GraphQL sont conçus pour être utilisés ensemble. Le système [!DNL Catalog Service] GraphQL améliore le système principal pour accélérer les expériences de storefront des produits.

Vous pouvez éventuellement mettre en œuvre le [maillage API pour Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/) pour intégrer les deux systèmes Adobe Commerce GraphQL à des API privées et tierces et à d’autres interfaces logicielles à l’aide d’Adobe Developer. Le maillage peut être configuré pour s’assurer que les appels acheminés vers chaque point d’entrée contiennent les informations d’autorisation correctes dans les en-têtes.

## Détails architecturaux

Les sections suivantes décrivent certaines des différences entre les deux systèmes GraphQL.

### Gestion des schémas

Dans la mesure où Catalog Service fonctionne comme un service, les intégrateurs n’ont pas besoin de s’inquiéter de la version sous-jacente de Commerce. La syntaxe des requêtes est la même pour toutes les versions. En outre, le schéma est cohérent pour tous les commerçants. Cette cohérence facilite l’établissement des bonnes pratiques et accroît considérablement la réutilisation des widgets de storefront.

### Simplification des types de produits

Le schéma réduit la diversité des types de produits à deux cas d’utilisation :

- **Produits simples**—Le service de catalogue mappe les types de produits Adobe Commerce simples, virtuels, téléchargeables et de cartes-cadeaux aux `simpleProductViews`. Ce type possède :
   - Un prix et une quantité uniques et fixes
   - Prix normal (avant remises) et prix final (après remises)
   - Prise en charge des attributs du produit, tels que la couleur, la taille et d’autres caractéristiques

- **Produits complexes** : le service de catalogue mappe les types de produits configurables, groupés et groupés d’Adobe Commerce à `complexProductViews`. Les produits complexes sont des ensembles de plusieurs produits simples qui peuvent être configurés ou regroupés.
   - Chaque composant simple produit peut avoir son propre prix.
   - Les acheteurs peuvent indiquer des quantités pour des composants individuels.
   - Les options de produit (telles que la taille, la couleur et le matériau) sont unifiées et fonctionnent de la même manière, quel que soit le type de produit. Chaque sélection d’options pointe vers un produit simple spécifique avec ses propres attributs et son propre prix. Le produit final reste indéfini jusqu’à ce que l’acheteur sélectionne toutes les options requises.

#### Attributs de vue du produit

Les produits simples et complexes possèdent des attributs définis par le client qui peuvent être affichés sur le storefront. Ces attributs sont renvoyés sous la forme [ProductViewAttributes](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/#productviewattribute-type). Dans Adobe Commerce, les attributs disponibles sont définis lors de la création du produit. Vous pouvez ajouter des attributs supplémentaires à partir du serveur principal Adobe Commerce ou par programmation. Voir [Extension et personnalisation des données de flux d’exportation de données SaaS](../data-export/extensibility-and-customizations.md).

>[!TIP]
>
>Au lieu d’ajouter des types de données au serveur principal Commerce, vous pouvez utiliser le [maillage API avec le service de catalogue](mesh.md) pour étendre le schéma GraphQL du service de catalogue afin d’ajouter des données ou de configurer les données de catalogue existantes pour activer une nouvelle fonctionnalité.

### Prix

Les produits simples représentent l&#39;unité de vente de base qui a un prix. [!DNL Catalog Service] calcule le prix normal avant remises ainsi que le prix final après remises. Les calculs de tarification peuvent inclure des taxes sur les produits fixes. Ils excluent les promotions personnalisées.

Un produit complexe n&#39;a pas de prix fixe. Au lieu de cela, le service de catalogue renvoie les prix des simples liés. Par exemple, un commerçant peut initialement attribuer les mêmes prix à toutes les variantes d’un produit configurable. Si certaines tailles ou couleurs sont impopulaires, le marchand peut réduire les prix de ces variantes. Ainsi, le prix du produit complexe (configurable) présente d’abord une fourchette de prix, reflétant le prix des variantes standard et impopulaires. Une fois que l’acheteur a sélectionné une valeur pour toutes les options disponibles, le storefront affiche un prix unique.

Le service de catalogue garantit la précision des mises à jour et des calculs des prix en prenant en charge les prix avec des valeurs élevées (jusqu’à 16 chiffres) et une précision décimale élevée (jusqu’à 4 décimales).

>[!NOTE]
>
> Les clients Commerce avec [!DNL Catalog Service] peuvent bénéficier de mises à jour de modifications de prix et de temps de synchronisation plus rapides sur leurs sites web avec l’indexeur de prix [SaaS](../price-index/price-indexing.md).

## Mise en œuvre

Le processus de mise en œuvre implique :

1. [!BADGE PaaS uniquement]{type=Informative url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."} **[Installer et configurer le service de catalogue](installation.md)** : installez et configurez l’extension du service de catalogue et configurez la connexion SaaS à l’aide de l’[!DNL Commerce Services Connector].
2. **Mettre à jour le code storefront** : intégrez les requêtes GraphQL du service de catalogue à votre serveur frontal.
3. **Requêtes d’itinéraire** : toutes les requêtes du service de catalogue passent par la passerelle GraphQL (URL fournie lors de l’intégration)
4. **Surveillance et dépannage de la synchronisation des données** : vérification des performances améliorées et surveillance des résultats


