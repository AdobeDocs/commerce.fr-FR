---
title: Connecteur Adobe Commerce Optimizer
description: Découvrez les [!DNL Adobe Commerce Optimizer Connector] de synchronisation de catalogue, de recherche et de diffusion storefront entre [!DNL Adobe Commerce] et [!DNL Adobe Commerce Optimizer].
feature: Integration, Storefront, Configuration
badgePaas: label="PaaS uniquement" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."
autotag-review: '2026-06-09T19:00:00.000Z'
nudge: true
TQID: 'https://experienceleague.adobe.com/v769V06jl-9YfovpL3HOB-FxovIMZyHxOlHXHvkQmbc'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
    internal-label: Commerce ecosystem
  - id: 00451af3-7b97-5414-9992-3a6c269e413f
    internal-label: Paas
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 76cfaac4-e563-56dd-8938-708bf8b84956
    internal-label: Attributes
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: adedf70c-c1e1-5734-acdc-c5c43b114964
    internal-label: Release Notes
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: e9004f3c-09ae-5d24-acd2-fa0987fdb66e
    internal-label: Companies
  - id: f37757d8-3174-5335-b977-1161792f965d
    internal-label: Personalization
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
    internal-label: Storefront configuration
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
    internal-label: Cloud architecture
  - id: dad884f1-e840-49a1-970e-2f965bdbc410
    internal-label: Extensions
  - id: 3c398179-d35a-51ba-b317-6c5b95feef5e
    internal-label: Logs
  - id: a1d22079-48b9-5e69-9ee6-eb236068ef34
    internal-label: Search
  - id: e396cff5-f586-484c-89f0-7f1da3308f92
    internal-label: GraphQL
  - id: f56d26ed-050b-4fb7-b29b-8e6e994e80a2
    internal-label: B2B
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
source-git-commit: a3ade1a31d3c2905b601f71bda118de89c43cf59
workflow-type: tm+mt
source-wordcount: '1204'
ht-degree: 0%
---
# [!DNL Adobe Commerce Optimizer Connector]

Le [!DNL Adobe Commerce Optimizer Connector] est une intégration native et propriétaire entre [!DNL Adobe Commerce] (cloud ou sur site) et [!DNL Adobe Commerce Optimizer]. Il synchronise les données de catalogue et de tarification de vos magasins de [!DNL Adobe Commerce] dans [!DNL Adobe Commerce Optimizer] afin que vous puissiez :

- Puissance **découverte et recommandations de produits pilotées par l’IA**
- Exécutez **storefronts découplés hautes performances** (y compris les storefronts Commerce optimisés par [!DNL Edge Delivery Services]).
- Analysez les indicateurs de performance clés **avant et après** et l’intégrité de la synchronisation des données à un seul endroit

[!DNL Adobe Commerce] reste votre système d’enregistrement pour les produits, les prix et la structure du catalogue. [!DNL Adobe Commerce Optimizer] devient votre couche d’expérience et de marchandisage, offrant des résultats rapides et pertinents à tout storefront ou canal connecté.

## Principaux avantages {#key-benefits}

| Bénéfice | Ce que cela signifie pour vous |
| --- | --- |
| **Aucun connecteur personnalisé à créer** | Utilisez une intégration propriétaire prise en charge au lieu d’écrire et de gérer des flux et des scripts personnalisés. |
| **Retour sur investissement plus rapide avec[!DNL Adobe Commerce Optimizer]** | Activez Recherche optimisée par l&#39;IA, les recommandations et les vitrines découplées en plus de votre déploiement [!DNL Adobe Commerce] existant. |
| **Aligné sur les portées de Commerce** | Mappe automatiquement les sites web, les vues de magasin et les groupes de clients dans [!DNL Adobe Commerce Optimizer] éléments de catalogue (sources de catalogue et tarifs). |
| **Visibilité opérationnelle** | Surveillez l’intégrité du flux, les heures de la dernière synchronisation et l’état par SKU à partir d’une vue [!UICONTROL Data Feed Sync Status] dédiée. |
| **Une voie vers le SaaS tournée vers l&#39;avenir** | Fournit un chemin de migration échelonnée de Commerce sur le cloud ou sur site vers [!DNL Adobe Commerce as a Cloud Service] + [!DNL Adobe Commerce Optimizer], sans reconfiguration de plateforme. |

## Architecture du connecteur {#connector-architecture}

Le diagramme suivant illustre l’architecture de bout en bout du connecteur, du [!DNL Adobe Commerce] à l’[!DNL Adobe Commerce Optimizer] et à l’extraction jusqu’aux storefronts et aux systèmes de passage en caisse.

![Diagramme d&#39;architecture de bout en bout du connecteur ](./assets/aco-connector-end2end-architecture.png){width="700" zoomable="yes"}

Dans cette architecture :

- [!DNL Adobe Commerce] (sur le cloud ou sur site) est le système d&#39;enregistrement et le producteur d&#39;aliments pour animaux
- Le connecteur exporte les flux de catalogue, de prix et de catégories
- [!DNL Adobe Commerce Optimizer] ingère et normalise les données de flux dans les sources de catalogue, les livres de prix et les vues de catalogue
- Les storefronts (storefront Commerce sur les builds [!DNL Edge Delivery Services] ou découplés personnalisés) appellent [!DNL Adobe Commerce Optimizer] API GraphQL pour la découverte et les recommandations et appellent [!DNL Adobe Commerce] ou une autre plateforme tierce connectée pour les opérations de panier et de passage en caisse

Basé sur [[!DNL SaaS Data Export]](/help/data-export/overview.md), le connecteur mappe les flux collectés au format [!DNL Catalog Data Ingestion API] et gère l’authentification et l’envoi. Voir [Pipeline de synchronisation du connecteur](/help/aco-connector/connector-sync-pipeline.md) pour le comportement de synchronisation, le contrôle de l’étendue et la gestion des erreurs.

## Fonctionnement du connecteur avec [!DNL Adobe Commerce] {#how-the-connector-works-with-adobe-commerce}

Le [!DNL Adobe Commerce Optimizer Connector] prend en charge la synchronisation de catalogues B2C. Il synchronise les flux de catalogue et de tarification à partir d’une instance [!DNL Adobe Commerce] et mappe les vues de magasin, les sites web et les groupes de clients aux sources de catalogue et aux tarifs dans [!DNL Adobe Commerce Optimizer]. Il ne synchronise pas le catalogue partagé B2B ni la configuration d’affectation d’entreprise. Après la synchronisation, configurez les vues et les politiques de catalogue dans [!DNL Adobe Commerce Optimizer] Studio.

![Mappage des données [!DNL Adobe Commerce] aux [!DNL Adobe Commerce Optimizer]](./assets/storeview-to-catalogview-mapping.png){width="750" zoomable="yes"}

### Mappage de catalogue de base

Le connecteur mappe [!DNL Adobe Commerce] données de catalogue au modèle de catalogue [!DNL Adobe Commerce Optimizer] :

- **Affichage de magasin → Sources de catalogue** — Chaque affichage de magasin devient une source de catalogue distincte dans [!DNL Adobe Commerce Optimizer]. Cette source comprend des attributs de produit localisés et des données spécifiques à la vue du magasin.
- **Annuaires des prix → site Web** — Chaque site Web [!DNL Adobe Commerce] correspond à un ou plusieurs annuaires des prix en [!DNL Adobe Commerce Optimizer]. Tarification du site Web et exportation des prix du groupe de clients sous forme de livres de prix et d&#39;entrées de prix.
- **Écritures du → de groupe client** — [!DNL Adobe Commerce] tarification du groupe client apparaît en tant qu&#39;écritures supplémentaires dans les livres de prix correspondants.

Une fois que le connecteur a synchronisé les données du catalogue, configurez le modèle de marchandisage dans [!DNL Adobe Commerce Optimizer] Studio. Par exemple, configurez les éléments suivants :

- **Vues et politiques de catalogue** pour les sous-ensembles spécifiques à une région, une marque ou un client
- **Découverte de produits** pour la recherche, les facettes et les règles de marchandisage.
- **[!DNL Product Recommendations]**

### Comportement du connecteur B2B {#b2b-shared-catalog-projection-specification}

Le [!DNL Adobe Commerce Optimizer Connector for B2B] étend le connecteur de base avec une projection unidirectionnelle du catalogue partagé B2B et de la configuration d’affectation d’entreprise dans des expériences de catalogue protégées. [!DNL Adobe Commerce] reste la source de vérité pour les données de catalogue et de tarification ; le connecteur B2B s’appuie sur le catalogue de base et la synchronisation des prix et gère ses projections générées par le connecteur.

Pour le mappage de projection, le flux d’autorisation d’exécution et la limite de protection, consultez [projection du catalogue partagé B2B](b2b-shared-catalog-projection.md). Pour obtenir des instructions de configuration, voir [Prise en main du connecteur B2B](/help/aco-connector/get-started-b2b-shared-catalogs.md).

>[!NOTE]
>
>Pour plus d’informations sur la configuration des [!DNL Adobe Commerce Optimizer], voir [[!DNL Adobe Commerce Optimizer] Outils de marchandisage](/help/optimizer/overview.md#quick-tour).

## Workflows standard {#typical-workflows}

Ces workflows décrivent comment les équipes configurent et utilisent le [!DNL Adobe Commerce Optimizer Connector]. Pour plus d’informations sur la configuration de l’intégration et l’activation de ces workflows, voir [Prise en main](/help/aco-connector/get-started.md).

### Installation et configuration initiales {#initial-setup}

Voir [Étapes de configuration](/help/aco-connector/get-started.md#configuration-steps) dans le guide _Prise en main_.

### Synchronisation des données en cours {#ongoing-sync}

Après la configuration initiale, le connecteur prend en charge les éléments suivants :

- **Synchronisation complète du catalogue** pour la migration initiale ou des modifications structurelles importantes
- **Synchronisations delta** pour les mises à jour continues lorsque les produits ou les prix changent
- **Commandes de resynchronisation** pour synchroniser les flux ciblés

Pour le comportement de synchronisation automatisé, les plannings cron et le traitement des erreurs, consultez [Pipeline de synchronisation du connecteur](/help/aco-connector/connector-sync-pipeline.md). Avant une synchronisation complète du catalogue ou une mise à jour volumineuse, utilisez [Estimer le volume de données et l’heure de synchronisation](/help/aco-connector/reference/estimate-data-volume-sync-time.md) pour planifier le minutage et éviter toute interruption du site.

Les flux suivants sont disponibles pour le [!DNL Adobe Commerce Optimizer Connector] :

- `products` - données des produits
- `productAttributes` - métadonnées pour les attributs de produit
- `priceBooks` - catalogue des prix
- `prices` - prix des produits
- `categories` - données des catégories

Pour plus d’informations, consultez les rubriques suivantes :

- Vérifier la synchronisation des données du catalogue et resynchroniser manuellement les flux du connecteur : [Gérer la synchronisation](/help/aco-connector/data-sync-status.md)
- Pour les opérations de resynchronisation de l’interface de ligne de commande [!DNL Adobe Commerce], voir [Flux de synchronisation utilisant l’interface de ligne de commande Commerce](/help/data-export/data-export-cli-commands.md)
- [Modules [!DNL Adobe Commerce Optimizer Connector] et points d’entrée de flux](/help/aco-connector/reference/connector-reference.md)
- [Mappage des champs pour les flux du connecteur](/help/aco-connector/reference/field-mapping.md)

### Configurer le marchandisage et les storefronts {#merchandising-storefronts}

Une fois que [!DNL Adobe Commerce] données sont disponibles dans [!DNL Adobe Commerce Optimizer], utilisez [[!DNL Adobe Commerce Optimizer] Studio](/help/optimizer/overview.md#quick-tour) pour connecter les expériences de marchandisage et de storefront à votre catalogue synchronisé. Les étapes suivantes standard sont les suivantes :

- **Vues et politiques de catalogue** — Pour le connecteur de base, définissez des sous-ensembles et des règles d&#39;accès spécifiques à la région, à la marque ou au client à partir du menu [!UICONTROL Store setup]. Pour savoir qui peut interroger une vue de catalogue, consultez [Vues de catalogue privé](/help/optimizer/setup/private-catalog-view.md)
- **Découverte de produits et recommandations** — Configurez la recherche, les facettes, les règles de marchandisage, les synonymes et les unités de recommandation dans le menu [!UICONTROL Merchandising]. Le comportement de recherche et de recommandation est géré dans [!DNL Adobe Commerce Optimizer] ; les paramètres [!DNL Live Search] et [!DNL Product Recommendations] de l’administrateur [!DNL Adobe Commerce] ne s’appliquent plus à ces flux
- **Connexions Storefront** — Pointez les storefronts Commerce sur des versions [!DNL Edge Delivery Services] ou tierces découplées vers les points d’entrée appropriés du client [!DNL Adobe Commerce Optimizer], de la vue de catalogue et de l’API de marchandisage. Pour les intégrations découplées personnalisées, voir [Intégration storefront découplée](/help/aco-connector/headless-storefront.md). Pour obtenir un exemple d’intégration tierce, consultez la section Connecteur Salesforce Commerce [ [!DNL Adobe Commerce Optimizer]](/help/optimizer/developer/salesforce-connector.md)
- **Passage en caisse** — Conservez le panier, le passage en caisse, la gestion des commandes et les comptes clients sur [!DNL Adobe Commerce] ou une plateforme tierce connectée. Utilisez des [!DNL App Builder] et des [!DNL API Mesh] pour la remise du panier si nécessaire.

Pour obtenir des conseils de configuration détaillés, consultez [Prise en main](/help/aco-connector/get-started.md) et le [[!DNL Adobe Commerce Optimizer] Outils de marchandisage](/help/optimizer/overview.md#quick-tour).

## Scénarios pris en charge {#supported-scenarios}

Le [!DNL Adobe Commerce Optimizer Connector] de base prend en charge les commerçants B2C avec des déploiements sur le cloud et sur site [!DNL Adobe Commerce] qui souhaitent adopter des [!DNL Adobe Commerce Optimizer] sans reconstruire leur serveur principal.

Le [!DNL Adobe Commerce Optimizer Connector for B2B] distinct étend le connecteur de base pour synchroniser la configuration de catalogue partagé et projeter automatiquement les catalogues partagés personnalisés en tant que vues de catalogue privé. Pour plus d’informations, voir Projection du catalogue [B2B](b2b-shared-catalog-projection.md).

**Cas d’utilisation courants :**

- **Migration du storefront vers Edge Delivery**
Gardez votre serveur principal [!DNL Adobe Commerce] existant, déplacez PLP/Search/PDP vers [!DNL Edge Delivery Services] vitrines alimentées par [!DNL Adobe Commerce Optimizer].

- **Évolution des performances du catalogue et de la recherche**
Déchargez l’indexation et la recherche de catalogues lourds pour [!DNL Adobe Commerce Optimizer] les services SaaS (Software as a Service) tout en conservant la propriété des produits et des prix dans [!DNL Adobe Commerce].

## Responsabilités et conditions préalables à la mise en œuvre {#responsibilities-prerequisites}

[!DNL Adobe Commerce] est le système d’enregistrement des produits, des prix et des groupes de clients. Apportez des modifications aux [!DNL Adobe Commerce] et le connecteur les synchronise avec [!DNL Adobe Commerce Optimizer].

**[!DNL Adobe Commerce Optimizer]est responsable de :**

- Modélisation de catalogue (sources de catalogue, catalogue des prix, vues de catalogue, politiques)
- Découverte de produits et recommandations
- Mesures Storefront, tableaux de bord de synchronisation des données et rapports de mesures de succès

**Le connecteur ne :**

- Modifier [!DNL Adobe Commerce] flux de panier, de passage en caisse ou de commande
- Approvisionnement automatique des projets de storefront (Commerce Storefront / [!DNL Edge Delivery Services] tooling handles that)

**Avant de commencer :**

- Vérifiez que [!DNL Adobe Commerce] répond aux exigences minimales de version et de [!DNL Adobe Commerce Optimizer Connector]. Voir [Prise en main](/help/aco-connector/get-started.md#requirements-to-use-the-integration) pour plus d’informations.
- Assurez-vous de disposer de l’accès à l’organisation IMS, d’une instance [!DNL Adobe Commerce Optimizer], ainsi que des informations d’identification et de région nécessaires.

>[!MORELIKETHIS]
>
> - [Prise en main de l’ [!DNL Adobe Commerce Optimizer Connector]](/help/aco-connector/get-started.md) — Configurez l’intégration et activez les workflows clés.
> - [Pipeline de synchronisation du connecteur](/help/aco-connector/connector-sync-pipeline.md) — Découvrez le mécanisme de synchronisation, l’initialisation et la gestion des erreurs.
> - [Gérer la synchronisation ](/help/aco-connector/data-sync-status.md) — Vérifier la synchronisation des données de catalogue et resynchroniser manuellement les flux.
> - [Mappage de champs pour les flux du connecteur](/help/aco-connector/reference/field-mapping.md) — Examinez le mappage de données au niveau du champ pour tous les flux.
> - [Scénarios de dépannage](/help/aco-connector/troubleshooting/troubleshooting-scenarios.md) — Résolvez les erreurs de configuration ou les résultats de synchronisation inattendus.
> - [Notes de mise à jour](/help/aco-connector/release-notes.md) — Consultez les mises à jour du connecteur et les problèmes connus.
