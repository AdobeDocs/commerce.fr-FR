---
title: Notes de mise à jour de [!DNL Adobe Commerce as a Cloud Service]
description: Découvrez les dernières fonctionnalités et améliorations d’ [!DNL Adobe Commerce as a Cloud Service].
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Developer, User, Leader
level: Beginner
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
exl-id: cf06dec6-8d6b-413e-9977-df88373c188e
source-git-commit: fb4c497c9efc184ffb6bd884cb2f37ad9cc87b02
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 0%

---

# Notes de mise à jour

Les notes de mise à jour suivantes contiennent des mises à jour de [!DNL Adobe Commerce as a Cloud Service].

>[!NOTE]
>
>Si vous utilisez Adobe Commerce On-Premise ou Adobe Commerce sur une infrastructure cloud, consultez les [notes de mise à jour d’Adobe Commerce](https://experienceleague.adobe.com/fr/docs/commerce-operations/release/notes/overview).

## Janvier 2026 {#latest}

[!BADGE &#x200B; Sandbox &#x200B;]{type=Caution tooltip="Les éléments répertoriés ne sont actuellement disponibles que dans les environnements Sandbox. Adobe commence par rendre les nouvelles versions disponibles dans les environnements Sandbox afin que vous disposiez du temps nécessaire pour tester les modifications à venir avant que la version ne soit disponible dans les environnements de production."}

Les éléments suivants ne sont actuellement disponibles que dans les environnements Sandbox de [!DNL Adobe Commerce as a Cloud Service]. Cette version devrait passer aux environnements de production le 20 janvier 2026.

>[!BEGINSHADEBOX]

### Améliorations de l’authentification

Les jetons d’accès pour l’authentification des administrateurs Adobe IMS ne sont désormais acceptés que par le biais de requêtes POST. <!-- CCSAAS-4421 -->

### Listes déroulantes B2B

Les modifications suivantes ont été apportées aux composants de liste déroulante B2B :

* [!DNL Commerce Storefront on Edge Delivery Services] inclut désormais des composants de liste déroulante [B2B](http://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/?lang=fr). Les listes déroulantes B2B suivantes sont désormais disponibles :

   * **Gestion de l’entreprise** - Active la gestion des profils d’entreprise et les autorisations basées sur les rôles pour les storefronts Adobe Commerce.
   * **Sélecteur d’entreprise** - Fournit un composant d’interface utilisateur permettant aux utilisateurs de basculer entre plusieurs entreprises auxquelles ils sont associés.
   * **Commandes fournisseur** - Gère les workflows de commande fournisseur, les règles d&#39;approbation et l&#39;historique des commandes fournisseur pour les transactions B2B.
   * **Gestion des devis** - Active les devis négociables pour les clients B2B avec des workflows de demande, de négociation et d&#39;approbation de devis.
   * **Listes de demandes d&#39;approvisionnement** - Fournit des outils pour la création et la gestion des listes de demandes d&#39;approvisionnement pour les achats répétés et les commandes groupées.

     >[!NOTE]
     >
     >Une documentation détaillée sur les composants de liste déroulante B2B sera disponible lorsque cette fonctionnalité sera promue en production.

* Publication du package de compatibilité B2B Storefront. Ce package améliore le schéma GraphQL B2B [!DNL Adobe Commerce] pour améliorer le développement sur les systèmes B2B.

<!-- 
* [!DNL Commerce Storefront on Edge Delivery Services] now includes [B2B drop-in components](http://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/?lang=fr). For a complete list of available B2B drop-in blocks, refer to the [storefront documentation](http://experienceleague.adobe.com/developer/commerce/storefront/merchants/b2b-commerce-blocks/).

* Released the [B2B Storefront Compatibility Package](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility-b2b/). This package enhances the [!DNL Adobe Commerce] B2B GraphQL schema to help improve development on B2B systems. -->

### Liens cliquables vers des dispositifs de suivi d’expédition externes

Transformez les numéros de suivi des expéditions inclus dans les e-mails des acheteurs en texte brut en liens cliquables en [activant les URL de suivi personnalisées](https://experienceleague.adobe.com/fr/docs/commerce-admin/stores-sales/delivery/shipping-settings#shipment-tracking-urls). Cette fonctionnalité est prise en charge pour USPS, UPS, FedEx et DHL. <!-- See PR #716 in commerce-admin -->

### Assistance Google reCAPTCHA Enterprise

[!DNL Adobe Commerce as a Cloud Service] storefronts prennent désormais en charge [reCAPTCHA Enterprise](https://experienceleague.adobe.com/fr/docs/commerce-admin/systems/security/captcha/security-google-recaptcha-enterprise). Cette fonctionnalité offre une protection de robots avancée en utilisant l’analyse de risque adaptative et le machine learning pour distinguer précisément les utilisateurs humains des robots automatisés. Il renforce la sécurité du site, empêche les activités frauduleuses et réduit le spam et les abus afin de maintenir une expérience d&#39;achat fiable. <!-- CCSAAS-4242 -->

### Accès administrateur spécifique à l’instance

Vous pouvez désormais [attribuer l’accès utilisateurs](./user-management.md#add-users) à des instances [!DNL Adobe Commerce as a Cloud Service] individuelles dans Admin Console. <!-- CCSAAS-4337 --><!-- See PR #332 -->

### Observability

Gagnez en visibilité sur votre instance de [!DNL Adobe Commerce as a Cloud Service] grâce à l’observabilité [OpenTelemetry](https://developer.adobe.com/commerce/extensibility/observability/), désormais disponible automatiquement. OpenTelemetry fournit des mesures, des journaux et des traces pour vous aider à surveiller les performances, à résoudre les problèmes plus rapidement et à optimiser votre storefront. Cette fonctionnalité permet d’obtenir des informations proactives sur l’intégrité du système et améliore la fiabilité pour vos clients.

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

* Ajout de la possibilité de charger et de récupérer des pièces jointes de devis négociables, ainsi que des fichiers et des images associés aux clients et aux adresses des clients dans Amazon S3 à l’aide d’URL présignées dans [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/uploads) et [REST](https://developer.adobe.com/commerce/webapi/rest/modules/s3-uploads). Avec REST, vous pouvez également charger des images de catégorie. <!-- CCSAAS-3250 -->

* Ajout des points d’entrée `POST /V1/customers` et `PUT /V1/customers/{customerId}` à l’[API REST](https://developer.adobe.com/commerce/webapi/rest/reference/) pour créer et mettre à jour des clients. Ces points d’entrée nécessitent une autorisation d’administrateur. <!-- CCSAAS-3112 -->

* Ajout de la mutation [`exchangeOtpForCustomerToken`](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/exchange-otp-customer-token/), qui nécessite l’adresse e-mail et le mot de passe à usage unique (OTP) d’un acheteur et qui reçoit un jeton client en échange. Cette mutation est généralement utilisée dans les scénarios où un client doit s’authentifier à l’aide d’un mot de passe à usage unique envoyé à son adresse e-mail ou téléphone.

* Si une adresse définie dans l’écran de configuration [!UICONTROL **Stocker les adresses e-mail**] de l’administrateur contient une valeur se terminant par `example.com`, Commerce n’envoie pas d’e-mails à cette adresse. Au lieu de cela, le système consigne que l’e-mail n’a pas été envoyé.  <!-- CCSAAS-3533 -->

#### Attributs d’ordre personnalisés

* Les utilisateurs administrateurs peuvent désormais afficher et modifier les [attributs de commande personnalisés](https://experienceleague.adobe.com/fr/docs/commerce-admin/stores-sales/order-management/orders/order-processing#custom-order-attributes) directement à partir des écrans Afficher, Modifier et Créer dans le panneau d’administration. Cette amélioration améliore la gestion des données de commande personnalisées créées via GraphQL. <!-- CEXT-5044 -->

>[!ENDSHADEBOX]
