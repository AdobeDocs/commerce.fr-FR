---
title: Migrer vers  [!DNL Adobe Commerce as a Cloud Service]
description: Découvrez comment migrer vers [!DNL Adobe Commerce as a Cloud Service].
feature: Cloud
exl-id: 9065c92a-f6b2-4464-8ec0-5c549bf78104
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
role: Developer
level: Intermediate
autotag-review: '2026-06-18T16:12:28.840Z'
TQID: 'https://experienceleague.adobe.com/GmxaQdGKvAIDpZ2jvmlLFSYw0IFQysIMOT0lUnsJBsI'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
subfeature_v2:
  - id: e91a50b1-0b31-436e-9033-00e4776e94cb
  - id: f56d26ed-050b-4fb7-b29b-8e6e994e80a2
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: addc3a3a-2b1c-4fdf-aea4-4b1eb2931ba6
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: e03840ea9e0e43a005f385914e8599804383e79d
workflow-type: tm+mt
source-wordcount: 3305
ht-degree: 0%

---

# Migrer vers [!DNL Adobe Commerce as a Cloud Service]

Ce guide aide les développeurs à passer de la [!DNL Adobe Commerce on Cloud] ou sur site à la [!DNL Adobe Commerce as a Cloud Service] (SaaS). Ce modèle SaaS offre des performances, une évolutivité et une intégration améliorées au [!DNL Adobe Experience Cloud].

>[!NOTE]
>
>Pour plus d’informations sur les outils de migration, consultez la section [outil de migration de données en bloc](./bulk-data/migration-tool.md).

## Vue d’ensemble

La migration d’un magasin de [!DNL Adobe Commerce] établi vers [!DNL Adobe Commerce as a Cloud Service] va au-delà du déplacement des données. Une véritable migration couvre les domaines suivants :

- Application : personnalisations et extensions conçues pour des installations [!DNL Adobe Commerce on Cloud] ou sur site.
- Données - catalogues, commandes, clients et configuration
- Storefront
- Intégrations avec des systèmes externes

[!DNL Adobe Commerce as a Cloud Service] est une plateforme SaaS sans version, ce qui signifie qu&#39;aucune de ces zones ne peut être migrée sans les adapter. Les personnalisations sont modernisées dans les applications [!DNL App Builder], les vitrines sont reconstruites sur Edge Delivery Services (EDS), les données sont migrées dans le nouveau client [!DNL Adobe Commerce as a Cloud Service] et les intégrations sont rétablies à l’aide de modèles SaaS.

Au lieu de considérer la migration comme un projet monolithique unique, Adobe fournit un workflow de migration intégré construit autour de [trois outils de migration](#migration-tools-workflow).

Ce workflow partagé consolide la découverte, aligne les équipes d’ingénierie et de diffusion et fournit un plan de migration cohérent.

![diagramme de flux de migration](../assets/migration-flow.png)

### Comparaison entre PaaS et SaaS

[!DNL Adobe Commerce on Cloud] ou sur site (PaaS) et [!DNL Adobe Commerce as a Cloud Service] (SaaS) diffèrent dans la façon dont ils sont gérés et dont les commerçants interagissent avec la plateforme.

**Principales différences**

- [!BADGE PaaS uniquement]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."}
- **[!DNL Adobe Commerce on Cloud Infrastructure]** : le commerçant gère le code de l’application, les mises à niveau, les correctifs et la configuration de l’infrastructure.
- **[!DNL Adobe Commerce]sur site** : le commerçant gère le code de l’application, les mises à niveau, les correctifs et la configuration de l’infrastructure dans l’environnement hébergé d’Adobe.

  >[!NOTE]
  >
  >[&#x200B; Modèle de responsabilité partagée &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-operations/security-and-compliance/shared-responsibility) pour les services (MySQL, Elasticsearch et autres).

- [!BADGE SaaS uniquement]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."} **SaaS (nouveau - [!DNL Adobe Commerce as a Cloud Service])** : Adobe gère entièrement l’application principale, l’infrastructure et les mises à jour. Les commerçants se concentrent sur la personnalisation via des points d’extensibilité (API, App Builder, SDK d’interface utilisateur). Le code de l’application principale est verrouillé.

**Implications architecturales**

- **Plateforme sans version** : les mises à jour continues n’impliquent plus de mises à niveau de versions majeures pour le cœur de l’application.
- **Microservices et API-first** : confiance accrue dans les API pour l’extensibilité et l’intégration.
- **Headless par défaut (facultatif)** : Prise en charge renforcée des storefronts découplés (par exemple, le storefront Commerce optimisé par Edge Delivery Services).
- **&#x200B;**&#x200B;: impact sur les performances front-end et le déploiement.

**Nouveaux outils et concepts**

- [Maillage &#x200B;](https://developer.adobe.com/app-builder/) et [API pour Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/)
- [Commerce Optimizer](../../optimizer/overview.md)
- [Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/)
- Approvisionnement en libre-service avec [Commerce Cloud Manager](../getting-started.md#create-an-instance)

### Le parcours de migration

La migration se déroule en plusieurs phases :

- **Évaluer** - Analysez l’implémentation existante et tenez compte des points suivants : personnalisations d’inventaire, intégrations, caractéristiques du storefront et structures de données. Après analyse, créez une feuille de route avec des recommandations de migration, un score de complexité et des estimations d’effort.
- **Moderniser l’application et migrer les données** - Recréez les personnalisations sous forme d’applications [!DNL App Builder] lors de la migration des données d’entreprise dans [!DNL Adobe Commerce as a Cloud Service].
- **Moderniser le storefront** - Reconstruisez le storefront sur Edge Delivery Services (EDS) pour Commerce.
- **Découper et utiliser** - Basculer le trafic vers les [!DNL Adobe Commerce as a Cloud Service], mettre hors service les systèmes existants et passer en fonctionnement continu.

La migration est généralement itérative, et non linéaire. Les entreprises peuvent évaluer plusieurs environnements, valider des recommandations, se moderniser de manière incrémentielle et affiner les plans d’implémentation avant le basculement final en production.

### Workflow des outils de migration

Chacun des workflows suivants possède son propre outil. Utilisez-les ensemble pour terminer votre migration, l’évaluation de migration servant de plan directeur commun tout au long de la migration.

| Workflow | Outil | Description |
| --- | --- | --- |
| [Évaluation](#migration-assessment-tool) | **Outil d’évaluation de la migration** | Évaluation basée sur l’IA de la mise en œuvre existante qui répertorie les modules personnalisés, les extensions tierces, les intégrations, les observations de storefront, le schéma de base de données, les tables personnalisées, les recommandations de migration, la notation de la complexité et les estimations d’effort de modernisation. |
| [Modernisation des applications et du storefront](#code-and-storefront-migration-commerce-developer-mcp) | **MCP du développeur de** | Modernisation de l’application Commerce assistée par l’IA, accélération de la migration des personnalisations vers [!DNL App Builder], prise en charge de la transformation du storefront vers Edge Delivery Services (EDS) et guidage des développeurs à travers un parcours de modernisation de l’application plus large avec une mise en œuvre examinée et validée par les équipes d’ingénieurs. |
| [Migration des données](#data-migration-commerce-data-migration-service) | **Service De Migration Des Données** | Extraction, chargement et vérification de l’intégrité des données de catalogue, de client et de commande dans [!DNL Adobe Commerce as a Cloud Service]. |

Ces pistes ne sont pas autonomes. Les utiliser ensemble dans le bon ordre réduit la reprise.

- **Exécuter d’abord l’évaluation** - L’exécution d’abord identifie les personnalisations non prises en charge, estime l’effort de migration, expose les considérations relatives à la migration des données et met en évidence les dépendances d’intégration avant le début de la mise en œuvre. L’évaluation devient le plan directeur de la migration utilisé par les workflows de modernisation de l’application et de migration des données.
- **Modernisation de l’application** - Le MCP du développeur de Commerce utilise l’évaluation de la migration pour déterminer les personnalisations à moderniser et la manière de procéder. Ensuite, le MCP génère les applications [!DNL App Builder] et les composants storefront correspondants.
- **Migration des données** - Le questionnaire de définition de la migration des données capture la portée, les volumes et les tables personnalisées qui ont été affichées par l’évaluation.
- **Données personnalisées et tierces** - Les données contenues dans les tables personnalisées par des extensions tierces sont identifiées lors de l’évaluation. Cependant, elles ne sont pas gérées par le processus de migration standard des données, qui requiert une personnalisation [!DNL App Builder].

La modernisation du storefront n&#39;est pas seulement une migration de l&#39;interface utilisateur. Outre la migration des fonctionnalités d’entreprise, vous devez tenir compte de l’architecture de l’expérience, de la modernisation des composants réutilisables, de l’optimisation des performances et de l’adoption des modèles Edge Delivery Services.

Les intégrations sont évaluées dans le cadre de l’évaluation de la migration, mais leur mise en œuvre varie en fonction du scénario. Les intégrations peuvent utiliser les API [!DNL App Builder], [!DNL API Mesh], Adobe I/O Events et [!DNL Adobe Commerce as a Cloud Service].

Ces outils de migration continuent à se développer et à gérer un workflow de migration unifié centré sur l’évaluation de la migration.

### Étapes suivantes

Lorsque vous êtes prêt à migrer, commencez par créer une évaluation. L’évaluation de la migration établit le plan que le reste de la migration suit.

L’outil d’évaluation de la migration et le MCP du développeur de Commerce utilisent l’IA pour vous aider à découvrir, planifier et mettre en œuvre. Comme pour tout workflow d’ingénierie, les recommandations et mises en œuvre générées par l’IA doivent être soigneusement examinées et validées par votre équipe dans le cadre des processus standard d’architecture, de test et d’assurance qualité.

## Outil d’évaluation de la migration

Avant de commencer le développement ou la migration, vous devez tenir compte de la taille de la migration et déterminer les éléments qui nécessitent un développement. Un magasin de [!DNL Adobe Commerce] [!DNL Adobe Commerce on Cloud] sur site ou sur site comporte probablement des modules personnalisés, des intégrations, des personnalisations de storefront et des structures de données, qui peuvent ne pas être évidentes tant que quelqu’un n’a pas analysé la mise en œuvre. L’outil d’évaluation de la migration analyse automatiquement votre base de code pour identifier ces éléments à développer.

### Aperçu de l’évaluation

L’outil d’évaluation de la migration effectue une évaluation IA de la mise en œuvre existante et produit une évaluation structurée de la modernisation ainsi qu’une feuille de route de migration [!DNL Adobe Commerce as a Cloud Service]. Il offre également une vue d’ensemble complète de la migration en évaluant les personnalisations des applications, les intégrations, les structures de données, les caractéristiques du storefront et d’autres détails d’implémentation qui influencent la modernisation. Il transforme la découverte en un processus rapide et répétable qui vous permet d’évaluer l’effort, le risque et le séquencement avant de prendre des engagements.

L&#39;évaluation produite par l&#39;outil d&#39;évaluation de la migration n&#39;est pas seulement un rapport. L’évaluation devient un artefact de migration partagé qui informe la planification, la mise en œuvre et la validation tout au long du cycle de vie de la migration. Dans la première phase du parcours de migration, ses résultats couvrent à la fois les efforts de modernisation des applications et de migration des données qui s’ensuivent.

Pour plus d’informations sur les éléments inclus dans un rapport d’évaluation de la migration et sur la manière de l’utiliser, consultez la section [&#x200B; Évaluation de la migration &#x200B;](./assessment.md).

### Étapes d’évaluation

Une évaluation s’exécute par rapport à la mise en œuvre existante et procède à une série d’étapes automatisées :

- **Inventaire** : répertorie l’implémentation. Inclut : modules personnalisés, dépendances du compositeur, extensions tierces, configuration, composants storefront (le cas échéant), fichiers, points d’extensibilité, événements, modules externes, API, tâches cron, files d’attente, schéma de base de données et tables de base de données personnalisées.
- **Analyser** — Effectue une analyse statique pour identifier les personnalisations du magasin, les différences par rapport à une installation [!DNL Adobe Commerce] standard et la manière dont ces personnalisations interagissent dans l&#39;application.
- **Classifier** — Utilise l’IA pour interpréter chaque personnalisation, résumer l’action de la personnalisation, regrouper les fonctionnalités associées, identifier les modèles d’implémentation et fournir des recommandations de migration contextuelles.
- **Mapper et recommander** — Mappe chaque fonctionnalité à son équivalent [!DNL Adobe Commerce as a Cloud Service], y compris : les fonctionnalités par défaut, les applications [!DNL App Builder] ou les services Adobe. L’évaluation recommande ensuite un chemin de modernisation et évalue la complexité, les dépendances et les efforts de mise en œuvre.
- **Rapport** — Produit une feuille de route exportable pour la planification de l&#39;exécution de la migration, qui vous permet de communiquer les risques aux parties prenantes. Il identifie également les priorités, les dépendances, la dette technique et les risques de mise en œuvre.

### Valeur d’évaluation

La valeur d’une évaluation est le degré de confiance que vous pouvez avoir avant de vous engager dans des détails de développement. Au lieu d’estimer une migration avec des pratiques de définition de la portée régulières, l’évaluation fournit une compréhension de la mise en œuvre fondée sur des données probantes. Cela inclut les personnalisations qui sont simples à migrer, qui nécessitent une reconception et qui peuvent être supprimées complètement. Les évaluations font régulièrement apparaître les fonctionnalités obsolètes ou inutilisées, ce qui vous permet de réduire la dette technique.

Chaque recommandation comprend des preuves à l’appui ainsi que des citations renvoyant à l’implémentation sous-jacente, ce qui permet aux architectes et aux ingénieurs de valider pendant la planification. Comme chaque évaluation suit la même méthodologie, vous pouvez comparer plusieurs besoins de développement à l’aide d’un framework de notation et de planification cohérent.

L&#39;évaluation n&#39;est pas seulement un point de départ. L’outil de migration en aval utilise les résultats de l’évaluation pour accélérer la mise en œuvre et maintenir la cohérence avec le plan de migration approuvé. L’analyse de personnalisation devient le plan directeur de la modernisation de l’application, tandis que l’évaluation des données répertorie l’effort de migration des données en analysant la taille de la base de données, l’inventaire des entités et les tables personnalisées.

### Portée de l’évaluation

L’outil d’évaluation de la migration se concentre sur la compréhension du paysage migratoire complet. Il analyse les modules personnalisés, les plug-ins, les événements, les API, les tâches cron, les files d’attente, les intégrations à des systèmes externes, les caractéristiques du storefront et le schéma de base de données dont dépendent ces personnalisations. L&#39;évaluation cartographie ce qu&#39;elle découvre par rapport aux capacités [!DNL Adobe Commerce as a Cloud Service] disponibles et identifie où les fonctionnalités devraient être modernisées en utilisant l&#39;architecture [!DNL App Builder] ou repensée pour l&#39;architecture SaaS.

L’évaluation est davantage un outil de planification qu’un outil d’exécution. Il détermine les éléments à moderniser, évalue la complexité de la mise en œuvre et fournit des recommandations. Les décisions d’implémentation et la validation de l’architecture restent des activités collaboratives entre Adobe, les partenaires et les équipes d’ingénierie client.

Les données stockées dans des tables personnalisées par des extensions tierces sont affichées à titre de considération de migration. La migration des données standard ne migre pas automatiquement ces données. Des applications de [!DNL App Builder] personnalisées peuvent être nécessaires pour prendre en charge ces scénarios. Pour plus d’informations, consultez le [guide de migration des données](#data-migration-commerce-data-migration-service).

L’évaluation fournit une analyse des workflows de personnalisation et de migration des données du storefront :

- Migration du code et des storefronts : l’analyse de l’application de l’évaluation devient le plan directeur de Commerce Developer MCP
- Migration des données : l’inventaire des entités, l’analyse des caractéristiques de la base de données et l’analyse de tables personnalisées de l’évaluation définissent la portée du service de migration des données de Commerce.

Vous pouvez également réexécuter des évaluations à mesure que vos applications évoluent. Cela permet à vos équipes de valider les travaux de correction, de mesurer les progrès de modernisation et d’affiner en permanence les plans de migration tout au long de l’engagement.

### Étapes suivantes

Chaque migration [!DNL Adobe Commerce as a Cloud Service] doit commencer par une évaluation. Il s’agit d’un moyen économique d’établir la portée, de réduire l’incertitude et de créer un plan directeur de migration partagé avant le début de la mise en œuvre.

Pour plus d’informations sur les outils d’évaluation et le workflow de développement en aval, consultez [Adobe Commerce Developer MCP](https://developer.adobe.com/commerce/extensibility/developer-agent/).

## Migration du code et du storefront (MCP pour les développeurs et développeuses Commerce)

Dans [!DNL Adobe Commerce on Cloud] ou sur site, les personnalisations peuvent utiliser PHP en cours de traitement : modules, plug-ins et observateurs d&#39;événements qui s&#39;exécutent dans l&#39;application. [!DNL Adobe Commerce as a Cloud Service] est une plateforme SaaS sans version et ce modèle ne s’applique plus. Les personnalisations s’exécutent en tant qu’applications [!DNL Adobe Developer App Builder] hors processus qui s’intègrent à Commerce par le biais d’événements et d’API. La modernisation des personnalisations d’un magasin pour cette architecture est généralement l’effort d’ingénierie le plus important dans une migration [!DNL Adobe Commerce as a Cloud Service].

### Présentation de la migration du code

À partir de l’évaluation de la migration, le MCP Commerce Developer offre une expérience de conversation IDE pour moderniser les personnalisations PHP héritées en applications [!DNL App Builder]. Il fournit également une assistance pour la reconstruction des vitrines sur Edge Delivery Services (EDS). En utilisant directement les résultats de l’outil d’évaluation de la migration, le MCP Commerce Developer maintient l’alignement de l’implémentation sur la feuille de route de migration approuvée en réduisant l’interprétation manuelle, en maintenant la traçabilité et en assurant la cohérence tout au long du processus.

Bien que la migration soit le principal cas d’utilisation, le MCP pour les développeurs Commerce est conçu comme un agent de développement d’IA complet pour [!DNL Adobe Commerce]. Le MCP prend en charge la modernisation, le nouveau développement, les workflows opérationnels et toutes les mises à jour de [!DNL Adobe Commerce as a Cloud Service]. Ce niveau de flexibilité permet aux équipes de continuer à créer et à étendre des applications Commerce bien après la migration.

### MCP du développeur de Commerce

À l’aide des résultats de l’[évaluation de la migration](#migration-assessment-tool), le MCP de développement Commerce transforme les personnalisations identifiées en applications [!DNL App Builder] par le biais d’un workflow de développement itératif. Tenez compte des recommandations suivantes lors du développement à l’aide de ces outils :

- **Commencez par le plan directeur** - Le MCP Commerce Developer utilise l’évaluation de la migration, en utilisant les personnalisations, recommandations et priorités de migration identifiées comme base de la planification de l’implémentation.

- **Planifier chaque personnalisation** - Pour chaque personnalisation, le MCP de développement Commerce développe une spécification qui décrit l’architecture [!DNL Adobe Commerce as a Cloud Service] recommandée, les modèles d’intégration requis et toute reconception nécessaire pour passer à une application hors processus.

- **Créer en collaboration** - Au lieu de générer initialement du code, le MCP de développement Commerce vous aide tout au long du cycle de vie du développement en planifiant les implémentations, en discutant de l’architecture, en générant et en affinant le code, en validant les modèles recommandés et en fournissant des conseils de déploiement. Les développeurs peuvent affiner de manière itérative les implémentations générées par le langage naturel, ce qui permet aux détails du projet d’évoluer en collaboration tout au long de l’effort de modernisation.

  - Les implémentations générées sont conçues pour accélérer la diffusion tout en restant entièrement révisables, testables et extensibles par les équipes d’ingénieurs.

- **Intégrer et déployer** - Le MCP Commerce Developer connecte les applications à Commerce par le biais de modèles d’intégration appropriés, facilite les workflows de déploiement et valide les mises en œuvre par rapport aux modèles architecturaux recommandés avant le déploiement, ce qui améliore la cohérence et réduit les efforts en double.

  - Le MCP Commerce Developer contient le MCP [!DNL Adobe Commerce App Builder], qui fournit des connaissances de domaine, des modèles d’implémentation, des conseils architecturaux, une expertise contextuelle des produits et des pratiques de codage validées directement dans votre workflow de développement. Cela permet de s’assurer que les recommandations de MCP restent alignées sur les bonnes pratiques d’Adobe, que les développeurs travaillent directement avec le MCP Développeur de Commerce ou en combinaison avec d’autres agents, tels que Claude, Cursor ou Copilot.

### Modernisation du storefront

Sur le front-end, le MCP Commerce Developer modernise [storefronts](https://experienceleague.adobe.com/developer/commerce/storefront/) on Edge Delivery Services (EDS) pour Commerce à l’aide des blocs Modèle Adobe Commerce, Composants de dépôt et EDS.

Le MCP Développeur Commerce charge les projets storefront existants en fonction du standard Commerce. Il modernise votre vitrine en :

- Génération de blocs EDS réactifs
- Génération de données de page compatibles avec Commerce (accueil, PLP, PDP, panier, passage en caisse, compte)
- Composition et extension de composants de liste déroulante
- Traduire les conceptions en implémentations EDS
- Conversion de vitrines monolithiques héritées en une architecture de blocs EDS composables

Le MCP apporte également son aide pour :

- Modernisation des composants
- Composition de blocs réutilisable
- Optimisation de l’expérience
- Alignement sur les bonnes pratiques actuelles de Edge Delivery Services

### Valeur du MCP du développeur

Passer des personnalisations PHP en cours de traitement aux applications composables en [!DNL App Builder] représente un changement architectural significatif. Le MCP pour les développeurs de Commerce comble cette lacune en incorporant les connaissances [!DNL Adobe Commerce], les modèles d’implémentation [!DNL App Builder] et les bonnes pratiques des produits directement dans le workflow de développement.

L’inclusion de ce contexte offre une cohérence améliorée à la fois en termes de vitesse de diffusion et de qualité d’ingénierie. Les équipes peuvent moderniser les applications plus rapidement tout en produisant des implémentations qui suivent des conseils architecturaux cohérents.

En intégrant des modèles d’implémentation recommandés, le MCP Commerce Developer réduit la dépendance à l’expertise individuelle et aide les entreprises à adapter les efforts de modernisation de manière cohérente sur l’ensemble des projets.

Le processus de migration est également l’occasion d’améliorer la mise en œuvre existante. Les équipes peuvent simplifier les personnalisations héritées, supprimer les fonctionnalités obsolètes, adopter les fonctionnalités SaaS et moderniser l’architecture de l’application plutôt que de remonter la dette technique historique.

Dans la mesure où le MCP Commerce Developer consulte directement l’évaluation de la migration, chaque effort de modernisation maintient la traçabilité jusqu’à l’évaluation d’origine, en veillant à ce que la mise en œuvre reste alignée sur la feuille de route de migration approuvée.

Le MCP Commerce Developer encourage également la conception d’applications composables en encourageant les applications [!DNL App Builder] modulaires qui peuvent évoluer indépendamment à mesure que les besoins de l’entreprise changent.

### Portée du MCP du développeur

Sur le serveur principal, le MCP Commerce Developer modernise la couche de personnalisation et d’intégration en transformant les modules PHP, les modules externes et les observateurs d’événements en applications [!DNL App Builder] et établit des modèles d’intégration pour les connecter à Adobe Commerce. Il accélère également le développement au niveau du passage en caisse, des paiements et de l’interface utilisateur d’administration.

Sur le front-end, le MCP Commerce Developer [modernise les storefronts Commerce](#storefront-modernization) sur Edge Delivery Services.

Le MCP ne gère pas la migration des données. Les données commerciales sont migrées par le biais du service de migration de données [&#128279;](#data-migration-commerce-data-migration-service). Le MCP prend en charge les applications [!DNL App Builder] nécessaires lorsque la logique métier ou les tables personnalisées nécessitent la modernisation de l&#39;application.

### Étapes suivantes

La modernisation du code et du storefront commence une fois que la feuille de route de l’outil d’évaluation de la migration a établi la portée et les priorités de la migration.

Pour plus d’informations sur l’installation et l’utilisation de MCP, consultez la documentation de [Commerce Developer MCP](https://developer.adobe.com/commerce/extensibility/developer-agent/) .

## Migration des données (service de migration des données de Commerce)

La migration vers [!DNL Adobe Commerce as a Cloud Service] peut nécessiter la migration d’années de données, notamment : les catalogues, les commandes, les clients et la configuration.

Le service de migration des données de Commerce remplace une migration manuelle par un processus unique, répétable et automatisé. Cela rend les migrations de bases de données complexes plus prévisibles et plus efficaces.

### Service de migration des données de Commerce

Une migration utilise un workflow guidé, piloté par un outil de ligne de commande Docker (`./bin/console migration`). Un intégrateur ou un opérateur système exécute ce workflow sur le magasin source.

La migration des données de base est automatisée, mais la plupart des migrations impliquent des schémas, des extensions et des cas de périphérie non standard. C’est pourquoi toutes les migrations commencent par une [&#x200B; évaluation &#x200B;](#migration-assessment-tool) du magasin source. Après avoir validé les informations d’identification et la connectivité, enregistré la migration et établi une ligne de base de vérification, vous pouvez poursuivre la migration des données.

L’outil du service de migration effectue les étapes de gestion des données suivantes :

1. **Extraire et transformer** : extrait toutes les données pertinentes de la source en parallèle et les remodèle pour les [!DNL Adobe Commerce as a Cloud Service]. Les données incompatibles sont exclues du filtre et les attributs personnalisés et d’autres structures sont remappés.
1. **Charger** — Transfère les données extraites vers le service de migration des données de Commerce. Le service charge les données dans le [!DNL Adobe Commerce as a Cloud Service], puis reconstruit les index et ingère le catalogue.
1. **Vérifier** — Compare les données source et cible au niveau de la base de données. Ensuite, le service valide un exemple d’enregistrements actifs par le biais des API REST storefront GraphQL et admin pour vérifier les données.
1. **Rapport** : consolide les résultats de chaque étape dans un rapport de migration final.

Ces étapes de déplacement des données nécessitent une fenêtre de maintenance, mais pendant la phase de préparation, le magasin reste opérationnel, en réduisant au minimum les temps d’arrêt.

### Valeur du service de migration

Le service de migration des données de Commerce préserve l’intégrité des données à l’aide de preuves. Chaque migration est vérifiée en comparant les données source et cible et en validant un exemple d’enregistrements actifs par le biais des API. Les données qui ne sont pas correctement mappées aux [!DNL Adobe Commerce as a Cloud Service], comme les attributs personnalisés, sont filtrées et remappées automatiquement lors de l’extraction.

Le service de migration est conçu pour les bases de données à l’échelle de l’entreprise. La migration des données est partitionnée et traitée de manière asynchrone, ce qui permet à des catalogues volumineux et à de vastes historiques de commandes de migrer de manière fiable. Plusieurs migrations peuvent s’exécuter en parallèle à mesure que le pipeline se développe. Si une migration est interrompue, elle reprend à partir de la dernière étape terminée et les tâches bloquées sont détectées et font automatiquement l’objet d’une nouvelle tentative.

Les temps d’arrêt sont réduits de différentes manières :

- La majeure partie du travail est effectuée alors que le magasin reste en ligne, ce qui signifie que seul le basculement final nécessite une fenêtre de maintenance.
- La migration des données utilise des lectures et écritures SQL directes très efficaces et ignore les tables et enregistrements qui n&#39;ont pas besoin d&#39;être migrés.

Les migrations impliquant des données de production qui transitent par l’infrastructure d’Adobe, l’ensemble du chemin est sécurisé :

- Tous les chargements sont analysés à la recherche de logiciels malveillants avant d&#39;atteindre la cible
- La couche d’entrée valide les types de fichiers et bloque les opérations de base de données non sécurisées
- Chaque requête est authentifiée à l’aide de la vérification des signatures Adobe IMS et passerelle

Le service de migration des données de Commerce est en production dans le monde entier et a déjà fourni plusieurs migrations au niveau de l’entreprise.

### Données personnalisées et tierces

Le service de migration prend uniquement en charge les données commerciales de base propriétaires. Le service de migration ne gère pas les entités tierces personnalisées.

Les données tierces peuvent être migrées au cas par cas, ce qui nécessite une personnalisation correspondante de l’outil d’extraction Docker. Après avoir créé un outil personnalisé, les données peuvent être extraites de la source et écrites dans la base de données [!DNL App Builder] ou tierce.

Chaque extension modélisant ses données différemment, un chemin de migration pour les données tierces ne peut être conçu qu’après avoir déterminé le schéma et les emplacements du stockage source et cible. Les migrations de données tierces doivent être identifiées précocement pour permettre la définition de la portée.

### Étapes suivantes

Lorsque vous êtes prêt à migrer, renseignez le [questionnaire de définition de la portée de la migration des données](../assets/data-migration-scoping-questionnaire.xlsx), qui nécessite la topologie source, la portée de l&#39;entité, les volumes, les contraintes de conformité, la mécanique de basculement et toutes les [tables personnalisées](#custom-and-third-party-data) requises pour planifier la migration. Le fait de remplir ce questionnaire permet à Adobe d’évaluer votre environnement et de planifier une fenêtre de migration.

Consultez la documentation du [&#x200B; Guide de l’outil de migration de données en bloc &#x200B;](bulk-data/migration-tool.md) pour en savoir plus sur le workflow, les données prises en charge et la vérification.

Les intégrateurs système préparant un environnement source peuvent également utiliser l’interface de ligne de commande [Adobe Commerce Cloud CLI](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/dev-tools/cloud-cli/cloud-cli-overview) standard et le [Adobe Developer Console](https://developer.adobe.com) pour les informations d’identification IMS.
