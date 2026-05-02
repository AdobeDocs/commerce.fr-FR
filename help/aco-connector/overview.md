---
title: Connecteur Adobe Commerce Optimizer
description: Découvrez comment connecter vos données de votre projet cloud ou local Commerce à Adobe Commerce Optimizer
feature: Personalization, Integration, Configuration
badgePaas: label="PaaS uniquement" type="Informative" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."
source-git-commit: c9cce4766ef3f30390d50f53237328be1cfeefdf
workflow-type: tm+mt
source-wordcount: '1233'
ht-degree: 0%

---


# Connecteur Adobe Commerce Optimizer

Le connecteur Adobe Commerce Optimizer est une intégration native et propriétaire entre Adobe Commerce (cloud ou sur site) et Adobe Commerce Optimizer. Il synchronise les données de catalogue et de prix de vos magasins Adobe Commerce dans Commerce Optimizer afin que vous puissiez :

- Puissance **découverte et recommandations de produits pilotées par l’IA**
- Exécutez **storefronts découplés hautes performances** (y compris les storefronts Commerce optimisés par Edge Delivery).
- Analysez les indicateurs de performance clés **avant et après** et l’intégrité de la synchronisation des données à un seul endroit

Commerce reste votre système d’enregistrement pour les produits, les prix et la structure de catalogue. Commerce Optimizer devient votre couche d’expérience et de marchandisage, offrant des résultats rapides et pertinents à n’importe quel storefront ou canal connecté.

## Principaux avantages {#key-benefits}

| Bénéfice | Ce que cela signifie pour vous |
| --- | --- |
| **Aucun connecteur personnalisé à créer** | Utilisez une intégration propriétaire prise en charge au lieu d’écrire et de gérer des flux et des scripts personnalisés. |
| **Retour sur investissement plus rapide avec Commerce Optimizer** | Activez Recherche optimisée par l&#39;IA, les recommandations et les vitrines découplées en plus de votre déploiement Adobe Commerce existant. |
| **Aligné sur les portées de Commerce** | Mappe automatiquement les sites web, les affichages de boutique et les groupes de clients dans des éléments de catalogue Commerce Optimizer (sources de catalogue et tarifs). |
| **Visibilité opérationnelle** | Surveillez l’intégrité du flux, les heures de la dernière synchronisation et l’état par SKU à partir d’une vue dédiée État de synchronisation des flux de données . |
| **Une voie vers le SaaS tournée vers l&#39;avenir** | Fournit un chemin de modernisation à faible risque de PaaS vers Adobe Commerce as a Cloud Service + Optimizer, sans replateforme. |

## Architecture du connecteur {#connector-architecture}

Le diagramme suivant illustre l’architecture de bout en bout du connecteur, d’Adobe Commerce à Commerce Optimizer, en passant par les storefronts et les systèmes de passage en caisse.

![Diagramme d&#39;architecture de bout en bout du connecteur Commerce Optimizer Commerce](./assets/aco-connector-end2end-architecture.png){width="700" zoomable="yes"}

Dans cette architecture :

- Adobe Commerce (sur le cloud ou sur site) est le système d’enregistrement et le producteur de flux
- Le connecteur exporte les flux de catalogue, de prix et de catégories
- Commerce Optimizer ingère et normalise les données de flux dans les sources de catalogue, les catalogue de prix et les vues de catalogue
- Les storefronts (storefront Commerce sur Edge Delivery ou builds découplés personnalisés) appellent les API Commerce Optimizer GraphQL pour la découverte et les recommandations et appellent Commerce ou une autre plateforme tierce connectée pour les opérations de panier et de passage en caisse

## Fonctionnement du connecteur avec Adobe Commerce {#how-it-works}

- Commerce Optimizer ingère et normalise les données de flux dans les sources de catalogue, les livres de prix et les vues de catalogue.

- Les storefronts (storefront Commerce sur Edge Delivery ou builds découplés personnalisés) appellent les API Commerce Optimizer GraphQL pour la découverte et les recommandations et appellent Commerce ou une autre plateforme tierce connectée pour les opérations de panier et de passage en caisse.

## Fonctionnement du connecteur avec Adobe Commerce

Le connecteur Adobe Commerce Optimizer fonctionne en utilisant vos portées Commerce existantes (sites web et vues de magasin) et la segmentation de la clientèle pour renseigner le modèle de catalogue Commerce Optimizer :

![Mappage des données Commerce à Adobe Commerce Optimizer](/help/aco-connector/assets/storeview-to-catalogview-mapping.png){width="750" zoomable="yes"}

- **Vues de magasin → sources de catalogue** — Chaque vue de magasin devient une Source de catalogue distincte dans Commerce Optimizer. Cette source comprend des attributs de produit localisés et des données spécifiques à la vue du magasin
- **Sites Web → Catalogues de prix** — Chaque site Web Commerce est mappé à un ou plusieurs Catalogues de prix dans Commerce Optimizer. Tarification de site Web et exportation de prix de groupe client en tant que livres de prix et entrées de prix
- **Groupes de clients → Variantes de prix** — La tarification du groupe de clients Commerce apparaît en tant qu&#39;entrées supplémentaires dans les tarifs correspondants

Une fois que Commerce Optimizer a ingéré les données, vous pouvez configurer les éléments suivants :

- **Vues et politiques de catalogue** dans Commerce Optimizer (pour la création de sous-ensembles spécifiques à une région, une marque ou un client)
- **Découverte de produits** (recherche, facettes, règles de marchandisage)
- **Recommandations de produits**

Lorsque vous activez le connecteur, l’instance Adobe Commerce reste le système d’enregistrement des données de catalogue et de prix. Lorsque vous mettez à jour des données dans Commerce, le connecteur synchronise ces mises à jour sur l’instance [!DNL Adobe Commerce Optimizer].

>[!NOTE]
>
>Pour plus d’informations sur la configuration de Commerce Optimizer, voir [[!DNL Adobe Commerce Optimizer] Outils de marchandisage](../optimizer/overview.md#quick-tour).

## Workflows standard {#typical-workflows}

Ces workflows décrivent comment les équipes configurent et utilisent le connecteur Adobe Commerce Optimizer. Pour plus d’informations sur la configuration de l’intégration et l’activation de ces workflows, voir [Prise en main](get-started.md).

### Installation et configuration initiales {#initial-setup}

1. **Installez le package de connecteur dans Adobe Commerce** à l’aide du compositeur :

   `composer require adobe-commerce/commerce-data-export-aco-adapter`

1. **Configurez les détails d’authentification et d’environnement** dans Commerce Admin ou via l’interface de ligne de commande :

   ```terminal
   bin/magento aco:config:init \
     --org_id=<your-org> \
     --tenant_id=<your-tenant> \
     --client_id=<your-client-id> \
     --client_secret=<your-secret> \
     --region=na1 \
     --type=production
   ```

1. **Mappage des étendues de Commerce à Commerce Optimizer:**

   - Confirmer les sites web et les affichages de boutique qui doivent être inclus dans la portée
   - Assurez-vous que les groupes de clients et les règles de prix sont modélisés comme prévu

1. **Vérifier la connectivité :**

   - Exécutez une synchronisation de test et vérifiez que les sources de catalogue, les tarifs et les produits initiaux apparaissent dans Commerce Optimizer
   - Utiliser la page Statut de la synchronisation des flux de données dans Commerce et les tableaux de bord de synchronisation des données dans Commerce Optimizer pour la validation

### Synchronisation des données en cours {#ongoing-sync}

Après la configuration initiale, le connecteur prend en charge les éléments suivants :

- **Synchronisation complète du catalogue** pour la migration initiale ou des modifications structurelles importantes
- **Synchronisations delta** pour les mises à jour continues lorsque les produits ou les prix changent
- **Commandes de resynchronisation** pour les flux ciblés (y compris les catégories à partir de la version 1.0.12) :

   - `bin/magento saas:resync --feed=products`
   - `bin/magento saas:resync --feed=prices`
   - `bin/magento saas:resync --feed=categories`

### Configurer le marchandisage et les storefronts {#merchandising-storefronts}

Une fois que les données Commerce sont disponibles dans Commerce Optimizer, utilisez Commerce Optimizer Studio pour connecter les expériences de marchandisage et de storefront à votre catalogue synchronisé.

**Pour configurer le marchandisage et les storefronts :**

1. **Créer des vues de catalogue et des politiques** dans Commerce Optimizer Studio :

   - Filtrer le catalogue par marque, région, segment client ou canal
   - Application des règles d’accès aux données par storefront ou partenaire

1. **Configurer la découverte de produit et les recommandations** dans l’interface utilisateur d’Optimizer :

   - Création de règles de marchandisage, de facettes, de synonymes et d’unités de recommandation
   - Le connecteur transfère toute la configuration de recherche et de recommandation à Commerce Optimizer (les règles de recherche en direct et les recommandations de produits dans l’administration Commerce ne s’appliquent plus à ces flux)

1. **Connectez les storefronts** à Commerce Optimizer :

   - Pour un storefront Commerce optimisé par Edge Delivery Services, configurez-le pour utiliser le client Optimizer et la vue de catalogue corrects, et pour appeler les points d’entrée de recherche et de recommandation via l’API de marchandisage
   - Pour les storefronts tiers, utilisez les API ou SDK publics Optimizer pour les appels de recherche et de recommandation

   >[!NOTE]
   >
   >Pour obtenir un exemple d’intégration tierce, consultez Connecteur Salesforce Commerce pour Commerce Optimizer [&#128279;](../optimizer/developer/salesforce-connector.md).

1. **Conserver le passage en caisse** sur votre plateforme existante :

   - conserver le panier, le passage en caisse, la gestion des commandes et les comptes clients dans Adobe Commerce ou une plateforme tierce ;
   - Utiliser App Builder et le maillage API pour la remise de panier lorsque vous intégrez des systèmes de paiement externes

## Scénarios pris en charge {#supported-scenarios}

Le connecteur est conçu pour les commerçants B2C avec des déploiements sur le cloud et on-premise d’Adobe Commerce qui souhaitent adopter Commerce Optimizer sans reconstruire leur serveur principal.

**Cas d’utilisation courants :**

- **Modernisation du storefront uniquement**
Conservez votre serveur principal Commerce existant, déplacez PLP/Search/PDP vers les storefronts Edge Delivery optimisés par Commerce Optimizer.

- **Évolution des performances du catalogue et de la recherche**
Déchargez l’indexation de catalogue et la recherche lourdes vers les services SaaS de Commerce Optimizer tout en conservant la propriété des produits et des prix dans Commerce.

- **Adoption progressive du SaaS**
Utilisez le connecteur comme étape vers Adobe Commerce as a Cloud Service + Optimizer, avec un catalogue Commerce composable compatible

## Responsabilités et conditions préalables à la mise en œuvre {#responsibilities-prerequisites}

Commerce est la source de vérité pour les produits, les prix et les groupes de clients. Apportez des modifications dans Commerce ; le connecteur les synchronise avec Commerce Optimizer.

**Commerce Optimizer est responsable de :**

- Modélisation de catalogue (sources de catalogue, registres des prix, vues de catalogue, politiques)
- Découverte de produits et recommandations
- Mesures Storefront, tableaux de bord de synchronisation des données et rapports Mesures de succès

**Le connecteur ne :**

- Modifier les flux de panier, de passage en caisse ou de commande Commerce
- Approvisionnement automatique des projets de storefront (Commerce Storefront / Edge Delivery tooling handles that)

**Avant de commencer :**

- Vérifiez que Commerce répond à la configuration minimale requise en termes de version et de connecteur de services. Voir [Prise en main](get-started.md#prerequisites) pour plus d’informations.
- Assurez-vous de disposer de l’accès à l’organisation IMS, d’une instance [!DNL Adobe Commerce Optimizer], ainsi que des informations d’identification et de région nécessaires.

## Documentation connexe {#related-documentation}

- Configurez l’intégration et activez les workflows clés : [Prise en main du connecteur Adobe Commerce Optimizer](get-started.md)
- En savoir plus sur les concepts et l’architecture de Commerce Optimizer : [qu’est-ce que Adobe Commerce Optimizer ?](../optimizer/overview.md)
