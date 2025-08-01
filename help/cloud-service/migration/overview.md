---
title: Migrer vers  [!DNL Adobe Commerce as a Cloud Service]
description: Découvrez comment migrer vers [!DNL Adobe Commerce as a Cloud Service].
exl-id: 9065c92a-f6b2-4464-8ec0-5c549bf78104
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
role: Architect
source-git-commit: 2ecf5e0960b2e63cc95016e8ee5509b3c475de13
workflow-type: tm+mt
source-wordcount: '3031'
ht-degree: 0%

---

# Migrer vers [!DNL Adobe Commerce as a Cloud Service]

[!DNL Adobe Commerce as a Cloud Service] fournit un guide complet pour les développeurs et développeuses qui passent d’une implémentation Adobe Commerce PaaS existante à la nouvelle offre Adobe Commerce as a Cloud Service (SaaS). Adobe Commerce as a Cloud Service représente une transition importante vers un modèle SaaS entièrement géré et sans version, offrant des performances améliorées, une évolutivité, des opérations simplifiées et une intégration plus étroite avec Adobe Experience Cloud au sens large.

>[!NOTE]
>
>Pour plus d’informations sur les outils de migration, consultez la section [ Outil de migration de données en bloc ](./bulk-data.md).

## Comprendre le changement - comparer PaaS et SaaS

**Principales différences**

* [!BADGE PaaS uniquement]{type=Informative url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."} **PaaS (actuel)** : le commerçant gère le code de l’application, les mises à niveau, les correctifs et la configuration de l’infrastructure dans l’environnement hébergé d’Adobe. [ Modèle de responsabilité partagée ](https://experienceleague.adobe.com/fr/docs/commerce-operations/security-and-compliance/shared-responsibility) pour les services (MySQL, Elasticsearch et autres).
* [!BADGE SaaS uniquement]{type=Positive url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."} **SaaS (nouveau - [!DNL Adobe Commerce as a Cloud Service])** : Adobe gère entièrement l’application principale, l’infrastructure et les mises à jour. Les commerçants se concentrent sur la personnalisation via des points d’extensibilité (API, App Builder, SDK d’interface utilisateur). Le code de l’application principale est verrouillé.

**Implications architecturales**

* **Plateforme sans version** : les mises à jour continues n’impliquent plus de mises à niveau de versions majeures pour le cœur de l’application.
* **Microservices et API-first** : confiance accrue dans les API pour l’extensibilité et l’intégration.
* **Headless par défaut (facultatif)** : Prise en charge renforcée des storefronts découplés (par exemple, le storefront Commerce optimisé par Edge Delivery Services).
* **Edge Delivery Services** : impact sur les performances front-end et le déploiement.

**Nouveaux outils et concepts**
* [Maillage Adobe Developer App Builder](https://developer.adobe.com/app-builder/) et [API pour Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway)
* [Commerce Optimizer](../../optimizer/overview.md)
* [Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=fr)
* Approvisionnement en libre-service avec [Commerce Cloud Manager](../getting-started.md#create-an-instance)

## Chemins de migration

[!DNL Adobe Commerce as a Cloud Service] prend en charge plusieurs chemins de migration, selon votre chronologie, votre storefront et vos personnalisations.

Au lieu d’une migration complète, [!DNL Adobe Commerce as a Cloud Service] prend en charge une migration par phases, à l’aide de Commerce Optimizer ou d’une approche incrémentielle.

* **Migration incrémentielle** : cette approche implique la migration de vos données, de vos personnalisations et de vos intégrations par étapes. Cette approche est idéale pour les grands commerçants avec de nombreuses personnalisations qui souhaitent effectuer une transition progressive de leurs personnalisations et données complexes vers [!DNL Adobe Commerce as a Cloud Service] à leur propre rythme.

![migration incrémentielle](../assets/incremental.png){width="600" zoomable="yes"}

* **Commerce Optimizer**—Cette approche vous permet de migrer de manière itérative, en utilisant Commerce Optimizer comme phase de transition pour déplacer des personnalisations et des données complexes vers [!DNL Adobe Commerce as a Cloud Service] à votre propre rythme. Commerce Optimizer permet d’accéder aux services de marchandisage optimisés par les vues et politiques de catalogue, au storefront Commerce optimisé par Edge Delivery et aux visuels de produit optimisés par AEM Assets.

![ migration itérative ](../assets/optimizer.png){width="600" zoomable="yes"}

* **Migration complète** : cette approche implique la migration de toutes les données, personnalisations et intégrations en une seule fois. Cette approche est idéale pour les petits commerçants ayant peu de personnalisations et qui souhaitent passer rapidement au [!DNL Adobe Commerce as a Cloud Service].

Le tableau suivant présente un aperçu du processus de migration pour différents storefronts et configurations :

|                    | STOREFRONT LUMA | PWA Storefront | Commerce Storefront optimisé par Edge Delivery | Découplé |
|--------------------|----------------------------------------|----------------------------------------|------------------------------------------------------|----------------------------------------|
| Migration des données | Obligatoire | Obligatoire | Obligatoire | Obligatoire |
| Storefront | Migration vers Commerce Storefront optimisé par Edge Delivery | Migrer vers le storefront Commerce optimisé par Edge Delivery ou maintenir | Pas d&#39;impact | Pas d&#39;impact |
| Maillage API | Créer un nouveau maillage | Créer un nouveau maillage ou reconfigurer un maillage existant | Créer un nouveau maillage ou reconfigurer un maillage existant | Créer un nouveau maillage ou reconfigurer un maillage existant |
| Intégrations | Utilisation du kit de démarrage de l’intégration | Utilisation du kit de démarrage de l’intégration | Utilisation du kit de démarrage de l’intégration | Utilisation du kit de démarrage de l’intégration |
| Personnalisations | Déplacer vers App Builder et le maillage API | Déplacer vers App Builder et le maillage API | Déplacer vers App Builder et le maillage API | Déplacer vers App Builder et le maillage API |
| Gestion d’Assets | Migration requise en cas d’utilisation d’OOTB | Migration requise en cas d’utilisation d’OOTB | Migration requise en cas d’utilisation d’OOTB | Migration requise en cas d’utilisation d’OOTB |
| Extensions | Migrer vers App Builder | Migrer vers App Builder | Migrer vers App Builder | Migrer vers App Builder |

Comme l’indique le tableau, les mesures d’atténuation pour chaque migration seront les suivantes :

* **Migration des données** : à l’aide de l’[outil de migration](./bulk-data.md) fourni pour migrer les données de votre instance existante vers [!DNL Adobe Commerce as a Cloud Service].
* **Storefront** : les storefronts Commerce existants optimisés par Edge Delivery et les storefronts découplés ne nécessitent pas d’atténuation, mais les storefronts Luma nécessitent une migration vers le storefront Commerce optimisé par Edge Delivery. Les storefronts PWA Studio peuvent être migrés vers les storefronts Commerce optimisés par Edge Delivery ou maintenus dans leur état actuel. Adobe fournira des accélérateurs pour faciliter la migration des storefront.
* **[Maillage API](https://developer.adobe.com/graphql-mesh-gateway)** : créez un nouveau maillage ou modifiez le maillage existant. Adobe fournira des maillages préconfigurés pour faciliter ce processus.
* **Intégrations** : toutes les intégrations doivent utiliser le [kit de démarrage de l’intégration](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/) ou l’API [[!DNL Adobe Commerce as a Cloud Service] REST](https://developer.adobe.com/commerce/webapi/reference/rest/saas/).
* **Personnalisations** : toutes les personnalisations doivent être déplacées vers App Builder et le maillage API.
* **Gestion Assets**—La gestion de toutes les ressources nécessite une migration. Si vous utilisez déjà AEM Assets, il n’est pas nécessaire d’effectuer une migration.
* **Extensions** : toutes les extensions en cours de traitement doivent être recréées en tant qu’extensions hors processus. D’ici la fin de l’année 2025, Adobe donnera accès à nos extensions les plus populaires afin de réduire les temps de création.

## Phases de migration

Les phases suivantes décrivent les étapes et considérations nécessaires pour migrer vers [!DNL Adobe Commerce as a Cloud Service].

### Évaluation et planification préalables à la migration

Cette phase est essentielle pour minimiser les risques, établir un chemin de migration clair et identifier les problèmes avant qu’ils ne se produisent.

**Découverte et audit de l’environnement actuel**

**Analyse Codebase :**

* Identifiez tous les modules, thèmes et remplacements personnalisés.
* Analysez les modifications du code principal et déterminez celles qui nécessiteront une refactorisation dans le cadre de la migration.
* Évaluez les extensions tierces et déterminez leur compatibilité avec [!DNL Adobe Commerce as a Cloud Service]. Existe-t-il des alternatives compatibles avec SaaS ou devez-vous créer des intégrations d’API personnalisées ou des applications App Builder ?
* Identifiez tout code ou toute fonctionnalité obsolète qui ne sera pas migré.

**Audit des données :**

* Évaluez la taille et la complexité de votre base de données.
* Identifiez les données ou les tables inutilisées pour le nettoyage.
* Passez en revue les processus d’import/export de données existants.

**Révision des intégrations :**

* Répertoriez tous les systèmes externes intégrés à Adobe Commerce (ERP, CRM, PIM, passerelles de paiement, fournisseurs d’expédition, OMS et tous les autres systèmes).
* Évaluez les méthodes d’intégration (API, scripts personnalisés et autres méthodes).
* Évaluez la compatibilité avec l’approche API-first de [!DNL Adobe Commerce as a Cloud Service] et App Builder.

**Références de performances :**

* Documentez les scores Lighthouse actuels, les temps de chargement des pages et les indicateurs clés de performance (KPI), qui fournissent une base de référence pour mesurer les améliorations post-migration.

**Révision de la configuration de sécurité :**

* Évaluez les règles WAF personnalisées, les places sur la liste autorisée IP et toute autre configuration de sécurité.

**Définir la portée et la stratégie de migration :**

* **Migration par phases ou migration tout-en-un :** évaluez les avantages et les inconvénients de chaque approche.
* **Identifier les processus métier principaux :** les fonctionnalités qui doivent être migrées en premier, telles que :
   * Règles de tarification complexes
   * Règles métier personnalisées appliquées avant qu&#39;une commande ne soit officiellement passée ou traitée
   * Calculs d&#39;impôts complexes
   * Validations d’adresses
   * Logique personnalisée déclenchée après le passage d’une commande
* **Storefront découplé ou monolithique :** point de décision pour le développement d’un nouveau storefront ou l’adaptation de storefronts existants.
* **Stratégie d’intégration :** déterminer comment les intégrations existantes seront reformées (maillage API, App Builder, API directe).
* **Stratégie de migration des données :** déterminez si vous avez l’intention de migrer à l’aide de données historiques complètes, de données partielles ou sans données migrées.

**Préparation et formation de l’équipe :**

* Familiarisez-vous avec les concepts [!DNL Adobe Commerce as a Cloud Service], les processus de développement et les nouveaux outils.
* Participez à une formation pratique sur les pipelines de déploiement Adobe App Builder, Edge Delivery Services et [!DNL Adobe Commerce as a Cloud Service].

**Configuration et approvisionnement de l’environnement :**

* Configurez votre sandbox [!DNL Adobe Commerce as a Cloud Service] et vos environnements de développement à l’aide de Commerce Cloud Manager.

### Phases de migration incrémentielle

**Refactorisation stratégique et externalisation**

Cette phase se compose du cœur de la migration et se concentre sur l’adaptation de votre base de code au paradigme natif du cloud [!DNL Adobe Commerce as a Cloud Service]. Cela implique l’adoption stratégique de nouveaux services Adobe et le déplacement de la logique personnalisée en dehors de la plateforme Commerce principale.

#### &#x200B;1. Migration des personnalisations et des extensions « en cours » vers App Builder

Il s’agit d’une phase cruciale pour réaliser un « noyau verrouillé » et pérenniser votre solution, au cœur de la philosophie architecturale [!DNL Adobe Commerce as a Cloud Service].

* **Externaliser une logique complexe vers App Builder** : analysez les modules personnalisés et les extensions tierces existants dans votre base de code PaaS. Pour une logique commerciale complexe, des intégrations sur mesure ou des microservices qui ne nécessitent pas de manipulation directe et en cours de processus du modèle de données Commerce principal, refactorisez-les et reformez-les en tant qu’applications sans serveur dans Adobe Developer App Builder.
* **Tirer parti du maillage API** : pour les scénarios nécessitant des données provenant de plusieurs systèmes principaux (par exemple, votre serveur principal Commerce PaaS, ERP, CRM et microservices App Builder personnalisés), implémentez une couche de maillage API dans App Builder. Cela consolide des API disparates en un point d’entrée GraphQL unique et performant utilisé par votre nouveau storefront ou d’autres services, simplifiant la récupération de données complexes.
* **Architecture pilotée par les événements** : utilisez Adobe I/O Events pour déclencher des actions App Builder en fonction des événements se produisant dans votre instance PaaS (par exemple, mises à jour de produit, enregistrements de clients, changements de statut de commande) ou d’autres systèmes connectés. Cela favorise la communication asynchrone, réduit le couplage étroit et améliore la résilience du système.

**Avantage** : cette étape réduit considérablement la dette technique associée aux personnalisations profondément intégrées, accélère considérablement la transition de votre instance Commerce vers [!DNL Adobe Commerce as a Cloud Service], améliore l’évolutivité et le déploiement indépendant de la logique personnalisée et favorise des cycles de développement plus rapides pour les extensions.

#### &#x200B;2. Adoptez les services de marchandisage Adobe Commerce basés sur SaaS et intégrez les données de catalogue

Il s’agit d’un point d’intégration initial essentiel avec deux options concernant la gestion des données de catalogue :

>[!BEGINTABS]

>[!TAB Option 1 - Service SaaS de catalogue existant]

**Utilisation du service SaaS de catalogue existant intégré au serveur principal PaaS**

Cette option sert d’étape transitoire, s’appuyant sur une intégration existante où votre serveur principal PaaS renseigne une instance existante du service SaaS Adobe Commerce avec des données provenant des [service de catalogue](../../catalog-service/guide-overview.md), [recherche en direct](../../live-search/overview.md) et [recommandations de produits](../../product-recommendations/overview.md).

* **Synchronisation des données de catalogue** : assurez-vous que votre instance Adobe Commerce PaaS continue à synchroniser les données de produit et de catalogue avec votre service Adobe Commerce Catalog SaaS existant. Cela repose généralement sur des connecteurs ou des modules établis au sein de votre instance PaaS. Le service SaaS de catalogue reste la source faisant autorité pour les fonctions de recherche et de marchandisage, et ses données proviennent de votre serveur principal PaaS.
* **Maillage API pour l’optimisation** : bien que le storefront découplé (sur Edge Delivery Services) et d’autres services puissent directement consommer des données du service SaaS de catalogue, Adobe recommande vivement d’utiliser le maillage API (dans App Builder). Le maillage API permet d’unifier les API du service SaaS de catalogue avec d’autres API nécessaires de votre serveur principal PaaS (par exemple, les vérifications d’inventaire en temps réel de la base de données transactionnelle ou les attributs de produit personnalisés qui ne sont pas entièrement répliqués vers le service SaaS de catalogue) en un seul point d’entrée GraphQL performant. Cela permet également la mise en cache, l’authentification et la transformation de réponse centralisées.
* **Intégrer la recherche en direct et les recommandations de produits** : configurez les services SaaS de recherche en direct et de recommandations de produits pour [ingérer des données de catalogue](https://experienceleague.adobe.com/fr/docs/commerce/live-search/install#configure-the-data) directement à partir de votre service SaaS de catalogue Adobe Commerce existant, qui est à son tour renseigné par votre serveur principal PaaS.

**Avantage** : permet d’accéder plus rapidement à un storefront découplé et à des fonctionnalités de marchandisage SaaS avancées en exploitant un service SaaS de catalogue existant et opérationnel et son pipeline d’intégration à votre serveur principal PaaS. Cependant, il conserve la dépendance sur le serveur principal PaaS pour la source de données de catalogue principale et ne fournit pas les fonctionnalités d’agrégation multi-source inhérentes au nouveau modèle de données de catalogue composable. Cette option est une étape valide vers une architecture composable plus complète.

>[!TAB Option 2 - Modèle de données de catalogue composable]

**Adoption du nouveau modèle de données de catalogue composable (CCDM)**

Il s’agit de l’approche stratégique à l’épreuve du temps pour tirer parti de Adobe Commerce Optimizer. Le CCDM fournit un service de catalogue flexible, évolutif et unifié conçu pour l’agrégation de données multi-sources et le marchandisage dynamique.

* **Ingestion et unification des données**
   * Commencez par ingérer des données de produit et de catalogue à partir de votre instance Adobe Commerce PaaS existante (et/ou d’autres systèmes PIM/ERP) dans le nouveau modèle de données de catalogue composable (CCDM).
   * Mappez les attributs de produit existants au schéma flexible du CCDM. Hiérarchisez les données de produit critiques pour l’ingestion initiale.
   * Établir des pipelines de données robustes pour une synchronisation continue. Cela peut impliquer :
      * **Piloté par les événements** (via App Builder) : utilisez Adobe I/O Events à partir de votre instance PaaS pour déclencher des applications Adobe App Builder personnalisées ou accessibles au public. Ces applications transforment et transmettent les modifications de données (création, mise à jour et suppression) au CCDM via ses API.
      * **Ingestion par lots** : pour les chargements initiaux volumineux ou les mises à jour en bloc périodiques, utilisez des transferts de fichiers sécurisés (par exemple, CSV ou JSON) vers une zone de transit, traités par les services d’ingestion Adobe Experience Platform (AEP) dans CCDM.
      * **Intégration directe de l’API** (avec orchestration App Builder) : pour les scénarios plus complexes, App Builder peut agir comme une couche d’orchestration, effectuer des appels directs d’API vers votre serveur principal PaaS, transformer les données et les transmettre au CCDM.
* **Vue Catalogue et définition de politique** : configurez des vues de catalogue (regroupements logiques pour une présentation de catalogue unique, telle que des vues de magasin, des régions et des segments B2B/B2C) et définissez des politiques (ensembles de règles pour la présentation, le filtrage et le marchandisage des produits) dans le CCDM. Cela permet un contrôle dynamique sur les assortiments de produits et la logique d’affichage par vue de catalogue.
* **Intégrer la recherche en direct et les recommandations de produits** : une fois que les données de catalogue sont présentes dans le CCDM, intégrez les services de recherche en direct et de recommandations de produits basés sur SaaS Adobe. Ils exploitent des modèles d’IA d’Adobe Sensei et de machine learning pour une pertinence de recherche supérieure et des recommandations personnalisées, et consomment des données directement à partir du CCDM.

**Avantage** : en abstrayant la gestion et la découverte de catalogues dans le CCDM et les services SaaS associés, vous améliorez les performances, obtenez des fonctionnalités de marchandisage pilotées par l’IA, déchargez considérablement les opérations de lecture de votre ancien serveur principal et activez une solide expérience d’extraction de la partie supérieure de l’entonnoir.

>[!ENDTABS]

#### &#x200B;3. Créer votre storefront sur Edge Delivery Services

Avec la mise en place de pipelines de données de marchandisage et l’externalisation des personnalisations, l’accent se déplace vers la création de votre front-end haute performance.

* **Configuration initiale** : configurez votre projet à l’aide de la norme standard d’Adobe Commerce Storefront pour Edge Delivery Services. Il s’agit d’un front-end découplé fondamental basé sur les technologies web modernes.
* **Connexion aux services de catalogue et au maillage API** : votre storefront Commerce consommera des données principalement par le biais des API GraphQL :
   * **Option 1** : à partir du service SaaS de catalogue existant (via le maillage API) pour obtenir des informations sur les produits et les règles de marchandisage.
   * **Option 2** : du CCDM pour les informations sur les produits et les règles de marchandisage.
   * À partir du maillage API pour toutes les données orchestrées de votre serveur principal hérité (instance PaaS) ou des services App Builder personnalisés (par exemple, l’inventaire en temps réel, les attributs de produit personnalisés et les points de fidélité s’affichent).
* **Migration de contenu (AEM Services)** : migrez votre contenu statique existant (par exemple, les pages « À propos de nous », les publications de blog et les bannières marketing) vers AEM Services, qui alimente Commerce Storefront. Tirez parti des fonctionnalités de création de contenu d’AEM et assurez-vous que les ressources sont optimisées pour Edge Delivery Services.
* **Développement des composants principaux de l’interface utilisateur** : créez des composants d’interface utilisateur essentiels pour les pages de détails du produit (PDP), les pages de liste de produits (PLP) et les pages de contenu général à l’aide des composants déroulants Edge Delivery Services et des composants React/Vue personnalisés. Hiérarchisez les principaux flux commerciaux.
* **Intégration au panier/passage en caisse existant** : au départ, le storefront Edge Delivery Services orchestre un transfert vers votre PaaS Adobe Commerce existant (ou une autre plateforme tierce) pour la gestion du panier et le passage en caisse. Cela implique généralement :
   * **Redirection** : redirection de l’utilisateur vers les URL de panier et de passage en caisse natives de la plateforme héritée, en transmettant les identifiants de session et de panier nécessaires.
   * **Interaction directe avec l’API** (avec l’orchestration App Builder) : création de composants personnalisés de l’interface utilisateur de panier et de passage en caisse dans Edge Delivery Services qui interagissent directement avec les API de panier et de passage en caisse du serveur principal PaaS. Cela implique souvent App Builder en tant que serveur principal pour front-end (BFF) pour orchestrer des appels vers plusieurs services principaux (par exemple, le panier PaaS, les passerelles de paiement et les calculatrices d’expédition).

**Avantage** : offre une expérience de storefront ultra-rapide, optimisée pour l’optimisation du référencement et très flexible. Cette phase contribue directement à une expérience client supérieure et jette les bases de l’innovation frontale future.

#### &#x200B;4. Migration des données (processus échelonné)

La migration des données est un processus critique à plusieurs facettes qui s’exécute simultanément à la refactorisation et au développement du storefront, afin d’assurer la cohérence et l’intégrité des données.

* **Nettoyer et optimiser les données existantes** : avant toute migration à grande échelle, effectuez un nettoyage, une déduplication et une validation complets des données sur votre base de données PaaS existante. Cette étape proactive est essentielle pour minimiser le transfert des problèmes de données hérités et assurer la qualité des données dans le nouvel environnement.

**Migration des données en bloc**

La migration de données en bloc implique de prendre une image mémoire complète des données de votre instance Adobe Commerce PaaS, de transformer l’ensemble de ce jeu de données et de l’importer dans Adobe Commerce as a Cloud Service en même temps. Cette méthode est généralement utilisée pour la population initiale de données.

* **Disponibilité des outils** : un [outil de migration de données en bloc](./bulk-data.md) dédié à l’utilisation par les clients pour les migrations de données en bloc Commerce propriétaires sera disponible sur demande à la mi-juillet 2025. Si les clients ont besoin d’aide à la migration de données en bloc au préalable, Adobe peut faciliter le transfert de données en leur nom sur demande.

* **Processus** :
   * **Exportation complète des données** : extrayez un jeu de données complet de votre instance Adobe Commerce PaaS (par exemple, les produits, les catégories, les comptes clients, les données de commande historiques, les blocs statiques et le contenu de page).
   * **Transformation des données** : effectuez les transformations nécessaires pour aligner les données extraites sur les exigences de schéma des nouveaux composants Adobe Commerce as a Cloud Service, y compris le modèle de données de catalogue composable (CCDM), le cas échéant, et tous les autres services ou bases de données Adobe pertinents. Cela peut impliquer des scripts personnalisés ou des outils de mappage de données spécialisés.
   * **Import initial** : importez le jeu de données complet transformé dans les composants respectifs d’Adobe Commerce as a Cloud Service. Pour les données de produit et de catégorie, cela renseigne le service de catalogue choisi (CCDM ou SaaS de catalogue existants). Pour les données de commande et de client, cela renseigne le serveur principal transactionnel ou les services associés.
   * **Validation** : validez rigoureusement les données importées afin de garantir l’exhaustivité, la précision et la cohérence sur tous les nouveaux systèmes.

**Migrations de données itératives**

Les migrations de données itératives se concentrent sur la synchronisation des modifications incrémentielles et des deltas de l&#39;instance PaaS source vers les nouveaux composants Cloud Service, en assurant la fraîcheur des données jusqu&#39;au basculement et après.

* **Disponibilité des outils** : des outils spécifiquement conçus pour les migrations de données itératives seront disponibles au second semestre 2025.

* **Processus** :
   * **Identification Delta** : définissez des mécanismes pour identifier les modifications (créations, mises à jour et suppressions) dans les jeux de données critiques de votre environnement PaaS depuis la dernière synchronisation. Cela peut impliquer la capture de données de modification (CDC), des comparaisons d’horodatage ou des déclencheurs basés sur un événement.
   * **Synchronisation continue** : mettez en œuvre des mécanismes robustes pour une synchronisation incrémentielle continue des données de votre environnement PaaS vers les nouveaux composants Cloud Service (par exemple, CCDM et serveur principal transactionnel). Cela est essentiel pour maintenir la fraîcheur des données et minimiser le temps d’arrêt pendant la transition.
   * **Utilisation d’événements** : utilisez Adobe I/O Events dans la mesure du possible pour déclencher des actions App Builder pour les mises à jour en temps réel ou en quasi temps réel de votre instance PaaS vers les nouveaux services. Par exemple, une mise à jour de produit dans PaaS peut déclencher un événement qui met à jour l’entrée correspondante dans CCDM.
   * **Mises à jour pilotées par les API** : pour les données qui ne sont pas pilotées par les événements, utilisez des appels API planifiés (via App Builder ou d’autres plateformes d’intégration) pour extraire les modifications de PaaS et les pousser vers les nouveaux systèmes.
   * **Gestion et surveillance des erreurs** : implémentez une gestion, une journalisation et une surveillance des erreurs robustes pour tous les pipelines de données itératives afin de garantir l’intégrité des données tout au long du processus.

### Post-migration et opérations en cours

**Basculement et activation DNS :**

* Planifiez avec soin le basculement DNS avec un temps d’arrêt minimal.
* Surveillez l’intégrité et les performances du site immédiatement après le lancement.

**Opérations après le lancement :**

**Déclassement de l’environnement PaaS :**

* Archivez ou supprimez en toute sécurité les anciennes instances et données PaaS après la période de validation.

**Workflow de développement en cours :**

* Adoptez la nature sans version d’[!DNL Adobe Commerce as a Cloud Service], qui comporte de petits déploiements continus plutôt que de grandes mises à niveau.
* Utilisez Cloud Manager pour gérer les environnements et les déploiements.
* Tirez parti d’App Builder pour étendre les fonctionnalités sans affecter le cœur de la solution.

**Surveillance, performance et sécurité :**

* Surveillez en permanence les performances, les erreurs et les journaux de sécurité du site.
* Utilisez les fonctionnalités de sécurité intégrées d’Adobe et suivez les bonnes pratiques.

**Formation et documentation :**

* Formez les nouveaux développeurs et utilisateurs professionnels à la plateforme et aux workflows [!DNL Adobe Commerce as a Cloud Service].
* Mettez à jour la documentation interne pour les intégrations et les processus personnalisés.
