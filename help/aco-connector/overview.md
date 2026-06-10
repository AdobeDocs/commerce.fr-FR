---
title: '[!DNL Adobe Commerce Optimizer Connector]'
description: 'Découvrez l [!DNL Adobe Commerce]  intégration entre et  [!DNL Adobe Commerce Optimizer]  pour la synchronisation des catalogues, la recherche et la diffusion storefront. [!DNL Adobe Commerce Optimizer Connector] '
feature: Integration, Storefront, Configuration
badgePaas: label="PaaS uniquement" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."
autotag-review: '2026-06-09T19:00:00.000Z'
TQID: 'https://experienceleague.adobe.com/-C-XP5YYxwyGrkvVR6CDd-FpDybqnlaKMmFPKOKUbFA'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
  - id: dad884f1-e840-49a1-970e-2f965bdbc410
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 6d4493db5e0714577a8800007cc6d2c552578fa4
workflow-type: tm+mt
source-wordcount: 1037
ht-degree: 0%

---

# Connecteur Adobe Commerce Optimizer

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
| **Aligné sur les portées de Commerce** | Mappe automatiquement les sites web, les affichages de boutique et les groupes de clients dans [!DNL Adobe Commerce Optimizer] éléments de catalogue (sources de catalogue et tarifs). |
| **Visibilité opérationnelle** | Surveillez l’intégrité du flux, les heures de la dernière synchronisation et l’état par SKU à partir d’une vue [!UICONTROL Data Feed Sync Status] dédiée. |
| **Une voie vers le SaaS tournée vers l&#39;avenir** | Fournit une voie de modernisation à faible risque de PaaS vers [!DNL Adobe Commerce as a Cloud Service] + [!DNL Adobe Commerce Optimizer], sans replateforme. |

## Architecture du connecteur {#connector-architecture}

Le diagramme suivant illustre l’architecture de bout en bout du connecteur, du [!DNL Adobe Commerce] à l’[!DNL Adobe Commerce Optimizer] et à l’extraction jusqu’aux storefronts et aux systèmes de passage en caisse.

![Diagramme d&#39;architecture de bout en bout du connecteur &#x200B;](./assets/aco-connector-end2end-architecture.png){width="700" zoomable="yes"}

Dans cette architecture :

- [!DNL Adobe Commerce] (sur le cloud ou sur site) est le système d&#39;enregistrement et le producteur d&#39;aliments pour animaux
- Le connecteur exporte les flux de catalogue, de prix et de catégories
- [!DNL Adobe Commerce Optimizer] ingère et normalise les données de flux dans les sources de catalogue, les livres de prix et les vues de catalogue
- Les storefronts (storefront Commerce sur les builds [!DNL Edge Delivery Services] ou découplés personnalisés) appellent [!DNL Commerce Optimizer] API GraphQL pour la découverte et les recommandations et appellent [!DNL Adobe Commerce] ou une autre plateforme tierce connectée pour les opérations de panier et de passage en caisse

## Fonctionnement du connecteur avec [!DNL Adobe Commerce]

Le [!DNL Adobe Commerce Optimizer Connector] fonctionne en utilisant vos portées Commerce existantes (sites web et vues de magasin) et la segmentation de la clientèle pour renseigner le modèle de catalogue [!DNL Adobe Commerce Optimizer] :

![Mappage des données Commerce à Adobe Commerce Optimizer](./assets/storeview-to-catalogview-mapping.png){width="750" zoomable="yes"}

- **Vues de magasin → sources de catalogue** — Chaque vue de magasin devient une Source de catalogue distincte dans [!DNL Adobe Commerce Optimizer]. Cette source comprend des attributs de produit localisés et des données spécifiques à la vue du magasin
- **Sites Web → Catalogues de prix** — Chaque site Web [!DNL Adobe Commerce] correspond à un ou plusieurs Catalogues de prix en [!DNL Commerce Optimizer]. Tarification de site Web et exportation de prix de groupe client en tant que livres de prix et entrées de prix
- **Groupes de clients → Variantes de prix** — [!DNL Adobe Commerce] tarification du groupe de clients apparaît en tant qu&#39;entrées supplémentaires dans les tarifs correspondants

Une fois que [!DNL Commerce Optimizer] a ingéré les données, vous pouvez configurer les éléments suivants :

- **Vues et politiques de catalogue** dans [!DNL Adobe Commerce Optimizer] Studio (pour la création de sous-ensembles spécifiques à une région, une marque ou un client)
- **Découverte de produits** (recherche, facettes, règles de marchandisage)
- **[!DNL Product Recommendations]**

Lorsque vous activez le connecteur, l’instance [!DNL Adobe Commerce] reste le système d’enregistrement pour les données de catalogue et de prix. Lorsque vous mettez à jour des données dans [!DNL Adobe Commerce], le connecteur synchronise ces mises à jour sur l’instance [!DNL Adobe Commerce Optimizer].

>[!NOTE]
>
>Pour plus d’informations sur la configuration des [!DNL Adobe Commerce Optimizer], voir [[!DNL Adobe Commerce Optimizer] Outils de marchandisage](../optimizer/overview.md#quick-tour).

## Workflows standard {#typical-workflows}

Ces workflows décrivent comment les équipes configurent et utilisent le [!DNL Adobe Commerce Optimizer Connector]. Pour plus d’informations sur la configuration de l’intégration et l’activation de ces workflows, voir [Prise en main](get-started.md).

### Installation et configuration initiales {#initial-setup}

Voir [Étapes de configuration](./get-started.md#configuration-steps) dans le guide _Prise en main_.

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

- Pour [!DNL Adobe Commerce] opérations de resynchronisation de l’interface de ligne de commande, reportez-vous à la commande [CLI resync](../data-export/data-export-cli-commands.md#sync-using-cli-commands){target="_blank"}
- [Modules [!DNL Commerce Optimizer Connector] et points d’entrée de flux](reference/connector-reference.md)
- [Mappage des champs pour les flux du connecteur](reference/field-mapping.md)

### Configurer le marchandisage et les storefronts {#merchandising-storefronts}

Une fois que [!DNL Adobe Commerce] données sont disponibles dans [!DNL Adobe Commerce Optimizer], utilisez [[!DNL Commerce Optimizer] Studio](https://experienceleague.adobe.com/en/docs/commerce/optimizer/overview#quick-tour) pour connecter les expériences de marchandisage et de storefront à votre catalogue synchronisé.

**Pour configurer le marchandisage et les storefronts dans [!DNL Commerce Optimizer] Studio :**

1. **Créer des vues et des politiques de catalogue** à partir du menu [!UICONTROL Store setup].

   - Filtrer le catalogue par marque, région, segment client ou canal
   - Application des règles d’accès aux données par storefront ou partenaire

1. **Configurer la découverte de produit et les recommandations** à partir du menu [!UICONTROL Merchandising].

   - Création de règles de marchandisage, de facettes, de synonymes et d’unités de recommandation
   - Le connecteur décharge toute la configuration de recherche et de recommandation sur [!DNL Commerce Optimizer] ([!DNL Live Search] règles et les [!DNL Product Recommendations] de l’administrateur Commerce ne s’appliquent plus à ces flux)

1. **Connectez vos storefronts** pour [!DNL Commerce Optimizer] :

   - Pour un storefront Commerce optimisé par [!DNL Edge Delivery Services], configurez-le pour utiliser le client Optimizer et la vue de catalogue corrects, et pour appeler les points d’entrée de recherche et de recommandation via l’API de marchandisage
   - Pour les storefronts tiers, utilisez les API ou SDK publics Optimizer pour les appels de recherche et de recommandation

   >[!NOTE]
   >
   >Pour obtenir un exemple d’intégration tierce, consultez la section Connecteur Commerce Salesforce [&#x200B; [!DNL Adobe Commerce Optimizer]](../optimizer/developer/salesforce-connector.md).

1. **Conserver le passage en caisse** sur votre plateforme existante :

   - conserver le panier, le passage en caisse, la gestion des commandes et les comptes clients dans un [!DNL Adobe Commerce] ou une plateforme tierce ;
   - Utilisez des [!DNL App Builder] et des [!DNL API Mesh] pour la remise du panier lorsque vous intégrez des systèmes de paiement externes

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

- Vérifiez que [!DNL Adobe Commerce] répond aux exigences minimales de version et de [!DNL Commerce Optimizer Connector]. Voir [Prise en main](get-started.md#requirements-to-use-the-integration) pour plus d’informations.
- Assurez-vous de disposer de l’accès à l’organisation IMS, d’une instance [!DNL Adobe Commerce Optimizer], ainsi que des informations d’identification et de région nécessaires.

## Documentation connexe {#related-documentation}

- Configurez l’intégration et activez les workflows clés : [Prise en main de l’ [!DNL Commerce Optimizer Connector]](get-started.md)
- En savoir plus sur [!DNL Adobe Commerce Optimizer] concepts et l’architecture : [En quoi consiste  [!DNL Adobe Commerce Optimizer] ?](../optimizer/overview.md)
- Découvrez le mécanisme de synchronisation, l’initialisation et la gestion des erreurs : [pipeline de synchronisation du connecteur](connector-sync-pipeline.md)
- Mappage des données au niveau du champ pour tous les flux : [Mappage des champs pour les flux du connecteur](reference/field-mapping.md)
- Intégrer des storefronts découplés à l’aide de GraphQL et du codage de bundle : [Intégration de storefront découplé](headless-storefront.md)
- Diagnostiquer les problèmes de synchronisation et de configuration : [dépannage](troubleshooting.md)
