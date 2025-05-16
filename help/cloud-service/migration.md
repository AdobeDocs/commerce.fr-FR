---
title: Migrer vers  [!DNL Adobe Commerce as a Cloud Service]
description: Découvrez comment migrer vers [!DNL Adobe Commerce as a Cloud Service].
exl-id: 9065c92a-f6b2-4464-8ec0-5c549bf78104
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
source-git-commit: 34057c1e55ff117ea7aab4407f31548ce826691b
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 0%

---

# Migrer vers [!DNL Adobe Commerce as a Cloud Service]

{{accs-early-access}}

[!DNL Adobe Commerce as a Cloud Service] fournit la plupart des configurations prêtes à l’emploi. Cependant, si vous migrez depuis une instance Adobe Commerce on Cloud ou on-premise existante, vous devez effectuer différentes actions de migration en fonction de votre configuration spécifique.

## Chemins de migration

[!DNL Adobe Commerce as a Cloud Service] prend en charge plusieurs chemins de migration, selon votre chronologie, votre storefront et vos personnalisations.

Au lieu d’une migration complète, [!DNL Adobe Commerce as a Cloud Service] prend en charge une migration par phases, à l’aide de Commerce Optimizer ou d’une approche incrémentielle.

* **Migration incrémentielle** : cette approche implique la migration de vos données, de vos personnalisations et de vos intégrations par étapes. Cette approche est idéale pour les grands commerçants avec de nombreuses personnalisations qui souhaitent effectuer une transition progressive de leurs personnalisations et données complexes vers [!DNL Adobe Commerce as a Cloud Service] à leur propre rythme.

![migration incrémentielle](./assets/incremental.png){width="600" zoomable="yes"}

* **Commerce Optimizer**—Cette approche vous permet de migrer de manière itérative, en utilisant Commerce Optimizer comme phase de transition pour déplacer des personnalisations et des données complexes vers [!DNL Adobe Commerce as a Cloud Service] à votre propre rythme. Commerce Optimizer permet d’accéder aux services de marchandisage optimisés par les politiques et canaux de catalogue, au storefront Commerce optimisé par Edge Delivery et aux visuels de produit optimisés par AEM Assets.

![ migration itérative ](./assets/optimizer.png){width="600" zoomable="yes"}

* **Migration complète** : cette approche implique la migration de toutes les données, personnalisations et intégrations en une seule fois. Cette approche est idéale pour les petits commerçants ayant peu de personnalisations et qui souhaitent passer rapidement au [!DNL Adobe Commerce as a Cloud Service].

Le tableau suivant présente un aperçu du processus de migration pour différents storefronts et configurations :

|                    | STOREFRONT LUMA | PWA Storefront | Commerce Storefront optimisé par Edge Delivery | Découplé |
|--------------------|----------------------------------------|----------------------------------------|------------------------------------------------------|----------------------------------------|
| Migration des données | Obligatoire | Obligatoire | Obligatoire | Obligatoire |
| Storefront | Migration vers Commerce Storefront optimisé par Edge Delivery | Migrer vers le storefront Commerce optimisé par Edge Delivery ou maintenir | Pas D’Impact | Pas D’Impact |
| Maillage API | Créer un nouveau maillage | Créer un nouveau maillage ou reconfigurer un maillage existant | Créer un nouveau maillage ou reconfigurer un maillage existant | Créer un nouveau maillage ou reconfigurer un maillage existant |
| Intégrations | Utilisation du kit de démarrage de l’intégration | Utilisation du kit de démarrage de l’intégration | Utilisation du kit de démarrage de l’intégration | Utilisation du kit de démarrage de l’intégration |
| Personnalisations | Déplacer vers App Builder et le maillage API | Déplacer vers App Builder et le maillage API | Déplacer vers App Builder et le maillage API | Déplacer vers App Builder et le maillage API |
| Gestion d’Assets | Migration requise en cas d’utilisation d’OOTB | Migration requise en cas d’utilisation d’OOTB | Migration requise en cas d’utilisation d’OOTB | Migration requise en cas d’utilisation d’OOTB |
| Extensions | Migrer vers App Builder | Migrer vers App Builder | Migrer vers App Builder | Migrer vers App Builder |

Comme l’indique le tableau, les mesures d’atténuation pour chaque migration seront les suivantes :

* **Migration des données** : utilisation de l’outil de migration fourni pour migrer les données de votre instance existante vers [!DNL Adobe Commerce as a Cloud Service].
* **Storefront** : les storefronts EDS et découplés existants ne nécessitent pas d’atténuation, mais les storefronts LUMA nécessitent une migration vers le storefront Commerce optimisé par Edge Delivery. Les storefronts PWA Studio peuvent être migrés vers les storefronts Commerce optimisés par Edge Delivery ou maintenus dans leur état actuel. Adobe fournira des accélérateurs pour faciliter la migration des storefront.
* **[Maillage API](https://developer.adobe.com/graphql-mesh-gateway)** : créez un nouveau maillage ou modifiez le maillage existant. Adobe fournira des maillages préconfigurés pour faciliter ce processus.
* **Intégrations** : toutes les intégrations doivent utiliser le [kit de démarrage de l’intégration](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/) ou l’API [[!DNL Adobe Commerce as a Cloud Service] REST](https://developer.adobe.com/commerce/services/reference/cloud-service/core-admin/).
* **Personnalisations** : toutes les personnalisations doivent être déplacées vers App Builder et le maillage API.
* **Gestion Assets**—La gestion de toutes les ressources nécessite une migration. Si vous utilisez déjà AEM Assets, il n’est pas nécessaire d’effectuer une migration.
* **Extensions** : toutes les extensions en cours de traitement doivent être recréées en tant qu’extensions hors processus. D’ici la fin de l’année 2025, Adobe donnera accès à nos extensions les plus populaires afin de réduire les temps de création.

## Phases de migration

La migration de votre instance Adobe Commerce actuelle vers une nouvelle instance [!DNL Adobe Commerce as a Cloud Service] implique principalement les phases suivantes :

* **[Préparation](#readiness-phase)** : commencez par déterminer si votre déploiement est prêt à être déplacé vers ACCS. Au cours de cette phase, vous devez également vous familiariser avec les modifications introduites par l’ACCS&#x200B;
* **[Implémentation](#implementation-phase)** - Préparez ensuite votre code, votre storefront, vos extensions et vos intégrations pour la migration. Pour faciliter la transition, Adobe autorise des [approches itératives à court et à long terme](#migration-paths). &#x200B;
* **[Mise en production](#go-live-phase)** : testez et confirmez que tout est en place, puis effectuez la migration des données.
* **[Post-activation](#post-go-live-phase)** : en collaboration avec Adobe, surveillez les problèmes et améliorez les performances en fonction des besoins, une fois la migration terminée.

### Phase de préparation

1. Commencez par examiner l’architecture [!DNL Adobe Commerce as a Cloud Service], le framework d’extensibilité et les fonctionnalités de storefront :

   * [Adobe Commerce sur l’architecture des services cloud](./overview.md) : passez en revue l’architecture de la plateforme et ses différences par rapport à votre instance Adobe Commerce actuelle.
   * [Adobe Commerce Extensibility Framework](https://developer.adobe.com/commerce/extensibility/) : déterminez comment vous souhaitez effectuer la transition de vos personnalisations actuelles.
   * [Commerce Storefront optimisé par Edge Delivery ](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=fr)—Examinez la solution storefront recommandée.

1. Contrôlez la compatibilité de votre personnalisation :

   * Identifiez vos modules personnalisés actuels et les intégrations tierces.
   * Évaluez les personnalisations qui doivent être réimplémentées à l’aide d’App Builder.
   * Mappez vos personnalisations actuelles à leurs équivalents d’extensions App Builder.

1. Confirmez vos exigences de storefront et assurez-vous qu’elles s’alignent sur les fonctionnalités de diffusion Adobe Edge.

1. Passez en revue vos intégrations tierces actuelles et confirmez la compatibilité des API avec la plateforme [!DNL Adobe Commerce as a Cloud Service].

### Phase de mise en œuvre

Les étapes suivantes décrivent le processus de développement et d’exécution de la migration :

1. Créez une instance [!DNL Adobe Commerce as a Cloud Service] dans le [Gestionnaire Commerce Cloud](./getting-started.md#create-an-instance).

1. Installez les applications et les personnalisations requises. [!DNL Adobe Commerce as a Cloud Service] a accès à nos applications les plus populaires. Si vous avez besoin d’applications ou de personnalisations supplémentaires, vous pouvez les implémenter à nouveau à l’aide d’App Builder.

1. Configurez l’un des storefronts GraphQL suivants :

   * [Création d’un storefront Commerce](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/?lang=fr)
   * [Utilisez PWA Studio pour créer un storefront personnalisé basé sur GraphQL](https://developer.adobe.com/commerce/pwa-studio/)

1. Migrez vos données de votre instance Commerce précédente vers ACCS :

   * Migrez les données Adobe Commerce natives à l’aide de l’outil de migration de données.
   * Migration des extensions et personnalisations tierces
   * Migrez les données de configuration et d’intégration :
      * Transférez les configurations du maillage API, les services tiers et les intégrations système à l’aide du [kit de démarrage de l’intégration Adobe Commerce](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/).

### Phase d’activation

Avant de lancer, valider et tester votre nouvelle instance [!DNL Adobe Commerce as a Cloud Service] à l’aide d’un environnement sandbox :

* **Tests fonctionnels** : assurez-vous que les données migrées, les fonctionnalités de storefront et les personnalisations fonctionnent de manière transparente.

* **Tests de performance**—Évaluez la vitesse et l&#39;évolutivité de vos magasins pour garantir des performances optimales à l&#39;échelle mondiale.

* **Audit de sécurité** : passez en revue les mesures de sécurité, y compris le contrôle d’accès aux API et toutes les vulnérabilités potentielles.

Une fois que vous avez validé et testé votre nouvelle instance de sandbox [!DNL Adobe Commerce as a Cloud Service], vous pouvez lancer votre instance de production.

### Phase de post-activation

Après la mise en production, effectuez les activités suivantes après le lancement :

1. Suivi de la mise en production

   * Rediriger le trafic vers la nouvelle plateforme et surveiller les performances.
   * Désactivez votre ancienne instance Adobe Commerce.

1. Surveillance après lancement

   * Utilisez des outils de surveillance pour garantir la stabilité des opérations et résoudre les problèmes qui surviennent après le lancement.
