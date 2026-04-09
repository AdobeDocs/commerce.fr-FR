---
title: Lancer la liste de contrôle
description: 'Découvrez comment valider la configuration, le storefront, l’optimisation du moteur de recherche (SEO), le réseau CDN, les intégrations, la sécurité, les analyses et les tests pour la production [!DNL Adobe Commerce Optimizer] '
solution: Commerce
feature: Integration, Storefront, Search, Catalog Management, Personalization
feature-set: Commerce
role: Admin, Developer
level: Intermediate
topic: Administration
recommendations: noCatalog
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et  [!DNL Adobe Commerce Optimizer]  (infrastructure SaaS gérée par Adobe)."
source-git-commit: 37b8b8a334ca11daacfd3da03b0441e77329e2e1
workflow-type: tm+mt
source-wordcount: '1940'
ht-degree: 0%

---


# Liste de contrôle de Launch

Utilisez cette liste de contrôle pour vérifier que votre projet de [!DNL Adobe Commerce Optimizer] de production est configuré, testé et prêt à être lancé. Travaillez sur chaque section avec votre équipe et suivez l’achèvement dans votre propre plan de projet ou votre propre outil de suivi. Pour les fonctionnalités du produit et les zones d’interface utilisateur référencées ci-dessous, consultez la [[!DNL Adobe Commerce Optimizer] documentation](../overview.md).

## Cas d’utilisation et architecture {#use-case}

Utilisez cette liste de contrôle lorsque vous diffusez une expérience B2C qui combine [!DNL Adobe Commerce Optimizer] et Edge Delivery Services (EDS) avec une instance Adobe Commerce on Cloud existante.

Votre solution comprend généralement les composants suivants :

- **Cloud** : Adobe Commerce on Cloud gère les données de catalogue, les clients, les ressources et les flux d’achat (passage en caisse, gestion des commandes, expédition, etc.).
- **Optimizer** : [!DNL Adobe Commerce Optimizer] offre des expériences de marchandisage.
- **Storefront** : le storefront Adobe Commerce sur Edge Delivery Services fournit l’interface utilisateur.
- **Services tiers**—Prestataires de services de paiement, d&#39;expédition et de taxe.
- ****—Extensibilité.
- **Maillage API**—Routage des requêtes.

## Vérification d’Adobe Commerce sur le cloud {#verify-cloud}

Vérifiez que votre environnement Adobe Commerce on Cloud est prêt pour la production.

▢ L’instance cloud est [configurée](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/start/new-project).
Les données de test ▢ et factices sont supprimées de l’instance.
▢ Les données de production sont chargées sur l’instance.
▢ Vous connaissez le point d’entrée [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/).
▢ L’instance répond aux exigences [prêt pour le lancement](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/launch/checklist).

## Vérification de l’instance Commerce Optimizer {#verify-optimizer}

Vérifiez que votre instance de production [!DNL Adobe Commerce Optimizer] est correctement configurée.

▢ L’instance de production est active. Consultez [Prise en main](../get-started.md) pour savoir comment le configurer.
▢ L’instance se trouve dans la bonne région.
▢ Le type d’environnement est Production.
▢ Vous connaissez l’ID d’organisation, l’ID client, l’URL d’ingestion et l’URL Commerce Optimizer. Voir [Prise en main](../get-started.md).
▢ limites et limites configurées correspondent aux valeurs confirmées par votre conseiller technique client Adobe (CTA).
▢ Les artefacts de test et les données factices ont été supprimés de l’instance.

## Vérification du site de storefront {#verify-storefront-site}

Vérifiez que votre site de storefront Edge Delivery Services existe et que l’accès est restreint.

▢ Le site storefront existe. Voir [Création d’un storefront](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/).
▢ Vous connaissez le nom du site.
▢ Seules les personnes autorisées ont [l’autorisation de publier](https://tools.aem.live/tools/user-admin/index.html).
▢ Seules les personnes autorisées ont [l’autorisation de créer](https://docs.da.live/administrators/guides/permissions).

## Vérifier l’intégration de Cloud et Optimizer {#cloud-optimizer-integration}

Vérifiez qu’Adobe Commerce sur le cloud et [!DNL Adobe Commerce Optimizer] échangent correctement des données.

### Sous Adobe Commerce

Effectuez ces vérifications dans votre projet cloud.

▢ Le connecteur Commerce Optimizer est [installé et configuré](../../aco-connector/get-started.md).
▢ La commande de l’interface de ligne de commande `aco:conf:show` confirme la connexion à l’instance Commerce Optimizer de production. L’ID d’organisation, l’ID client, l’URL d’ingestion et l’URL Commerce Optimizer correspondent en production.
▢ Portées de la synchronisation dans [Configuration de l’exportation](../../aco-connector/get-started.md) correspondent à vos besoins.
▢ [Statut de synchronisation des flux de données](../../aco-connector/get-started.md) confirme l’exportation des données à partir de l’instance cloud.

### Dans Commerce Optimizer

Effectuez ces vérifications dans l’interface utilisateur de [!DNL Adobe Commerce Optimizer].

▢ Le tableau de bord [synchronisation des données](../setup/data-sync.md) affiche les données reçues. Les produits, les prix et les attributs s’affichent pour le service de catalogue, la découverte de produits et les recommandations.
▢ [Les tarifs](../setup/pricebooks.md) sont créés automatiquement à partir des groupes de clients sur Cloud.
▢ [Vues de catalogue](../setup/catalog-view.md) existent et vous connaissez leurs identifiants.
▢ [Politiques](../setup/policies.md) existent et vous connaissez leurs identifiants.
▢ [Facettes](../merchandising/facets/overview.md) sont configurées.
▢ [Synonymes](../merchandising/synonyms/overview.md) sont configurés.
▢ [règles de marchandisage](../merchandising/rules/overview.md) sont configurées.
▢ [La facettisation des prix et le langage de recherche](../settings.md) correspondent à vos besoins lorsque vous utilisez ces fonctionnalités.
▢ [recommandations de produits](../merchandising/recommendations/create.md) existent et se comportent comme prévu dans l’aperçu.
▢ [Données de performances de recherche](../manage-results/search-performance.md) apparaît dans le *Admin*.
▢ [Données de performances Recommendations](../manage-results/recommendation-performance.md) s’affiche dans l’*Admin*.

## Vérifier l’intégration du storefront et du cloud {#storefront-cloud-integration}

Vérifiez que le storefront lit à partir du point d’entrée Adobe Commerce GraphQL correct.

### Sous Adobe Commerce

▢ packages de compatibilité Storefront sont [installés](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility/install/).

### Sur le storefront

▢ Le paramètre de `commerce-core-endpoint` storefront pointe vers votre point d’entrée [Cloud GraphQL](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/).
▢ Si vous utilisez le maillage API comme proxy pour Cloud GraphQL, `commerce-core-endpoint` pointe vers le point d’entrée du maillage API plutôt que vers le point d’entrée Cloud GraphQL.

## Vérifier l’intégration de storefront et d’Optimizer {#storefront-optimizer-integration}

Confirmez les paramètres Commerce Optimizer dans la configuration du storefront.

▢ Votre storefront utilise les paramètres [Commerce Optimizer corrects](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/).
▢ `adobe-commerce-optimizer` est `true`.
▢ `commerce-endpoint` pointe vers le point d’entrée GraphQL de Commerce Optimizer de production ou vers le point d’entrée du maillage API lorsque vous utilisez ce dernier.
▢ `headers.cs.AC-view-ID` contient l’ID de vue de catalogue de votre instance Commerce Optimizer de production.

## Vérification des services tiers sur le cloud {#third-party-services}

Confirmez les intégrations qui s’exécutent sur votre système commercial hôte (hors [!DNL Adobe Commerce Optimizer]).

▢ **Paiements :** la passerelle de paiement est en ligne et testée (Stripe, PayPal, Adyen, etc.).
▢ **Expédition :** les connexions API d’expédition fonctionnent (UPS, FedEx, etc.).
▢ **Expédition :** la plateforme d’exécution est connectée et testée (par exemple, ShipStation).
▢ **Taxe :** l&#39;intégration du calcul de la taxe est validée (Avalara, TaxJar, etc.).
▢ **Taxe :** La synchronisation des logiciels de comptabilité fonctionne (QuickBooks, etc.).
▢ **Inventaire :** l’intégration de la gestion PIM, ERP ou de l’inventaire est testée et synchronisée.
▢ **Architecture :** le système commercial hôte gère le paiement, l’expédition, les taxes et les stocks (pas les [!DNL Adobe Commerce Optimizer]).
▢ **Architecture :** le maillage API et App Builder restent synchronisés entre le système Commerce hôte et [!DNL Adobe Commerce Optimizer].
▢ **E-mail :** la diffusion e-mail transactionnelle fonctionne (confirmation de commande, expédition, etc.).
▢ **E-mail :** les modèles d’e-mail correspondent à votre marque et utilisent les liens appropriés.

## Vérification d’App Builder et du maillage API {#app-builder-mesh}

Confirmez la configuration de l’extensibilité pour la production.

### App Builder

▢ L’espace de travail de production comprend toutes les configurations et tous les services requis.
▢ L’application de production passe le test dans tous les scénarios de création.
▢ limites et limites du produit ont été examinées et confirmées en fonction de la [description du produit Adobe Developer App Builder](https://helpx.adobe.com/legal/product-descriptions/adobe-developer-app-builder.html){target="_blank"} et des [paramètres et limites du système App Builder](https://developer.adobe.com/app-builder/docs/guides/runtime_guides/system-settings){target="_blank"}.
▢ L’application de production utilise des points d’entrée de production App Builder.
▢ extensions de panneau *Admin* personnalisées sont déployées dans l’espace de travail de production.

### Maillage API

▢ configurations et les sources sont prêtes pour la production.

### Événements

▢ Adobe I/O Events est configuré et les abonnements sont vérifiés.

## Finalisation de l’expérience storefront {#finalize-storefront}

Contenu polonais, SEO, performances, sécurité et comportement du réseau CDN avant le lancement.

### Contenu et création

Confirmez la création du workflow et des composants storefront.

▢ La liste de contrôle de mise en production d’[AEM/EDS](https://www.aem.live/docs/go-live-checklist) est terminée.
▢ La source de création est basée sur un document ou l’éditeur universel (et configurée).
▢ Le contenu est publié à l’aide du cycle de prévisualisation → de publication.
▢ l’assurance qualité du contenu et de la conception est terminée sur le domaine `.aem.live`.
▢ Un favicon est configuré et diffusé correctement par le site.
▢ da.live et les visuels de produits utilisent des informations d’identification dédiées [configurées](https://docs.da.live/administrators/guides/permissions).
▢ listes déroulantes (panier, passage en caisse, PDP, PLP, authentification, compte) sont [personnalisées](../storefront.md) et testées.
▢ marque Storefront reflète les jetons de conception CSS, la typographie et les couleurs.

### SEO et indexation

Confirmez les métadonnées, les URL et le comportement de l’explore.

▢ métadonnées de titre du document sont présentes pour les pages clés (en particulier les PDP et les PLP). Voir [Métadonnées d’optimisation du moteur de recherche](https://experienceleague.adobe.com/developer/commerce/storefront/setup/seo/metadata/){target="_blank"} dans la documentation de _Adobe Commerce Storefront_.
Les PDP ▢ incluent [métadonnées et données structurées](https://experienceleague.adobe.com/developer/commerce/storefront/setup/seo/metadata/){target="_blank"} (par exemple, JSON-LD).
▢ formats d’URL de produit sont cohérents (par exemple, `domain/product-name`).
▢ les URL de redirection vers les URL canoniques.
▢ Le projet comprend des `robots.txt` qui permettent l’indexation le cas échéant, qui font référence aux plans de site et qui bloquent les chemins que vous ne souhaitez pas indexer (par exemple, `/drafts`).
Les fichiers ▢ [Redirection](https://www.aem.live/docs/redirects) couvrent les modifications d’URL liées à la migration (par exemple, après la suppression de `.html`).
▢ plan de site existe et est envoyé à la console de recherche de Google selon les besoins.
▢ URL canoniques renvoient `2xx` statut (non `3xx` ou `4xx`).
▢ sites multilingues incluent des balises `hreflang` dans le plan du site.
▢ Le rapport de couverture de la console de recherche de Google est à jour.

### Pré-rendu

Confirmez le rendu côté serveur lorsque vous l’activez.

Le pré-rendu ▢ est activé pour les pages clés. Voir [Pré-rendu pour AEM](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-prerender/){target="_blank"} dans la documentation du _storefront Adobe Commerce_.
▢ URL utilisent des minuscules afin que le pré-rendu ne rompe pas les liens.
▢ source HTML comprend des métadonnées et du corps de contenu qui confirment les travaux de pré-rendu.
▢ Paramètres régionaux affichent les pages traduites correctes, le cas échéant.
▢ balisage HTML supplémentaire est [configuré](https://www.aem.live/docs/redirects) selon les besoins.

### Performances et surveillance

Confirmez les lignes de base de performances et le câblage d’analyse.

▢ Votre storefront suit les [bonnes pratiques de performances](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/performance/){target="_blank"} dans la documentation _Adobe Commerce Storefront_.
▢ (facultatif) Google Analytics et Google Tag Manager sont configurés.
▢ [Événements Storefront](https://github.com/adobe/commerce-events/tree/main/examples/events/snowplow-debugger) l’implémentation est valide et les données apparaissent dans vos tableaux de bord [!DNL Live Search] et [!DNL Product Recommendations] dans Adobe Commerce *Admin*.
▢ Le paramètre `environment` analytics dans la configuration [Commerce](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/){target="_blank"} est `"Testing"` pendant le développement et `"Production"` lors de la mise en production. Voir [instrumentation Analytics](https://experienceleague.adobe.com/developer/commerce/storefront/setup/analytics/instrumentation/){target="_blank"}.
▢ scores Lighthouse atteignent vos cibles (par exemple, `100` sur les pages clés) grâce aux conseils de cette rubrique.

### Sécurité et accès

Confirmez les autorisations et les secrets.

▢ Les autorisations appropriées sont configurées pour le contenu DA et les sites EDS. Voir [Autorisations DA.live](https://da.live/docs/administration/permissions) et [Configuration de l’authentification pour la création](https://www.aem.live/docs/authentication-setup-authoring).
▢ L’intégration des visuels de produit est configurée. Voir [ Présentation de l’accès à AEM Cloud Service](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/accessing/overview#).
▢ Les liens de réinitialisation du mot de passe dans les modèles d’e-mail correspondent à votre configuration Edge Delivery Services. Voir la FAQ sur storefront : [Que dois-je faire si mes liens de modèle d’e-mail sont rompus après la migration vers Edge Delivery Services ou Helix ?](https://experienceleague.adobe.com/developer/commerce/storefront/troubleshooting/faq/#what-should-i-do-if-my-email-template-links-are-broken-after-migrating-to-edge-delivery-services-or-helix){target="_blank"}.
▢ Les clés de production pour les intégrations et les fournisseurs de paiement sont en place.
Les domaines ▢ sont placés sur la liste autorisée et les webhooks d’arrière-plan fonctionnent.

### Réseau CDN et mise en cache

Confirmez le comportement du réseau CDN, du DNS et du cache.

▢ La configuration du réseau CDN utilise le point d’entrée de production GraphQL (`yourproject.com/graphql`) pour les extensions et scripts Sidekick (par exemple, la génération du plan de site et l’importateur d’images).
▢ Lorsque vous utilisez Adobe Commerce Fastly, un jeton de purge du réseau CDN est disponible et [configuration du site](https://tools.aem.live/tools/cdn-setup/index.html) comprend `authToken` et `serviceId`.
▢ [configuration du réseau CDN](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/content-delivery-network/){target="_blank"} valide la mise en cache et l’invalidation.
▢ Pour les [configurations multi-magasin](https://experienceleague.adobe.com/developer/commerce/storefront/setup/seo/indexing/#multi-store-setups){target="_blank"}, les requêtes du service de catalogue et du [!DNL Live Search] incluent un buster de cache spécifique au magasin (par exemple, un paramètre de requête ou une règle de réseau CDN).
▢ L’invalidation des notifications push fonctionne de bout en bout (publication d’une modification, puis vérification sur le domaine de production).
▢ TTL DNS est suffisamment bas avant le basculement.
▢ enregistrements DNS A et CNAME sont corrects pour tous les domaines et noms d’hôtes.
▢ Le certificat SSL/TLS est configuré et vérifié pour le domaine de production.
▢ redirections `www` et apex se comportent correctement.

## Sécurité et conformité {#security-compliance}

Confirmez les tâches de conformité et de posture de sécurité.

▢ **SSL :** un certificat SSL/TLS approuvé est installé.
▢ **SSL:** HTTPS est appliqué à l’échelle du site.
▢ **Accès :** les mots de passe par défaut *Administrateur* ont été modifiés et une politique de mot de passe forte est en place. Voir [!DNL Adobe Commerce Optimizer] [Gestion des utilisateurs et des identités](../user-management.md).
▢ **Accès :** l’URL *Admin* n’est pas la valeur par défaut.
▢ **Accès :** l’authentification à deux facteurs est activée pour tous les utilisateurs *Administrateur*.
▢ **Accès :** aucun utilisateur administrateur inactif ou inutilisé n’est associé au projet.
▢ **Pare-feu :** le pare-feu d’application web (WAF) est configuré et vérifié.
Le test de pénétration de la sécurité ▢ **PCI:** en production (étendue PCI) est terminé.
▢ **Analyse :** l’outil d’analyse de sécurité Adobe est enregistré et une analyse initiale est terminée.
▢ **Accès :** la politique CORS autorise uniquement les origines approuvées.
▢ **Conformité :** le modèle de [responsabilité partagée](../shared-responsibility.md) pour [!DNL Adobe Commerce Optimizer] est à jour et définit clairement les responsabilités d’Adobe par rapport aux responsabilités du client.
▢ **Conformité :** la politique de confidentialité, le consentement des cookies et les exigences du RGPD ou du CCPA sont vérifiés.

## Analyses et surveillance {#analytics-monitoring}

Confirmez la mesure et les lignes de base.

▢ **RUM :** Real User Monitoring (RUM) est instrumenté pour les comparaisons avant et après.
▢ **Analytics :** la collecte de données Adobe Experience Platform est configurée (le cas échéant).
▢ **Analytics :** vérification que les balises MarTech se déclenchent sur le nom d’hôte de production.
▢ **Analytics :** les analyses de base sont documentées ; des fluctuations après le lancement (pages vues, taux de rebond, etc.) sont attendues.
▢ **Événements :** le suivi des conversions fonctionne de bout en bout (ajout au panier → passage en caisse → confirmation).

## Test {#testing}

Confirmez la qualité avant et après le lancement.

▢ **Fonctionnel :** les flux principaux fonctionnent de bout en bout : parcourez → recherche → filtrez → ajoutez au panier → passez en caisse → la création de compte.
▢ **Fonctionnel :** les passerelles de paiement acceptent les transactions réelles et de test.
▢ **Fonctionnel :** le placement des commandes, l’e-mail de confirmation et le suivi des commandes.
▢ **Fonctionnel :** les options d’expédition et les calculs de taxe sont précis.
▢ **Fonctionnel :** les coupons, les remises et les programmes de fidélité se comportent comme prévu.
▢ **UAT :** le test d’acceptation utilisateur est terminé pour l’évaluation et la production.
▢ **Performances :** les tests de charge et de contrainte sont terminés et Adobe CTA ou le CSE obtient les résultats.
▢ **Performances :** le temps de chargement de la page est de moins de trois secondes sur les ordinateurs de bureau et les appareils mobiles.
▢ **Performances :** les scores Lighthouse atteignent les cibles sur les pages clés (par exemple, via PageSpeed Insights).
▢ **Performances :** les images, scripts et ressources sont optimisés.
▢ **Compatibilité :** Chrome, Firefox, Safari et Edge se comportent comme prévu.
▢ **Compatibilité :** les dispositions réactives fonctionnent sur les appareils mobiles, les tablettes et les ordinateurs de bureau.
▢ **Compatibilité :** les performances sont acceptables sur les réseaux 3G, 4G et Wi-Fi.
▢ **Accessibilité :** un audit d’accessibilité est terminé (WCAG, lecteur d’écran, navigation au clavier).
▢ **Fonctionnel :** un plan de surveillance 404 est en place après le lancement.
▢ **UAT :** un plan de restauration existe et réussit le test en cas de problèmes de lancement.

## Jour et après le lancement {#launch-post-launch}

Confirmez les tâches de communication, d’assistance et de suivi.

▢ **Coordination du lancement :** votre date de lancement est confirmée pour Adobe ; le CTA a été averti par e-mail.
▢ **Support technique :** le numéro d’appel d’urgence P1 est enregistré : US (+1) 800-497-0335, puis appuyez sur 6 pour Commerce.
▢ **Assistance :** votre équipe est formée pour ouvrir un ticket d’assistance **avant** d’appeler la ligne d’assistance P1.
▢ **Post-lancement :** vérifiez les scores Lighthouse sur le domaine de production.
▢ **Post-lancement :** surveiller la console de recherche Google pour détecter les erreurs d’indexation et d’explore.
▢ **Post-lancement :** surveillez les rapports 404 et ajoutez des redirections pour les URL héritées à trafic élevé.
▢ **Post-lancement :** confirmez les données MarTech et d’analyse en production.
▢ **Post-lancement :** demandez à votre CTA, CSE ou AM d’activer la surveillance High-SLA.
▢ Un plan de reprise après sinistre existe et réussit les tests.
▢ Un processus est en place pour suivre et mettre à niveau les packages standard et d’extension vers les versions actuelles.
