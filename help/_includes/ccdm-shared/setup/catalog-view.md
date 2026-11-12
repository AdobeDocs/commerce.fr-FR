---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 0%
---
<!--This shared include file contains the conceptual and architecture overview of catalog views for Adobe Merchandising Services-->

Une vue de catalogue définit les produits et les prix qu’un client peut récupérer. Il combine des sources de catalogue, des calques de catalogue, des politiques et des livres de prix pour prendre en charge différentes marques, régions, unités commerciales ou canaux.

## Que sont les vues de catalogue ?

Les vues Catalogue définissent l’organisation et l’affichage de votre catalogue de produits. Ils agissent comme des filtres qui déterminent :

- **Quels produits sont visibles** en fonction de la structure de l&#39;entreprise (marques, régions, revendeurs) ?
- **Quel prix est affiché** dans les tarifs liés
- **Comment les produits sont filtrés** à l’aide de politiques (attributs tels que la marque, le modèle, la catégorie)
- **Quelle [source de catalogue](/help/optimizer/setup/catalog-sources.md) est utilisée** en fonction d’attributs tels que les paramètres régionaux ?
- **Qui peut accéder aux données de la vue** via [la protection du catalogue](private-catalog-view.md) et [les clés d&#39;accès restreintes](restricted-access-keys.md)

Par exemple, vous pouvez créer des vues de catalogue distinctes pour :

- Une marque ou une unité opérationnelle
- Une région géographique
- Un revendeur ou un canal partenaire
- Un segment client avec une tarification spécifique

## Aperçu de l’architecture

Les vues de catalogue font partie du framework des services Adobe Merchandising qui remplace le framework de site web, de magasin et de révision utilisé dans les bases d’Adobe Commerce par un modèle plus flexible :

Architecture De ![[!DNL Merchandising Services]](/help/assets/ccdm-shared/setup/merchandising-svcs-architecture.png)

### Fonctionnement

**1. Ingestion de données**
Les données de catalogue d’un serveur principal Adobe Commerce ou d’un autre serveur principal tiers (par exemple, PIM ou ERP) et d’autres systèmes sont ingérées dans la couche de données des services Adobe Merchandising. Chaque SKU contient des informations sur les paramètres régionaux et des attributs de produit qui correspondent aux vues de catalogue, aux politiques et aux paramètres régionaux. Le processus d’ingestion des données dépend du système source et de la méthode d’intégration :

- **Serveur principal Adobe Commerce** : le système exporte les flux du catalogue Commerce, les mappe au format attendu par l’API REST d’ingestion de données et synchronise les données de flux avec la couche de données des services Adobe Merchandising. Dans ce modèle, Adobe Commerce gère la synchronisation initiale et les mises à jour suivantes. Les flux comprennent les produits, les catégories, les attributs de produit, les prix et les catalogues de prix.

- **Serveur principal ou système source tiers**—Un connecteur ou un service d’intégration récupère les données de catalogue de la source, par le biais d’API, d’événements ou de flux d’exportation, puis les mappe et les valide par rapport au schéma de modèle de données de catalogue composable (CCDM) et synchronise les données avec la couche Services Adobe Merchandising à l’aide de l’API REST Data Ingestion. L’intégration est responsable du chargement initial et de l’envoi des modifications ultérieures. Un connecteur spécifique à une plateforme, tel que le connecteur Commerce Adobe [Salesforce](https://experienceleague.adobe.com/fr/docs/commerce/optimizer/developer/salesforce-connector), peut fournir un point de départ.

**2. Catalogue de base unifié**
Les données ingérées créent un catalogue de base unifié dans le pipeline de données du service de catalogue. Cette source unique élimine la duplication des données entre les unités opérationnelles.

**3. Vues du catalogue**
Plusieurs vues de catalogue représentent différentes unités commerciales (par exemple, « Texas Retail », « Texas Retail Seasonal »). Pour plus de flexibilité, les paramètres régionaux, les politiques et les tarifs peuvent être partagés entre les vues de catalogue.

**4. Diffusion Multicanal**
Les données de catalogue filtrées sont diffusées vers des destinations telles que Edge Delivery Services, des marchés, des plateformes publicitaires et des micro-vitrines personnalisées. Pour plus d&#39;informations sur la diffusion des données de catalogue, consultez la [documentation destinée aux développeurs](https://developer.adobe.com/commerce/services/optimizer/).

Lorsque la vue de catalogue **[!UICONTROL Catalog Protection]** est activée, la diffusion vers cette destination nécessite un jeton signé valide d’une [clé d’accès restreint](restricted-access-keys.md) attribuée ; les requêtes non autorisées sont refusées au lieu de recevoir les données de catalogue.

### Composants clés

| Composant | Objectif | Exemple |
|---|---|---|
| **Vue Catalogue** | Unité opérationnelle ou canal de distribution | Réseau de concessionnaires, Boutique régionale |
| **Politique** | Filtre de produit basé sur les attributs | Marque, modèle, catégorie |
| **Paramètre Régional** | Paramètre de langue/région | en-US, fr-CA, es-MX |
| **Catalogue De Prix** | Structure de tarification | Vente au détail, vente en gros, employé |
| **Clé d&#39;accès restreinte** | Informations d’identification de jeton signé qui permettent d’accéder à une vue de catalogue protégée | Clé du portail partenaire, clé de tarification B2B |

### Flux de données

1. **Ingérer** - données de catalogue à partir du serveur principal Adobe Commerce
2. **Processus** - Appliquez des vues de catalogue, des politiques et des prix
3. **Diffuser** - Diffuser le catalogue filtré sur les vitrines, les marchés, etc

## Fonctionnalités clés

| Fonctionnalité | Bénéfice |
|---|---|
| **Catalogue De Base Unique** | Élimination de la duplication des données entre les unités opérationnelles |
| **Tarification flexible** | Plusieurs tarifs par SKU pour différents segments de clientèle |
| **Évolutif** | Gestion efficace de plus de 200 millions de SKU |
| **Multicanal** | Fournir des catalogues aux vitrines, aux marchés et aux plateformes publicitaires |
| **Mises à jour en temps réel** | Mise à jour rapide des données de catalogue pour les promotions et les campagnes |
| **Vues de catalogue privé** | Restreindre une vue de catalogue aux clients autorisés à l’aide de la validation de jeton signé |

## Cas d’utilisation

### Conglomérat multimarque

**Défi** : gérer plusieurs marques, pays et langues<br>
**Solution** : catalogue unique avec vues de catalogue pour chaque combinaison marque/région

### Concessionnaire de pièces automobiles

**Défi** : 3 000 revendeurs proposant les mêmes produits mais des prix différents<br>
**Solution** : un catalogue avec vues de catalogue et livres de prix spécifiques au concessionnaire

### Retailer multi-emplacement

**Défi** : prix et stock différents par emplacement<br>
**Solution** : vues de catalogue basées sur l’emplacement avec des politiques spécifiques à la région

>[!NOTE]
>
>Pour plus d’informations sur l’ingestion et la diffusion des données de catalogue, consultez la [documentation destinée aux développeurs](https://developer.adobe.com/commerce/services/optimizer/).
