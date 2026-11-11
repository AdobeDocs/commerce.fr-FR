---
title: Modèle de données de catalogue composable et services de marchandisage
description: Découvrez comment le modèle de données de catalogue composable modifie la diffusion du catalogue dans [!DNL Adobe Commerce as a Cloud Service] et ce que les commerçants et les équipes de storefront doivent savoir.
feature: Catalog Management, Personalization, Saas
role: Leader
level: Beginner
autotag-review: '2026-11-09T05:07:21.124Z'
TQID: 'https://experienceleague.adobe.com/5Aaumfx9-lOBMDOg59rr-MMl-0sgFLSVUzngkdzfyR0'
product_v2:
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 22bad240-8308-569b-a9d5-578f1ff890ca
    internal-label: Customers
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 76cfaac4-e563-56dd-8938-708bf8b84956
    internal-label: Attributes
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: a8ae7a5a-6cdc-5922-bd0d-6feb44b04984
    internal-label: Upgrade
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
    internal-label: Catalog management
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
  - id: e9004f3c-09ae-5d24-acd2-fa0987fdb66e
    internal-label: Companies
  - id: f37757d8-3174-5335-b977-1161792f965d
    internal-label: Personalization
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
    internal-label: Reporting
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
source-git-commit: 0bda134570bb3bf2f43da545917dedc95394df5e
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 0%
---

# Services de marchandisage

Adobe Commerce as a Cloud Service prend désormais en charge le modèle de données de catalogue composable (CCDM) via les services de marchandisage. Adobe Commerce Optimizer a introduit ce modèle de données. Le CCDM offre aux deux produits une base commune pour les fonctionnalités de navigation dans les catalogues de storefront et de marchandisage, tandis que Commerce Foundation continue à gérer les produits, les prix et les transactions.

Cette rubrique explique les modifications apportées au CCDM, les fonctionnalités qui se poursuivent et ce que la modification signifie pour les commerçants, les partenaires et les développeurs de storefront.

## Quels changements le CCDM apporte-t-il ?

Le modèle de catalogue d’origine utilise le service de catalogue pour fournir des données de produit aux storefronts, avec la recherche en direct et les recommandations de produits offrant des fonctionnalités de recherche, de marchandisage et de recommandation. Dans ce modèle, Commerce se synchronise à l’aide de l’exportation de données [SaaS](https://experienceleague.adobe.com/fr/docs/commerce/saas-data-export/overview).

Avec le CCDM, ces fonctionnalités fonctionnent sur la même base de catalogue que celle qui alimente Adobe Commerce Optimizer. Les [vues de catalogue](https://experienceleague.adobe.com/en/docs/commerce-admin/merchandising-with-ccdm/setup/catalog-view) et les [politiques](https://experienceleague.adobe.com/en/docs/commerce-admin/merchandising-with-ccdm/setup/policies) définissent le contexte de catalogue disponible pour un storefront. Les politiques déterminent l’assortiment de produits et les règles de marchandisage peuvent s’appliquer à toutes les vues de catalogue ou être personnalisées pour une vue spécifique.

Cela modifie la configuration, l’accès et le marchandisage du catalogue. Le CCDM s’appuie sur les fonctionnalités de recherche, de recommandations et de marchandisage du catalogue Commerce d’origine tout en introduisant des contrôles au niveau de la vue du catalogue. D’autres fonctionnalités de gestion et de création de rapports sont décrites ci-dessous.

Commerce Foundation reste la source canonique des produits et des prix. Les données de produit et de prix se synchronisent d’une manière avec le CCDM via une intégration native d’Adobe Commerce as a Cloud Service. La configuration du site web, du magasin et de l’affichage du magasin reste dans Commerce, aux côtés des workflows de panier, de passage en caisse et de gestion des commandes existants.

## Octroi de licences et approvisionnement

Les services de marchandisage sont inclus dans le SKU Adobe Commerce as a Cloud Service existant. Il ne s’agit pas d’un second produit ou abonnement, et il ne nécessite pas d’achat, de droit ou de client Adobe Commerce Optimizer distinct.

## Aperçu de l’architecture

[!DNL Commerce Foundation] reste l&#39;enregistrement principal pour les produits et les prix et continue à gérer les transactions. L’intégration native synchronise les données de produit et de prix de [!DNL Commerce] vers le CCDM. Vous n’installez pas de connecteur distinct ni d’application [!DNL App Builder] pour cette synchronisation.

Les storefronts utilisent des services de marchandisage pris en charge par le CCDM pour récupérer les données du catalogue et le contexte pour la navigation, la recherche, les recommandations et le marchandisage. Les requêtes utilisent le contexte du catalogue pour récupérer les produits et les prix pour l’audience prévue. Vous continuez à gérer la configuration du site web, du magasin et de l’affichage du magasin dans [!DNL Commerce].

Le diagramme suivant montre la position des services de marchandisage dans l’architecture plus large d’Adobe Commerce as a Cloud Service.

Architecture de ![Commerce présentant le flux de données du catalogue dans les services de marchandisage](./assets/data-flow-ccdm.png){zoomable="yes"}

## Quelles sont les nouveautés pour les commerçants ?

Le nouveau modèle permet d’étendre les règles de marchandisage existantes à toutes les vues de catalogue ou à une vue spécifique. Vous pouvez ainsi appliquer le marchandisage à chaque audience storefront. Découvrez comment [étendre une règle de marchandisage aux vues de catalogue](https://experienceleague.adobe.com/en/docs/commerce-admin/merchandising-with-ccdm/merchandising/rules/add).

Dans Admin, vous pouvez configurer le contexte du catalogue avec [!UICONTROL Catalog Views] et [!UICONTROL Policies]. Vous pouvez également utiliser [!UICONTROL Success Metrics] pour consulter le chiffre d’affaires, la conversion, l’engagement, l’acquisition et le taux de rebond. Voir [Mesures de succès](https://experienceleague.adobe.com/en/docs/commerce-admin/merchandising-with-ccdm/manage-results/success-metrics) pour plus d’informations.

## Considérations avant l&#39;adoption

Examinez l’impact du modèle CCDM sur vos workflows de licence, d’intégration de catalogues, de storefront et d’administration avant d’adopter les services de marchandisage.

### Gestion des catalogues et intégrations

Continuer la gestion des produits et des prix dans [!DNL Commerce Foundation]. L’intégration native les synchronise avec le CCDM. Ne créez pas de second catalogue de produits pour les services de marchandisage.

### Implémentation de Storefront

La manière dont votre storefront récupère les données de catalogue dépend de votre implémentation :

- **[!DNL Adobe Commerce Storefront]** compléments : les compléments gèrent la transition. Aucune modification du code n’est requise. Consultez la [documentation sur la configuration du storefront](https://experienceleague.adobe.com/en/tools/commerce-storefront/).
- **Storefronts personnalisés ou autres**—Mettez à jour les en-têtes de votre demande de catalogue comme décrit dans la [référence de configuration des en-têtes](https://experienceleague.adobe.com/en/tools/commerce-storefront/setup/configuration/commerce-configuration/#headers).

Examinez vos requêtes de catalogue et les en-têtes de requête pour le modèle basé sur le CCDM. Ne supposez pas que les requêtes ou en-têtes existants restent inchangés. Les requêtes du GraphQL de marchandisage diffèrent des requêtes utilisées dans le modèle de services de catalogue d’origine. Les requêtes supplémentaires prennent en charge le CCDM. Utilisez la [référence de l’API Merchandising GraphQL](https://developer.adobe.com/commerce/services/reference/graphql/) et vérifiez le contexte de catalogue requis par rapport à la [référence de l’en-tête storefront](https://experienceleague.adobe.com/en/tools/commerce-storefront/setup/configuration/commerce-configuration/#headers).

### Applications et extensions tierces

Examinez les applications et extensions tierces qui lisent des données de catalogue ou consomment des événements de catalogue avec leur fournisseur. La compatibilité dépend de la manière dont chaque application ou extension utilise ces interfaces.

### Expérience d’administrateur

Adobe Commerce as a Cloud Service avec CCDM utilise [[!DNL Adobe Unified Experience]](https://experienceleague.adobe.com/fr/docs/commerce-admin/start/admin/admin-unified-experience) (Unified Shell). Adobe a publié Unified Shell séparément du CCDM. Les instances existantes sur le modèle de services de catalogue d’origine conservent l’accès à la fois à Classic et à Unified Shell.

### Limites

Le modèle CCDM ne modifie pas les limites d’Adobe Commerce as a Cloud Service. Le partage d’une base de catalogue avec Optimizer ne signifie pas que Commerce hérite de la capacité ou des limites d’Optimizer.

## Disponibilité et migration

Les organisations qui commencent à utiliser Adobe Commerce as a Cloud Service après cette version bénéficient par défaut de services de marchandisage. Si votre organisation a besoin du modèle de données de catalogue d’origine, contactez l’équipe de votre compte Adobe pour déterminer si une exception est disponible.

Les organisations qui disposaient d’Adobe Commerce as a Cloud Service avant cette version peuvent choisir l’un des modèles de catalogue lors de l’approvisionnement d’une nouvelle instance [1. &#x200B;](./getting-started.md#create-an-instance)Par défaut, le sélecteur [!UICONTROL Enable CCDM] est désactivé. Une fois que le CCDM est activé, vous ne pouvez pas le désactiver.

Les instances existantes ne changent pas automatiquement. Lors de la disponibilité générale (GA), vous ne pouvez pas migrer une instance de services de catalogue d’origine existante vers les services de marchandisage.
