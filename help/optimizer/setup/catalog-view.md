---
title: Vues du catalogue
description: Découvrez les vues de catalogue et comment les créer pour organiser votre catalogue de produits par structure d’entreprise, politiques et prix.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et  [!DNL Adobe Commerce Optimizer]  (infrastructure SaaS gérée par Adobe)."
exl-id: 76c1b81c-b456-4334-89bd-6027308cbc47
TQID: https://experienceleague.adobe.com/Jmze0Pq3kSNMIXqkkML-hmmlZnv-XKgeEgRB8Q8NZ6s
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
nudge: true
source-git-commit: 42c252f70f6ed1d7a5c1fd2832324308294da264
workflow-type: tm+mt
source-wordcount: 1317
ht-degree: 0%

---

# Vues de catalogue pour les services de marchandisage

Une vue de catalogue définit les produits et les prix qu’un client peut récupérer. Il combine des sources de catalogue, des calques de catalogue, des politiques et des livres de prix pour prendre en charge différentes marques, régions, unités commerciales ou canaux.

## Que sont les vues de catalogue ?

Les vues Catalogue définissent l’organisation et l’affichage de votre catalogue de produits. Ils agissent comme des filtres qui déterminent :

- **Quels produits sont visibles** en fonction de la structure de l’entreprise (marques, régions, revendeurs) ?
- **Quel prix est affiché** via les livres de prix liés
- **Comment les produits sont filtrés** à l’aide de politiques (attributs tels que la marque, le modèle, la catégorie)
- **Qu’est-ce que [source du catalogue](catalog-sources.md) est utilisé** en fonction d’attributs tels que les paramètres régionaux
- **Qui peut accéder aux données de la vue** via [Protection du catalogue](private-catalog-view.md) et [clés d’accès restreintes](restricted-access-keys.md)

Par exemple, vous pouvez créer des vues de catalogue distinctes pour :

- Une marque ou une unité opérationnelle
- Une région géographique
- Un revendeur ou un canal partenaire
- Un segment client avec une tarification spécifique

## Création d’une vue de catalogue

Avant de créer une vue de catalogue, préparez les éléments suivants selon les besoins :

- Une [source de catalogue](catalog-sources.md)
- [Politiques](policies.md) qui définissent des filtres de produit
- [Calques de catalogue](catalog-layer.md) si vous devez remplacer les attributs de produit
- [Classeurs de prix](pricebooks.md) pour le prix affiché dans la vue
- [Clés d’accès limitées](restricted-access-keys.md) si vous souhaitez créer une vue de catalogue privée

### Configuration

Dans cette section, créez une vue de catalogue, sélectionnez une [politique](policies.md) et un [catalogue](pricebooks.md).

1. Dans le menu de gauche, accédez à **[!UICONTROL Store setup]**, puis cliquez sur **[!UICONTROL Catalog views]**.

1. Cliquez sur **[!UICONTROL Create catalog view]**. &#x200B;

1. Configurez les détails de la vue Catalogue :

   - **Nom** : saisissez le nom de la vue du catalogue, par exemple `Celport`. &#x200B;
   - **Sources de catalogue** : sélectionnez la [source de catalogue](catalog-sources.md) par exemple `en-US`.
   - **Calques de catalogue** : passez en revue les calques ingérés et leur priorité.
   - **Politiques** : utilisez la liste déroulante pour sélectionner les politiques appropriées. Par exemple, « Marque », « Modèle ». &#x200B;Vérifiez que vous avez déjà [créé une politique](policies.md).

1. Sélectionnez le catalogue à lier à la vue du catalogue.

   - **Utiliser tous les tarifs disponibles** : cette option extrait les données de tarification de tous les tarifs disponibles.
   - **Autoriser les tarifs catalogue sélectionnés uniquement** : cette option affiche la boîte de dialogue **Ajouter des tarifs catalogue autorisés**. Utilisez cette boîte de dialogue pour sélectionner le catalogue de prix spécifique à utiliser pour la vue Catalogue.
   - **Livre de prix unique uniquement** : sélectionnez cette option si un seul livre de prix s&#39;applique. Cette option est obligatoire si vous souhaitez configurer une vue de catalogue privée, qui ne peut référencer qu&#39;un seul catalogue. Voir [Restriction du catalogue des prix sur les vues de catalogue privé](private-catalog-view.md#price-book-restriction-on-private-catalog-views).
   - **Désactiver la tarification**—Cette option n&#39;est pas disponible pour le moment.

   >[!NOTE]
   >
   >Un ID de catalogue des prix contrôle la tarification demandée. Cela ne limite pas l’accès à la vue Catalogue. Pour restreindre l’accès, activez la protection du catalogue pour créer une [vue de catalogue privée](private-catalog-view.md).

1. (Facultatif) Activez/désactivez le **[!UICONTROL Catalog Protection]** pour **[!UICONTROL Enabled]** de restreindre les données de cette vue de catalogue aux clients disposant d’un jeton signé valide. Voir [Protection d’une vue de catalogue](private-catalog-view.md#protect-a-catalog-view) pour connaître les étapes de configuration.

1. Cliquez sur **[!UICONTROL Add]** pour créer la vue du catalogue avec les tarifs et les politiques associés.

La page Vues du catalogue se met à jour pour afficher la nouvelle vue du catalogue&#x200B;

Une fois ces étapes terminées, la vue de catalogue est maintenant configurée pour afficher les produits et les prix en fonction des sources et des politiques sélectionnées.

### Spécification des vues de catalogue pour les recommandations et les règles de découverte de produits

Vous pouvez définir une vue de catalogue lorsque vous [créez des unités de recommandation](../merchandising/recommendations/create.md) ou [&#x200B; des règles de marchandisage](../merchandising/rules/add.md).

## Calques de catalogue

Les calques de catalogue vous permettent de remplacer les attributs de produit sélectionnés sans modifier les données du catalogue source. Utilisez des calques pour personnaliser les noms, les descriptions, les images, les liens ou les métadonnées d’une vue de catalogue.

Voir [&#x200B; Calques de catalogue &#x200B;](catalog-layer.md).

## Rendre une vue de catalogue privée

Par défaut, une vue de catalogue est publique pour les applications clientes qui peuvent accéder à l’API de marchandisage GraphQL. Pour restreindre l’accès, configurez une vue de catalogue privé en activant **[!UICONTROL Catalog Protection]**.

Pour savoir comment protéger une vue de catalogue et vérifier que l’accès est appliqué, consultez [Vues de catalogue privé](private-catalog-view.md).

## Gestion des vues de catalogue

Pour mettre à jour ou afficher les propriétés des vues de catalogue existantes, suivez ces instructions.

### Modifier une vue de catalogue

1. Dans l’espace de travail **[!UICONTROL Catalog views]**, recherchez la vue du catalogue.
1. Pour ouvrir le menu d’actions, sélectionnez (**[!UICONTROL ...]**).
1. Sélectionnez **[!UICONTROL Edit]** pour accéder à l’éditeur de vue de catalogue.
1. Mettez à jour le nom, les sources de catalogue, les politiques, les informations sur le catalogue et les paramètres de **[!UICONTROL Catalog Protection]** (y compris les clés d’accès restreint affectées) si nécessaire.
1. Cliquez sur **[!UICONTROL Save]**.

### Suppression d’une vue de catalogue

1. Dans l’espace de travail **[!UICONTROL Catalog views]**, recherchez la vue du catalogue.
1. Pour ouvrir le menu d’actions, sélectionnez (**[!UICONTROL ...]**).
1. Sélectionnez **[!UICONTROL Delete]**.
1. Confirmez la suppression.

   Lorsque la boîte de dialogue de confirmation s’affiche, cliquez sur **[!UICONTROL Delete]**.

### Afficher les détails de la vue Catalogue

Cette option permet d’afficher rapidement tous les paramètres de la vue de catalogue, tout en restant sur la table **[!UICONTROL Catalog views]**.

Dans l’espace de travail **[!UICONTROL Catalog views]**, sélectionnez l’icône ![informations](../assets/info-icon.png) d’une vue de catalogue pour afficher ses détails de configuration.

![Vue catalogue - Détails](../assets/catalog-view-details.png)

De là, vous pouvez voir les détails de configuration de la vue de catalogue, tels que :

- Afficher l’ID
- Nom
- Sources de catalogue
- Politiques
- Date de création
- Données modifiées

Certains de ces paramètres de configuration sont nécessaires lorsque vous configurez votre storefront ou que vous utilisez l’API d’ingestion de données.

## Aperçu de l’architecture

Les vues de catalogue font partie de la structure des services de marchandisage qui remplace la structure du site web, du magasin et du magasin utilisée dans les bases d’Adobe Commerce par un modèle plus flexible :

![[!DNL Merchandising Services] Architecture &#x200B;](../assets/merchandising-svcs-architecture.png)

### Fonctionnement

**1. Ingestion de données**
Les données de catalogue provenant de PIM, ERP et d’autres systèmes sont ingérées dans le framework de services de marchandisage. Chaque SKU contient des informations sur les paramètres régionaux et des attributs de produit qui correspondent aux vues de catalogue, aux politiques et aux paramètres régionaux. Pour plus d’informations sur l’ingestion de données, consultez la [documentation destinée aux développeurs](https://developer.adobe.com/commerce/services/optimizer/).

**2. Catalogue de base unifié**
Les données ingérées créent un catalogue de base unifié dans le pipeline de données du service de catalogue. Cette source unique élimine la duplication des données entre les unités opérationnelles.

**3. Vues du catalogue**
Plusieurs vues de catalogue représentent différentes unités commerciales (par exemple, « Texas Retail », « Texas Retail Seasonal »). Pour plus de flexibilité, les paramètres régionaux, les politiques et les tarifs peuvent être partagés entre les vues de catalogue.

**4. Diffusion Multicanal**
Les données de catalogue filtrées sont diffusées vers des destinations telles que Edge Delivery Services, des marchés, des plateformes publicitaires et des micro-vitrines personnalisées. Pour plus d’informations sur la diffusion des données de catalogue, consultez la [documentation destinée aux développeurs](https://developer.adobe.com/commerce/services/optimizer/).

Lorsqu’une vue de catalogue a **[!UICONTROL Catalog Protection]** activée, la diffusion vers cette destination nécessite un jeton signé valide d’une [clé d’accès restreint](restricted-access-keys.md) attribuée ; les requêtes non autorisées sont refusées au lieu de recevoir les données de catalogue.

### Composants clés

| Composant | Objectif | Exemple |
|---|---|---|
| **Vue Catalogue** | Unité opérationnelle ou canal de distribution | Réseau de concessionnaires, Boutique régionale |
| **Politique** | Filtre de produit basé sur les attributs | Marque, modèle, catégorie |
| **Paramètres régionaux** | Paramètre de langue/région | en-US, fr-CA, es-MX |
| **Prix catalogue** | Structure de tarification | Vente au détail, vente en gros, employé |
| **Clé d’accès restreinte** | Informations d’identification de jeton signé qui permettent d’accéder à une vue de catalogue protégée | Clé du portail partenaire, clé de tarification B2B |

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
| **Vues de catalogue privé** | Restreindre une vue de catalogue aux clients autorisés à l’aide de la validation de jeton signé |

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

>[!NOTE]
>
>Pour plus d’informations sur l’ingestion et la diffusion des données de catalogue, consultez la [documentation destinée aux développeurs](https://developer.adobe.com/commerce/services/optimizer/).

## Plus comme ceci

- [Sources de catalogue](catalog-sources.md) : définissez la portée faisant autorité des produits, attributs et catégories pour le comportement de recherche, de filtrage et de tri
- [Calques de catalogue](catalog-layer.md) : découvrez comment modifier les données d’un produit sans modifier la source d’origine.
- [Vues de catalogue privées](private-catalog-view.md) : créez une vue de catalogue privée pour restreindre l&#39;accès aux clients autorisés
- [Clés d&#39;accès restreint](restricted-access-keys.md) : créez, attribuez et faites pivoter les clés utilisées pour signer les jetons pour la protection du catalogue
- [Politiques](policies.md) : créez des politiques pour filtrer les produits dans les vues de catalogue
- [Classeurs de prix](pricebooks.md) : gérez les structures de prix pour différents segments de clientèle
