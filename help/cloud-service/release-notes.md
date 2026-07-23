---
title: Notes de mise à jour de [!DNL Adobe Commerce as a Cloud Service]
description: Découvrez les dernières fonctionnalités et améliorations d’ [!DNL Adobe Commerce as a Cloud Service].
feature-set: Commerce
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Developer, User, Leader
level: Beginner
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
exl-id: cf06dec6-8d6b-413e-9977-df88373c188e
nudge: true
autotag-review: '2026-06-18T16:04:15.842Z'
TQID: 'https://experienceleague.adobe.com/MmwdYWe5Et9m0BvtrVYNK2jiJ3fZBnUe2K6xMdIbMUk'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
subfeature_v2:
  - id: adedf3b3-e153-47a3-ae73-b5d65067b544
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: b05e2183cc0e4b8352a150df9dabfc9dfdb31750
workflow-type: tm+mt
source-wordcount: 5265
ht-degree: 0%

---

# Notes de mise à jour

Les notes de mise à jour suivantes contiennent des mises à jour de [!DNL Adobe Commerce as a Cloud Service].

>[!NOTE]
>
>Si vous utilisez Adobe Commerce On-Premise ou Adobe Commerce sur une infrastructure cloud, consultez les [notes de mise à jour d’Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-operations/release/notes/overview).

## Juillet 2026 - #1 de mise à jour {#latest}

<!-- [!BADGE Production]{type=Neutral tooltip="The items listed are currently available in Production environments."} -->

[!BADGE &#x200B; Sandbox &#x200B;]{type=Caution tooltip="Les éléments répertoriés ne sont actuellement disponibles que dans les environnements Sandbox. Adobe commence par rendre les nouvelles versions disponibles dans les environnements Sandbox afin de donner le temps de tester les modifications à venir avant que la version ne soit disponible dans les environnements de production."}

Les éléments suivants ne sont actuellement disponibles que dans les environnements Sandbox et devraient passer aux environnements de production le 28 juillet 2026.

>[!BEGINSHADEBOX]

### Modifier les commandes avec REST

>[!IMPORTANT]
>
>Cette fonctionnalité est désactivée par défaut. Pour l’activer, contactez votre responsable du succès client Adobe Commerce ou créez un ticket d’assistance.

Les nouveaux points d’entrée de l’API REST répliquent la fonctionnalité [!DNL Commerce Admin] [!UICONTROL **Modifier l’ordre**] qui permet aux intégrations de modifier un ordre par programmation :

| Méthode | Point d’entrée | Description |
| --- | --- | --- |
| `POST` | `/V1/orders/{orderId}/edit/start` | Copiez la commande dans un nouveau panier modifiable et renvoyez l’ID de panier. |
| `POST` | `/V1/orders/{orderId}/edit/submit` | Envoyez le panier modifié comme nouvelle commande et annulez la commande d’origine. |

Après avoir appelé `edit/start`, modifiez le panier renvoyé à l’aide des points d’entrée REST de panier standard, puis appelez `edit/submit`. La nouvelle commande hérite du mode de paiement de la commande d’origine, à moins que vous ne la remplaciez par le panier. Elle est créée en tant que remplacement lié de l’original annulé. Les deux points d’entrée nécessitent la ressource ACL `Magento_Sales::actions_edit`. <!-- ACCS-1284 -->

### Filtrer les commandes et les factures par société

Les points d’entrée `GET /V1/orders` et `GET /V1/invoices` de l’API REST prennent désormais en charge le filtrage par `company_id` et `company_name`, ce qui permet aux intégrations B2B de récupérer les commandes ou les factures d’une entreprise spécifique dans une seule requête. <!-- ACCS-1111, CCSAAS-5076 -->

### Importer plus de codes de coupon par fichier

La limite d’importation de coupons en bloc par fichier peut être ajustée en contactant votre responsable du succès client Adobe Commerce ou en créant un ticket d’assistance. <!-- CCSAAS-5176 -->

### Gérer les modèles d’e-mail personnalisés via l’API

Les nouveaux points d’entrée d’API REST suivants permettent aux intégrations de répertorier, de récupérer et de créer des [modèles d’e-mail personnalisés](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/custom-email/) :

| Méthode | Point d’entrée | Description |
| --- | --- | --- |
| `GET` | `/V1/custom-email/templates` | Répertoriez vos modèles d’e-mail personnalisés, en renvoyant l’identifiant, le code, l’objet et le type de chaque modèle. |
| `GET` | `/V1/custom-email/templates/{id}` | Récupérer un modèle unique, y compris son corps et ses styles |
| `POST` | `/V1/custom-email/templates` | Créez un modèle d’e-mail personnalisé et renvoyez son identifiant attribué par le serveur. |

Utilisez un ID de modèle renvoyé avec le point d’entrée `POST /V1/custom-email/send` au lieu de rechercher l’ID manuellement.

Tous les points d’entrée `custom-email` nécessitent l’accès à la `Marketing > Communications > Email template` [ressource de rôle](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/user-accounts/permissions-user-roles#step-2assign-resources). <!-- CCSAAS-5089, CCSAAS-5090 -->

### Gérer la chaîne de commande complète via l’API REST

>[!IMPORTANT]
>
>Cette fonctionnalité est expérimentale et doit être activée en contactant votre responsable du succès client Adobe Commerce ou en créant un ticket d’assistance.

Les nouveaux points d’entrée de l’API REST `orderChain` permettent aux intégrations de modifier un ordre à l’aide de son identifiant et de résoudre automatiquement la chaîne complète des ordres modifiés :

| Méthode | Point d’entrée | Description |
| --- | --- | --- |
| `POST` | `/V1/orderChain/{orderId}/invoice` | Créez une facture pour la commande, en résolvant les articles sur la facture dans la chaîne de commande. |
| `POST` | `/V1/orderChain/{id}/cancel` | Annule la commande courante dans la chaîne. |
| `POST` | `/V1/orderChain/{id}/hold` | Mettre la commande en attente. |
| `POST` | `/V1/orderChain/{id}/unhold` | Supprimez le blocage de la commande. |
| `POST` | `/V1/orderChain/{id}/emails` | Envoyez une notification électronique de commande. |
| `POST` | `/V1/orderChain/{id}/comments` | Ajoutez un commentaire à la commande. |
| `GET` | `/V1/orderChain/{id}/comments` | Récupérez les commentaires de commande. |
| `GET` | `/V1/orderChain/{id}/statuses` | Récupérez le statut actuel de la commande. |

`GET` points d’entrée qui prennent en charge le filtrage des factures, des expéditions, des avoirs et des retours prennent désormais en charge le filtrage par `order_original_id`. Le filtrage par `order_original_id` renvoie des détails sur l’ensemble de la chaîne de commande, et pas seulement sur une seule commande. Un exemple de point d’entrée qui prend en charge cette fonctionnalité est `GET /V1/invoices`. <!-- ACCS-1004, ACCS-1005 -->

### Rechercher les valeurs d’attribut personnalisées dans la grille de commande

>[!IMPORTANT]
>
>Cette fonctionnalité est désactivée par défaut. Pour l’activer, contactez votre responsable du succès client Adobe Commerce ou créez un ticket d’assistance.

Les commerçants peuvent désormais filtrer la grille de commande [!DNL Commerce Admin] en fonction des valeurs stockées dans les attributs personnalisés de commande. Un filtre [!UICONTROL **Attributs personnalisés**] est disponible dans la ligne de filtre de grille d’ordre.<!-- ACCS-923 -->

### Définir une source d’inventaire désignée pour les articles du panier

La nouvelle mutation `setNominatedSourceOnCartItems` GraphQL attribue une source d’inventaire spécifique aux articles du panier, prenant en charge des scénarios tels que le retrait en magasin (BOPIS) et l’expédition en magasin. La mutation accepte un `cart_id` et une liste d’éléments, chacun avec un `cart_item_uid` et un `source_code`, et renvoie tout `rejected_items` avec un code d’erreur structuré : `UNKNOWN_SOURCE`, `SOURCE_DISABLED`, `NOT_ENOUGH_QTY` ou `SKU_SOURCE_CONFLICT`. Chaque SKU d’un panier est résolu sur une source nommée unique et la transmission d’une `source_code` nulle ou vide efface la nomination. <!-- ACCS-932 -->

### Abonnement à un événement pour les paniers correspondant aux règles de rappel

Un nouvel événement `observer.reminder_matched_carts` est émis une fois que les règles de rappel par e-mail ont exécuté leur logique de correspondance, transportant des informations sur les paniers correspondants. Les intégrations peuvent s’abonner à cet événement et transférer les données vers un système externe, tel qu’une plateforme marketing, au lieu de compter sur les e-mails de rappel natifs. <!-- CCSAAS-5173 -->

### Supprimer les e-mails transactionnels par zone ou modèle

Une nouvelle configuration [!UICONTROL **Suppression des e-mails**] ([!UICONTROL **Magasins**] > [!UICONTROL **Configuration**] > [!UICONTROL **Adobe Services**] > [!UICONTROL **Suppression des e-mails**]) permet aux administrateurs d’arrêter de manière sélective [!DNL Commerce] d’envoyer des e-mails transactionnels. Vous pouvez supprimer des e-mails par domaine fonctionnel (par exemple, compte client, Order Management, retours, passage en caisse, marketing ou B2B) ou par une liste exacte d’identifiants de modèle.<!-- ACCS-1025 -->

### Afficher l’historique des modifications de commande dans Admin

La page Détails de la commande [!DNL Commerce Admin] affiche désormais la chaîne de modification complète d’une commande qui inclut la commande d’origine et toutes les commandes enfants créées par le biais de modifications ultérieures. Les commerçants peuvent naviguer entre les commandes, activer/désactiver la visibilité des commandes annulées et accéder à toutes les factures, expéditions, avoirs et commentaires de commande associés à partir de la vue de chaîne<!-- ACCS-968 -->.

>[!NOTE]
>
>Pour activer cette fonctionnalité, contactez votre responsable du succès client Adobe Commerce.

### Affichage des ressources synchronisées dans [!DNL AEM Assets]

L’intégration [!DNL AEM Assets] comprend désormais une page [!UICONTROL **Statut de synchronisation**] ([!UICONTROL **Magasins**] > [!UICONTROL **AEM Assets**] > [!UICONTROL **Statut de synchronisation**]) avec une vue de liste centrée sur les ressources de toutes les ressources synchronisées, y compris le filtrage, les colonnes triables telles que la date de la dernière synchronisation et les détails d’erreur pour les synchronisations ayant échoué.<!-- ACAP-1246 -->

### Améliorations et correctifs

Les améliorations, optimisations et correctifs suivants sont inclus dans cette version :

* Les catalogues partagés volumineux sont désormais plus faciles à gérer dans l’administration, avec des temps de chargement améliorés et une probabilité réduite de dépassements de délai. <!-- CCSAAS-4946, CCSAAS-4925, CCSAAS-1245, CCSAAS-1246 -->

* Correction d&#39;un échec de création d&#39;expédition qui se produisait lors de la création d&#39;expéditions pour des commandes contenant des produits configurables. <!-- ACCS-1095 -->

* Correction d’un problème dans le [!DNL Commerce Admin] en raison duquel le menu de navigation de gauche pouvait disparaître. <!-- ACCS-1035 -->

* Amélioration des performances d’affectation et d’annulation d’affectation dans les catalogues partagés. <!-- ACCS-1324, CCSAAS-5177, CCSAAS-5190, CCSAAS-5192 -->

* Amélioration des performances de l’intégration [!DNL AEM Assets]. <!-- ACAP-1242 -->

* Correction d’une erreur qui pouvait se produire lors de l’ajout d’un SKU de produit simple à un produit configurable dans le [!DNL Commerce Admin]. <!-- ACCS-1132 -->

* Correction d’un problème en raison duquel la file d’attente de messages pouvait arrêter le traitement de nouveaux messages lorsqu’elle accumulait trop d’enregistrements obsolètes. <!-- ACCS-1292 -->

* Correction d’un problème en raison duquel la création de la commande d’administration échouait avec une erreur « SKU non disponible dans le catalogue partagé ». <!-- ACCS-1318 -->

* Correction d’un blocage qui se produisait lors de la création ou de la modification de produits groupés. <!-- CCSAAS-5211 -->

* Correction d&#39;un problème en raison duquel le placement de la commande ne réservait pas le stock à la source désignée pour les articles utilisant le retrait en magasin ou l&#39;expédition en magasin. <!-- ACCS-1374 -->

* Les frais personnalisés obsolètes sont désormais effacés de la réponse à la requête de panier. <!-- ACCS-1400 -->

* Correction d’un problème dans l’intégration [!DNL AEM Assets] en raison duquel les attributs de rôle de ressource de produit perdaient les données des paramètres régionaux lors de l’exportation du catalogue. <!-- ACCS-1401 -->

* Amélioration de l’avertissement reçu lors de l’enregistrement d’une intégration indiquant que [!DNL Dynamic Media] n’est pas activé. <!-- ACAP-1298 -->

* Les champs Nom de l’événement et Alias sont désormais validés pour être en minuscules lorsque vous vous abonnez à un événement. <!-- CEXT-6164 -->

* Les modèles de règles d’expression régulière Webhook sont désormais validés lorsque vous enregistrez un webhook conditionnel. <!-- CEXT-6287 -->

{{accs-release}}

>[!ENDSHADEBOX]

## Juin 2026 - version #1

[!BADGE Production]{type=Neutral tooltip="Les éléments répertoriés sont actuellement disponibles dans les environnements de production."}

<!-- [!BADGE Sandbox]{type=Caution tooltip="The items listed are currently only available in Sandbox environments. Adobe makes new releases available in Sandbox environments first to provide time to test upcoming changes before the release is available on Production environments."} -->

Les éléments suivants ont été publiés dans les environnements de production le 4 juin 2026.

>[!BEGINSHADEBOX]

### Ajout et modification de codes de coupon personnalisés dans Admin

Les commerçants peuvent désormais [créer et modifier des codes de coupon personnalisés](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-coupon#method-3-custom-coupon-codes) directement à partir de la [!DNL Commerce Admin] sur les règles de prix de panier manuelles. Un nouveau bouton [!UICONTROL **Ajouter un coupon personnalisé**] est disponible dans la section [!UICONTROL **Gérer les codes coupon**] lors de la modification d’une règle de prix de panier. <!-- CCSAAS-4508 -->

### Suivi des expéditions à l&#39;aide de transporteurs par défaut et personnalisés

Le suivi des commandes est désormais fiable pour les transporteurs d’expédition par défaut et personnalisés dans le [!DNL Commerce Admin], ce qui aide les commerçants à offrir des expériences de suivi après achat cohérentes. Auparavant, la sélection d&#39;un opérateur, tel qu&#39;UPS ou FedEx, et l&#39;application d&#39;un identifiant de tracking pouvaient empêcher l&#39;affichage du lien de tracking. Aucune action du commerçant n&#39;est requise pour restaurer ce comportement. La prise en charge des liens de suivi est également disponible pour les [opérateurs personnalisés](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/shipping-reference/) créés avec le [!DNL App Builder Integration Starter Kit]. <!-- ACCS-891 -->

### Affichage des types d’entrée d’attribut dans la grille Attributs de produit

Une nouvelle colonne [!UICONTROL **Type d’attribut**] est désormais visible dans la grille Attributs du produit dans ([!UICONTROL **Magasins**] > _[!UICONTROL Attributes]_>[!UICONTROL **Produit**]), qui affiche le type d’entrée (champ de texte, liste déroulante ou oui/non) pour chaque attribut de produit, y compris les types fournis par les extensions. Cela facilite l’identification et la gestion des attributs lorsque vous utilisez des jeux d’attributs volumineux. <!-- ACCS-925 -->

### Personnaliser l’en-tête de réponse pour les e-mails personnalisés

Les commerçants peuvent désormais configurer l’en-tête [!UICONTROL **Répondre-à**] utilisé par le point d’entrée [POST /rest/V1/custom-email/send](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/custom-email/), de sorte que les réponses des clients peuvent être acheminées vers une adresse différente de celle de l’expéditeur. <!-- ACCS-1037 -->

### Affichez les prix de niveau sur la page de modification de produit dans les environnements de catalogue partagé volumineux

Les commerçants ayant un grand nombre de catalogues partagés peuvent maintenant accéder à l&#39;onglet en lecture seule [!UICONTROL **Prix de niveau**] sur la page de modification du produit dans le [!DNL Commerce Admin]. <!-- CCSAAS-4922 -->

### Améliorations et correctifs

Les améliorations, optimisations et correctifs suivants sont inclus dans cette version :

* Correction d’un problème en raison duquel le point d’entrée REST POST `V1/async/custom-email/send` renvoyait une erreur de validation `UnstructuredArray`. Le point d’entrée asynchrone fonctionne désormais de manière cohérente avec le point d’entrée `V1/custom-email/send` POST synchrone. <!-- ACCS-921 -->

* Correction d’un problème où les attributs sérialisables personnalisés sur des entités telles que Société étaient involontairement effacés lors de la mise à jour de l’entité par le biais de REST sans inclure les attributs personnalisés dans la payload. Les attributs personnalisés sont désormais conservés lorsqu’ils ne sont pas fournis. <!-- ACCS-946 -->

* Correction d’une erreur « le client n’est pas autorisé » qui empêchait les connexions GraphQL invitées lorsque l’en-tête `X-Adobe-Company` était présent dans la requête. <!-- ACCS-949 -->

* Correction d’un problème en raison duquel la modification ou la suppression d’une entreprise dans le [!DNL Commerce Admin] pouvait échouer avec une erreur « Aucune entité de ce type » après l’affectation d’un client ou d’une cliente à l’entreprise via le point d’entrée REST PUT `V1/customers/companies`. <!-- ACCS-856 -->

* Correction d&#39;un problème lié aux statuts de grille de commande client obsolètes. <!-- CCSAAS-4915 -->

* Correction d’un problème dans le [!DNL Commerce Admin] en raison duquel les fichiers joints en tant qu’exemples et liens sur des produits téléchargeables renvoyaient une erreur `404` lorsqu’ils étaient accessibles à partir de la page de modification du produit. <!-- CCSAAS-4394 -->

* Correction d’une erreur « Clé de tableau non définie « simple_sku » qui pouvait se produire lors de la création d’une expédition pour une commande contenant des produits configurables. <!-- CCSAAS-4877 -->

* La requête `guestOrderByToken` GraphQL renvoie désormais un message d’erreur plus informatif lorsqu’elle est appelée avec un jeton incorrect, au lieu d’une erreur de serveur interne. <!-- CCSAAS-4921 -->

* La requête `customer` GraphQL renvoie désormais un message d’erreur plus informatif lorsque les commandes client ne peuvent pas être chargées. <!-- ACCS-867 -->

* Le point d’entrée REST GET `V1/customers/{customerId}` renvoie désormais le champ de configuration `assistance_allowed` . <!-- USF-4132 -->

{{accs-release}}

>[!ENDSHADEBOX]

## Mai 2026 - #1 de publication

[!BADGE Production]{type=Neutral tooltip="Les éléments répertoriés sont actuellement disponibles dans les environnements de production."}

Les éléments suivants ont été publiés dans les environnements de production le 7 mai 2026.

>[!BEGINSHADEBOX]

### Ignorer reCAPTCHA pour l’authentification OTP par programmation

Une nouvelle option de configuration vous permet d’ignorer la validation reCAPTCHA pour la mutation [`exchangeOtpForCustomerToken`](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/exchange-otp-customer-token/) de GraphQL. Cela active les workflows de pointage B2B où l’échange de mot de passe à usage unique (OTP) est lancé par programmation sans entrée de formulaire, ce qui rend la validation reCAPTCHA inutile. Cette fonctionnalité s’appuie sur la fonctionnalité [connexion par code unique](https://experienceleague.adobe.com/en/docs/commerce-admin/customers/customer-accounts/manage/login-as-customer){target="_blank"} introduite dans la version de mars 2026. La mutation `exchangeOtpForCustomerToken` continue de nécessiter reCAPTCHA par défaut lorsque reCAPTCHA est activé pour la connexion client. Contactez votre responsable du succès client Adobe Commerce pour activer cette option. <!-- ACCS-850 -->

### Modifier les commandes partiellement facturées

Le bouton [!UICONTROL **Modifier**] est maintenant disponible sur l&#39;écran [!UICONTROL **Affichage des commandes**] pour les commandes partiellement facturées, ce qui donne aux commerçants une plus grande flexibilité pour modifier les commandes qui sont toujours en cours. Auparavant, les commandes comportant des factures ne pouvaient pas être modifiées, même s&#39;il restait des articles non facturés. Tant qu’un article de la commande peut toujours être facturé, la commande peut être modifiée. Les commerçants avec des intégrations personnalisées qui reposent sur la restriction de modification précédente doivent passer en revue leurs workflows. <!-- ACCS-849 -->

### Améliorations et correctifs

Les améliorations, optimisations et correctifs suivants sont inclus dans cette version :

* Correction d’un problème où l’attribut d’extension `stock_item` n’était pas renvoyé sur le point d’entrée de liste de l’API REST `GET /V1/products`. La réponse correspond désormais au contrat d’API documenté. <!-- ACCS-819 -->

* Correction d’un problème en raison duquel les liens de réinitialisation de mot de passe dans les e-mails renvoyaient une erreur 404. <!-- ACCS-797 -->

* Amélioration des performances des requêtes d’historique de commandes pour les sociétés utilisant des filtres de période. <!-- ACCS-859 -->

* Correction d’un problème en raison duquel les utilisateurs d’une entreprise B2B pouvaient voir les commandes d’homologues avant qu’un utilisateur ne rejoigne l’entreprise. <!-- ACCS-859 -->

* Résolution des problèmes de délai d’expiration de passage en caisse qui pouvaient affecter les performances de l’API REST lors du chargement des devis avec `trigger_recollect` activé. <!-- CCSAAS-4904 -->

* Correction de problèmes de chargement de page qui pouvaient se produire après l’envoi d’une commande dans le [!DNL Commerce Admin]. <!-- CCSAAS-4413 -->

* Correction d&#39;un problème en raison duquel les commandes avec le même horodatage pouvaient afficher des informations obsolètes sur le statut des commandes dans la grille des commandes client. <!-- CCSAAS-4890 -->

{{accs-release}}

>[!ENDSHADEBOX]

## Avril 2026 - #3 de publication

[!BADGE Production]{type=Neutral tooltip="Les éléments répertoriés sont actuellement disponibles dans les environnements de production."}

Les éléments suivants ont été publiés dans les environnements de production le 27 avril 2026.

>[!BEGINSHADEBOX]

### Améliorations et correctifs

Les améliorations, optimisations et correctifs suivants sont inclus dans cette version :

* Ajout du point d’entrée `GET /V1/order-statuses` de l’API REST pour récupérer tous les statuts de commande configurés avec leurs affectations d’état. <!-- CEXT-6100 -->

* Correction d’un problème en raison duquel les `custom_attributes` d’entités telles que Commande, Panier, Facture, Avoir et Société ne s’affichaient pas dans le schéma REST. <!-- CCSAAS-4818 -->

* Résolution des erreurs de traitement des messages en double (`MessageLockException`) dans le client d’API en bloc asynchrone. <!-- CCSAAS-4805 -->

* Les attributs de produit numériques s’affichent désormais sous la forme de filtres de plage de/à dans la grille de produits [!DNL Commerce Admin] lorsque l’attribut est activé pour les options de filtre. <!-- ACCS-761 -->

* Correction d’un problème en raison duquel les e-mails de rappel d’abandon de panier n’affichaient pas les images du produit lors de l’utilisation de [!DNL AEM Assets]. <!-- ACCS-798 -->

* Correction d’un problème en raison duquel une erreur false « taille maximale de chargement » pouvait s’afficher lors de l’ajout de fichiers, d’exemples ou de liens vers des produits téléchargeables. <!-- ACCS-813 -->

* Correction d’un problème en raison duquel l’enregistrement d’un produit affecté à plusieurs catalogues partagés pouvait entraîner une erreur. <!-- ACCS-788 -->

* Correction d’un problème en raison duquel la requête d’historique de commandes pouvait être lente et entraîner des erreurs de mémoire insuffisante pour la base de données pour les entreprises ayant de nombreuses commandes. <!-- ACCS-808 -->

* Correction d’un problème en raison duquel la validation du fichier d’importation pouvait échouer. <!-- CCSAAS-4364 -->

* Suppression de la configuration **[!UICONTROL Recently Viewed/Compared Products]** de la section **[!UICONTROL Catalog]** dans **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**, car elle n’est pas prise en charge par [!DNL Adobe Commerce as a Cloud Service] admin. <!-- ACCS-793 -->

>[!ENDSHADEBOX]

## Avril 2026 - #2 de publication

[!BADGE Production]{type=Neutral tooltip="Les éléments répertoriés sont actuellement disponibles dans les environnements de production."}

<!-- [!BADGE Sandbox]{type=Caution tooltip="The items listed are currently only available in Sandbox environments. Adobe makes new releases available in Sandbox environments first to provide time to test upcoming changes before the release is available on Production environments."} -->

Les éléments suivants ont été publiés dans les environnements de production le 16 avril 2026.

>[!BEGINSHADEBOX]

### Mise en œuvre de totaux de devis personnalisés avec webhooks

Le `plugin.magento.out_of_process_totals_collector.api.get_total_modifications.execute` [webhook](https://developer.adobe.com/commerce/extensibility/webhooks/) est désormais disponible dans [!DNL Adobe Commerce as a Cloud Service]. Utilisez-le pour implémenter des modifications de totaux de devis personnalisés via l’extensibilité hors processus. <!-- CEXT-5896 -->

### Règles de rappel d’e-mail réutilisables (expérimentales)

>[!IMPORTANT]
>
>Cette fonctionnalité est expérimentale et doit être activée en contactant votre responsable du succès client Adobe Commerce ou en créant un ticket d’assistance.

[Règles de rappel d’e-mail](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/communications/email-reminders/email-reminder-rules#rule-repeatability) prennent désormais en charge un paramètre de réutilisation de règle facultatif qui permet à la même règle de s’appliquer à nouveau à un client une fois que la condition de déclencheur d’origine ne s’applique plus.

Par exemple, si un client abandonne un panier, effectue l’achat et abandonne ultérieurement un nouveau panier, la règle peut se déclencher à nouveau. Sans ce paramètre, un client qui efface le déclencheur d’origine est définitivement exclu des futures correspondances de la même règle.

### Afficher le rapport des transactions de Payment Services

Si vous avez [[!DNL Payment Services]](https://experienceleague.adobe.com/en/docs/commerce/payment-services/get-started/production) activé, l’interface utilisateur [Tableau de bord](../payment-services/payments-home.md) est désormais disponible dans le [!DNL Commerce Admin], ce qui permet d’accéder au rapport [Transactions](../payment-services/reporting.md#transactions-report-view) pour afficher et gérer les transactions de paiement. <!-- PAY-6510 -->

### Améliorations et correctifs

Les améliorations, optimisations et correctifs suivants sont inclus dans cette version :

* Correction d’une erreur 500 sur la page Entreprises d’affectation de catalogue partagé qui pouvait se produire lors de l’utilisation de catalogues partagés volumineux avec Admin UI SDK. <!-- CCSAAS-4783 -->

* Correction d’un problème en raison duquel les clients de l’entreprise ne pouvaient pas voir leurs propres commandes si celles-ci étaient passées avant que le client ne soit affecté à l’entreprise. <!-- ACCS-746 -->

>[!ENDSHADEBOX]

## Avril 2026

[!BADGE Production]{type=Neutral tooltip="Les éléments répertoriés sont actuellement disponibles dans les environnements de production."}

Les éléments suivants ont été publiés dans les environnements de production le 1er avril 2026.

>[!BEGINSHADEBOX]

### Ajouter des fichiers aux produits

[!DNL Adobe Commerce as a Cloud Service] prend désormais en charge [l’ajout de fichiers aux produits](./product-files.md) à l’aide d’attributs de produit de type fichier). Vous pouvez charger les fichiers manuellement sur la page de modification du produit, par programmation via l’API REST, ou en bloc en fournissant des URL externes au format CSV. <!-- ACCS-535, ACCS-565 -->

### Vérification du statut d’abonnement aux alertes de prix et de stock via GraphQL

Grâce aux nouvelles requêtes GraphQL, [`isSubscribedProductAlertStock`](https://developer.adobe.com/commerce/webapi/graphql/schema/products/queries/is-subscribed-product-alert-stock/){target="_blank"} et [`isSubscribedProductAlertPrice`](https://developer.adobe.com/commerce/webapi/graphql/schema/products/queries/is-subscribed-product-alert-price/){target="_blank"}, les storefronts peuvent déterminer si un acheteur est déjà abonné aux alertes de stock ou de prix pour un produit. <!-- ACCS-334 -->

### Créer des attributs de produit numériques qui prennent en charge les valeurs négatives

Un nouveau `numeric` [type d’entrée d’attribut de produit](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/attributes-input-types) permet aux commerçants de créer des attributs décimaux qui prennent en charge les valeurs négatives. <!-- ACCS-600 -->

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

>[!ENDSHADEBOX]

## Mars 2026 - #2 de publication

[!BADGE Production]{type=Neutral tooltip="Les éléments répertoriés sont actuellement disponibles dans les environnements de production."}

Les éléments suivants ont été publiés dans les environnements de production le 24 mars 2026.

>[!BEGINSHADEBOX]

### Connectez-vous en tant que client à l’aide de codes uniques

Les administrateurs peuvent désormais générer des [codes à usage unique](https://experienceleague.adobe.com/en/docs/commerce-admin/customers/customer-accounts/manage/login-as-customer) pour l’emprunt d’identité du client via l’API [!DNL Commerce Admin] et REST. Le code unique peut être échangé contre un jeton d’accès client par le biais des mutations GraphQL `generateCustomerToken` ou `exchangeOtpForCustomerToken`, ce qui permet d’activer les flux « Connexion en tant que client » sans mot de passe pour les scénarios d’achat assistés par le vendeur. <!-- ACCS-404 -->

Pour obtenir des conseils sur l’implémentation de cette fonctionnalité à l’aide d’API, consultez la documentation [API REST](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/login-as-customer/) et [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/generate-token/).

### Gérer les comptes de carte cadeau via l’API REST

[Comptes de carte cadeau](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/gift-card-accounts/) peuvent désormais être créés, mis à jour, supprimés et interrogés via l’API REST. En outre, la prise en charge de l’importation en bloc JSON est disponible via le point d’entrée `/V1/import/json`, ce qui permet aux intégrations tierces de synchroniser les cartes-cadeaux par programmation. <!-- ACCS-476 -->

### Déclencher des e-mails transactionnels via l’API REST

Un nouveau point d’entrée de l’API REST (`POST /V1/custom-email/send`) vous permet de [déclencher des e-mails transactionnels](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/custom-email/) à la demande en spécifiant un identifiant de modèle d’e-mail, l’adresse e-mail du destinataire et les variables de modèle. L’API prend en charge les tableaux imbriqués en tant que variables de modèle pour le contenu d’e-mail complexe. <!-- ACCS-325, ACCS-481 -->

### Abonnez-vous au webhook des taux d’obtention des frais d’expédition hors processus .

Le webhook `plugin.out_of_process_shipping_methods.api.shipping_rate_repository.get_rates` est désormais disponible dans la liste Admin Webhooks de [!DNL Adobe Commerce as a Cloud Service]. Utilisez-le pour implémenter [méthodes d’expédition personnalisées](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/shipping-use-cases/#shipping-methods). <!-- ACCS-478 -->

### Chargement de PDF et d’autres fichiers via les attributs de produit

Un nouveau « fichier » [Type d’entrée d’attribut](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/attributes-input-types) vous permet de créer des jeux d’attributs dans lesquels vous pouvez charger des fichiers, tels que des PDF, sur des produits individuels. Vous pouvez configurer les extensions de fichier autorisées et la taille de fichier maximale en accédant à [!UICONTROL **Magasins**] > [!UICONTROL **Configuration**] > [!UICONTROL _Catalogue_] > [!UICONTROL **Attributs de fichier de produit**]. <!-- ACCS-535, ACCS-565 -->

### Configuration des attributs personnalisés d’entreprise

Les administrateurs peuvent désormais gérer les attributs personnalisés de l’entreprise sur la page d’édition Entreprise de la [!DNL Commerce Admin]. Les attributs personnalisés peuvent être configurés, enregistrés et validés à partir de l’interface utilisateur d’administration pour [!DNL Adobe Commerce as a Cloud Service].

Pour configurer les attributs personnalisés de l’entreprise, accédez à [!UICONTROL **Clients**] > [!UICONTROL **Entreprises**] et sélectionnez une entreprise pour ouvrir la page de modification. Sélectionnez ensuite l’onglet [!UICONTROL **Attributs personnalisés**] pour ajouter de nouveaux attributs.
<!-- ACCS-294 -->

### S’abonner aux alertes de prix et de stocks via GraphQL

Les storefronts EDS fonctionnent désormais avec [alertes de prix et de stocks](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/configuration/product-alerts/alert-setup). <!-- ACCS-334 -->

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

* Réactivation des points d’entrée GET `/V1/directory/countries` et GET `/V1/directory/countries/:countryId` de l’API REST pour les intégrations d’administration, ce qui permet aux clients de rechercher des données de pays et de région valides. <!-- ACCS-518 -->

* Correction d’un problème de délai d’expiration qui pouvait se produire dans l’API REST lorsqu’un utilisateur disposait d’un catalogue partagé volumineux. <!-- ACCS-4657 -->

* Correction d’un problème en raison duquel les sociétés B2B bloquées pouvaient toujours ajouter des produits au panier. <!-- ACCS-552 -->

* Si les grilles Client ou Société contiennent une grande quantité de données, les boutons d’exportation ne sont plus disponibles pour éviter les erreurs. <!-- ACCS-320 -->

* Correction d’un problème en raison duquel les tailles de fichiers joints ne s’affichaient pas correctement. <!-- ACCS-566 -->

* Correction d’un problème lié à la création et la suppression des types d’attributs « Fichier » dans le [!DNL Commerce Admin]. <!-- ACCS-605, ACCS-606 -->

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

Auparavant, la limite du nombre de sites web, de boutiques et d’affichages de boutique était limitée à 50. Vous pouvez maintenant envoyer une [demande d’assistance](https://experienceleague.adobe.com/home?support-tab=home#support) pour modifier ces limites, si nécessaire. <!-- ACCS-398 -->

### Personnaliser les messages d’authentification du storefront avec des codes d’erreur structurés

La mutation [`generateCustomerToken` GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/generate-token/){target="_blank"} renvoie désormais des codes d’erreur saisis avec les messages d’erreur, ce qui permet aux storefronts d’afficher des messages d’interface utilisateur spécifiques par raison d’échec. Les codes d’erreur disponibles sont les suivants : `CUSTOMER_MISSING_EMAIL`, `CUSTOMER_MISSING_PASSWORD`, `CUSTOMER_SIGN_IN_INCORRECT_OR_LOCKED`, `CUSTOMER_ACCOUNT_NOT_CONFIRMED` et `CUSTOMER_GENERIC_ERROR`. <!-- ACCS-301 -->

### Envoyer des rappels automatisés par e-mail pour l’inactivité du panier et de la liste de souhaits

Le module [Rappel par e-mail](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/communications/email-reminders/email-reminder-rules) (`Magento_Reminder`) est désormais actif dans [!DNL Adobe Commerce as a Cloud Service]. Il permet aux commerçants de créer des règles de rappel automatisées qui déclenchent des e-mails aux clients en fonction de l’inactivité du panier et de la liste de souhaits. <!-- CCSAAS-4597 -->

### S’abonner au webhook des événements de suppression de catégorie

Le webhook `observer.catalog_category_delete_before` est désormais disponible dans [!DNL Adobe Commerce as a Cloud Service]. Utilisez-la pour exécuter la logique avant qu’une catégorie ne soit supprimée. <!-- CEXT-5862 -->

### Suivre les commandes passées par des invités avec un e-mail enregistré

Une nouvelle configuration facultative au niveau du magasin permet aux clients de [suivre les commandes des invités](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/point-of-purchase/checkout/checkout-guest#allow-guest-order-access-for-registered-emails) qu’ils ont passées, si la commande a été passée à l’aide d’une adresse e-mail correspondant à un compte client enregistré. <!-- ACCS-289 -->

### Améliorations et correctifs

Les améliorations, optimisations et correctifs suivants sont inclus dans cette version :

* Correction d’un problème en raison duquel certains administrateurs d’organisation pouvaient accéder incorrectement aux instances du client sans droits par client. <!-- ACCS-335 -->

* Correction d’un problème en raison duquel un utilisateur était déconnecté du [!DNL Commerce Admin] lors de la modification d’un catalogue partagé. <!-- ACCS-318 -->

* Correction d’un problème en raison duquel certains champs de Webhooks s’affichaient incorrectement dans l’interface utilisateur de [!DNL Commerce Admin]. <!-- CEXT-5874 -->

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

>[!ENDSHADEBOX]

## Février 2026 - #1 de mise à jour

[!BADGE Production]{type=Neutral tooltip="Les éléments répertoriés sont actuellement disponibles dans les environnements de production."}

Les éléments suivants ont été publiés dans les environnements de production d’[!DNL Adobe Commerce as a Cloud Service] le 10 février 2026.

>[!BEGINSHADEBOX]

### Personnaliser les méthodes d’expédition et afficher les rapports d’administration

Les améliorations suivantes ont été apportées au [!DNL Commerce Admin] :

* Amélioration de la fonctionnalité hors processus [payloads webhook d’expédition](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/shipping-use-cases/#payload) pour inclure les attributs personnalisés d’adresse d’expédition. Cette modification permet aux commerçants de mettre en œuvre des méthodes d’expédition personnalisées. <!-- ACCS-235 -->

* Ajout d’un accès aux rapports d’administration, y compris les rapports pour [Clients](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/customer-reports), [Marketing](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/marketing-reports), [Produits](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/product-reports) et [Ventes](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/sales-reports). <!-- CCSAAS-3085 -->

>[!NOTE]
>
>Les rapports non disponibles dans [!DNL Adobe Commerce as a Cloud Service] sont étiquetés comme PaaS uniquement ([!BADGE PaaS uniquement]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."}).

### Capturer des montants de facture personnalisés via l’API REST

L’API Invoice prend désormais en charge les [montants de capture personnalisés](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#custom-capture-amounts) à l’aide d’attributs d’extension. <!-- ACCS-186, ACCS-197, ACCS-143 -->

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

>[!ENDSHADEBOX]

## Janvier 2026

[!BADGE Production]{type=Neutral tooltip="Les éléments répertoriés sont actuellement disponibles dans les environnements de production."}

Les éléments suivants ont été publiés dans les environnements de production d’[!DNL Adobe Commerce as a Cloud Service] le 20 janvier 2026.

>[!BEGINSHADEBOX]

### Listes déroulantes B2B

Les modifications suivantes ont été apportées aux composants de liste déroulante B2B :

* [!DNL Commerce Storefront on Edge Delivery Services] inclut désormais des composants de liste déroulante [B2B](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/). Les listes déroulantes B2B suivantes sont désormais disponibles :

  * **[Gestion de l’entreprise](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/company-management/)** - Active la gestion des profils d’entreprise et les autorisations basées sur les rôles pour les storefronts Adobe Commerce.
  * **[Sélecteur d’entreprise](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/company-switcher/)** - Fournit un composant d’interface utilisateur permettant aux utilisateurs de basculer entre plusieurs entreprises auxquelles ils sont associés.
  * **[Commandes fournisseur](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/purchase-order/)** - Gère les workflows de commande fournisseur, les règles d&#39;approbation et l&#39;historique des commandes fournisseur pour les transactions B2B.
  * **[Gestion des devis](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/quote-management/)** - Active les devis négociables pour les clients B2B avec des workflows de demande, de négociation et d&#39;approbation de devis.
  * **[Listes de demandes d&#39;approvisionnement](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/requisition-list/)** - Fournit des outils pour la création et la gestion des listes de demandes d&#39;approvisionnement pour les achats répétés et les commandes groupées.

* Publication du package de compatibilité B2B Storefront. Ce package améliore le schéma GraphQL B2B [!DNL Adobe Commerce] pour améliorer le développement sur les systèmes B2B.

<!-- 
* [!DNL Commerce Storefront on Edge Delivery Services] now includes [B2B drop-in components](http://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/). For a complete list of available B2B drop-in blocks, refer to the [storefront documentation](http://experienceleague.adobe.com/developer/commerce/storefront/merchants/b2b-commerce-blocks/).

* Released the [B2B Storefront Compatibility Package](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility-b2b/). This package enhances the [!DNL Adobe Commerce] B2B GraphQL schema to help improve development on B2B systems. 
-->

### Liens cliquables vers des dispositifs de suivi d’expédition externes

Transformez les numéros de suivi des expéditions inclus dans les e-mails des acheteurs en texte brut en liens cliquables en [activant les URL de suivi personnalisées](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/delivery/shipping-settings#shipment-tracking-urls). Cette fonctionnalité est prise en charge pour USPS, UPS, FedEx et DHL. <!-- See PR #716 in commerce-admin -->

### Assistance Google reCAPTCHA Enterprise

[!DNL Adobe Commerce as a Cloud Service] storefronts prennent désormais en charge [reCAPTCHA Enterprise](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/captcha/security-google-recaptcha-enterprise). Cette fonctionnalité offre une protection de robots avancée en utilisant l’analyse de risque adaptative et le machine learning pour distinguer précisément les utilisateurs humains des robots automatisés. Il renforce la sécurité du site, empêche les activités frauduleuses et réduit le spam et les abus afin de maintenir une expérience d&#39;achat fiable. <!-- CCSAAS-4242 -->

### Accès administrateur spécifique à l’instance

Vous pouvez désormais [attribuer l’accès utilisateurs](./user-management.md#add-users) à des instances [!DNL Adobe Commerce as a Cloud Service] individuelles dans Admin Console. <!-- CCSAAS-4337 -->
<!-- See PR #332 -->

### Observability

En utilisant [!DNL App Builder], vous pouvez obtenir une visibilité plus approfondie de votre instance de [!DNL Adobe Commerce as a Cloud Service] grâce à l’observabilité [OpenTelemetry](https://developer.adobe.com/commerce/extensibility/observability/), désormais disponible automatiquement. OpenTelemetry fournit des mesures, des journaux et des traces pour vous aider à surveiller les performances, à résoudre les problèmes plus rapidement et à optimiser votre storefront. Cette fonctionnalité permet d’obtenir des informations proactives sur l’intégrité du système et améliore la fiabilité pour vos clients.

>[!NOTE]
>
>L’observabilité d’OpenTelemetry nécessite l’utilisation de [!DNL App Builder] ou d’autres offres d’extensibilité hors processus (OOPE).

### Hiérarchiser la tarification pour les règles de prix de catalogue

Vous pouvez désormais combiner des remises de tarification échelonnée avec des remises de règle de catalogue à l&#39;aide de [règles de prix de catalogue](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/pricing/product-price-tier#enable-tier-pricing-for-catalog-price-rules). Cette amélioration vous permet de créer des stratégies de tarification plus dynamiques et plus concurrentielles, en récompensant les achats en gros tout en appliquant des remises promotionnelles. Le résultat est une plus grande flexibilité pour attirer les clients, augmenter la valeur des commandes et générer des conversions.<!-- See PR #708 in commerce-admin -->

### Améliorations et correctifs

Les améliorations, optimisations et correctifs suivants inclus dans cette version sont sélectionnés :

* Correction d&#39;une erreur qui pouvait se produire lors du chargement d&#39;un fichier dans S3. <!-- CCSAAS-4189 -->

* Correction d’une erreur `User is not entitled to access this instance` qui pouvait se produire lors de la connexion à l’administration Commerce ou de l’accès à l’API REST. <!-- CCSAAS-4324 -->

* Correction d’une erreur qui se produisait lors de la prévisualisation ou de la mise en file d’attente d’une newsletter dans la grille Modèle de newsletter. <!-- CCSAAS-4398 -->

* Correction d’une erreur `404` qui se produisait lorsque les utilisateurs cliquaient sur le bouton [!UICONTROL **Recharger les données**] du tableau de bord d’administration. <!-- CCSAAS-4468 -->

* Correction d’un problème où les attributs personnalisés du produit ne pouvaient pas être mis à jour via l’API REST lorsqu’[!DNL AEM Assets integration] était activé et que le produit contenait des images. <!-- ACAP-1178 -->

* Diverses améliorations des performances et de l’optimisation.
<!-- CCSAAS-4255 -->
<!-- CCSAAS-4233 -->
<!-- CCSAAS-4220 -->
<!-- CCSAAS-4252 -->
<!-- CCSAAS-4330 -->
<!-- CCSAAS-3669 -->
<!-- CCSAAS-4462 -->

>[!ENDSHADEBOX]

## Novembre 2025

>[!BEGINSHADEBOX]

### Améliorations

* [Gestion des utilisateurs](./user-management.md) - Modification du rôle **Administrateur de produit** dans Admin Console afin de mettre automatiquement à jour l’accès des utilisateurs et utilisatrices à l’administrateur Commerce. <!-- CCSAAS-3012 -->

* Ajout de la possibilité de charger et de récupérer des pièces jointes de devis négociables, ainsi que des fichiers et des images associés aux clients et aux adresses des clients dans Amazon S3 à l’aide d’URL présignées dans [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/uploads) et [REST](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/s3-uploads). Avec REST, vous pouvez également charger des images de catégorie. <!-- CCSAAS-3250 -->

* Ajout des points d’entrée `POST /V1/customers` et `PUT /V1/customers/{customerId}` à l’[API REST](https://developer.adobe.com/commerce/webapi/rest/reference/) pour créer et mettre à jour des clients. Ces points d’entrée nécessitent une autorisation IMS. <!-- CCSAAS-3112 -->

* Ajout de la mutation [&#128279;](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/exchange-otp-customer-token/), qui nécessite l’adresse e-mail et le mot de passe à usage unique (OTP) d’un acheteur et qui reçoit un jeton client en échange. `exchangeOtpForCustomerToken`Cette mutation est généralement utilisée dans les scénarios où un client doit s’authentifier à l’aide d’un mot de passe à usage unique envoyé à son adresse e-mail ou téléphone.

* Si une adresse définie dans l’écran de configuration [!UICONTROL **Stocker les adresses e-mail**] de l’administrateur contient une valeur se terminant par `example.com`, Commerce n’envoie pas d’e-mails à cette adresse. Au lieu de cela, le système consigne que l’e-mail n’a pas été envoyé.  <!-- CCSAAS-3533 -->

#### Attributs d’ordre personnalisés

* Les utilisateurs administrateurs peuvent désormais afficher et modifier les [attributs de commande personnalisés](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing#custom-order-attributes) directement à partir des écrans Afficher, Modifier et Créer dans le panneau d’administration. Cette amélioration améliore la gestion des données de commande personnalisées créées via GraphQL. <!-- CEXT-5044 -->

>[!ENDSHADEBOX]
