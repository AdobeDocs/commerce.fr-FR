---
title: Présentation de [!DNL Merchandising Services]
description: Découvrez comment  [!DNL Merchandising Services]  pour Adobe Commerce vous aide à configurer votre catalogue en fonction de votre modèle commercial et de votre stratégie de mise sur le marché
recommendations: noCatalog
exl-id: afa7c148-10fb-4161-8bcc-13084f85c42c
source-git-commit: 31270ceac79977b6ecdf8043b0c162031d129de7
workflow-type: tm+mt
source-wordcount: '1664'
ht-degree: 0%

---

# Présentation de [!DNL Merchandising Services]

Un catalogue de produits est essentiel pour les expériences d’achat en ligne, ce qui permet aux clients de parcourir, de rechercher et d’effectuer des achats. Pour l&#39;efficacité opérationnelle, un catalogue de produits doit refléter fidèlement la structure de l&#39;entreprise. Les entreprises doivent souvent vendre leurs produits à des prix variables en fonction du marché géographique, du canal de distribution, du segment de clientèle et d&#39;autres variables. Pour ce faire, une plateforme d’e-commerce doit offrir un modèle de données de catalogue flexible qui permet aux entreprises de produire des variantes de leur catalogue adaptées à ces scénarios. Adobe répond à ces besoins en proposant des services de marchandisage optimisés par des canaux et des politiques. Les services de marchandisage fournissent des blocs de création que les commerçants peuvent utiliser pour créer et gérer des catalogues à grande échelle. Cela permet aux entreprises de configurer des catalogues qui s’alignent sur leur structure commerciale et leurs stratégies de mise sur le marché.

À un niveau élevé, avec les services de marchandisage, vous pouvez :

- Utilisez un catalogue de base unique pour tous les besoins de votre entreprise. Faites évoluer rapidement votre catalogue sur de nouvelles marques, de nouveaux marchés, de nouvelles unités commerciales, de nouveaux canaux de mise sur le marché et de nouveaux segments de clientèle, sans avoir à procéder à une refonte complète de l’architecture. Cela élimine la duplication des données et configure votre plateforme e-commerce pour une efficacité opérationnelle élevée.
- Déverrouillez la syndication du catalogue et diffusez le contenu approprié en concevant votre catalogue de produits de manière à refléter votre activité, notamment les produits, les clients, les prix et la distribution.
- Ingérez et mettez à jour rapidement les données de catalogue et diffusez rapidement les mises à jour sur le storefront pour vos promotions et besoins de campagne.
- Obtenez des scores lighthouse parfaits avec des composants d’interface utilisateur prêts à l’emploi et ultra-rapides optimisés par Edge Delivery Services pour une navigation transparente et des recommandations de produits.
- Adoptez une architecture composable moderne à l’aide de l’architecture d’extensibilité d’Adobe ([App Builder](https://experienceleague.adobe.com/fr/playlists/commerce-get-started-app-builder-development)) pour importer des données de produit et alimenter les storefronts de commerce découplé à l’aide d’Adobe [maillage API](https://experienceleague.adobe.com/fr/playlists/commerce-get-started-app-builder-and-api-mesh).

>[!INFO]
>
>Pour en savoir plus sur les API disponibles dans les services de marchandisage optimisés par les canaux et les politiques, consultez la [documentation pour les développeurs](https://developer-stage.adobe.com/commerce/services/composable-catalog).

## Architecture

Les services de marchandisage optimisés par les canaux et les politiques constituent un modèle de données de catalogue hautement évolutif et flexible qui permet de déverrouiller facilement des cas d’utilisation multimarques, multiservices et multilingues. Ce modèle remplace l’utilisation des portées de produit Adobe Commerce classiques (site web, boutique, révision) par de nouvelles portées de produit Services de marchandisage (canal, politique et paramètres régionaux).

Le diagramme suivant offre une vue d’ensemble de la structure de marchandisage.

![[!DNL Merchandising Services] Architecture ](assets/merchandising-svcs-architecture.png)

En haut de ce diagramme, les données de catalogue (PIM, ERP, etc.) sont ingérées dans le framework des services de marchandisage. Ces données de catalogue contiennent des SKU. Chaque SKU contient des détails de portée (paramètres régionaux) et des attributs de produit, qui correspondent aux nouvelles portées de produit de services de marchandisage (canaux, politiques et paramètres régionaux).

Lorsque toutes ces données sont ingérées dans le framework de marchandisage, un nouveau catalogue de base unifié est disponible dans le pipeline de données du service de catalogue. Dans la partie suivante du diagramme, vous voyez plusieurs canaux. Chaque canal représente une unité opérationnelle. Par exemple, *commerce de détail au Texas*, *commerce de détail saisonnier au Texas* etc. Comme vous pouvez le voir dans le diagramme, les paramètres régionaux, les politiques et les tarifs peuvent tous être partagés sur l’ensemble des canaux&#x200B;

Enfin, le diagramme montre comment ces données de catalogue distinctes peuvent être affichées à divers emplacements, tels qu’un storefront Edge Delivery Services, un marketplace, un canal publicitaire, un micro-storefront personnalisé, etc.

Pour découvrir comment ingérer vos données de catalogue dans le marchandisage à l’aide de l’API d’ingestion des données de catalogue et comment configurer vos paramètres régionaux, politiques et tarifs à l’aide de l’API de gestion de catalogue et de règles, consultez la [documentation destinée aux développeurs](https://developer-stage.adobe.com/commerce/services/composable-catalog/).

Pour en savoir plus sur les concepts qui constituent les services de marchandisage, consultez les sections suivantes.

## Gestion de catalogue de produits

La gestion des catalogues de produits englobe deux aspects distincts : les données de produit et le contexte de produit. Les Services de Marchandisage respectent la séparation de ces fonctions, offrant une gestion indépendante pour chacune.

- **Données sur les produits** - Quel produit est vendu et à quel prix ?
- **Product Context** - Qui vend à qui et où ?

![[!DNL Merchandising Services] aspects ](assets/merchandising-svcs-parts.png)

### Données de produit

Les données de produit comprennent les types suivants :

- **Produits** - SKU individuels ou ensembles de SKU qui représentent des biens physiques ou des services intangibles avec des attributs qui représentent le produit, notamment la description, le poids, la taille, les dimensions, etc. Les attributs spécifient également le canal et les portées de politique pour un SKU. Les produits peuvent être regroupés en différents types de produits, tels que simples, configurables, groupés, groupés de groupements, abonnements, etc.
- **Métadonnées** - Les métadonnées d’attributs de produit définissent et gèrent la manière dont les attributs de produit sont affichés sur le storefront dans les listes de produits, les pages de détails, les résultats de recherche, etc. Les métadonnées définissent également la manière dont les attributs de produit sont utilisés dans la recherche : tri, filtrage, poids de la recherche, etc.
- **Prix et livres** - Détermine les prix de vente des produits. Dans les services de marchandisage, un SKU de produit et un prix sont découplés. Vous pouvez donc définir plusieurs carnets de prix pour un seul SKU. En découplant les prix du SKU, vous pouvez déverrouiller les prix spécifiques à la portée pour différents niveaux de clients, unités commerciales et zones géographiques. Vous pouvez définir des prix réguliers et réduits et gérer tout cela à grande échelle.
- **Assets** - Artefacts associés à des produits, tels que des images, des vidéos, des fichiers PDF ou d’autres types de fichiers (future feuille de route).

### Gestion du contexte du produit

La gestion du contexte produit couvre les aspects suivants :

- **Canal** - Le canal de distribution définit le chemin par lequel une entreprise souhaite vendre des produits. Un canal est l’abstraction de plus haut niveau qui encapsule les paramètres régionaux et les politiques.
   - Exemple : Concessionnaires pour l&#39;industrie automobile. Filiales de conglomérats multimarques. Lieu de fabrication des fournisseurs.
- **Politique** - Filtre d’accès aux données qui vous permet de diffuser le contenu approprié à la destination appropriée. Ce concept offre des fonctionnalités de syndication de catalogue.
   - Exemple : magasins physiques de point de vente, places de marché, pipelines de publicités (Google, Facebook, Instagram)
- **Portée** - Représente la langue (paramètre régional) des catalogues, par exemple `en-US`. La portée est définie au niveau du SKU lors de l’ingestion des données de catalogue.

Lors de l’ingestion et de la mise à jour des données de produit, un SKU contient les détails des portées et des attributs (les attributs mappent aux canaux et aux politiques). Ils définissent les identifiants de contexte de produit auxquels appartient un SKU :

![[!DNL Merchandising Services] les identifiants de contexte de produit](assets/merchandising-svcs-product-id.png)

Dans l’image ci-dessus, chaque SKU fournit :

- Identifiants d’étendue&#x200B;
   - Paramètre régional : obligatoire&#x200B;
- Attributs de produit
   - Les attributs de produit sont utilisés pour mapper les canaux et politiques appropriés&#x200B;
   - Exemple : en tant que constructeur automobile, vous pouvez choisir de créer une combinaison de canal et de politique pour les attributs de produit : (1) Concessionnaires (2) Marques de voitures&#x200B;
- Prix et registres des prix attribués
   - Chaque SKU peut avoir plusieurs prix définis à l’aide de plusieurs répertoires de prix.
   - Exemple : Vous offrez aux employés un prix régulier réduit sur les pièces automobiles avec une remise supplémentaire de 25 %. Vous proposez aux clients de VIP un prix normal plus élevé avec une remise de 10 %. Les informations sur le prix de la SKU du produit garantissent que le bon prix s’affiche pour chaque segment client.

Les définitions de canal et de politique sont créées à l’aide d’API dédiées :

Mappage ![[!DNL Merchandising Services] canal, de politique et de portée](assets/merchandising-svcs-scope-map.png)

- **Portée** (paramètres régionaux) - Définie au niveau du SKU lors de l’ingestion des données de produit&#x200B;
- **Canal** - Définition créée à l’aide d’API dédiées. &#x200B;
- **Politique** - Définition créée à l’aide d’API dédiées.

## Fonctionnalités clés

| Fonctionnalités clés | Bénéfice |
|---|---|
| **Ingestion directe des données de catalogue dans le pipeline des services de storefront** : ingérez vos données de catalogue directement dans le pipeline des services de catalogue pour le cycle de vie de navigation et de recherche du storefront (page d’affichage des produits, page de liste des produits, page des résultats de recherche, etc.). | <ul><li>Ingérez directement des données de catalogue dans le pipeline de service storefront qui alimente : le service de catalogue, la découverte de produits (recherche en direct) et les recommandations de produits. Vous pouvez ainsi diffuser des mises à jour de catalogue à grande échelle pour des millions de SKU. Cela permet de déverrouiller la gestion des promotions à grande échelle sensibles au facteur temps. </li></ul> |
| **Nouvelles portées de produits du catalogue** : le canal, la politique et la portée sont de nouvelles portées de produits introduites par les services de marchandisage. Ces étendues de produit remplacent les étendues du site web, du magasin et de l’espace de stockage dans la couche de services de storefront. [En savoir plus](#product-context-management). | <ul><li>Grâce aux nouvelles portées, les services de marchandisage vous permettent de vous adapter facilement à des cas d’utilisation multi-géographie, multi-unités commerciales, multi-marques et multilingues à l’aide d’un seul catalogue de base.</li><li>Élimination de la redondance de données dans la gestion de catalogues.</li></ul> |
| **Évoluer vers des dizaines de millions de SKU** | Déverrouillez la gestion de catalogue à grande échelle. Vous pouvez ainsi ingérer et gérer facilement plus de 200MM SKU. |
| **Prise en charge des types de produits** | <ul><li>Simple, configurable</li><li>Lots et lots de lots (future feuille de route)</li><li>Abonnements et plans (future feuille de route)</li></ul> |
| **Commerce découplé** | <ul><li>Prise en charge complète des implémentations de commerce découplé par le biais du service de catalogue, de la découverte de produits (recherche en direct) et des API de recommandations de produits.</li></ul> |
| **Composants d’IU modernes et ultra-rapides** | <ul><li>Prise en charge des composants de l’interface utilisateur prêts à l’emploi pour la recherche de produits et les recommandations de produits.</li><li>Les composants de l’interface utilisateur sont extensibles et flexibles afin qu’ils puissent être utilisés à la fois par le service Edge Delivery d’Adobe et par toute autre mise en œuvre de storefront.</li></ul> |

## Quel type de commerçant bénéficie le plus des Services de Marchandisage ?

Le tableau suivant met en évidence les défis courants rencontrés par les commerçants et la manière dont les services de marchandisage optimisés par les canaux et les politiques les relèvent.

| Type de commerçant | Cas d’utilisation | Problèmes résolus |
|---|---|---|
| Conglomérat multimarque | <ul><li>Ils vendent plusieurs marques</li><li>Elles se vendent dans plusieurs pays</li><li>Elles se vendent dans différentes langues</li></ul> | Utilisez un catalogue unifié de base unique et atteignez l’efficacité opérationnelle tout en vous étendant à plusieurs marques, zones géographiques et langues. |
| Conglomérat de pièces automobiles/de fabrication | <ul><li>Vend des pièces d&#39;auto ou de machine. Les produits sont les mêmes pour tous les clients.</li><li>Différents concessionnaires vendent des pièces aux clients</li><li>Chaque concessionnaire a ses propres prix, stocks et modes d&#39;expédition</li></ul> | Pour disposer de différentes intégrations d’expédition, chaque concessionnaire doit disposer d’un site web distinct. Cependant, des sites web distincts forcent le modèle de données de catalogue type à dupliquer les données. Ainsi, s&#39;il y a 3000 revendeurs aux États-Unis, un marchand crée 3000 copies de catalogue même si le même catalogue est utilisé par tous les revendeurs. Cette duplication des données interfère avec les limites de performances. Les services de marchandisage éliminent la duplication des données. |
| Entreprise d&#39;emballage/logistique | <ul><li>Ils disposent de plusieurs lieux d’expédition</li><li>Ils ont un prix différent pour chaque client</li><li>Le même produit disponible dans 2 sites pour 2 clients ont 4 prix possibles</li></ul> | Malgré l’utilisation de groupes de clients pour couvrir le prix par client, le modèle de données de catalogue standard n’a pas la capacité de gérer le prix par emplacement. De plus, les commerçants veulent des règles de visibilité uniques par emplacement/site web. La gestion de ces règles complexes de prix et de visibilité peut être déverrouillée à grande échelle avec les services de marchandisage. |

### Que faire ensuite

- Ingérez des données dans les services de marchandisage à l’aide de l’API [data ingestion](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/using-the-api/).
- Gérez votre catalogue et définissez les canaux, politiques et portées à l’aide de l’API [catalog management](https://developer-stage.adobe.com/commerce/services/composable-catalog/admin/using-the-api/)
- [Suivez un tutoriel](https://developer-stage.adobe.com/commerce/services/composable-catalog/merchandising-services-use-case/) qui montre comment une entreprise disposant d’un seul catalogue de base peut utiliser les API Merchandising Services pour ajouter des données de produit, définir des catalogues à l’aide de projections et récupérer les données du catalogue à afficher dans un storefront découplé.
