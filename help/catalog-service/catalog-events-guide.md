---
title: Guide d’intégration des événements de catalogue et de Adobe I/O Events
description: Découvrez comment vérifier les données du catalogue, configurer pour  [!DNL Adobe I/O Events]  vous abonner à des types d’événements de catalogue et valider la diffusion pour les consommateurs et consommatrices.
level: Intermediate
recommendations: noCatalog
role: Admin, Developer
feature: Services, Catalog Service
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c32adafa-ed01-4b31-997e-2413013911b0
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 15aaeadde61b9d70ec107db2ed4c118d1f8ee731
workflow-type: tm+mt
source-wordcount: 1567
ht-degree: 0%

---

# Guide d’intégration des événements de catalogue et des [!DNL Adobe I/O Events]

Les événements de catalogue sont des notifications générées par l’ordinateur qui décrivent les modifications de catalogue prises en charge mises à disposition par le biais de [!DNL Catalog Service]. Ils activent des workflows pilotés par les événements tels que :

* Garder les caches ou services externes synchronisés avec les mises à jour du catalogue.
* Déclencher des processus en aval lorsque des produits, des variantes, des prix ou des catégories changent.
* Optimiser les cas d’utilisation Experience Edge et [!DNL Edge Delivery Services] qui nécessitent des mises à jour de catalogue en temps quasi réel.

Pour le chemin d’accès de bout en bout du [!DNL Adobe Commerce] aux consommateurs d’événements, consultez la section [&#x200B; Diffusion d’événements via  [!DNL Adobe I/O Events]](#event-delivery-through-adobe-io-events).

## Types d’événement pris en charge {#supported-event-types}

Les événements de catalogue se concentrent sur les modifications pertinentes pour le storefront exposées par le biais de [!DNL Adobe Developer Console]. Les abonnements suivants sont actuellement pris en charge.

| Abonnement | Événements |
| --- | --- |
| Mise à jour du produit | Modifications apportées à la création, la mise à jour et la suppression de produits disponibles via [!DNL Catalog Service] |
| Mise à jour des prix | Prix créer, mettre à jour et supprimer les modifications qui affectent les données du catalogue de storefront |

Chaque événement comprend :

* Identifiant d’événement qui décrit le type de modification.
* Contexte d’entité et d’environnement, tel que l’ID d’instance et le SKU.
* Payload qui décrit l’entité modifiée et les informations de portée pertinentes.


## Exemples de payloads d’événement

**Événement ProductUpdated**

```json
{
  "imsOrgId": "aaa-0",
  "instanceId": "instance-9",
  "eventCode": "productUpdated",
  "sku": "1234",
  "links": [
    {"type":  "variantOf", "sku": "5678"}
   ],
  "scope": [
    { "storeViewCode": "US-us" },
    { "storeViewCode": "FR-fr" },
    { "storeViewCode": "DE-de" }
  ]
}
```

**Événement PriceUpdated**

```json
{
  "imsOrgId": "aaa-0",
  "instanceId": "instance-9",
  "eventCode": "priceUpdated",
  "sku": "1234",
  "scope": [
    {
      "websiteCode": "website1",
      "customerGroupCode": "customer-group-code1"
    },
    {
      "websiteCode": "website2",
      "customerGroupCode": "customer-group-code2"
    }
  ]
}
```

## Diffusion d’événement via [!DNL Adobe I/O Events] {#event-delivery-through-adobe-io-events}

[!DNL Adobe I/O Events] fournit des événements de catalogue à vos intégrations. Le diagramme suivant montre le flux de haut niveau des modifications de catalogue de [!DNL Adobe Commerce] à [!DNL Catalog Service] et [!DNL Adobe I/O Events] aux consommateurs abonnés :

![Flux de haut niveau d’événements de catalogue d’Adobe Commerce vers les consommateurs abonnés via le service de catalogue et Adobe I/O Events](assets/catalog-service-event-pipeline.png)

Les étapes suivantes expliquent plus en détail chaque remise :

1. **Service de catalogue Adobe Commerce →**

[!DNL Adobe Commerce] exporte les données du catalogue vers [!DNL Catalog Service] à l’aide des extensions d’exportation de données SaaS prises en charge.

1. **Traitement du service de catalogue**

   * [!DNL Catalog Service] traite les modifications de catalogue prises en charge et les prépare pour la diffusion d’événements.

1. **Service de catalogue → Adobe I/O Events**

* Les événements de catalogue sont publiés vers [!DNL Adobe I/O Events].
* Les consommateurs et consommatrices s’abonnent en utilisant la journalisation, les webhooks, [!DNL Adobe I/O Runtime], Amazon EventBridge ou d’autres mécanismes de diffusion pris en charge.

[!DNL Adobe I/O Events] fournit :

* *Diffusion au moins une fois* par abonné (des événements en double sont possibles).
* Aucune garantie de commande sur les diffusions.

Vos clients doivent gérer les événements en double et la diffusion dans le désordre. Voir [Idempotency](#idempotency) pour obtenir des conseils d’implémentation.

## Cas d’utilisation {#use-cases}

Vous pouvez utiliser des événements de catalogue dans plusieurs scénarios.

### Diffusion statique de site et de périphérie

* Régénérer ou invalider des pages de catalogue et des fragments de storefront lors de modifications des données de catalogue.
* Évitez d’interroger fréquemment les API [!DNL Catalog Service].

### Indexation et mise en cache de la recherche

* Déclenchez des mises à jour incrémentielles dans les index de recherche en aval.
* Mettez à jour les calques de cache ou les vues externes du catalogue lorsque les données de produit ou de catégorie changent.

### Intégration avec des systèmes externes

* Transférer les modifications du catalogue vers des systèmes externes tels que PIM, des moteurs de tarification ou d’autres systèmes métier.
* Gardez les applications en aval synchronisées sans accès direct à la base de données.

### Surveillance et observabilité

Combinez les événements de catalogue avec la surveillance existante (par exemple, [!DNL Grafana] et [!DNL Prometheus]) pour :

* Surveillez le débit des événements.
* Détection des anomalies dans le volume de mise à jour du catalogue.

## Activer les événements de catalogue {#enable-catalog-events}

Pour activer les événements de catalogue de bout en bout, procédez comme suit.

>[!PREREQUISITES]
>
>Avant d’activer les événements de catalogue, vérifiez que vous disposez des éléments suivants :
>
>* Un environnement Adobe Commerce pris en charge avec [!DNL Catalog Service] activé.
>* [La connexion  [!DNL Adobe I/O]  est configurée pour Adobe Commerce](https://developer.adobe.com/commerce/extensibility/events/configure-commerce).
>* Accès à [!DNL Adobe Developer Console] dans la même organisation IMS que celle dans laquelle l’environnement Commerce est configuré.
>* Pour vérifier que la synchronisation avec les services SaaS Commerce est effectuée, utilisez le **[!UICONTROL Data Management Dashboard]** dans l’interface d’administration.
>* Les versions v6.0, [!DNL Live Search] v4.1.0+ ou [!DNL Catalog Service] v1.17+ de Recommandations de produits sont requises pour la vérification des tableaux de bord. Adobe recommande de mettre à jour votre projet Commerce vers les dernières versions prises en charge de ces services. Pour les versions de service antérieures, utilisez [Synchronisation des catalogues](https://experienceleague.adobe.com/fr/docs/commerce/user-guides/data-services/catalog-sync) pour vérifier la synchronisation.


>[!NOTE]
>
>Pour utiliser les événements de catalogue, commencez par configurer l’environnement Commerce pour [!DNL Adobe I/O Events], puis enregistrez un abonnement à un événement dans [!DNL Adobe Developer Console].
>
>Si votre environnement n’apparaît pas dans [!DNL Adobe Developer Console] après la configuration, vérifiez que vous êtes connecté à l’organisation IMS appropriée et que votre compte dispose de l’accès requis. Si l’environnement n’apparaît toujours pas, contactez l’assistance Adobe.

### Vérifier les données du catalogue {#verify-catalog-data}

Vérifiez que [!DNL Catalog Service] dispose des données de catalogue actuelles de votre instance [!DNL Commerce] avant de procéder à la configuration. Les événements de catalogue dépendent de [!DNL SaaS Data Export]’achèvement de deux étapes. Confirmez-les **les deux** :

1. Confirmez la réussite de l’exportation du **flux depuis Commerce**.

   À partir de l’administration [!DNL Adobe Commerce], ouvrez la page [Statut de synchronisation des flux de données](https://experienceleague.adobe.com/fr/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) (**[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Feed Sync Status]**) et vérifiez que le dernier statut d’exportation a réussi pour chaque flux de [!DNL Catalog Service].

1. Confirmez la réussite de la **synchronisation avec les services Commerce connectés** à partir de l’administrateur [!DNL Adobe Commerce].

   À partir de l’administration [!DNL Adobe Commerce], ouvrez le [tableau de bord de gestion des données](https://experienceleague.adobe.com/fr/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard) (**[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Management Dashboard]**) et vérifiez que les données des produits synchronisés incluent les produits attendus.

### S’inscrire et s’abonner à [!DNL Adobe I/O Events] {#register-events}

Définissez les événements Commerce auxquels vous abonner, puis enregistrez-les dans le projet.

Si votre instance ne figure pas dans la liste de sélection, elle n’est pas connectée à [!DNL Adobe I/O]. Pour obtenir des instructions sur la résolution du problème, consultez [Configuration de la connexion [!DNL Adobe I/O]  &#x200B;](https://developer.adobe.com/commerce/extensibility/events/configure-commerce#configure-the-adobe-io-connection) dans la documentation *Adobe Commerce Developer*.

1. À partir du [!DNL Adobe Developer Console], connectez-vous à la même organisation IMS que celle utilisée pour le projet Commerce.

1. Créez un projet pour les événements de catalogue Commerce ou ajoutez l’API d’événements à un projet existant.

   * Sélectionnez **[!UICONTROL APIs and services]** dans le volet de navigation supérieur.

   * Sur la page **[!UICONTROL Browse APIs and services]**, sélectionnez l’onglet **[!UICONTROL Events]** .

   * Recherchez rapidement les API d’événements de catalogue Commerce. Saisissez _Catalogue_ dans la zone de recherche, ou filtrez selon le produit **[!UICONTROL Commerce]**.

   * Sur la carte **[!UICONTROL Commerce Catalog Events]**, sélectionnez **[!UICONTROL Project]**.

   ![Fournisseur d’événements de catalogue Commerce sélectionné sur la page Parcourir les API et services &#x200B;](assets/catalog-event-select-provider.png){width="600" zoomable="yes"}

1. Configurez l’enregistrement des événements.

   Sélectionnez l’instance Commerce à partir de laquelle recevoir les notifications d’événement. Sélectionnez ensuite **[!UICONTROL Next]**.

   ![instance Commerce sélectionnée dans l&#39;écran d&#39;enregistrement de l&#39;événement](assets/catalog-event-registration.png){width="600" zoomable="yes"}

1. Choisissez les événements auxquels vous abonner.

   Sélectionnez les abonnements aux événements pris en charge que vous souhaitez recevoir, par exemple **[!UICONTROL Product Update]** ou **[!UICONTROL Price Update]**. Sélectionnez ensuite **[!UICONTROL Next]**.

   ![Catégories d’événement sélectionnées pour l’abonnement dans l’écran d’enregistrement](assets/catalog-event-subscription.png){width="600" zoomable="yes"}

1. Ajoutez des informations d’identification de serveur à serveur OAuth.

   Saisissez un **[!UICONTROL Credential name]**. Sélectionnez ensuite **[!UICONTROL Next]**.

1. Saisissez un **[!UICONTROL Event registration name]** et un **[!UICONTROL Event registration description]**. Sélectionnez ensuite **[!UICONTROL Next]**.

1. Sur l’écran d’enregistrement final, acceptez le client par défaut, l’API de journalisation.

   Le consommateur d’API de journalisation par défaut vous permet de tester l’enregistrement des événements et de confirmer que les événements sont diffusés. Si vous avez déjà configuré un webhook ou un client d’action [!DNL Adobe I/O Runtime], sélectionnez-le ici. Sinon, modifiez l’enregistrement de l’événement ultérieurement lorsque votre client est prêt.

   ![Valeur par défaut du client API de journalisation sélectionnée dans l’écran de fin de l’enregistrement de l’événement](assets/catalog-event-consumer.png){width="600" zoomable="yes"}

1. Sélectionnez **[!UICONTROL Complete registration]**.

### Configurer le client d’événement {#configure-consumer}

1. Configurez un client, par exemple :

   * Un point d’entrée webhook
   * Une action [!DNL Adobe I/O Runtime]
   * Autre destination prise en charge

1. Si vous n’avez pas sélectionné de client lors de l’enregistrement, modifiez l’enregistrement de l’événement pour ajouter les détails du client.

   * Dans la [!DNL Adobe Developer Console], modifiez votre projet. Sélectionnez ensuite l’enregistrement d’événement que vous avez créé.

   * Sur la page des détails de l’enregistrement de l’événement, sélectionnez **[!UICONTROL Edit Events Registration]**.

   * Sélectionnez **[!UICONTROL Next]** jusqu’à ce que vous atteigniez l’écran de sélection du client. Sélectionnez ensuite le client que vous avez configuré.

   * Mettez à jour le client vers la destination configurée. Sélectionnez ensuite **[!UICONTROL Save configured events]**.

### Validation du flux d’événements {#validate-event-flow}

Les événements de catalogue sont activés pour votre environnement. Lorsque les données du catalogue changent dans [!DNL Commerce], les mises à jour [!DNL Catalog Service] transitent par [!DNL Adobe I/O Events] et le consommateur auquel vous êtes abonné reçoit l’événement de catalogue correspondant. Examinez les [limites et bonnes pratiques](#limits-and-best-practices) avant de créer des intégrations de production.
1. Effectuer une simple modification de catalogue prise en charge, comme mettre à jour un nom de produit ou modifier un prix.

1. Confirmez les résultats suivants :

   * La modification est visible via les API [!DNL Catalog Service].
   * Votre client [!DNL Adobe I/O Events] reçoit le produit ou l’événement de prix correspondant.


## Limites et bonnes pratiques {#limits-and-best-practices}

Lorsque vous créez des événements de catalogue, suivez ces bonnes pratiques.

### Idempotence {#idempotency}

[!DNL Adobe I/O Events] pouvez diffuser le même événement de catalogue plusieurs fois et les événements d’un seul produit peuvent arriver dans le désordre. Concevez les consommateurs de manière à ce qu’ils soient idempotents en :

* Utilisation des ID d’entité avec un champ de version ou d’horodatage.
* Ignorer en toute sécurité les notifications en double pour la même modification.

### Débit et contre-pression

Les catalogues volumineux avec des taux de mise à jour élevés peuvent générer un volume d’événements significatif. Assurez-vous que :

* Les consommateurs et consommatrices peuvent traiter les événements à un débit maximal.
* Vous utilisez la mise en mémoire tampon, le traitement par lots ou les files d’attente si nécessaire.

### Sécurité et isolement

* [!DNL Adobe I/O Events] applique *l’isolement client*.
* Votre organisation ne reçoit des événements que pour ses propres environnements et droits.

### Évolution des schémas

Les payloads d’événement de catalogue suivent le même modèle conceptuel que les API [!DNL Catalog Service]. Pour rester compatible avec le transfert :

* Dans la mesure du possible, évitez d’appliquer strictement les schémas.
* Ignorez les champs inconnus au lieu d’échouer.

## Résolution des problèmes liés aux événements de catalogue {#troubleshoot-catalog-events}

Si des événements de catalogue sont manquants ou retardés, procédez comme suit.

1. **Vérifier les données du service de catalogue**

   [Utilisez l [!DNL Catalog Service] API](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/) pour vérifier que la modification du catalogue est stockée correctement.

1. **Vérifier les[!DNL SaaS Data Export]**

   Les événements de catalogue nécessitent des données actives en [!DNL Catalog Service]. Confirmez les deux étapes du chemin d’exportation :

   * **Exportation des flux depuis Commerce** — Sur la page [État de synchronisation des flux de données](https://experienceleague.adobe.com/fr/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) ou dans `var/log/saas-export.log`, vérifiez que [!DNL Catalog Service] flux ont bien été exportés depuis [!DNL Commerce].

   * **Synchroniser avec les services SaaS Commerce connectés** — Vérifiez que les données ont bien été synchronisées avec le [!DNL Catalog Service] dans le tableau de bord [Data Management](https://experienceleague.adobe.com/fr/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard), [Synchronisation de catalogue](https://experienceleague.adobe.com/fr/docs/commerce/user-guides/data-services/catalog-sync) ou dans les journaux d’exportation.

   Pour résoudre les problèmes liés aux tâches d’exportation et de synchronisation, voir [Synchronisation des données avec l’exportation de données SaaS](../data-export/data-sync-manage.md) et [Journalisation et dépannage](../data-export/troubleshooting/logging.md).

1. **Valider [!DNL Adobe I/O Events] configuration**

   Confirmez que :

   * Vous êtes connecté à l’organisation IMS appropriée dans [!DNL Adobe Developer Console].
   * Le fournisseur de **[!UICONTROL Commerce Catalog Events]** est activé.
   * Le fournisseur de **[!UICONTROL Commerce Catalog Events]** et l’environnement attendus sont visibles.
   * L’abonnement est actif.
   * Votre point d’entrée, action ou client de journal peut recevoir et traiter des événements de test.

1. **Contactez l’assistance Adobe**

   Lors de l’ouverture d’un ticket d’assistance, sélectionnez le motif du problème qui correspond à l’application **&#x200B;**&#x200B;et incluez les informations suivantes :

   * Détails du service de catalogue (environnement, région).
   * [!DNL Adobe I/O Events] les détails de l’abonnement.
   * Heure approximative et description des événements manquants.

   Pour obtenir de l’aide supplémentaire, voir [tickets d’assistance](https://experienceleague.adobe.com/fr/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#support-case).

>[!MORELIKETHIS]
>
>
>* [&#x200B; Intégration et installation &#x200B;](installation.md)
>* [Prise en main du service de catalogue](get-started.md)
>* [Synchroniser les données avec l’exportation de données SaaS](../data-export/data-sync-manage.md)
>* [Récupérer des données de catalogue avec l’API GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/){target="_blank"}
>* [[!DNL Catalog Service]  et maillage API &#x200B;](mesh.md)
>* [Configurer la [!DNL Adobe I/O] connexion](https://developer.adobe.com/commerce/extensibility/events/configure-commerce#configure-the-adobe-io-connection){target="_blank"}
>* [[!DNL Adobe I/O Events]](https://developer.adobe.com/events/docs/guides/){target="_blank"}
