---
title: Migrer vers  [!DNL Adobe Commerce as a Cloud Service]
description: Découvrez comment migrer vers [!DNL Adobe Commerce as a Cloud Service].
feature: Cloud
exl-id: 9065c92a-f6b2-4464-8ec0-5c549bf78104
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
role: Developer
level: Intermediate
source-git-commit: af56d52f98a83310b858f82f16693f5323c1b962
workflow-type: tm+mt
source-wordcount: '3016'
ht-degree: 0%

---

# Migrer vers [!DNL Adobe Commerce as a Cloud Service]

[!DNL Adobe Commerce as a Cloud Service] fournit un guide complet pour les développeurs et développeuses qui passent d’une implémentation Adobe Commerce PaaS existante à la nouvelle offre Adobe Commerce as a Cloud Service (SaaS). Adobe Commerce as a Cloud Service représente une transition importante vers un modèle SaaS entièrement géré et sans version, offrant des performances améliorées, une évolutivité, des opérations simplifiées et une intégration plus étroite avec le [!DNL Adobe Experience Cloud] au sens large.

>[!NOTE]
>
>Pour plus d’informations sur les outils de migration, consultez la section [&#x200B; Outil de migration de données en bloc &#x200B;](./bulk-data.md).

## Comprendre le changement - comparer PaaS et SaaS

**Principales différences**

* [!BADGE PaaS uniquement]{type=Informative url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."} **PaaS (actuel)** : Merchant gère le code de l’application, les mises à niveau, les correctifs et la configuration de l’infrastructure dans l’environnement hébergé de Adobe. [Modèle de responsabilité](https://experienceleague.adobe.com/fr/docs/commerce-operations/security-and-compliance/shared-responsibility) partagée pour les services (MySQL, Elasticsearch et autres).
* [!BADGE SaaS uniquement]{type=Positive url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."} **SaaS (Nouveau - [!DNL Adobe Commerce as a Cloud Service])** : Adobe gère entièrement l’application, l’infrastructure et les mises à jour principales. Les commerçants se concentrent sur la personnalisation via des points d’extensibilité (API, App Builder, SDK d’interface utilisateur). Le code de l’application principale est verrouillé.

**Implications architecturales**

* **Plate-forme** sans version : Les mises à jour continues signifient qu’il n’y a plus de mises à niveau majeures de la version pour le noyau.
* **Microservices et API-first** : dépendance accrue aux API pour l’extensibilité et l’intégration.
* **Headless par défaut (facultatif)** : prise en charge renforcée des vitrines découplées (par exemple, Boutique Commerce optimisée par Edge Delivery Services).
* **Edge Delivery Services** : impact sur les performances et le déploiement frontaux.

**Nouveaux outils et concepts**

* [Maillage Adobe Developer App Builder](https://developer.adobe.com/app-builder/) et [API pour Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway)
* [Commerce Optimizer](../../optimizer/overview.md)
* [Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=fr)
* Approvisionnement en libre-service avec [Commerce Cloud Manager](../getting-started.md#create-an-instance)

## Chemins de migration

[!DNL Adobe Commerce as a Cloud Service] Prend en charge plusieurs chemins de migration, en fonction de votre chronologie, de votre vitrine et de vos personnalisations.

Au lieu d’une migration complète, [!DNL Adobe Commerce as a Cloud Service] prend en charge une migration par phases, à l’aide de Commerce Optimizer ou d’une approche incrémentielle.

* **Migration incrémentielle** : cette approche implique la migration de vos données, de vos personnalisations et de vos intégrations par étapes. Cette approche est idéale pour les grands commerçants avec de nombreuses personnalisations qui souhaitent effectuer une transition progressive de leurs personnalisations et données complexes vers [!DNL Adobe Commerce as a Cloud Service] à leur propre rythme.

![migration incrémentielle](../assets/incremental.png){width="600" zoomable="yes"}

* **Commerce Optimizer**—Cette approche vous permet de migrer de manière itérative, en utilisant Commerce Optimizer comme phase de transition pour déplacer des personnalisations et des données complexes vers [!DNL Adobe Commerce as a Cloud Service] à votre propre rythme. Commerce Optimizer permet d’accéder aux services de marchandisage optimisés par les vues et politiques de catalogue, au storefront Commerce optimisé par Edge Delivery et à [!DNL Product Visuals powered by AEM Assets].

![Migration itérative](../assets/optimizer.png){width="600" zoomable="yes"}

* **Migration** complète : cette approche implique la migration simultanée de toutes les données, personnalisations et intégrations. Cette approche est idéale pour les petits commerçants avec peu de personnalisations et qui souhaitent passer rapidement à [!DNL Adobe Commerce as a Cloud Service].

Le tableau suivant fournit une vue d’ensemble du processus de migration pour différentes vitrines et configurations :

|                    | Vitrine LUMA | PWA Vitrine | Commerce Storefront optimisé par Edge Delivery | Découplé |
|--------------------|----------------------------------------|----------------------------------------|------------------------------------------------------|----------------------------------------|
| Migration des données | Obligatoire | Obligatoire | Obligatoire | Obligatoire |
| Vitrine | Migration vers Commerce Storefront optimisée par Edge Delivery | Migration vers Commerce Storefront optimisé par Edge Delivery ou maintenance | Pas d&#39;impact | Aucun impact |
| Maillage API | Créer un nouveau maillage | Créer un nouveau maillage ou reconfigurer un maillage existant | Créer un nouveau maillage ou reconfigurer un maillage existant | Créer un nouveau maillage ou reconfigurer un maillage existant |
| Intégrations | Tirer parti du kit de démarrage d’intégration | Tirer parti du kit de démarrage d’intégration | Tirer parti du kit de démarrage d’intégration | Tirer parti du kit de démarrage d’intégration |
| Personnalisations | Déplacer vers App Builder et le maillage API | Déplacer vers App Builder et le maillage API | Déplacer vers App Builder et le maillage API | Déplacer vers App Builder et le maillage API |
| Gestion d’Assets | Migration requise en cas d’utilisation d’OOTB | Migration requise en cas d’utilisation d’OOTB | Migration requise en cas d’utilisation d’OOTB | Migration requise en cas d’utilisation d’OOTB |
| Extensions | Migration vers App Builder | Migration vers App Builder | Migration vers App Builder | Migration vers App Builder |

Comme l’indique le tableau, les mesures d’atténuation pour chaque migration seront les suivantes :

* **Migration des données** : à l’aide de l’[outil de migration](./bulk-data.md) fourni pour migrer les données de votre instance existante vers [!DNL Adobe Commerce as a Cloud Service].
* **Storefront** : les vitrines Commerce existantes optimisées par Edge Delivery et les vitrines sans tête ne nécessitent pas d’atténuation, mais les vitrines Luma nécessitent une migration vers Commerce Storefront optimisées par Edge Delivery. PWA Studio vitrines peuvent être migrées vers Commerce Storefront optimisées par Edge Delivery ou conservées dans leur état actuel. Adobe fournira des accélérateurs pour faciliter la migration des vitrines.
* **[Maillage](https://developer.adobe.com/graphql-mesh-gateway)** API : créez un maillage ou modifiez le maillage existant. Adobe fournirons des maillages préconfigurés pour faciliter ce processus.
* **Intégrations : toutes les intégrations** doivent tirer parti du [kit](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/) de démarrage d’intégration ou de l’API [[!DNL Adobe Commerce as a Cloud Service] &#x200B;](https://developer.adobe.com/commerce/webapi/reference/rest/saas/)REST.
* **Personnalisations** : toutes les personnalisations doivent être déplacées vers App Builder et API Mesh.
* **Gestion Assets**—La gestion de toutes les ressources nécessite une migration. Si vous utilisez déjà [!DNL AEM Assets], il n’est pas nécessaire d’effectuer une migration.
* **Extensions** : toutes les extensions en cours de traitement doivent être recréées en tant qu’extensions hors processus. D’ici la fin de l’année 2025, Adobe donnera accès à nos extensions les plus populaires afin de réduire les temps de création.

## Phases de migration

Les phases suivantes décrivent les étapes nécessaires et les considérations relatives à la migration vers [!DNL Adobe Commerce as a Cloud Service].

### Évaluation et planification préalables à la migration

Cette phase est essentielle pour minimiser les risques, établir un chemin de migration clair et identifier les problèmes avant qu’ils ne se produisent.

**Découverte et audit de l’environnement actuel**

**Analyse de la base de code :**

* Identifiez tous les modules, thèmes et remplacements personnalisés.
* Analysez les modifications du code principal et déterminez celles qui devront être refactorisées dans le cadre de la migration.
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

**Évaluations de performances :**

* Documentez les scores Lighthouse actuels, les temps de chargement des pages et les indicateurs de performance clés (KPI), ce qui fournit une base de référence pour mesurer les améliorations post-migration.

**Examen de la configuration de la sécurité :**

* Évaluez toutes les règles WAF personnalisées, les listes d’adresses IP autorisées et toute autre configuration de sécurité.

**Définir la portée et la stratégie de migration :**

* **Migration par phases ou migration tout-en-un :** évaluez les avantages et les inconvénients de chaque approche.
* **Identifier les processus métier principaux :** hiérarchiser les fonctionnalités qui doivent être migrées en premier, telles que :
   * Des règles de tarification complexes
   * Règles métier personnalisées appliquées avant qu&#39;une commande ne soit officiellement passée ou traitée
   * Calculs d&#39;impôts complexes
   * Validations d’adresses
   * Logique personnalisée déclenchée après la passation d’une commande
* **Vitrine sans tête vs monolithique :** point de décision pour le développement de nouvelles vitrines ou l’adaptation de devantures existantes.
* **Stratégie d’intégration :** Déterminez comment les intégrations existantes seront re-plates-formes (API Mesh, App Builder, API directe).
* **Stratégie de migration des données :** déterminez si vous avez l’intention de migrer en utilisant des données historiques complètes, des données partielles ou aucune donnée migrée.

**Préparation et formation de l’équipe :**

* Familiarisez-vous avec [!DNL Adobe Commerce as a Cloud Service] les concepts, les workflows de développement et les nouveaux outils.
* Participez à une formation pratique sur les pipelines de déploiement Adobe App Builder, Edge Delivery Services et [!DNL Adobe Commerce as a Cloud Service].

**Configuration et approvisionnement de l’environnement :**

* Configurez votre sandbox [!DNL Adobe Commerce as a Cloud Service] et vos environnements de développement à l’aide de Commerce Cloud Manager.

### Phases de migration incrémentielle

**Refactorisation stratégique et externalisation**

Cette phase se compose du cœur de la migration et se concentre sur l’adaptation de votre base de code au paradigme natif du cloud [!DNL Adobe Commerce as a Cloud Service]. Cela implique l’adoption stratégique de nouveaux services Adobe et le déplacement de la logique personnalisée en dehors de la plateforme Commerce principale.

#### &#x200B;1. Migration des personnalisations et des extensions « en cours » vers App Builder

Il s’agit d’une phase cruciale pour réaliser un « noyau verrouillé » et pérenniser votre solution, au cœur de la philosophie architecturale [!DNL Adobe Commerce as a Cloud Service].

* **Externaliser une logique complexe vers App Builder** : analysez les modules personnalisés et les extensions tierces existants dans votre base de code PaaS. Pour une logique commerciale complexe, des intégrations sur mesure ou des microservices qui ne nécessitent pas de manipulation directe et en cours de processus du modèle de données Commerce principal, refactorisez-les et reformez-les en tant qu’applications sans serveur dans Adobe Developer App Builder.
* **Tirer parti du maillage API** : pour les scénarios nécessitant des données provenant de plusieurs systèmes principaux (par exemple, votre serveur principal Commerce PaaS, ERP, CRM et microservices App Builder personnalisés), implémentez une couche de maillage API dans App Builder. Cela consolide des API disparates en un seul point de terminaison GraphQL performant consommé par votre nouvelle vitrine ou d’autres services, simplifiant ainsi la récupération de données complexes.
* **Architecture** pilotée par les événements : utilisez Adobe événements d’E/S pour déclencher des actions du générateur d’applications en fonction des événements survenant dans votre instance PaaS (par exemple, mises à jour de produits, enregistrements de clients, modifications de statut des commandes) ou d’autres systèmes connectés. Cela favorise la communication asynchrone, réduit le couplage étroit et améliore la résilience du système.

**Avantage** : cette étape réduit considérablement la dette technique associée aux personnalisations profondément intégrées, accélère considérablement la transition de votre instance Commerce vers [!DNL Adobe Commerce as a Cloud Service], améliore l’évolutivité et le déploiement indépendant de la logique personnalisée et favorise des cycles de développement plus rapides pour les extensions.

#### &#x200B;2. Adoptez les services de marchandisage Adobe Commerce basés sur SaaS et intégrez les données de catalogue

Il s’agit d’un point d’intégration initial essentiel avec deux options concernant la gestion des données de catalogue :

>[!BEGINTABS]

>[!TAB Option 1 - Service SaaS de catalogue existant]

**Tirez parti du service SaaS de catalogue existant intégré au backend PaaS**

Cette option sert d’étape transitoire, s’appuyant sur une intégration existante où votre serveur principal PaaS renseigne une instance existante du service SaaS Adobe Commerce avec des données provenant des [service de catalogue](../../catalog-service/guide-overview.md), [recherche en direct](../../live-search/overview.md) et [recommandations de produits](../../product-recommendations/overview.md).

* **Synchronisation des données de catalogue** : assurez-vous que votre instance Adobe Commerce PaaS continue à synchroniser les données de produit et de catalogue avec votre service Adobe Commerce Catalog SaaS existant. Cela repose généralement sur des connecteurs ou des modules établis au sein de votre instance PaaS. Le service SaaS de catalogue reste la source faisant autorité pour les fonctions de recherche et de marchandisage, et ses données proviennent de votre serveur principal PaaS.
* **Maillage API pour l’optimisation** : bien que le storefront découplé (sur Edge Delivery Services) et d’autres services puissent directement consommer des données du service SaaS de catalogue, Adobe recommande vivement d’utiliser le maillage API (dans App Builder). Le maillage API permet d’unifier les API du service SaaS de catalogue avec d’autres API nécessaires de votre serveur principal PaaS (par exemple, les vérifications d’inventaire en temps réel de la base de données transactionnelle ou les attributs de produit personnalisés qui ne sont pas entièrement répliqués vers le service SaaS de catalogue) en un seul point d’entrée GraphQL performant. Cela permet également la mise en cache, l’authentification et la transformation de réponse centralisées.
* **Intégrez les Recommendations** Live Search et de produits : configurez les services SaaS Live Search et Recommendations produit pour [ingérer les données](https://experienceleague.adobe.com/fr/docs/commerce/live-search/install#configure-the-data) de catalogue directement à partir de votre service SaaS Adobe Commerce Catalog existant, qui à son tour est alimenté par votre backend PaaS.

**Avantage** : Cela permet d’accéder plus rapidement à une vitrine sans tête et à des fonctionnalités avancées de marchandisage SaaS en tirant parti d’un service SaaS de catalogue existant et opérationnel et de son pipeline d’intégration avec votre backend PaaS. Cependant, il conserve la dépendance sur le serveur principal PaaS pour la source de données de catalogue principale et ne fournit pas les fonctionnalités d’agrégation multi-source inhérentes au nouveau modèle de données de catalogue composable. Cette option est un tremplin valide vers une architecture composable plus complète.

>[!TAB Option 2 - Modèle de données de catalogue composable]

**Adoption du nouveau modèle de données de catalogue composable (CCDM)**

Il s’agit de l’approche stratégique à l’épreuve du temps pour tirer parti de Adobe Commerce Optimizer. Le CCDM fournit un service de catalogue flexible, évolutif et unifié conçu pour l’agrégation de données multi-sources et le marchandisage dynamique.

* **Assimilation et unification des données**
   * Commencez par ingérer les données de produit et de catalogue de votre instance PaaS Adobe Commerce existante (et/ou d’autres systèmes PIM/ERP) dans le nouveau modèle CCDM (Composable Catalog Data Model).
   * Mappez les attributs de produits existants au schéma souple du CCDM. Établissez la priorité des données critiques sur les produits en vue de la première assimilation.
   * Établir des pipelines de données robustes pour une synchronisation continue. Cela peut impliquer :
      * **Piloté par les événements** (via App Builder) : utilisez Adobe I/O Events à partir de votre instance PaaS pour déclencher des applications Adobe App Builder personnalisées ou accessibles au public. Ces applications transforment et transmettent les modifications de données (création, mise à jour et suppression) au CCDM via ses API.
      * **Ingestion par lots** : pour les chargements initiaux volumineux ou les mises à jour en bloc périodiques, utilisez des transferts de fichiers sécurisés (par exemple, CSV ou JSON) vers une zone de transit, traités par les services d’ingestion Adobe Experience Platform (AEP) dans CCDM.
      * **Intégration directe de l’API** (avec orchestration App Builder) : pour les scénarios plus complexes, App Builder peut agir comme une couche d’orchestration, effectuer des appels directs d’API vers votre serveur principal PaaS, transformer les données et les transmettre au CCDM.
* **Vue Catalogue et définition de politique** : configurez des vues de catalogue (regroupements logiques pour une présentation de catalogue unique, telle que des vues de magasin, des régions et des segments B2B/B2C) et définissez des politiques (ensembles de règles pour la présentation, le filtrage et le marchandisage des produits) dans le CCDM. Cela permet un contrôle dynamique sur les assortiments de produits et la logique d’affichage par vue de catalogue.
* **Intégrer la recherche en direct et les recommandations de produits** : une fois que les données de catalogue sont présentes dans le CCDM, intégrez les services de recherche en direct et de recommandations de produits basés sur SaaS Adobe. Ils exploitent l’IA d’Adobe et des modèles de machine learning pour une pertinence de recherche supérieure et des recommandations personnalisées, utilisant les données directement à partir du CCDM.

**Avantage** : en abstrayant la gestion et la découverte de catalogues dans le CCDM et les services SaaS associés, vous améliorez les performances, obtenez des fonctionnalités de marchandisage basées sur l’IA, déchargez considérablement les opérations de lecture de votre serveur principal hérité et activez une solide expérience d’extraction de la partie supérieure de l’expérience funnel.

>[!ENDTABS]

#### &#x200B;3. Créer votre storefront sur Edge Delivery Services

Avec la mise en place de pipelines de données de marchandisage et l’externalisation des personnalisations, l’accent se déplace vers la création de votre front-end haute performance.

* **Configuration initiale** : configurez votre projet à l’aide du modèle standard Adobe Commerce Storefront pour les services de livraison Edge. Cela fournit une interface sans tête fondamentale construite sur les technologies Web modernes.
* **Connectez-vous aux services de catalogue et au maillage** d’API : votre vitrine de commerce consommera des données principalement via les API GraphQL :
   * **Option 1** : à partir du service SaaS de catalogue existant (via le maillage API) pour obtenir des informations sur les produits et les règles de marchandisage.
   * **Option 2** : du CCDM pour les informations sur les produits et les règles de marchandisage.
   * À partir du maillage API pour toutes les données orchestrées de votre serveur principal hérité (instance PaaS) ou des services App Builder personnalisés (par exemple, l’inventaire en temps réel, les attributs de produit personnalisés et les points de fidélité s’affichent).
* **Migration de contenu (AEM Services)** : migrez votre contenu statique existant (par exemple, les pages « À propos de nous », les articles de blog et les bannières marketing) vers AEM Services, qui alimente la vitrine Commerce. Tirez parti des capacités de création de contenu d’AEM et assurez-vous que les ressources sont optimisées pour les services de livraison Edge.
* **Développement des composants principaux de l’interface utilisateur** : créez des composants d’interface utilisateur essentiels pour les pages de détails du produit (PDP), les pages de liste de produits (PLP) et les pages de contenu général à l’aide des composants déroulants Edge Delivery Services et des composants React/Vue personnalisés. Hiérarchisez les principaux flux commerciaux.
* **Intégration au panier/passage en caisse existant** : au départ, le storefront Edge Delivery Services orchestre un transfert vers votre PaaS Adobe Commerce existant (ou une autre plateforme tierce) pour la gestion du panier et le passage en caisse. Cela implique généralement :
   * **Redirection** : redirection de l’utilisateur vers les URL de panier et de passage en caisse natives de la plateforme héritée, en transmettant les identifiants de session et de panier nécessaires.
   * **Interaction directe avec l’API** (avec l’orchestration App Builder) : créez des composants d’interface utilisateur de panier et de paiement personnalisés dans Edge Delivery Services qui interagissent directement avec les API de panier et de paiement de votre backend PaaS. Cela implique souvent App Builder en tant que BFF (Backend-for-Frontend) pour orchestrer les appels à plusieurs services backend (par exemple, panier PaaS, passerelles de paiement et calculateurs d’expédition).

**Avantage** : Offre une expérience de vitrine ultra-rapide, optimisée pour le référencement et hautement flexible. Cette phase contribue directement à une expérience client supérieure et jette les bases de l’innovation front-end future.

#### &#x200B;4. Migration des données (processus par étapes)

La migration des données est un processus critique et à multiples facettes qui s’exécute parallèlement à la refactorisation et au développement de vitrines, garantissant ainsi la cohérence et l’intégrité des données.

* **Nettoyer et optimiser les données existantes** : avant toute migration à grande échelle, effectuez un nettoyage, une déduplication et une validation complets des données sur votre base de données PaaS existante. Cette étape proactive est essentielle pour minimiser le transfert des problèmes de données hérités et assurer la qualité des données dans le nouvel environnement.

**Migration des données en bloc**

La migration de données en bloc implique de prendre une image mémoire complète des données de votre instance Adobe Commerce PaaS, de transformer l’ensemble de ce jeu de données et de l’importer dans Adobe Commerce as a Cloud Service en même temps. Cette méthode est généralement utilisée pour la population initiale de données.

* **Disponibilité des outils** : un [outil de migration de données en bloc](./bulk-data.md) dédié à l’utilisation par les clients pour les migrations de données en bloc Commerce propriétaires sera disponible sur demande au 1er trimestre 2026. Si les clients ont besoin d’aide à la migration de données en bloc au préalable, Adobe peut faciliter le transfert de données en leur nom sur demande.

* **Processus** :
   * **Exportation complète des données** : extrayez un jeu de données complet de votre instance Adobe Commerce PaaS (par exemple, les produits, les catégories, les comptes clients, les données de commande historiques, les blocs statiques et le contenu de page).
   * **Transformation** des données : appliquer les transformations nécessaires pour aligner les données extraites sur les exigences de schéma du nouveau Adobe Commerce en tant que composants Cloud Service, y compris le modèle de données de catalogue composable (CCDM) s’il est adopté, et tout autre service ou base de données Adobe pertinent. Cela peut impliquer des scripts personnalisés ou des outils de mappage de données spécialisés.
   * **Importation** initiale : importez le jeu de données complet transformé dans les composants respectifs de Adobe Commerce en tant que Cloud Service. Pour les données de produit et de catégorie, cela remplit le service de catalogue choisi (CCDM ou SaaS de catalogue existant). Pour les données client et de commande, cela renseigne le backend transactionnel ou les services associés.
   * **Validation** : Validez rigoureusement les données importées pour assurer l’exhaustivité, l’exactitude et la cohérence entre tous les nouveaux systèmes.

**Migrations itératives de données**

Les migrations itératives de données se concentrent sur la synchronisation des modifications incrémentielles et des deltas de l’instance PaaS source vers les nouveaux composants Cloud Service, garantissant ainsi l’actualisation des données avant et après le basculement.

* **Disponibilité** des outils : des outils spécialement conçus pour les migrations itératives de données seront disponibles en 2026.

* **Processus** :
   * **Identification** Delta : établissez des mécanismes pour identifier les modifications (créations, mises à jour et suppressions) dans les ensembles de données critiques de votre environnement PaaS depuis la dernière synchronisation. Cela peut impliquer la capture de données modifiées (CDC), des comparaisons d’horodatage ou des déclencheurs basés sur des événements.
   * **Synchronisation continue** : mettez en œuvre des mécanismes robustes pour une synchronisation incrémentielle continue des données de votre environnement PaaS vers les nouveaux composants Cloud Service (par exemple, CCDM et serveur principal transactionnel). Cela est essentiel pour maintenir la fraîcheur des données et minimiser le temps d’arrêt pendant la transition.
   * **Utilisation d’événements** : utilisez Adobe I/O Events dans la mesure du possible pour déclencher des actions App Builder pour les mises à jour en temps réel ou en quasi temps réel de votre instance PaaS vers les nouveaux services. Par exemple, une mise à jour de produit dans PaaS peut déclencher un événement qui met à jour l’entrée correspondante dans CCDM.
   * **Mises à jour pilotées par les API** : pour les données qui ne sont pas pilotées par les événements, utilisez des appels API planifiés (via App Builder ou d’autres plateformes d’intégration) pour extraire les modifications de PaaS et les pousser vers les nouveaux systèmes.
   * **Gestion et surveillance des erreurs** : implémentez une gestion, une journalisation et une surveillance des erreurs robustes pour tous les pipelines de données itératives afin de garantir l’intégrité des données tout au long du processus.

### Post-migration et opérations en cours

**Basculement DNS et mise en service :**

* Planifiez soigneusement le basculement DNS avec un temps d’arrêt minimal.
* Surveillez l’intégrité et les performances du site immédiatement après le lancement.

**Opérations après le lancement :**

**Déclassement de l’environnement PaaS :**

* Archiver ou supprimer en toute sécurité les anciennes instances et données PaaS après la période de validation.

**Processus de développement continu :**

* Adoptez la nature sans version de [!DNL Adobe Commerce as a Cloud Service], qui a de petits déploiements continus plutôt que de grandes mises à niveau.
* Utilisez Cloud Manager pour gérer les environnements et les déploiements.
* Tirez parti d’App Builder pour étendre les fonctionnalités sans affecter le noyau.

**Surveillance, performance et sécurité :**

* Surveillez en permanence les performances, les erreurs et les journaux de sécurité du site.
* Utilisez les fonctionnalités de sécurité intégrées d’Adobe et suivez les bonnes pratiques.

**Formation et documentation :**

* Formez les nouveaux développeurs et utilisateurs professionnels à la plateforme et aux workflows [!DNL Adobe Commerce as a Cloud Service].
* Mettez à jour la documentation interne pour les intégrations et les processus personnalisés.
