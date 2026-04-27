---
title: Observability for  [!DNL Adobe Commerce as a Cloud Service]
description: Découvrez les outils d’observabilité et les fonctionnalités de télémétrie disponibles pour  [!DNL Adobe Commerce as a Cloud Service], y compris les mesures, la journalisation et le suivi.
feature: Cloud, Integration
role: Admin, Developer
level: Intermediate
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
source-git-commit: 3c10ecdea3d06295013c9c6e2d6869afd750a0b9
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---

# Observability

L’observabilité est un aspect essentiel des [!DNL Adobe Commerce as a Cloud Service] d’exploitation. Elle englobe la collecte, le traitement et la visualisation des données télémétriques, y compris les mesures, la journalisation et le suivi, afin que vous puissiez surveiller l’intégrité des applications, diagnostiquer les problèmes de performances et optimiser la fiabilité de votre plateforme commerciale et de ses intégrations.

## [!DNL Adobe Commerce as a Cloud Service]

### Présentation de l’observabilité

L’observabilité vous donne une visibilité sur l’intégrité et les performances de votre storefront Adobe Commerce et de toutes les applications App Builder connectées. En collectant des données de télémétrie dans votre écosystème de commerce, vous pouvez :

* **Suivez les mesures** telles que les temps de réponse de l’API, les taux de requête et d’erreur et l’utilisation des ressources pour surveiller les performances en temps réel et détecter les tendances.
* **Centralisez les journaux** de votre application, de votre infrastructure, du réseau CDN et des intégrations dans une vue unique pour un dépannage plus rapide.
* **Suivre les requêtes** de bout en bout lorsqu’elles circulent du front-end vers Commerce et les applications connectées, ce qui vous permet de localiser les goulots d’étranglement et les échecs avant qu’ils n’affectent les clients.

Ensemble, ces fonctionnalités vous permettent d’identifier et de résoudre rapidement les problèmes, d’optimiser les performances et d’assurer une expérience fiable à vos clients et clientes. La [présentation de l’observabilité](https://developer.adobe.com/commerce/extensibility/observability/) explique comment [!DNL Adobe Commerce as a Cloud Service] utilise OpenTelemetry pour unifier cette collection de télémétrie sur les applications d’événement, de Webhooks et d’App Builder.

![Architecture d’observabilité](./assets/observability.png){width="600" zoomable="yes"}

Adobe Commerce prend en charge les outils d’observabilité suivants par le biais d’OpenTelemetry :

* Elasticsearch
* Grafana
* Jaeger
* New Relic
* Prométhée
* Splunk
* Zipkin

### Configuration des abonnements

[Configurez les abonnements à l’observabilité](https://developer.adobe.com/commerce/extensibility/observability/configuration/) dans le [!UICONTROL Admin] ou via l’API REST pour acheminer les journaux, les mesures ou les traces vers un point d’entrée compatible avec OpenTelemetry. Chaque abonnement cible des composants spécifiques (webhooks, eventing ou [!UICONTROL Admin UI SDK]).

### API REST Observability

L’[API REST d’observabilité](https://developer.adobe.com/commerce/extensibility/observability/api/) fournit des points d’entrée qui créent, récupèrent, mettent à jour et suppriment des abonnements d’observabilité par programmation. Utilisez ces points d’entrée pour automatiser la configuration des instances.

## Adobe Developer App Builder

### instrumentation d’App Builder

[Implémentez l’observabilité dans  [!DNL App Builder]](https://developer.adobe.com/commerce/extensibility/observability/app-builder/) pour propager le contexte de suivi de Commerce dans vos actions [!DNL App Builder] afin que les journaux et les suivis des deux systèmes soient corrélés dans votre plateforme d’observabilité. Elle traite de l’instrumentation pour les intégrations basées sur des webhook et des événements.

[!DNL App Builder] fournit également des outils intégrés pour [gérer les journaux d’application](https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/application_logging/logging), y compris l’accès à l’interface de ligne de commande et à Developer Console, ainsi que le transfert des journaux vers des solutions externes telles que Splunk, Azure et New Relic.

### Bibliothèque de télémétrie

La bibliothèque [`@adobe/aio-lib-telemetry`](https://github.com/adobe/aio-lib-telemetry/blob/main/docs/usage.md) est ce que les actions App Builder utilisent pour émettre des traces et des journaux compatibles avec OpenTelemetry. Couvre l’installation, la configuration et la configuration de l’exportateur.

### Développement et tests locaux

[Testez votre configuration d’observabilité localement](https://developer.adobe.com/commerce/extensibility/observability/local-development/) avant le déploiement. Utilisez des [!DNL Grafana] pour la visualisation et le transfert par tunnel (par exemple, [!DNL Ngrok]) pour recevoir la télémétrie d’une instance Commerce distante sur votre ordinateur de développement.

## [!DNL API Mesh]

### Journalisation du maillage API

[Journalisation du maillage API](https://developer.adobe.com/graphql-mesh-gateway/mesh/advanced/logging/) permet de surveiller et de déboguer les requêtes qui traversent votre maillage à l’aide d’identifiants de rayon. Exportez les journaux en bloc ou transférez-les vers des plateformes telles que [!DNL New Relic] pour une analyse centralisée.

## Storefront

### CDN et surveillance des utilisateurs réels

[Proxy Real User Monitoring (RUM)](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/content-delivery-network/?lang=fr#proxy-rum-through-the-origin-to-avoid-a-tls-handshake) collecte de données via votre origine CDN pour éliminer une liaison TLS supplémentaire et améliorer la mesure des performances front-end.

## Vidéos d’observabilité

Les vidéos suivantes donnent un aperçu général des offres d’observabilité dans [!DNL Adobe Commerce as a Cloud Service] :

* [Vidéos d’observabilité App Builder](https://experienceleague.adobe.com/fr/docs/commerce-learn/tutorials/observability/overview){target="_blank"}
* [Vidéos sur le maillage API](https://experienceleague.adobe.com/fr/docs/commerce-learn/tutorials/extensibility/api-mesh/getting-started-api-mesh){target="_blank"}
