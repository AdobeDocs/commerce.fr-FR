---
title: Notes de mise à jour de [!DNL Adobe Commerce as a Cloud Service]
description: Découvrez les dernières fonctionnalités et améliorations d’ [!DNL Adobe Commerce as a Cloud Service].
feature-set: Commerce
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Developer, User, Leader
level: Beginner
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
exl-id: cf06dec6-8d6b-413e-9977-df88373c188e
source-git-commit: e1e8bf45e45f0f8661c3276faeed03d2e6ce506e
workflow-type: tm+mt
source-wordcount: '2348'
ht-degree: 0%

---

# Notes de mise à jour

Les notes de mise à jour suivantes contiennent des mises à jour de [!DNL Adobe Commerce as a Cloud Service].

>[!NOTE]
>
>Si vous utilisez Adobe Commerce On-Premise ou Adobe Commerce sur une infrastructure cloud, consultez les [notes de mise à jour d’Adobe Commerce](https://experienceleague.adobe.com/fr/docs/commerce-operations/release/notes/overview).

## Avril 2026 {#latest}

[!BADGE Production]{type=Neutral tooltip="Les éléments répertoriés sont actuellement disponibles dans les environnements de production."}

<!-- [!BADGE Sandbox]{type=Caution tooltip="The items listed are currently only available in Sandbox environments. Adobe makes new releases available in Sandbox environments first to provide time to test upcoming changes before the release is available on Production environments."} -->

Les éléments suivants ont été publiés dans les environnements de production le 1er avril 2026.

>[!BEGINSHADEBOX]

### Ajouter des fichiers aux produits

[!DNL Adobe Commerce as a Cloud Service] prend désormais en charge [l’ajout de fichiers aux produits](./product-files.md) à l’aide d’attributs de produit de type fichier). Vous pouvez charger les fichiers manuellement sur la page de modification du produit, par programmation via l’API REST, ou en bloc en fournissant des URL externes au format CSV. <!-- ACCS-535, ACCS-565 -->

### Vérification du statut d’abonnement aux alertes de prix et de stock via GraphQL

Grâce aux nouvelles requêtes GraphQL, [`isSubscribedProductAlertStock`](https://developer.adobe.com/commerce/webapi/graphql/schema/products/queries/is-subscribed-product-alert-stock/){target="_blank"} et [`isSubscribedProductAlertPrice`](https://developer.adobe.com/commerce/webapi/graphql/schema/products/queries/is-subscribed-product-alert-price/){target="_blank"}, les storefronts peuvent déterminer si un acheteur est déjà abonné aux alertes de stock ou de prix pour un produit. <!-- ACCS-334 -->

### Créer des attributs de produit numériques qui prennent en charge les valeurs négatives

Un nouveau `numeric` [type d’entrée d’attribut de produit](https://experienceleague.adobe.com/fr/docs/commerce-admin/catalog/product-attributes/attributes-input-types) permet aux commerçants de créer des attributs décimaux qui prennent en charge les valeurs négatives. <!-- ACCS-600 -->

### Configuration de requête reCAPTCHA pour plusieurs formulaires dans une seule requête GraphQL

La requête [`recaptchaFormConfigs` peut renvoyer &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/schema/store/queries/recaptcha-form-configs/) détails de configuration pour plusieurs types de formulaires dans une seule requête. <!-- ACCS-628 -->

### Afficher toutes les commandes d&#39;entreprise avec une nouvelle autorisation B2B

Un nouveau `view_all_company_orders` [rôle de société](https://developer.adobe.com/commerce/webapi/rest/b2b/roles/) permet aux clients de la société B2B d’afficher toutes les commandes au sein de leur société, y compris les commandes historiques créées par les utilisateurs administrateurs. <!-- ACCS-675 -->

### Améliorations et correctifs

Les améliorations, optimisations et correctifs suivants sont inclus dans cette version :

* Vous pouvez désormais filtrer les résultats de l’API REST Order et Company à l’aide des attributs personnalisés applicables, prenant en charge des scénarios tels que les recherches de commandes au niveau de l’entreprise. <!-- ACCS-633 -->

* Correction d’une erreur qui pouvait s’afficher dans la Developer Console du navigateur. <!-- CCSAAS-4650 -->

* Correction d’une erreur qui pouvait se produire lors de l’annulation d’une commande invitée avec des commentaires de commande. <!-- ACCS-674 -->

* Correction d&#39;une erreur qui pouvait se produire lors de l&#39;ajout d&#39;un produit groupé avec de nombreux articles associés à une liste de demandes d&#39;approvisionnement. <!-- ACCS-627 -->

{{accs-release}}

>[!ENDSHADEBOX]

## Mars 2026 - #2 de publication

[!BADGE Production]{type=Neutral tooltip="Les éléments répertoriés sont actuellement disponibles dans les environnements de production."}

Les éléments suivants ont été publiés dans les environnements de production le 24 mars 2026.

>[!BEGINSHADEBOX]

### Connectez-vous en tant que client à l’aide de codes uniques

Les administrateurs peuvent désormais générer des [codes à usage unique](https://experienceleague.adobe.com/fr/docs/commerce-admin/customers/customer-accounts/manage/login-as-customer) pour l’emprunt d’identité du client via l’API [!DNL Commerce Admin] et REST. Le code unique peut être échangé contre un jeton d’accès client par le biais des mutations GraphQL `generateCustomerToken` ou `exchangeOtpForCustomerToken`, ce qui permet d’activer les flux « Connexion en tant que client » sans mot de passe pour les scénarios d’achat assistés par le vendeur. <!-- ACCS-404 -->

Pour obtenir des conseils sur l’implémentation de cette fonctionnalité à l’aide d’API, consultez la documentation [API REST](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/login-as-customer/) et [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/generate-token/).

### Gérer les comptes de carte cadeau via l’API REST

[Comptes de carte cadeau](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/gift-card-accounts/) peuvent désormais être créés, mis à jour, supprimés et interrogés via l’API REST. En outre, la prise en charge de l’importation en bloc JSON est disponible via le point d’entrée `/V1/import/json`, ce qui permet aux intégrations tierces de synchroniser les cartes-cadeaux par programmation. <!-- ACCS-476 -->

### Déclencher des e-mails transactionnels via l’API REST

Un nouveau point d’entrée de l’API REST (`POST /V1/custom-email/send`) vous permet de [déclencher des e-mails transactionnels](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/custom-email/) à la demande en spécifiant un identifiant de modèle d’e-mail, l’adresse e-mail du destinataire et les variables de modèle. L’API prend en charge les tableaux imbriqués en tant que variables de modèle pour le contenu d’e-mail complexe. <!-- ACCS-325, ACCS-481 -->

### Abonnez-vous au webhook des taux d’obtention des frais d’expédition hors processus .

Le webhook `plugin.out_of_process_shipping_methods.api.shipping_rate_repository.get_rates` est désormais disponible dans la liste Admin Webhooks de [!DNL Adobe Commerce as a Cloud Service]. Utilisez-le pour implémenter [méthodes d’expédition personnalisées](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/shipping-use-cases/#shipping-methods). <!-- ACCS-478 -->

### Chargement de PDF et d’autres fichiers via les attributs de produit

Un nouveau « fichier » [Type d’entrée d’attribut](https://experienceleague.adobe.com/fr/docs/commerce-admin/catalog/product-attributes/attributes-input-types) vous permet de créer des jeux d’attributs dans lesquels vous pouvez charger des fichiers, tels que des PDF, sur des produits individuels. Vous pouvez configurer les extensions de fichier autorisées et la taille de fichier maximale en accédant à [!UICONTROL **Magasins**] > [!UICONTROL **Configuration**] > [!UICONTROL _Catalogue_] > [!UICONTROL **Attributs de fichier de produit**]. <!-- ACCS-535, ACCS-565 -->

### Configuration des attributs personnalisés d’entreprise

Les administrateurs peuvent désormais gérer les attributs personnalisés de l’entreprise sur la page d’édition Entreprise de la [!DNL Commerce Admin]. Les attributs personnalisés peuvent être configurés, enregistrés et validés à partir de l’interface utilisateur d’administration pour [!DNL Adobe Commerce as a Cloud Service].

Pour configurer les attributs personnalisés de l’entreprise, accédez à [!UICONTROL **Clients**] > [!UICONTROL **Entreprises**] et sélectionnez une entreprise pour ouvrir la page de modification. Sélectionnez ensuite l’onglet [!UICONTROL **Attributs personnalisés**] pour ajouter de nouveaux attributs.
<!-- ACCS-294 -->

### S’abonner aux alertes de prix et de stocks via GraphQL

Les storefronts EDS fonctionnent désormais avec [alertes de prix et de stocks](https://experienceleague.adobe.com/fr/docs/commerce-admin/inventory/configuration/product-alerts/alert-setup). <!-- ACCS-334 -->

En outre, il existe plusieurs nouvelles mutations de GraphQL auxquelles vous abonner ou vous désabonner des alertes de prix et d’actions :

+++Nouvelles mutations de GraphQL

```graphql
mutation {
  subscribeProductAlertStock(input: { sku: "ADB111" }) {
    success
    message
  }
}
```

```graphql
mutation {
  unsubscribeProductAlertStock(input: { sku: "ADB111" }) {
    success
    message
  }
}
```

```graphql
mutation {
  unsubscribeProductAlertStockAll {
    success
    message
  }
}
```

```graphql
mutation {
  subscribeProductAlertPrice(input: { sku: "ADB112" }) {
    success
    message
  }
}
```

```graphql
mutation {
  unsubscribeProductAlertPrice(input: { sku: "ADB115" }) {
    success
    message
  }
}
```

```graphql
mutation {
  unsubscribeProductAlertPriceAll {
    success
    message
  }
}
```

+++

### Améliorations et correctifs

Les améliorations, optimisations et correctifs suivants sont inclus dans cette version :

* Le rôle d’entreprise [!UICONTROL Sales] > [!UICONTROL View Orders] fonctionne désormais comme prévu. <!-- ACCS-604 -->

* L’attribut d’extension client `last_login_at` est désormais disponible via l’API REST, ce qui permet aux intégrations de récupérer la date de connexion la plus récente pour chaque client. <!-- ACCS-555 -->

* Correction d’un problème lié aux suggestions de formulaires d’intégration [!DNL AEM Assets]. <!-- ACCS-209 -->

* Correction d’un problème en raison duquel les actions d’affectation et de désaffectation d’entreprise en bloc sur la grille de catalogue partagé pouvaient provoquer une erreur. <!-- CCSAAS-4614 -->

* Correction d’un problème en raison duquel le prix personnalisé du panier était remplacé lorsque le même produit était ajouté au panier avec une quantité différente ou un prix personnalisé. <!-- ACCS-529 -->

* Les UID des éléments de la liste de demandes sont désormais cohérents avec les UID des éléments de panier et de liste de souhaits. <!-- ACCS-349 -->

* Correction d’un délai d’expiration de la page de modification de produit qui pouvait se produire avec des catalogues partagés volumineux. <!-- CCSAAS-4657 -->

* Réactivation des points d’entrée de l’API REST GET `/V1/directory/countries` et GET `/V1/directory/countries/:countryId` pour les intégrations d’administration, ce qui permet aux clients de rechercher des données de pays et de région valides. <!-- ACCS-518 -->

* Correction d’un problème de délai d’expiration qui pouvait se produire dans l’API REST lorsqu’un utilisateur disposait d’un catalogue partagé volumineux. <!-- ACCS-4657 -->

* Correction d’un problème en raison duquel les sociétés B2B bloquées pouvaient toujours ajouter des produits au panier. <!-- ACCS-552 -->

* Si les grilles Client ou Société contiennent une grande quantité de données, les boutons d’exportation ne sont plus disponibles pour éviter les erreurs. <!-- ACCS-320 -->

* Correction d’un problème en raison duquel les tailles de fichiers joints ne s’affichaient pas correctement. <!-- ACCS-566 -->

* Correction d’un problème lié à la création et la suppression des types d’attributs « Fichier » dans le [!DNL Commerce Admin]. <!-- ACCS-605, ACCS-606 -->

{{accs-release}}

>[!ENDSHADEBOX]


## Mars 2026 - #1 de publication

[!BADGE Production]{type=Neutral tooltip="Les éléments répertoriés sont actuellement disponibles dans les environnements de production."}

Les éléments suivants ont été publiés dans les environnements de production d’[!DNL Adobe Commerce as a Cloud Service] le 9 mars 2026.

>[!BEGINSHADEBOX]

### Outils et tutoriels de codage d’App Builder AI

Vous pouvez désormais utiliser l’outil de développement de codage [AI](https://developer.adobe.com/commerce/extensibility/developer-agent/){target="_blank"} pour créer des applications [!DNL App Builder] et convertir des extensions PHP [!DNL Adobe Commerce] existantes en applications [!DNL App Builder]. Les tutoriels suivants sont disponibles pour montrer comment utiliser les outils :

* [Tutoriels préalables](./tutorials/tutorial-prerequisites.md)
* [Tutoriel sur l’extension d’évaluations](./tutorials/ratings-extension.md)
* [Tutoriel sur l’extension des méthodes d’expédition](./tutorials/shipping-method-extension.md)

### Accéder à la gestion de l’application App Builder via l’administrateur

Le [!DNL Commerce Admin] comprend désormais un élément de menu lié à [App Management](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"}, un shell unifié permettant de gérer les applications [!DNL App Builder] associées à l’instance Commerce. Cet ajout est optimisé par la dernière mise à jour SDK de l’interface utilisateur d’administration. <!-- CEXT-5755 -->

### Modification de la limite de création de l’entité de requête

Auparavant, la limite du nombre de sites web, de boutiques et d’affichages de boutique était limitée à 50. Vous pouvez maintenant envoyer une [demande d’assistance](https://experienceleague.adobe.com/home?lang=fr&support-tab=home#support) pour modifier ces limites, si nécessaire. <!-- ACCS-398 -->

### Personnaliser les messages d’authentification du storefront avec des codes d’erreur structurés

La mutation [`generateCustomerToken` GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/generate-token/){target="_blank"} renvoie désormais des codes d’erreur saisis avec les messages d’erreur, ce qui permet aux storefronts d’afficher des messages d’interface utilisateur spécifiques par raison d’échec. Les codes d’erreur disponibles sont les suivants : `CUSTOMER_MISSING_EMAIL`, `CUSTOMER_MISSING_PASSWORD`, `CUSTOMER_SIGN_IN_INCORRECT_OR_LOCKED`, `CUSTOMER_ACCOUNT_NOT_CONFIRMED` et `CUSTOMER_GENERIC_ERROR`. <!-- ACCS-301 -->

### Envoyer des rappels automatisés par e-mail pour l’inactivité du panier et de la liste de souhaits

Le module [Rappel par e-mail](https://experienceleague.adobe.com/fr/docs/commerce-admin/marketing/communications/email-reminders/email-reminder-rules) (`Magento_Reminder`) est désormais actif dans [!DNL Adobe Commerce as a Cloud Service]. Il permet aux commerçants de créer des règles de rappel automatisées qui déclenchent des e-mails aux clients en fonction de l’inactivité du panier et de la liste de souhaits. <!-- CCSAAS-4597 -->

### S’abonner au webhook des événements de suppression de catégorie

Le webhook `observer.catalog_category_delete_before` est désormais disponible dans [!DNL Adobe Commerce as a Cloud Service]. Utilisez-la pour exécuter la logique avant qu’une catégorie ne soit supprimée. <!-- CEXT-5862 -->

### Suivre les commandes passées par des invités avec un e-mail enregistré

Une nouvelle configuration facultative au niveau du magasin permet aux clients de [suivre les commandes des invités](https://experienceleague.adobe.com/fr/docs/commerce-admin/stores-sales/point-of-purchase/checkout/checkout-guest#allow-guest-order-access-for-registered-emails) qu’ils ont passées, si la commande a été passée à l’aide d’une adresse e-mail correspondant à un compte client enregistré. <!-- ACCS-289 -->

### Améliorations et correctifs

Les améliorations, optimisations et correctifs suivants sont inclus dans cette version :

* Correction d’un problème en raison duquel certains administrateurs d’organisation pouvaient accéder incorrectement aux instances du client sans droits par client. <!-- ACCS-335 -->

* Correction d’un problème en raison duquel un utilisateur était déconnecté du [!DNL Commerce Admin] lors de la modification d’un catalogue partagé. <!-- ACCS-318 -->

* Correction d’un problème en raison duquel certains champs de Webhooks s’affichaient incorrectement dans l’interface utilisateur de [!DNL Commerce Admin]. <!-- CEXT-5874 -->

{{accs-release}}

>[!ENDSHADEBOX]

## Février 2026 - #2 de mise à jour

[!BADGE Production]{type=Neutral tooltip="Les éléments répertoriés sont actuellement disponibles dans les environnements de production."}

Les éléments suivants ont été publiés dans les environnements de production d’[!DNL Adobe Commerce as a Cloud Service] le 24 février 2026.

>[!BEGINSHADEBOX]

### Envoi de champs de contexte avec des événements commerciaux

[!DNL Adobe Commerce as a Cloud Service] prend désormais en charge les [champs de contexte](https://developer.adobe.com/commerce/extensibility/events/context-fields/) dans les payloads d’événement, ce qui vous permet d’inclure par défaut des données qui ne font pas partie de l’événement. <!-- CEXT-5713 -->

### Abonnez-vous aux événements d’enregistrement d’élément de devis à l’aide d’un nouveau webhook

Le webhook `observer.sales_quote_item_save_before` est désormais disponible dans [!DNL Adobe Commerce as a Cloud Service]. Utilisez-la pour exécuter la logique avant d&#39;enregistrer un article de devis. <!-- ACCS-346 -->

### Améliorations et correctifs

Les améliorations, optimisations et correctifs suivants sont inclus dans cette version :

* Correction d’une erreur qui entraînait des problèmes d’affichage dans la liste de produits [!DNL Commerce Admin]. La liste des produits limite désormais le nombre de catalogues partagés affichés pour améliorer les performances. <!-- CCSAAS-1242 -->

* Correction d’une erreur GraphQL qui empêchait l’ajout de cartes-cadeaux personnalisables au panier. <!-- ACCS-313 -->

{{accs-release}}

>[!ENDSHADEBOX]

## Février 2026 - #1 de mise à jour

[!BADGE Production]{type=Neutral tooltip="Les éléments répertoriés sont actuellement disponibles dans les environnements de production."}

Les éléments suivants ont été publiés dans les environnements de production d’[!DNL Adobe Commerce as a Cloud Service] le 10 février 2026.

>[!BEGINSHADEBOX]

### Personnaliser les méthodes d’expédition et afficher les rapports d’administration

Les améliorations suivantes ont été apportées au [!DNL Commerce Admin] :

* Amélioration de la fonctionnalité hors processus [payloads webhook d’expédition](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/shipping-use-cases/#payload) pour inclure les attributs personnalisés d’adresse d’expédition. Cette modification permet aux commerçants de mettre en œuvre des méthodes d’expédition personnalisées. <!-- ACCS-235 -->

* Ajout d’un accès aux rapports d’administration, y compris les rapports pour [Clients](https://experienceleague.adobe.com/fr/docs/commerce-admin/start/reporting/customer-reports), [Marketing](https://experienceleague.adobe.com/fr/docs/commerce-admin/start/reporting/marketing-reports), [Produits](https://experienceleague.adobe.com/fr/docs/commerce-admin/start/reporting/product-reports) et [Ventes](https://experienceleague.adobe.com/fr/docs/commerce-admin/start/reporting/sales-reports). <!-- CCSAAS-3085 -->

>[!NOTE]
>
>Les rapports non disponibles dans [!DNL Adobe Commerce as a Cloud Service] sont étiquetés comme PaaS uniquement ([!BADGE PaaS uniquement]{type=Informative url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."}).

### Capturer des montants de facture personnalisés via l’API REST

L’API Invoice prend désormais en charge les [montants de capture personnalisés](https://experienceleague.adobe.com/fr/docs/commerce-admin/stores-sales/order-management/invoices#custom-capture-amounts) à l’aide d’attributs d’extension. <!-- ACCS-186, ACCS-197, ACCS-143 -->

>[!NOTE]
>
>En raison de restrictions légales, le montant de la capture personnalisée n&#39;est disponible que dans la région Amérique du Nord (NA) et d&#39;autres régions où la surcapture des paiements est autorisée.

### Améliorations et correctifs

Les améliorations, optimisations et correctifs suivants sont inclus dans cette version :

* Correction du filtre de la grille de coupons pour afficher tous les coupons personnalisés créés via l’API ou par importation. <!-- CCSAAS-4509 -->

* Correction d’un problème dans le [!DNL Storefront Compatibility B2B Package] en raison duquel la mutation `setNegotiableQuoteShippingAddress` n’enregistrait pas les adresses saisies manuellement dans le carnet d’adresses du client, même lorsque `save_in_address_book` était défini sur `true`. <!-- LYNX-1031 -->

<!-- The above change will also be covered by the B2B changelog published on February 13, 2026. -->

* Correction d’un problème où les images du produit ne s’affichaient pas correctement dans [!DNL Edge Delivery Services] en raison de valeurs de `no_selection` corrompues dans les attributs personnalisés liés aux rôles des ressources. <!-- ACAP-1206 -->

* Correction d’un problème qui empêchait les comptes utilisateur fédérés avec des valeurs de prénom ou de nom nulles d’accéder à l’administrateur Commerce. <!-- ACCS-200 -->

* Simplification de la configuration du sélecteur de ressources en fournissant automatiquement des identifiants de client IMS spécifiques à une région. Les commerçants n’ont plus besoin d’envoyer de tickets d’assistance pour configurer le sélecteur de ressources afin de mapper les images de catégories de produits aux ressources. Le système utilise désormais automatiquement les ID client IMS dédiés en fonction de la région Commerce. <!-- ACCS-175 -->

* Diverses améliorations des performances et de l’optimisation. <!-- CCSAAS-4485, CCSAAS-4497, ACCS-196 -->

{{accs-release}}

>[!ENDSHADEBOX]

## Janvier 2026

[!BADGE Production]{type=Neutral tooltip="Les éléments répertoriés sont actuellement disponibles dans les environnements de production."}

Les éléments suivants ont été publiés dans les environnements de production d’[!DNL Adobe Commerce as a Cloud Service] le 20 janvier 2026.

>[!BEGINSHADEBOX]

### Listes déroulantes B2B

Les modifications suivantes ont été apportées aux composants de liste déroulante B2B :

* [!DNL Commerce Storefront on Edge Delivery Services] inclut désormais des composants de liste déroulante [B2B](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/?lang=fr). Les listes déroulantes B2B suivantes sont désormais disponibles :

   * **[Gestion de l’entreprise](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/company-management/?lang=fr)** - Active la gestion des profils d’entreprise et les autorisations basées sur les rôles pour les storefronts Adobe Commerce.
   * **[Sélecteur d’entreprise](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/company-switcher/?lang=fr)** - Fournit un composant d’interface utilisateur permettant aux utilisateurs de basculer entre plusieurs entreprises auxquelles ils sont associés.
   * **[Commandes fournisseur](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/purchase-order/?lang=fr)** - Gère les workflows de commande fournisseur, les règles d&#39;approbation et l&#39;historique des commandes fournisseur pour les transactions B2B.
   * **[Gestion des devis](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/quote-management/?lang=fr)** - Active les devis négociables pour les clients B2B avec des workflows de demande, de négociation et d&#39;approbation de devis.
   * **[Listes de demandes d&#39;approvisionnement](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/requisition-list/?lang=fr)** - Fournit des outils pour la création et la gestion des listes de demandes d&#39;approvisionnement pour les achats répétés et les commandes groupées.

* Publication du package de compatibilité B2B Storefront. Ce package améliore le schéma GraphQL B2B [!DNL Adobe Commerce] pour améliorer le développement sur les systèmes B2B.

<!-- 
* [!DNL Commerce Storefront on Edge Delivery Services] now includes [B2B drop-in components](http://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/?lang=fr). For a complete list of available B2B drop-in blocks, refer to the [storefront documentation](http://experienceleague.adobe.com/developer/commerce/storefront/merchants/b2b-commerce-blocks/).

* Released the [B2B Storefront Compatibility Package](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility-b2b/?lang=fr). This package enhances the [!DNL Adobe Commerce] B2B GraphQL schema to help improve development on B2B systems. -->

### Liens cliquables vers des dispositifs de suivi d’expédition externes

Transformez les numéros de suivi des expéditions inclus dans les e-mails des acheteurs en texte brut en liens cliquables en [activant les URL de suivi personnalisées](https://experienceleague.adobe.com/fr/docs/commerce-admin/stores-sales/delivery/shipping-settings#shipment-tracking-urls). Cette fonctionnalité est prise en charge pour USPS, UPS, FedEx et DHL. <!-- See PR #716 in commerce-admin -->

### Assistance Google reCAPTCHA Enterprise

[!DNL Adobe Commerce as a Cloud Service] storefronts prennent désormais en charge [reCAPTCHA Enterprise](https://experienceleague.adobe.com/fr/docs/commerce-admin/systems/security/captcha/security-google-recaptcha-enterprise). Cette fonctionnalité offre une protection de robots avancée en utilisant l’analyse de risque adaptative et le machine learning pour distinguer précisément les utilisateurs humains des robots automatisés. Il renforce la sécurité du site, empêche les activités frauduleuses et réduit le spam et les abus afin de maintenir une expérience d&#39;achat fiable. <!-- CCSAAS-4242 -->

### Accès administrateur spécifique à l’instance

Vous pouvez désormais [attribuer l’accès utilisateurs](./user-management.md#add-users) à des instances [!DNL Adobe Commerce as a Cloud Service] individuelles dans Admin Console. <!-- CCSAAS-4337 --><!-- See PR #332 -->

### Observability

En utilisant [!DNL App Builder], vous pouvez obtenir une visibilité plus approfondie de votre instance de [!DNL Adobe Commerce as a Cloud Service] grâce à l’observabilité [OpenTelemetry](https://developer.adobe.com/commerce/extensibility/observability/), désormais disponible automatiquement. OpenTelemetry fournit des mesures, des journaux et des traces pour vous aider à surveiller les performances, à résoudre les problèmes plus rapidement et à optimiser votre storefront. Cette fonctionnalité permet d’obtenir des informations proactives sur l’intégrité du système et améliore la fiabilité pour vos clients.

>[!NOTE]
>
>L’observabilité d’OpenTelemetry nécessite l’utilisation de [!DNL App Builder] ou d’autres offres d’extensibilité hors processus (OOPE).

### Hiérarchiser la tarification pour les règles de prix de catalogue

Vous pouvez désormais combiner des remises de tarification échelonnée avec des remises de règle de catalogue à l&#39;aide de [règles de prix de catalogue](https://experienceleague.adobe.com/fr/docs/commerce-admin/catalog/products/pricing/product-price-tier#enable-tier-pricing-for-catalog-price-rules). Cette amélioration vous permet de créer des stratégies de tarification plus dynamiques et plus concurrentielles, en récompensant les achats en gros tout en appliquant des remises promotionnelles. Le résultat est une plus grande flexibilité pour attirer les clients, augmenter la valeur des commandes et générer des conversions.<!-- See PR #708 in commerce-admin -->

### Améliorations et correctifs

Les améliorations, optimisations et correctifs suivants inclus dans cette version sont sélectionnés :

* Correction d&#39;une erreur qui pouvait se produire lors du chargement d&#39;un fichier dans S3. <!-- CCSAAS-4189 -->

* Correction d’une erreur `User is not entitled to access this instance` qui pouvait se produire lors de la connexion à l’administration Commerce ou de l’accès à l’API REST. <!-- CCSAAS-4324 -->

* Correction d’une erreur qui se produisait lors de la prévisualisation ou de la mise en file d’attente d’une newsletter dans la grille Modèle de newsletter. <!-- CCSAAS-4398 -->

* Correction d’une erreur `404` qui se produisait lorsque les utilisateurs cliquaient sur le bouton [!UICONTROL **Recharger les données**] du tableau de bord d’administration. <!-- CCSAAS-4468 -->

* Correction d’un problème où les attributs personnalisés du produit ne pouvaient pas être mis à jour via l’API REST lorsqu’[!DNL AEM Assets integration] était activé et que le produit contenait des images. <!-- ACAP-1178 -->

* Diverses améliorations des performances et de l’optimisation.<!-- CCSAAS-4255 --><!-- CCSAAS-4233 --><!-- CCSAAS-4220 --><!-- CCSAAS-4252 --><!-- CCSAAS-4330 --><!-- CCSAAS-3669 --><!-- CCSAAS-4462 -->

{{accs-release}}

>[!ENDSHADEBOX]

## Novembre 2025

>[!BEGINSHADEBOX]

### Améliorations

* [Gestion des utilisateurs](./user-management.md) - Modification du rôle **Administrateur de produit** dans Admin Console afin de mettre automatiquement à jour l’accès des utilisateurs et utilisatrices à l’administrateur Commerce. <!-- CCSAAS-3012 -->

* Ajout de la possibilité de charger et de récupérer des pièces jointes de devis négociables, ainsi que des fichiers et des images associés aux clients et aux adresses des clients dans Amazon S3 à l’aide d’URL présignées dans [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/uploads) et [REST](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/s3-uploads). Avec REST, vous pouvez également charger des images de catégorie. <!-- CCSAAS-3250 -->

* Ajout des points d’entrée `POST /V1/customers` et `PUT /V1/customers/{customerId}` à l’[API REST](https://developer.adobe.com/commerce/webapi/rest/reference/) pour créer et mettre à jour des clients. Ces points d’entrée nécessitent une autorisation IMS. <!-- CCSAAS-3112 -->

* Ajout de la mutation [`exchangeOtpForCustomerToken`, qui nécessite l’adresse e-mail et le mot de passe à usage unique (OTP) d’un acheteur et qui reçoit un jeton client en échange. &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/exchange-otp-customer-token/) Cette mutation est généralement utilisée dans les scénarios où un client doit s’authentifier à l’aide d’un mot de passe à usage unique envoyé à son adresse e-mail ou téléphone.

* Si une adresse définie dans l’écran de configuration [!UICONTROL **Stocker les adresses e-mail**] de l’administrateur contient une valeur se terminant par `example.com`, Commerce n’envoie pas d’e-mails à cette adresse. Au lieu de cela, le système consigne que l’e-mail n’a pas été envoyé.  <!-- CCSAAS-3533 -->

#### Attributs d’ordre personnalisés

* Les utilisateurs administrateurs peuvent désormais afficher et modifier les [attributs de commande personnalisés](https://experienceleague.adobe.com/fr/docs/commerce-admin/stores-sales/order-management/orders/order-processing#custom-order-attributes) directement à partir des écrans Afficher, Modifier et Créer dans le panneau d’administration. Cette amélioration améliore la gestion des données de commande personnalisées créées via GraphQL. <!-- CEXT-5044 -->

>[!ENDSHADEBOX]
