---
title: Vues du catalogue
description: Découvrez les vues de catalogue et comment les créer pour organiser votre catalogue de produits par structure d’entreprise, politiques et prix.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et [!DNL Adobe Commerce Optimizer] (infrastructure SaaS gérée par Adobe)."
exl-id: 76c1b81c-b456-4334-89bd-6027308cbc47
TQID: https://experienceleague.adobe.com/Jmze0Pq3kSNMIXqkkML-hmmlZnv-XKgeEgRB8Q8NZ6s
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
    internal-label: Optimization
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
nudge: true
source-git-commit: d081e975b03805a0f46d5194f8c3cd46e3c86839
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 0%
---
# Vues de catalogue pour les services de marchandisage

{{$include /help/_includes/ccdm-shared/setup/catalog-view.md}}

## Gestion des vues de catalogue

Suivez ces instructions pour gérer les vues de catalogue :

- [Créer une vue de catalogue](#create-a-catalog-view) : définissez le nom, la source du catalogue, les politiques et le catalogue des prix. Ensuite, [spécifiez la vue de catalogue pour les recommandations et les règles de découverte de produits](#specify-catalog-views-for-recommendations-and-product-discovery-rules), passez en revue les [couches de catalogue](#catalog-layers) qui remplacent les attributs de produit ou [rendez la vue de catalogue privée](#make-a-catalog-view-private).
- [Modifier une vue de catalogue](#edit-a-catalog-view)—Mettre à jour ses sources, ses politiques, son catalogue de prix et ses paramètres de protection.
- [Supprimer une vue de catalogue](#delete-a-catalog-view)—Supprimez une vue de catalogue dont vous n&#39;avez plus besoin.
- [Afficher les détails de la vue Catalogue](#view-catalog-view-details)—Examinez la configuration d&#39;une vue Catalogue à partir du tableau Vues Catalogue.

### Création d’une vue de catalogue

Avant de créer une vue de catalogue, préparez les éléments suivants selon les besoins :

- Une [source de catalogue](catalog-sources.md)
- [Politiques](policies.md) qui définissent des filtres de produit
- [Calques de catalogue](catalog-layer.md) si vous devez remplacer les attributs de produit
- [Tarifs](pricebooks.md) pour le prix affiché dans la vue
- [Clés d&#39;accès restreintes](restricted-access-keys.md) si vous souhaitez créer une vue de catalogue privée

#### Configuration

Dans cette section, vous créez une vue de catalogue, sélectionnez une [politique](policies.md) et un [catalogue de prix](pricebooks.md).

1. Dans le menu de gauche, accédez à **[!UICONTROL Store setup]**, puis cliquez sur **[!UICONTROL Catalog views]**.

1. Cliquez sur **[!UICONTROL Create catalog view]**. &#x200B;

1. Configurez les détails de la vue Catalogue :

   - **Nom** : saisissez le nom de la vue du catalogue, par exemple `Celport`. &#x200B;
   - **Sources de catalogue** : sélectionnez la [source de catalogue](catalog-sources.md), par exemple `en-US`.
   - **Calques du catalogue** : passez en revue les calques ingérés et la priorité.
   - **Politiques** : utilisez la liste déroulante pour sélectionner les politiques appropriées. Par exemple, « Marque », « Modèle ». &#x200B;Assurez-vous d’avoir déjà [créé une politique](policies.md).

1. Sélectionnez le catalogue à lier à la vue du catalogue.

   - **Utiliser tous les tarifs disponibles** : cette option extrait les données de tarification de tous les tarifs disponibles.
   - **Autoriser les tarifs catalogue sélectionnés uniquement** : cette option affiche la boîte de dialogue **Ajouter des tarifs catalogue autorisés**. Utilisez cette boîte de dialogue pour sélectionner le catalogue de prix spécifique à utiliser pour la vue Catalogue.
   - **Catalogue de prix unique uniquement** : sélectionnez cette option si un seul catalogue de prix s&#39;applique. Cette option est obligatoire si vous souhaitez configurer une vue de catalogue privée, qui ne peut référencer qu&#39;un seul catalogue. Voir [Restriction du catalogue des prix sur les affichages de catalogue privé](private-catalog-view.md#price-book-restriction-on-private-catalog-views).
   - **Désactiver le prix**—Cette option n&#39;est pas disponible pour le moment.

   >[!NOTE]
   >
   >Un ID de catalogue des prix contrôle la tarification demandée. Cela ne limite pas l’accès à la vue Catalogue. Pour restreindre l’accès, activez la protection du catalogue pour créer une [vue de catalogue privée](private-catalog-view.md).

1. (Facultatif) Basculez **[!UICONTROL Catalog Protection]** sur **[!UICONTROL Enabled]** pour limiter les données de cette vue de catalogue aux clients disposant d’un jeton signé valide. Voir [Protéger une vue de catalogue](private-catalog-view.md#protect-a-catalog-view) pour les étapes de configuration.

1. Cliquez sur **[!UICONTROL Add]** pour créer la vue de catalogue avec les tarifs et les politiques associés.

La page Vues du catalogue se met à jour pour afficher la nouvelle vue du catalogue&#x200B;

Une fois ces étapes terminées, la vue de catalogue est maintenant configurée pour afficher les produits et les prix en fonction des sources et des politiques sélectionnées.

#### Spécification des vues de catalogue pour les recommandations et les règles de découverte de produits

Vous pouvez spécifier une vue de catalogue lorsque vous [créez des unités de recommandation](../merchandising/recommendations/create.md) ou des [règles de marchandisage](../merchandising/rules/add.md).

#### Calques de catalogue

Les calques de catalogue vous permettent de remplacer les attributs de produit sélectionnés sans modifier les données du catalogue source. Utilisez des calques pour personnaliser les noms, les descriptions, les images, les liens ou les métadonnées d’une vue de catalogue.

Voir [Calques de catalogue](catalog-layer.md).

#### Rendre une vue de catalogue privée

Par défaut, une vue de catalogue est publique pour les applications clientes qui peuvent accéder à l’API de marchandisage GraphQL. Pour restreindre l’accès, configurez une vue de catalogue privé en activant **[!UICONTROL Catalog Protection]**.

Pour savoir comment protéger une vue de catalogue et vérifier que l’accès est appliqué, consultez [Vues de catalogue privé](private-catalog-view.md).

### Modifier une vue de catalogue

1. Dans l’espace de travail **[!UICONTROL Catalog views]**, recherchez la vue de catalogue.
1. Pour ouvrir le menu d&#39;actions, sélectionnez (**[!UICONTROL ...]**).
1. Sélectionnez **[!UICONTROL Edit]** pour accéder à l’éditeur de vue de catalogue.
1. Mettez à jour le nom, les sources de catalogue, les politiques, les informations du catalogue et les paramètres **[!UICONTROL Catalog Protection]** (y compris les clés d’accès restreint affectées) si nécessaire.
1. Cliquez sur **[!UICONTROL Save]**.

### Suppression d’une vue de catalogue

1. Dans l’espace de travail **[!UICONTROL Catalog views]**, recherchez la vue de catalogue.
1. Pour ouvrir le menu d&#39;actions, sélectionnez (**[!UICONTROL ...]**).
1. Sélectionnez **[!UICONTROL Delete]**.
1. Confirmez la suppression.

   Lorsque la boîte de dialogue de confirmation apparaît, cliquez sur **[!UICONTROL Delete]**.

### Afficher les détails de la vue Catalogue

Cette option permet d&#39;afficher rapidement tous les paramètres d&#39;affichage du catalogue, tout en restant sur la table **[!UICONTROL Catalog views]**.

Dans l’espace de travail **[!UICONTROL Catalog views]**, sélectionnez l’icône ![informations](/help/assets/ccdm-shared/recommendations/info-icon.png) d’une vue de catalogue pour afficher ses détails de configuration.

![Détails de la vue Catalogue](../assets/catalog-view-details.png)

De là, vous pouvez voir les détails de configuration de la vue de catalogue, tels que :

- Afficher l’ID
- Nom
- Sources de catalogue
- Politiques
- Date de création
- Données modifiées

Certains de ces paramètres de configuration sont nécessaires lorsque vous configurez votre storefront ou que vous utilisez l’API d’ingestion de données.
