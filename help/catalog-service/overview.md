---
title: '[!DNL Catalog Service]'
description: '[!DNL Catalog Service] pour Adobe Commerce permet de récupérer le contenu des pages d’affichage des produits et des pages de liste de produits beaucoup plus rapidement que les requêtes GraphQL natives d’Adobe Commerce.'
role: Admin, Developer
recommendations: noCatalog
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1078'
ht-degree: 0%

---


# [!DNL Catalog Service] pour Adobe Commerce

L’extension [!DNL Catalog Service] for Adobe Commerce fournit des données de catalogue riches en modèle de vue (lecture seule) pour effectuer rapidement et entièrement le rendu des expériences de storefront liées aux produits, notamment :

* Pages de détails du produit
* Pages de liste de produits et de catégories
* Pages de résultats de recherche
* Carrousels de produit
* Pages de comparaison de produits
* Toute autre page qui effectue le rendu des données de produit, comme les pages de panier, de commande et de liste de souhaits

L’[!DNL Catalog Service] utilise [GraphQL](https://graphql.org/) pour demander et recevoir des données de catalogue, y compris les produits, les attributs de produit, l’inventaire et les prix. GraphQL est un langage de requête qu’un client front-end utilise pour communiquer avec l’interface de programmation d’applications (API) définie sur un serveur principal tel qu’Adobe Commerce. GraphQL est une méthode de communication populaire, car elle est légère et permet à un intégrateur système de spécifier le contenu et l’ordre de chaque réponse.

Adobe Commerce comporte deux systèmes GraphQL. Le système GraphQL principal fournit un large éventail de requêtes (opérations de lecture) et de mutations (opérations d’écriture) qui permettent à un acheteur d’interagir avec de nombreux types de pages, notamment le produit, le compte client, le panier, le passage en caisse, etc. Toutefois, les requêtes qui renvoient des informations sur les produits ne sont pas optimisées pour accélérer le processus. Le système GraphQL des services ne peut exécuter des requêtes que sur les produits et les informations associées. Ces requêtes sont plus performantes que les requêtes principales similaires.

Les données disponibles pour le service de catalogue sont fournies par l’extension d’exportation de données SaaS. Cette extension synchronise les données entre l’application Commerce et les services Commerce connectés pour s’assurer que les requêtes envoyées aux points d’entrée de l’API GraphQL des services renvoient les données de catalogue les plus récentes. Pour plus d&#39;informations sur la gestion et le dépannage des opérations d&#39;exportation de données SaaS, consultez le [Guide d&#39;exportation de données SaaS](../data-export/overview.md).

[!DNL Catalog Service] clients peuvent utiliser l&#39;indexeur de prix [SaaS](../price-index/price-indexing.md), qui offre des mises à jour de prix et des temps de synchronisation plus rapides.

## Architecture

Le diagramme suivant présente les deux systèmes GraphQL :

![Diagramme d’architecture de catalogue](assets/catalog-service-architecture.png)

Dans le système GraphQL principal, le PWA envoie une requête à l’application Commerce, qui reçoit chaque requête, la traite, envoie éventuellement une requête par le biais de plusieurs sous-systèmes, puis renvoie une réponse au storefront. Cet aller-retour peut ralentir les temps de chargement des pages, ce qui peut entraîner une réduction des taux de conversion.

[!DNL Catalog Service] est une passerelle de services Storefront. Le service accède à une base de données distincte qui contient des détails sur les produits et des informations connexes, telles que les attributs de produit, les variantes, les prix et les catégories. Le service maintient la base de données synchronisée avec Adobe Commerce par le biais de l’indexation.
Le service contourne la communication directe avec l’application et peut donc réduire la latence du cycle de requête et de réponse.

Les systèmes GraphQL principaux et de service ne communiquent pas directement entre eux. Vous accédez à chaque système à partir d’une URL différente et les appels nécessitent des informations d’en-tête différentes. Les deux systèmes GraphQL sont conçus pour être utilisés ensemble. Le système [!DNL Catalog Service] GraphQL améliore le système principal pour accélérer les expériences de storefront des produits.

Vous pouvez éventuellement mettre en œuvre le [maillage API pour Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/) pour intégrer les deux systèmes Adobe Commerce GraphQL à des API privées et tierces et à d’autres interfaces logicielles à l’aide d’Adobe Developer. Le maillage peut être configuré pour s’assurer que les appels acheminés vers chaque point d’entrée contiennent les informations d’autorisation correctes dans les en-têtes.

## Détails architecturaux

Les sections suivantes décrivent certaines des différences entre les deux systèmes GraphQL.

### Gestion des schémas

Dans la mesure où Catalog Service fonctionne comme un service, les intégrateurs n’ont pas besoin de s’inquiéter de la version sous-jacente de Commerce. La syntaxe des requêtes est la même pour toutes les versions. En outre, le schéma est cohérent pour tous les commerçants. Cette cohérence facilite l’établissement des bonnes pratiques et accroît considérablement la réutilisation des widgets de storefront.

### Simplification des types de produits

Le schéma réduit la diversité des types de produits à deux cas d’utilisation :

* Les produits simples sont des produits définis avec un prix et une quantité uniques. Le service de catalogue mappe les types de produits simples, virtuels, téléchargeables et de cartes-cadeaux à `simpleProductViews`.

* Les produits complexes se composent de plusieurs produits simples. Le composant produits simples peut avoir des prix différents. Un produit complexe peut également être défini de sorte que l’acheteur puisse spécifier la quantité de produits simples du composant. Le service de catalogue mappe les types de produits configurables, groupés et groupés à `complexProductViews`.

Les options de produit complexes sont unifiées et distinguées par leur comportement, et non par leur type. Chaque valeur d’option représente un produit simple. Cette valeur d’option donne accès aux attributs de produit simples, y compris le prix. Lorsque l’acheteur sélectionne toutes les options d’un produit complexe, la combinaison des options sélectionnées pointe vers un produit simple spécifique. Le produit simple reste ambigu jusqu’à ce que l’acheteur sélectionne une valeur pour toutes les options disponibles.

#### Attributs de vue du produit

Les produits simples et complexes possèdent des attributs définis par le client qui peuvent être affichés sur le storefront. Ces attributs sont renvoyés sous la forme [ProductViewAttributes](https://developer.adobe.com/commerce/services/graphql/catalog-service/products/#productviewattribute-type). Dans Adobe Commerce, les attributs disponibles sont définis lors de la création du produit. Vous pouvez ajouter des attributs supplémentaires à partir du serveur principal Adobe Commerce ou par programmation. Voir [Extension et personnalisation des données de flux d’exportation de données SaaS](../data-export/extensibility-and-customizations.md).

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

Le processus d&#39;installation nécessite la configuration du connecteur de services Commerce [&#128279;](../landing/saas.md). Une fois cette opération effectuée, l’étape suivante consiste, pour un intégrateur de systèmes, à mettre à jour le code du storefront pour incorporer les requêtes [!DNL Catalog Service]. Toutes les requêtes [!DNL Catalog Service] sont acheminées vers la passerelle GraphQL. L’URL est fournie pendant le processus d’intégration.
