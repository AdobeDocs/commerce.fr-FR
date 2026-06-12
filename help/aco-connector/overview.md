---
title: '[!DNL Adobe Commerce Optimizer Connector]'
description: Découvrez les  [!DNL Adobe Commerce Optimizer Connector]  de synchronisation de catalogue, de recherche et de diffusion storefront entre [!DNL Adobe Commerce] et [!DNL Adobe Commerce Optimizer].
feature: Integration, Storefront, Configuration
badgePaas: label="PaaS uniquement" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."
autotag-review: '2026-06-09T19:00:00.000Z'
TQID: 'https://experienceleague.adobe.com/-C-XP5YYxwyGrkvVR6CDd-FpDybqnlaKMmFPKOKUbFA'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75id: c32adafa-ed01-4b31-997e-2413013911b0id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
subfeature_v2: id: ae62cf09-5996-4921-bda8-fbe67b62e470id: f8ddfd3b-6194-46e8-a176-0e918039be56id: dad884f1-e840-49a1-970e-2f965bdbc410
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: eddd9b14-83bd-4ff4-9072-54a4a484abb7id: e0eb8757-182f-49f3-94a4-1587d16f5094id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 23e4f419628a7838357752ecef0c242f1dcdd4c4
workflow-type: tm+mt
source-wordcount: 990
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
| **Une voie vers le SaaS tournée vers l&#39;avenir** | Fournit une voie de modernisation à faible risque de PaaS vers [!DNL Adobe Commerce as a Cloud Service] + [!DNL Adobe Commerce Optimizer], sans replateforme. |

## Architecture du connecteur {#connector-architecture}

Le diagramme suivant illustre l’architecture de bout en bout du connecteur, du [!DNL Adobe Commerce] à l’[!DNL Adobe Commerce Optimizer] et à l’extraction jusqu’aux storefronts et aux systèmes de passage en caisse.

![Diagramme d&#39;architecture de bout en bout du connecteur ](./assets/aco-connector-end2end-architecture.png){width="700" zoomable="yes"}

Dans cette architecture :

- [!DNL Adobe Commerce] (sur le cloud ou sur site) est le système d&#39;enregistrement et le producteur d&#39;aliments pour animaux
- Le connecteur exporte les flux de catalogue, de prix et de catégories
- [!DNL Adobe Commerce Optimizer] ingère et normalise les données de flux dans les sources de catalogue, les livres de prix et les vues de catalogue
- Les storefronts (storefront Commerce sur les builds [!DNL Edge Delivery Services] ou découplés personnalisés) appellent [!DNL Adobe Commerce Optimizer] API GraphQL pour la découverte et les recommandations et appellent [!DNL Adobe Commerce] ou une autre plateforme tierce connectée pour les opérations de panier et de passage en caisse

## Fonctionnement du connecteur avec [!DNL Adobe Commerce] {#how-the-connector-works-with-adobe-commerce}

Le [!DNL Adobe Commerce Optimizer Connector] fonctionne en utilisant vos portées Commerce existantes (sites web et vues de magasin) et la segmentation de la clientèle pour renseigner le modèle de catalogue [!DNL Adobe Commerce Optimizer] :

![Mappage des données Commerce à Adobe Commerce Optimizer](./assets/storeview-to-catalogview-mapping.png){width="750" zoomable="yes"}

- **Vue de magasin → Sources de catalogue** — Chaque vue de magasin devient une Source de catalogue distincte dans [!DNL Adobe Commerce Optimizer]. Cette source comprend des attributs de produit localisés et des données spécifiques à la vue du magasin
- **Annuaires des prix → site Web** — Chaque site Web [!DNL Adobe Commerce] correspond à un ou plusieurs annuaires des prix en [!DNL Adobe Commerce Optimizer]. Tarification de site Web et exportation de prix de groupe client en tant que livres de prix et entrées de prix
- **Groupe de clients → Variantes de prix** — [!DNL Adobe Commerce] tarification du groupe de clients apparaît comme entrées supplémentaires dans les registres de prix correspondants

Une fois que [!DNL Adobe Commerce Optimizer] a ingéré les données, vous pouvez configurer les éléments suivants :

- **Vues et politiques de catalogue** dans [!DNL Adobe Commerce Optimizer] Studio (pour la création de sous-ensembles spécifiques à une région, une marque ou un client)
- **Découverte de produits** (recherche, facettes, règles de marchandisage)
- **[!DNL Product Recommendations]**

Lorsque vous activez le connecteur, l’instance [!DNL Adobe Commerce] reste le système d’enregistrement pour les données de catalogue et de prix. Lorsque vous mettez à jour des données dans [!DNL Adobe Commerce], le connecteur synchronise ces mises à jour sur l’instance [!DNL Adobe Commerce Optimizer].

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
- **Commandes de resynchronisation** pour les flux ciblés

Les flux suivants sont disponibles pour le [!DNL Adobe Commerce Optimizer Connector] :

- `products` - données des produits
- `productAttributes` - métadonnées pour les attributs de produit
- `priceBooks` - catalogue des prix
- `prices` - prix des produits
- `categories` - données des catégories

Pour plus d’informations, consultez les rubriques suivantes :

- Pour [!DNL Adobe Commerce] opérations de resynchronisation de l’interface de ligne de commande, reportez-vous à la commande [CLI resync](/help/data-export/data-export-cli-commands.md#sync-using-cli-commands){target="_blank"}
- [Modules [!DNL Adobe Commerce Optimizer Connector] et points d’entrée de flux](/help/aco-connector/reference/connector-reference.md)
- [Mappage des champs pour les flux du connecteur](/help/aco-connector/reference/field-mapping.md)

### Configurer le marchandisage et les storefronts {#merchandising-storefronts}

Une fois que [!DNL Adobe Commerce] données sont disponibles dans [!DNL Adobe Commerce Optimizer], utilisez [[!DNL Adobe Commerce Optimizer] Studio](/help/optimizer/overview.md#quick-tour) pour connecter les expériences de marchandisage et de storefront à votre catalogue synchronisé. Les étapes suivantes standard sont les suivantes :

- **Vues et politiques de catalogue** — Définissez des sous-ensembles et des règles d&#39;accès spécifiques à la région, à la marque ou au client à partir du menu [!UICONTROL Store setup]
- **Découverte de produits et recommandations** — Configurez la recherche, les facettes, les règles de marchandisage, les synonymes et les unités de recommandation dans le menu [!UICONTROL Merchandising]. Le comportement de recherche et de recommandation est géré dans [!DNL Adobe Commerce Optimizer] ; les paramètres [!DNL Live Search] et [!DNL Product Recommendations] de l’administrateur [!DNL Adobe Commerce] ne s’appliquent plus à ces flux
- **Connexions Storefront** — Pointez les storefronts Commerce sur des versions [!DNL Edge Delivery Services] ou tierces découplées vers les points d’entrée appropriés du client [!DNL Adobe Commerce Optimizer], de la vue de catalogue et de l’API de marchandisage. Pour obtenir un exemple d’intégration tierce, consultez la section Connecteur Salesforce Commerce [ [!DNL Adobe Commerce Optimizer]](/help/optimizer/developer/salesforce-connector.md)
- **Passage en caisse** — Conservez le panier, le passage en caisse, la gestion des commandes et les comptes clients sur [!DNL Adobe Commerce] ou une plateforme tierce connectée. Utilisez des [!DNL App Builder] et des [!DNL API Mesh] pour la remise du panier si nécessaire.

Pour obtenir des conseils de configuration détaillés, consultez [Prise en main](/help/aco-connector/get-started.md) et le [[!DNL Adobe Commerce Optimizer] Outils de marchandisage](/help/optimizer/overview.md#quick-tour).

## Scénarios pris en charge {#supported-scenarios}

Le connecteur est conçu pour les commerçants B2C avec des déploiements sur le cloud et sur site [!DNL Adobe Commerce] qui souhaitent adopter des [!DNL Adobe Commerce Optimizer] sans reconstruire leur serveur principal.

**Cas d’utilisation courants :**

- **Modernisation du storefront uniquement**
Gardez votre serveur principal [!DNL Adobe Commerce] existant, déplacez PLP/Search/PDP vers [!DNL Edge Delivery Services] storefronts alimentés par [!DNL Adobe Commerce Optimizer]

- **Évolution des performances du catalogue et de la recherche**
Déchargez l’indexation et la recherche de catalogues lourds vers les services SaaS d’[!DNL Adobe Commerce Optimizer] tout en conservant la propriété des produits et des prix dans [!DNL Adobe Commerce]

- **Adoption progressive du SaaS**
Utilisez le connecteur comme étape vers [!DNL Adobe Commerce as a Cloud Service] + [!DNL Adobe Commerce Optimizer], avec un catalogue de [!DNL Adobe Commerce] composables compatible

## Responsabilités et conditions préalables à la mise en œuvre {#responsibilities-prerequisites}

[!DNL Adobe Commerce] est la source de vérité pour les produits, les prix et les groupes de clients. Apportez des modifications aux [!DNL Adobe Commerce] ; le connecteur les synchronise sur [!DNL Adobe Commerce Optimizer].

**[!DNL Adobe Commerce Optimizer]est responsable de :**

- Modélisation de catalogue (sources de catalogue, registres des prix, vues de catalogue, politiques)
- Découverte de produits et recommandations
- Mesures Storefront, tableaux de bord de synchronisation des données et rapports Mesures de succès

**Le connecteur ne :**

- Modifier [!DNL Adobe Commerce] flux de panier, de passage en caisse ou de commande
- Approvisionnement automatique des projets de storefront (Commerce Storefront / [!DNL Edge Delivery Services] tooling handles that)

**Avant de commencer :**

- Vérifiez que [!DNL Adobe Commerce] répond aux exigences minimales de version et de [!DNL Adobe Commerce Optimizer Connector]. Voir [Prise en main](/help/aco-connector/get-started.md#requirements-to-use-the-integration) pour plus d’informations.
- Assurez-vous de disposer de l’accès à l’organisation IMS, d’une instance [!DNL Adobe Commerce Optimizer], ainsi que des informations d’identification et de région nécessaires.

## Plus d’aide sur cette rubrique {#more-help-on-this-topic}

- Configurez l’intégration et activez les workflows clés : [Prise en main de l’ [!DNL Adobe Commerce Optimizer Connector]](/help/aco-connector/get-started.md)
- En savoir plus sur [!DNL Adobe Commerce Optimizer] concepts et l’architecture : [En quoi consiste  [!DNL Adobe Commerce Optimizer] ?](/help/optimizer/overview.md)
- Découvrez le mécanisme de synchronisation, l’initialisation et la gestion des erreurs : [pipeline de synchronisation du connecteur](/help/aco-connector/connector-sync-pipeline.md)
- Mappage des données au niveau du champ pour tous les flux : [Mappage des champs pour les flux du connecteur](/help/aco-connector/reference/field-mapping.md)
- Intégrer des storefronts découplés à l’aide de GraphQL et du codage de bundle : [Intégration de storefront découplé](/help/aco-connector/headless-storefront.md)
- Diagnostiquer les problèmes de synchronisation et de configuration : [dépannage](/help/aco-connector/troubleshooting.md)
