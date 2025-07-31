---
title: Vue Catalogue
description: Découvrez les vues de catalogue et comment les créer pour organiser votre catalogue de produits par structure d’entreprise, politiques et prix.
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
exl-id: 76c1b81c-b456-4334-89bd-6027308cbc47
source-git-commit: 2e47c770d204c9c7f959893704dd0ebcc6ac792a
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 0%

---


# Vues de catalogue pour les services de marchandisage

Les vues de catalogue constituent la base des services de marchandisage de Adobe Commerce Optimizer. Elles vous permettent d’organiser votre catalogue de produits par structure d’entreprise, politiques et prix. Ce modèle de données flexible prend en charge des scénarios multimarques, multiservices et multilingues tout en préservant l’efficacité opérationnelle.

## Que sont les vues de catalogue ?

Les vues Catalogue définissent l’organisation et l’affichage de votre catalogue de produits. Ils agissent comme des filtres qui déterminent :

- **Quels produits sont visibles** en fonction de la structure de l’entreprise (marques, régions, revendeurs) ?
- **Quel prix est affiché** via les livres de prix liés
- **Comment les produits sont filtrés** à l’aide de politiques (attributs tels que la marque, le modèle, la catégorie)
- **Quelle source de catalogue est utilisée** en fonction d’attributs tels que les paramètres régionaux ?

Considérez les vues de catalogue comme différentes « lentilles » à travers lesquelles les clients voient votre catalogue. Par exemple :

- Une vue de catalogue de revendeurs peut afficher uniquement les produits disponibles pour ce revendeur spécifique
- Une vue de catalogue régionale peut afficher des produits et des prix spécifiques à une zone géographique
- Une vue de catalogue de marques peut afficher uniquement les produits d’une marque particulière

## Création d’une vue de catalogue

Dans cette section, créez une vue de catalogue, sélectionnez une [politique](policies.md) et un [catalogue](pricebooks.md).

Avant de créer une vue de catalogue, vérifiez que vous disposez des éléments suivants :

- [Politiques créées](policies.md) pour définir des filtres de produit

- [Catalogues de prix ingérés](pricebooks.md) pour la tarification

1. Dans le menu de gauche, accédez à _Configuration du magasin_ , puis cliquez sur **[!UICONTROL Catalog views]**.

1. Cliquez sur **[!UICONTROL Create catalog view]**. &#x200B;

1. Configurez les détails de la vue Catalogue :

   - **Nom** : saisissez le nom de la vue du catalogue, par exemple `Celport`. &#x200B;
   - **Sources de catalogue** : sélectionnez la source du catalogue (paramètres régionaux), par exemple `en-US`.
   - **Politiques** : utilisez la liste déroulante pour sélectionner les politiques appropriées. Par exemple, « Marque », « Modèle ». &#x200B;Vérifiez que vous avez déjà [créé une politique](policies.md).

1. Sélectionnez le catalogue à lier à la vue du catalogue.

   - **Utiliser tous les tarifs disponibles**-Cette option extrait les données de tarification de tous les tarifs disponibles.
   - **Autoriser uniquement les catalogues de prix sélectionnés**-Cette option affiche la boîte de dialogue **Ajouter des catalogues de prix autorisés** dans laquelle vous pouvez sélectionner le catalogue spécifique à utiliser pour la vue catalogue.
   - **Désactiver le prix**-Cette option n’est pas disponible pour le moment.

1. Cliquez sur **[!UICONTROL Add]** pour créer la vue du catalogue avec les tarifs et les politiques associés.

La page Vues du catalogue se met à jour pour afficher la nouvelle vue du catalogue&#x200B;

Une fois ces étapes terminées, la vue de catalogue est maintenant configurée pour afficher les produits et les prix en fonction des sources et des politiques sélectionnées.

## Aperçu de l’architecture

Les vues de catalogue font partie de la structure des services de marchandisage qui remplace la structure du site web, du magasin et du magasin utilisée dans les bases d’Adobe Commerce par un modèle plus flexible :

![[!DNL Merchandising Services] Architecture ](../assets/merchandising-svcs-architecture.png)

### Fonctionnement

**1. Ingestion de données**
Les données de catalogue provenant de PIM, ERP et d’autres systèmes sont ingérées dans le framework de services de marchandisage. Chaque SKU contient des informations sur les paramètres régionaux et des attributs de produit qui correspondent aux vues de catalogue, aux politiques et aux paramètres régionaux. Pour plus d’informations sur l’ingestion de données, consultez la [documentation destinée aux développeurs](https://developer.adobe.com/commerce/services/optimizer/).

**2. Catalogue de base unifié**
Les données ingérées créent un catalogue de base unifié dans le pipeline de données du service de catalogue. Cette source unique élimine la duplication des données entre les unités opérationnelles.

3 **. Vues du catalogue**
Plusieurs vues de catalogue représentent différentes unités commerciales (par exemple, « Texas Retail », « Texas Retail Seasonal »). Pour plus de flexibilité, les paramètres régionaux, les politiques et les tarifs peuvent être partagés entre les vues de catalogue.

4 **. Diffusion Multicanal**
Les données de catalogue filtrées sont diffusées vers diverses destinations, notamment les vitrines Edge Delivery Services, les marchés, les plateformes publicitaires et les micro-vitrines personnalisées. Pour plus d’informations sur la diffusion des données de catalogue, consultez la [documentation destinée aux développeurs](https://developer.adobe.com/commerce/services/optimizer/).

### Composants clés

| Composant | Objectif | Exemple |
|---|---|---|
| **Vue Catalogue** | Unité opérationnelle ou canal de distribution | Réseau de concessionnaires, Boutique régionale |
| **Politique** | Filtre de produit basé sur les attributs | Marque, modèle, catégorie |
| **Paramètres régionaux** | Paramètre de langue/région | en-US, fr-CA, es-MX |
| **Prix catalogue** | Structure de tarification | Vente au détail, vente en gros, employé |

### Flux de données

1. **Ingest** - Données de produit des systèmes PIM/ERP
2. **Processus** - Appliquez des vues de catalogue, des politiques et des prix.
3. **Diffuser** - Diffuser le catalogue filtré aux vitrines, aux marchés, etc.

## Fonctionnalités clés

| Fonctionnalité | Bénéfice |
|---|---|
| **Catalogue à base unique** | Élimination de la duplication des données entre les unités opérationnelles |
| **Tarification flexible** | Plusieurs tarifs par SKU pour différents segments de clientèle |
| **Évolutive** | Gestion efficace de plus de 200 millions de SKU |
| **Multicanal** | Fournir des catalogues aux vitrines, aux marchés et aux plateformes publicitaires |
| **Mises à jour en temps réel** | Mise à jour rapide des données de catalogue pour les promotions et les campagnes |

## Cas d’utilisation

### Conglomérat multimarque

**Défi** : gérez plusieurs marques, pays et langues<br>
**Solution** : catalogue unique avec vues de catalogue pour chaque combinaison marque/région

### Concessionnaire de pièces automobiles

**Défi** : 3 000 concessionnaires avec les mêmes produits mais des prix différents<br>
**Solution** : Un catalogue avec vues de catalogue et livres de prix spécifiques au concessionnaire

### Retailer multi-emplacement

**Défi** : Différents prix et stocks par emplacement<br>
**Solution** : vues de catalogue basées sur l’emplacement avec des politiques spécifiques à la région

>[!INFO]
>
>Pour plus d’informations sur l’ingestion et la diffusion des données de catalogue, consultez la [documentation destinée aux développeurs](https://developer.adobe.com/commerce/services/optimizer/).
