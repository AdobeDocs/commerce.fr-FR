---
title: Collecter des données Commerce à l’aide de balises Adobe Experience Platform
description: Découvrez comment collecter des données Commerce à l’aide de balises Adobe Experience Platform.
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '2563'
ht-degree: 0%

---

# Collecter des données Commerce à l’aide de balises Adobe Experience Platform

Bien que vous puissiez utiliser l’extension [!DNL Data Connection] pour publier des événements de storefront et vous y abonner, certains commerçants peuvent déjà utiliser une solution de collecte de données, telle que les balises [Adobe Experience Platform](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/create-a-property.html?lang=fr). Pour ces commerçants, Adobe Commerce fournit une option de publication uniquement dans l’extension [!DNL Data Connection] qui utilise le SDK d’événement Adobe Commerce.

Flux de données d’extension ![[!DNL Data Connection]](assets/tags-data-flow.png)
_[!DNL Data Connection]le flux de données d’extension avec des balises_

Dans cette rubrique, vous apprendrez à mapper les valeurs d’événement storefront fournies par l’extension [!DNL Data Connection] à la solution de balises Adobe Experience Platform que vous utilisez déjà.

## Collecter des données d’événement à partir d’Adobe Commerce

Pour collecter des données d’événement Commerce :

- Installez [Adobe Commerce Events SDK](https://github.com/adobe/commerce-events/tree/main/packages/storefront-events-sdk). Pour les storefronts PHP, voir la rubrique [install](install.md). Pour les storefronts PWA Studio, consultez le guide [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/integrations/adobe-commerce/aep/).

  >[!NOTE]
  >
  > Ne **pas** [configurer](connect-data.md) l’identifiant d’organisation et l’identifiant du flux de données.

## Mappage des données du storefront Commerce vers Adobe Experience Platform

Pour mapper les données du storefront Commerce à Adobe Experience Platform, configurez et installez les éléments suivants à partir des balises Adobe Experience Platform :

1. [Configurer une propriété de balise](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/create-a-property.html?lang=fr) dans la collecte de données Adobe Experience Platform.

1. Sous **Création**, sélectionnez **Extensions** et installez et configurez les extensions suivantes :

   - [Couche de données client Adobe](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/client-data-layer/overview.html?lang=fr)

   - [Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html?lang=fr)

1. [Publier la balise](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/overview.html?lang=fr) dans votre environnement de développement.

1. Suivez les étapes **Mappage d’événements** ci-dessous pour configurer des éléments de données et des règles pour des événements spécifiques.

### Mappage des événements

La collecte de données à l’aide de balises étant différente de l’utilisation du SDK d’événement Adobe Commerce, il est important de comprendre les termes équivalents utilisés dans les deux frameworks.

| Terme des balises Adobe Experience Platform | Terme de SDK d’événement Adobe Commerce |
|---|---|
| _éléments de données_ | contexte |
| _règles_ | événement |
|  | _conditions des règles_ - écouteurs d’événement (à partir de l’ACDL)<br><br>_actions des règles_ - gestionnaires d’événements (à envoyer à Adobe Experience Platform) |

Lorsque vous mettez à jour les éléments de données et les règles dans les balises Adobe Experience Platform avec des données d’événement spécifiques à Adobe Commerce, vous suivez certaines étapes courantes.

Par exemple, ajoutons l’événement Adobe Commerce `signOut` aux balises Adobe Experience Platform. Les étapes décrites ci-dessous, à l’exception des valeurs spécifiques que vous définissez, décrivent comment ajouter des [éléments de données](https://experienceleague.adobe.com/docs/experience-platform/collection/e2e.html?lang=fr#data-element) et des [règles](https://experienceleague.adobe.com/docs/experience-platform/collection/e2e.html?lang=fr#create-a-rule), qui s’appliquent à tous les événements Adobe Commerce que vous ajoutez aux balises.

1. Créer un élément de données :

   ![Créer Un Élément De Données](assets/create-new-data-elements.png)
   _Créer Un Élément De Données_

1. Définissez **Name** sur `sign out`.

1. Définissez **Extension** sur `Adobe Experience Platform Web SDK`.

1. Définissez **Type d’élément de données** sur `XDM object`.

1. Sélectionnez les **Sandbox** et **Schema** à mettre à jour.

1. Sous **userAccount** > **logout**, définissez la **valeur** dans **Déconnexion du visiteur** sur `1`.

   ![Mettre à jour la valeur de déconnexion](assets/signout-value.png)
   _Mettre à jour la valeur de déconnexion_

1. Sélectionnez **Enregistrer**.

1. Créez une règle :

   ![Créer une règle](assets/create-new-rule.png)
   _Créer une règle_

1. Sélectionnez **Ajouter** sous **ÉVÉNEMENTS**.

1. Définissez **Extension** sur `Adobe Client Data Layer`.

1. Définissez **Type d’événement** sur `Data Pushed`.

1. Sélectionnez **Événement spécifique** et définissez le **Événement/Clé pour lequel vous souhaitez vous enregistrer** sur `sign-out`.

1. Sélectionnez **Conserver les modifications** pour enregistrer la nouvelle règle.

1. Ajoutez une action .

1. Définissez **Extension** sur `Adobe Experience Platform Web SDK`.

1. Définissez **Type d’action** sur `Send Event`.

1. Définissez **Instance** sur `Alloy`.

1. Définissez **Type** sur `userAccount.logout`.

1. Définissez **données XDM** sur `%sign out%`.

1. Cliquez sur **Enregistrer**.

   Vous avez créé un élément de données dans votre schéma pour l’événement `signOut` à partir d’Adobe Commerce. En outre, vous avez créé une règle avec une action spécifique qui doit se produire lorsque cet événement est déclenché à partir du storefront Adobe Commerce.

Répétez les étapes ci-dessus dans les balises pour chacun des événements Adobe Commerce décrits ci-dessous.

## Événements disponibles

Pour chacun des événements suivants, mappez les événements Adobe Commerce à votre XDM en suivant les étapes ci-dessus.

- [`SignOut`](#signout)
- [`SignIn`](#signin)
- [`createAccount`](#createaccount)
- [`editAccount`](#editaccount)
- [`pageView`](#pageview)
- [`productView`](#productview)
- [`searchRequestSent`](#searchrequestsent)
- [`searchResponseReceived`](#searchresponsereceived)
- [`addToCart`](#addtocart)
- [« openCart »](#opencart)
- [`viewCart`](#viewcart)
- [`removeFromCart`](#removefromcart)
- [`initier le passage en caisse`](#initiatecheckout)
- [`placeOrder`](#placeorder)

### SignOut

Déclenché lorsqu’un acheteur tente de se déconnecter.

#### Éléments de données

Créez l’élément de données suivant :

1. Déconnectez-vous :

   - **Nom** : `Sign out`
   - **Extension** : `Adobe Experience Platform Web SDK`
   - **Type d’élément de données** : `XDM object`
   - **Groupe de champs** : `userAccount` > `logout`
   - **Déconnexion du visiteur** : **Valeur** = `1`

#### Règles 

- **Nom** : `Sign out`
- **Extension** : `Adobe Client Data Layer`
- **Type d’événement** : `Data Pushed`
- **Événement spécifique** : `sign-out`

##### Actions

- **Extension** : `Adobe Experience Platform Web SDK`
- **Type d’action** : `Send event`
- **Type** : `userAccount.logout`
- **Données XDM** : `%sign-out%`

### SignIn

Déclenché lorsqu’un acheteur tente de se connecter.

#### Éléments de données

Créez les éléments de données suivants :

1. Adresse e-mail du compte :

   - **Nom** : `account email`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `accountContext.emailAddress`

1. Type de compte :

   - **Nom** : `account type`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `accountContext.accountType`

1. ID de compte :

   - **Nom** : `account id`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès*** : `accountContext.accountId`

1. Se connecter :

   - **Nom** : `sign in`
   - **Extension** : `Adobe Experience Platform Web SDK`
   - **Type d’élément de données** : `XDM object`
   - **Groupe de champs** : `person` > `accountID`
   - **ID de compte** : **Valeur** = `%account id%`
   - **Groupe de champs** : `person` > `accountType`
   - **Type de compte** : **Valeur** = `%account type%`
   - **Groupe de champs** : `person` > `personalEmailID`
   - **Adresse E-Mail Personnelle** : **Valeur** = `%account email%`
   - **Groupe de champs** : `personalEmail` > `address`
   - **Address** : **Value** = `%account email%`
   - **Groupe de champs** : `userAccount` > `login`
   - **Connexion du visiteur** : **Valeur** = `1`

#### Règles 

- **Nom** : `sign in`
- **Extension** : `Adobe Client Data Layer`
- **Type d’événement** : `Data Pushed`
- **Événement spécifique** : `sign-in`

##### Actions

- **Extension** : `Adobe Experience Platform Web SDK`
- **Type d’action** : `Send event`
- **Type** : `userAccount.login`
- **Données XDM** : `%sign in%`

### createAccount

Déclenché lorsqu’un acheteur tente de créer un compte.

#### Éléments de données

Créez les éléments de données suivants :

1. Adresse e-mail du compte :

   - **Nom** : `account email`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `accountContext.emailAddress`

1. Type de compte :

   - **Nom** : `account type`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `accountContext.accountType`

1. ID de compte :

   - **Nom** : `account id`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `accountContext.accountId`

1. Créer un compte :

   - **Nom** : `Create account`
   - **Extension** : `Adobe Experience Platform Web SDK`
   - **Type d’élément de données** : `XDM object`
   - **Groupe de champs** : `person` > `accountID`
   - **ID de compte** : **Valeur** = `%account id%`
   - **Groupe de champs** : `person` > `accountType`
   - **Type de compte** : **Valeur** = `%account type%`
   - **Groupe de champs** : `person` > `personalEmailID`
   - **Adresse E-Mail Personnelle** : **Valeur** = `%account email%`
   - **Groupe de champs** : `personalEmail` > `address`
   - **Address** : **Value** = `%account email%`
   - **Groupe de champs** : `userAccount` > `createProfile`
   - **Création du profil de compte** : **Valeur** = `1`

#### Règles 

- **Nom** : `Create account`
- **Extension** : `Adobe Client Data Layer`
- **Type d’événement** : `Data Pushed`
- **Événement spécifique** : `create-account`

##### Actions

- **Extension** : `Adobe Experience Platform Web SDK`
- **Type d’action** : `Send event`
- **Type** : `userAccount.createProfile`
- **Données XDM** : `%create account%`

### editAccount

Déclenché lorsqu’un acheteur tente de modifier un compte.

#### Éléments de données

Créez les éléments de données suivants :

1. Adresse e-mail du compte :

   - **Nom** : `account email`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `accountContext.emailAddress`

1. Type de compte :

   - **Nom** : `account type`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `accountContext.accountType`

1. ID de compte :

   - **Nom** : `account id`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `accountContext.accountId`

1. Modifier le compte :

   - **Nom** : `Edit account`
   - **Extension** : `Adobe Experience Platform Web SDK`
   - **Type d’élément de données** : `XDM object`
   - **Groupe de champs** : `person` > `accountID`
   - **ID de compte** : **Valeur** = `%account id%`
   - **Groupe de champs** : `person` > `accountType`
   - **Type de compte** : **Valeur** = `%account type%`
   - **Groupe de champs** : `person` > `personalEmailID`
   - **Adresse E-Mail Personnelle** : **Valeur** = `%account email%`
   - **Groupe de champs** : `personalEmail` > `address`
   - **Address** : **Value** = `%account email%`
   - **Groupe de champs** : `userAccount` > `updateProfile`
   - **Création du profil de compte** : **Valeur** = `1`

#### Règles

- **Nom** : `Edit account`
- **Extension** : `Adobe Client Data Layer`
- **Type d’événement** : `Data Pushed`
- **Événement spécifique** : `edit-account`

##### Actions

- **Extension** : `Adobe Experience Platform Web SDK`
- **Type d’action** : `Send event`
- **Type** : `userAccount.updateProfile`
- **Données XDM** : `%edit account%`

### pageView

Déclenché lorsqu’une page se charge.

#### Éléments de données

Créez les éléments de données suivants :

1. Nom de la page :

   - **Nom** : `page name`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `pageContext.pageName`

#### Règles 

- **Nom** : `page view`
- **Extension** : `Adobe Client Data Layer`
- **Type d’événement** : `Data Pushed`
- **Événement spécifique** : `page-view`

##### Actions

- **Extension** : `Adobe Experience Platform Web SDK`
- **Type d’action** : `Send event`
- **Type** : `web.webPageDetails.pageViews`
- **Données XDM** : `%page view%`

### productView

Déclenché lorsqu’une page de produit se charge.

#### Éléments de données

Créez les éléments de données suivants :

1. Nom du produit :

   - **Nom** : `product name`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `productContext.name`

1. SKU du produit :

   - **Nom** : `product sku`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `productContext.sku`

1. URL de l’image du produit :

   - **Nom** : `product image`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `productContext.mainImageUrl`

1. Devise du produit :

   - **Nom** : `product currency`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `productContext.pricing.currencyCode`

1. Code de devise :

   - **Nom** : `currency code`
   - **Extension** : `Core`
   - **Type d’élément de données** : `Custom Code`
   - **Ouvrez l’éditeur** :

   ```bash
   return _satellite.getVar('product currency') || _satellite.getVar('storefront').storeViewCurrencyCode
   ```

1. Prix spécial :

   - **Nom** : `special price`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `productContext.pricing.specialPrice`

1. Tarif normal :

   - **Nom** : `regular price`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `productContext.pricing.regularPrice`

1. Prix du produit :

   - **Nom** : `product price`
   - **Extension** : `Core`
   - **Type d’élément de données** : `Custom Code`
   - **Ouvrez l’éditeur** :

   ```bash
   return _satellite.getVar('product regular price') || _satellite.getVar('product special price')
   ```

1. Vue du produit :

   - **Nom** : `product view`
   - **Extension** : `Adobe Experience Platform Web SDK`
   - **Type d’élément de données** : `XDM object`
   - **Groupe de champs** : `productListItems`. Sélectionnez **Fournir des éléments individuels** et cliquez sur le bouton **Ajouter un élément**. Cette vue étant destinée à un PDP, vous pouvez remplir avec un seul élément.
   - **Groupe de champs** : `productListItems` > `name`
   - **Name** : **Value** = `%product name%`
   - **Groupe de champs** : `productListItems` > `SKU`
   - **SKU** : **Valeur** = `%product sku%`
   - **Groupe de champs** : `productListItems` > `priceTotal`
   - **Prix total** : **Valeur** = `%product price%`
   - **Groupe de champs** : `productListItems` > `currencyCode`
   - **Code de devise** : **Valeur** = `%currency code%`
   - **Groupe de champs** : `productListItems` > `ProductImageUrl`
   - **ProductImageUrl**: **Value** = `%product image%`
   - **Groupe de champs** : `commerce` > `productViews` > `value`
   - **value** : **Value** = `1`

#### Règles 

- **Nom** : `product view`
- **Extension** : `Adobe Client Data Layer`
- **Type d’événement** : `Data Pushed`
- **Événement spécifique** : `product-page-view`

##### Actions

- **Extension** : `Adobe Experience Platform Web SDK`
- **Type d’action** : `Send event`
- **Type** : `commerce.productViews`
- **Données XDM** : `%product view%`

### searchRequestSent

Déclenché par des événements dans la fenêtre contextuelle « rechercher en cours de frappe » et par des événements sur les pages de résultats de recherche.

#### Éléments de données

Créez les éléments de données suivants :

1. Entrée de recherche

   - **Nom** : `search input`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `searchInputContext.units[0]`

1. Rechercher l’expression de saisie

   - **Nom** : `search input phrase`
   - **Extension** : `Core`
   - **Type d’élément de données** : `Custom Code`
   - **Ouvrez l’éditeur** :

   ```bash
   return _satellite.getVar('search input').phrase;
   ```

1. Tri des entrées de recherche

   - **Nom** : `search input sort`
   - **Extension** : `Core`
   - **Type d’élément de données** : `Custom Code`
   - **Ouvrez l’éditeur** :

   ```bash
   const searchInput = _satellite.getVar('search input');
   const sortFromInput = searchInput ? searchInput.sort : [];
   const sort = sortFromInput.map((searchSort) => {
       return {
           attribute: searchSort.attribute,
           order: searchSort.direction,
       };
   });
   return sort;
   ```

1. Rechercher des filtres d’entrée

   - **Nom** : `search input filters`
   - **Extension** : `Core`
   - **Type d’élément de données** : `Custom Code`
   - **Ouvrez l’éditeur** :

   ```bash
   const searchInput = _satellite.getVar('search input');
   const filtersFromInput = searchInput ? searchInput.filter : [];
   const filters = filtersFromInput.map(
       (searchFilter) => {
           let value = [];
           let isRange = false;
           if (searchFilter.eq) {
               value.push(searchFilter.eq);
           } else if (searchFilter.in) {
               value = searchFilter.in;
           } else if (searchFilter.range) {
               isRange = true;
               value.push(String(searchFilter.range.from));
               value.push(String(searchFilter.range.to));
           }
           return {
               attribute: searchFilter.attribute,
               value,
               isRange,
           };
       }
   );
   
   return filters;
   ```

1. Requête de recherche :

   - **Nom** : `search request`
   - **Extension** : `Adobe Experience Platform Web SDK`
   - **Type d’élément de données** : `XDM object`
   - **Groupe de champs** : `siteSearch` > `phrase`
   - **value** : pas encore disponible
   - **Groupe de champs** : `siteSearch` > `sort`. Sélectionnez **Fournir l’objet entier**.
   - **Groupe de champs** : `siteSearch` > `filter`. Sélectionnez **Fournir l’objet entier**.
   - **Groupe de champs** : `searchRequest` > `id`
   - **Identifiant unique** : **Valeur** = `%search request ID%`
   - **Groupe de champs** : `searchRequest` > `value`
   - **value** : **Value** = `1`

#### Règles 

- **Nom** : `search request sent`
- **Extension** : `Adobe Client Data Layer`
- **Type d’événement** : `Data Pushed`
- **Événement spécifique** : `search-request-sent`

##### Actions

- **Extension** : `Adobe Experience Platform Web SDK`
- **Type d’action** : `Send event`
- **Type** : `searchRequest`
- **Données XDM** : `%search request%`

### searchResponseReceived

Déclenché lorsque la recherche en direct renvoie des résultats pour la fenêtre contextuelle ou la page de résultats de recherche « en cours de saisie ».

#### Éléments de données

Créez les éléments de données suivants :

1. Résultats de la recherche :

   - **Nom** : `search results`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `searchResultsContext.units[0]`

1. Nombre de produits du résultat de recherche :

   - **Nom** : `search result number of products`
   - **Extension** : `Core`
   - **Type d’élément de données** : `Custom Code`
   - **Ouvrez l’éditeur** :

   ```bash
   return _satellite.getVar('search result').products.length;
   ```

1. Résultats de la recherche de produits :

   - **Nom** : `search result products`
   - **Extension** : `Core`
   - **Type d’élément de données** : `Custom Code`
   - **Ouvrez l’éditeur** :

   ```bash
   const searchResult = _satellite.getVar('search result');
   const productsFromResult = searchResult.products ? searchResult.products : [];
   const products = productsFromResult.map(
       (product) => {
           return { SKU: product.sku, name: product.name };
       }
   );
   return products;
   ```

1. Suggestions de résultats de recherche :

   - **Nom** : `search result products`
   - **Extension** : `Core`
   - **Type d’élément de données** : `Custom Code`
   - **Ouvrez l’éditeur** :

   ```bash
   const searchResult = _satellite.getVar('search result');
   const suggestionsFromResult = searchResult.suggestions ? searchResult.suggestions : [];
   const suggestions = suggestionsFromResult.map((suggestion) => suggestion.suggestion);
   return suggestions;
   ```

1. URL de l’image du produit :

   - **Nom** : `product image`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `productContext.mainImageUrl`

1. Réponse de recherche :

   - **Nom** : `search response`
   - **Extension** : `Adobe Experience Platform Web SDK`
   - **Type d’élément de données** : `XDM object`
   - **Groupe de champs** : `siteSearch` > `suggestions`. Sélectionnez **Fournir l’objet entier**.
   - **Élément de données** : `%search result suggestions%`
   - **Groupe de champs** : `siteSearch` > `numberOfResults`
   - **value** : `%search result number of products%`
   - **Groupe de champs** : `productListItems`. Sélectionnez **Fournir l’objet entier**.
   - **Groupe de champs** : `productListItems` > `ProductImageUrl`
   - **ProductImageUrl**: **Value** = `%product image%`
   - **Élément de données** : `%search result products%`
   - **Groupe de champs** : `searchResponse` > `id`
   - **Identifiant unique** : **Valeur** = `%search response ID%`
   - **Groupe de champs** : `searchResponse` > `value`
   - **value** : **Value** = `1`

#### Règles 

- **Nom** : `search response received`
- **Extension** : `Adobe Client Data Layer`
- **Type d’événement** : `Data Pushed`
- **Événement spécifique** : `search-response-received`

##### Actions

- **Extension** : `Adobe Experience Platform Web SDK`
- **Type d’action** : `Send event`
- **Type** : `searchResponse`
- **Données XDM** : `%search response%`

### addToCart

Déclenché lorsqu’un produit est ajouté à un panier ou chaque fois que la quantité d’un produit dans le panier est incrémentée.

#### Éléments de données

Créez les éléments de données suivants :

1. Nom du produit :

   - **Nom** : `product name`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `productContext.name`

1. SKU du produit :

   - **Nom** : `product sku`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `productContext.sku`

1. Code de devise :

   - **Nom** : `currency code`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `productContext.pricing.currencyCode`

1. Prix spécial du produit :

   - **Nom** : `product special price`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `productContext.pricing.specialPrice`

1. URL de l’image du produit :

   - **Nom** : `product image`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `productContext.mainImageUrl`

1. Prix normal du produit :

   - **Nom** : `product regular price`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `productContext.pricing.regularPrice`

1. Produit  prix :

   - **Nom** : `product price`
   - **Extension** : `Core`
   - **Type d’élément de données** : `Custom Code`
   - **Ouvrez l’éditeur** :

   ```bash
   return _satellite.getVar('product regular price') || _satellite.getVar('product special price') 
   ```

1. Panier :

   - **Nom** : `cart`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `shoppingCartContext`

1. ID de panier :

   - **Nom** : `cart id`
   - **Extension** : `Core`
   - **Type d’élément de données** : `Custom Code`
   - **Ouvrez l’éditeur** :

   ```bash
   return _satellite.getVar('cart').id
   ```

1. Ajouter au panier :

   - **Nom** : `add to cart`
   - **Extension** : `Adobe Experience Platform Web SDK`
   - **Type d’élément de données** : `XDM object`
   - **Groupe de champs** : `productListItems`. Sélectionnez **Fournir des éléments individuels** et cliquez sur le bouton **Ajouter un élément**. Cette vue étant destinée à un PDP, vous pouvez remplir avec un seul élément.
   - **Groupe de champs** : `productListItems` > `name`
   - **Name** : **Value** = `%product name%`
   - **Groupe de champs** : `productListItems` > `SKU`
   - **SKU** : **Valeur** = `%product sku%`
   - **Groupe de champs** : `productListItems` > `priceTotal`
   - **Prix total** : **Valeur** = `%product price%`
   - **Groupe de champs** : `productListItems` > `currencyCode`
   - **Groupe de champs** : `productListItems` > `ProductImageUrl`
   - **ProductImageUrl**: **Value** = `%product image%`
   - **Code de devise** : **Valeur** = `%currency code%`
   - **Groupe de champs** : `commerce` > `cart` > `cartID`
   - **ID du panier** : **Valeur** = `%cart id%`
   - **Groupe de champs** : `commerce` > `productListAdds` > `value`
   - **value** : **Value** = `1`

#### Règles 

- **Nom** : `add to cart`
- **Extension** : `Adobe Client Data Layer`
- **Type d’événement** : `Data Pushed`
- **Événement spécifique** : `add-to-cart`

##### Actions

- **Extension** : `Adobe Experience Platform Web SDK`
- **Type d’action** : `Send event`
- **Type** : `commerce.productListAdds`
- **Données XDM** : `%add to cart%`

### openCart

Déclenché lorsqu’un nouveau panier est créé, ce qui se produit lorsqu’un produit est ajouté à un panier vide.

#### Éléments de données

Créez l’élément de données suivant :

1. Ouvrir le panier :

   - **Nom** : `open cart`
   - **Extension** : `Adobe Experience Platform Web SDK`
   - **Type d’élément de données** : `XDM object`
   - **Groupe de champs** : `commerce` > `productListOpens` > `value`
   - **value** : **Value** = `1`
   - **Groupe de champs** : `commerce` > `cart` > `cartID`
   - **ID du panier** : **Valeur** = `%cart id%`
   - **Groupe de champs** : `productListItems`. Par `productListItems`, plusieurs éléments peuvent être précalculés. Sélectionnez **productListItems** > **Fournir un tableau entier**.

#### Règles 

- **Nom** : `open cart`
- **Extension** : `Adobe Client Data Layer`
- **Type d’événement** : `Data Pushed`
- **Événement spécifique** : `open-cart`

##### Actions

- **Extension** : `Adobe Experience Platform Web SDK`
- **Type d’action** : `Send event`
- **Type** : `commerce.productListOpens`
- **Données XDM** : `%open cart%`

### viewCart

Déclenché lorsqu’une page du panier se charge.

#### Éléments de données

Créez les éléments de données suivants :

1. Storefront :

   - **Nom** : `storefront`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `storefrontInstanceContext`

1. URL de l’image du produit :

   - **Nom** : `product image`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `productContext.mainImageUrl`

   1. Panier :

   - **Nom** : `cart`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `shoppingCartContext`

1. ID de panier :

   - **Nom** : `cart id`
   - **Extension** : `Core`
   - **Type d’élément de données** : `Custom Code`
   - **Ouvrez l’éditeur** :

   ```bash
   return _satellite.getVar('cart').id
   ```

1. Éléments de la liste de produits :

   - **Nom** : `product list items:`
   - **Extension** : `Core`
   - **Type d’élément de données** : `Custom Code`
   - **Ouvrez l’éditeur** :

   ```bash
   const storefrontContext = _satellite.getVar('storefront');
   const cart = _satellite.getVar('cart');
   
   const returnList = [];
   cart.items.forEach(item => {
       const selectedOptions = [];
       item.configurableOptions?.forEach(option => {
           selectedOptions.push({
               attribute: option.optionLabel,
               value: option.valueLabel,
           });
       });
   
       const productListItem = {
           SKU: item.product.sku,
           name: item.product.name,
           quantity: item.quantity,
           priceTotal: item.prices.price.value * item.quantity,
           currencyCode: item.prices.price.currency ? item.prices.price.currency : storefrontContext.storeViewCurrencyCode,
           selectedOptions: selectedOptions,
       };
   
       returnList.push(productListItem);
   });
   return returnList;
   ```

1. Afficher le panier :

   - **Nom** : `view cart`
   - **Extension** : `Adobe Experience Platform Web SDK`
   - **Type d’élément de données** : `XDM object`
   - **Groupe de champs** : `productListItems`. Par `productListItems`, plusieurs éléments peuvent être précalculés. Sélectionnez **productListItems** > **Remplir le tableau entier**.
   - **Élément de données** : `%product list items%`
   - **Groupe de champs** : `productListItems` > `ProductImageUrl`
   - **ProductImageUrl**: **Value** = `%product image%`
   - **Groupe de champs** : `commerce` > `cart` > `cartID`
   - **ID du panier** : **Valeur** = `%cart id%`
   - **Groupe de champs** : `commerce` > `productListViews` > `value`
   - **value** : **Value** = `1`

#### Règles

- **Nom** : `view cart`
- **Extension** : `Adobe Client Data Layer`
- **Type d’événement** : `Data Pushed`
- **Événement spécifique** : `shopping-cart-view`

##### Actions

- **Extension** : `Adobe Experience Platform Web SDK`
- **Type d’action** : `Send event`
- **Type** : `commerce.productListViews`
- **Données XDM** : `%view cart%`

### removeFromCart

Déclenché lorsqu’un produit est retiré d’un panier ou chaque fois que la quantité d’un produit dans le panier est diminuée.

#### Éléments de données

Créez les éléments de données suivants :

1. Nom du produit :

   - **Nom** : `product name`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `productContext.name`

1. SKU du produit :

   - **Nom** : `product sku`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `productContext.sku`

1. Code de devise :

   - **Nom** : `currency code`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `productContext.pricing.currencyCode`

1. Prix spécial du produit :

   - **Nom** : `product special price`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `productContext.pricing.specialPrice`

1. Prix normal du produit :

   - **Nom** : `product regular price`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `productContext.pricing.regularPrice`

1. Produit  prix :

   - **Nom** : `product price`
   - **Extension** : `Core`
   - **Type d’élément de données** : `Custom Code`
   - **Ouvrez l’éditeur** :

   ```bash
   return _satellite.getVar('product regular price') || _satellite.getVar('product special price') 
   ```

1. Panier :

   - **Nom** : `cart`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `shoppingCartContext`

1. ID de panier :

   - **Nom** : `cart id`
   - **Extension** : `Core`
   - **Type d’élément de données** : `Custom Code`
   - **Ouvrez l’éditeur** :

   ```bash
   return _satellite.getVar('cart').id
   ```

1. Supprimer du panier :

   - **Nom** : `remove from cart`
   - **Extension** : `Adobe Experience Platform Web SDK`
   - **Type d’élément de données** : `XDM object`
   - **Groupe de champs** : `productListItems`. Sélectionnez **Fournir des éléments individuels** et cliquez sur le bouton **Ajouter un élément**. Cette vue étant destinée à un PDP, vous pouvez remplir avec un seul élément.
   - **Groupe de champs** : `productListItems` > `name`
   - **Name** : **Value** = `%product name%`
   - **Groupe de champs** : `productListItems` > `SKU`
   - **SKU** : **Valeur** = `%product sku%`
   - **Groupe de champs** : `productListItems` > `priceTotal`
   - **Prix total** : **Valeur** = `%product price%`
   - **Groupe de champs** : `productListItems` > `currencyCode`
   - **Code de devise** : **Valeur** = `%currency code%`
   - **Groupe de champs** : `commerce` > `cart` > `cartID`
   - **ID du panier** : **Valeur** = `%cart id%`
   - **Groupe de champs** : `commerce` > `productListRemovals` > `value`
   - **value** : **Value** = `1`

#### Règles 

- **Nom** : `remove from cart`
- **Extension** : `Adobe Client Data Layer`
- **Type d’événement** : `Data Pushed`
- **Événement spécifique** : `remove-from-cart`

##### Actions

- **Extension** : `Adobe Experience Platform Web SDK`
- **Type d’action** : `Send event`
- **Type** : `commerce.productListRemovals`
- **Données XDM** : `%remove from cart%`

### submitCheckout

Déclenché lorsque l’acheteur clique sur un bouton de passage en caisse.

#### Éléments de données

Créez les éléments de données suivants :

1. Storefront :

   - **Nom** : `storefront`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `storefrontInstanceContext`

1. URL de l’image du produit :

   - **Nom** : `product image`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `productContext.mainImageUrl`

1. Panier :

   - **Nom** : `cart`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `shoppingCartContext`

1. ID de panier :

   - **Nom** : `cart id`
   - **Extension** : `Core`
   - **Type d’élément de données** : `Custom Code`
   - **Ouvrez l’éditeur** :

   ```bash
   return _satellite.getVar('cart').id
   ```

1. Éléments de la liste de produits :

   - **Nom** : `product list items`
   - **Extension** : `Core`
   - **Type d’élément de données** : `Custom Code`
   - **Ouvrez l’éditeur** :

   ```bash
   const storefrontContext = _satellite.getVar('storefront');
   const cart = _satellite.getVar('cart');
   
   const returnList = [];
   cart.items.forEach(item => {
       const selectedOptions = [];
       item.configurableOptions?.forEach(option => {
           selectedOptions.push({
               attribute: option.optionLabel,
               value: option.valueLabel,
           });
       });
   
       const productListItem = {
           SKU: item.product.sku,
           name: item.product.name,
           quantity: item.quantity,
           priceTotal: item.prices.price.value * item.quantity,
           currencyCode: item.prices.price.currency ? item.prices.price.currency : storefrontContext.storeViewCurrencyCode,
           selectedOptions: selectedOptions,
       };
   
       returnList.push(productListItem);
   });
   return returnList;
   ```

1. Lancer le passage en caisse :

   - **Nom** : `initiate checkout`
   - **Extension** : `Adobe Experience Platform Web SDK`
   - **Type d’élément de données** : `XDM object`
   - **Groupe de champs** : `productListItems`. Par `productListItems`, plusieurs éléments peuvent être précalculés. Sélectionnez **productListItems** > **Remplir le tableau entier**.
   - **Élément de données** : `%product list items%`
   - **Groupe de champs** : `productListItems` > `ProductImageUrl`
   - **ProductImageUrl**: **Value** = `%product image%`
   - **Groupe de champs** : `commerce` > `cart` > `cartID`
   - **ID du panier** : **Valeur** = `%cart id%`
   - **Groupe de champs** : `commerce` > `checkouts` > `value`
   - **value** : **Value** = `1`

#### Règles 

- **Nom** : `initiate checkout`
- **Extension** : `Adobe Client Data Layer`
- **Type d’événement** : `Data Pushed`
- **Événement spécifique** : `initiate-checkout`

##### Actions

- **Extension** : `Adobe Experience Platform Web SDK`
- **Type d’action** : `Send event`
- **Type** : `commerce.checkouts`
- **Données XDM** : `%initiate checkout%`

### placeOrder

Déclenché lorsque l’acheteur passe une commande.

#### Éléments de données

Créez les éléments de données suivants :

1. Adresse e-mail du compte :

   - **Nom** : `account email`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `accountContext.emailAddress`

1. Storefront :

   - **Nom** : `storefront`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `storefrontInstanceContext`

1. URL de l’image du produit :

   - **Nom** : `product image`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `productContext.mainImageUrl`

1. Panier :

   - **Nom** : `cart`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `shoppingCartContext`

1. ID de panier :

   - **Nom** : `cart id`
   - **Extension** : `Core`
   - **Type d’élément de données** : `Custom Code`
   - **Ouvrez l’éditeur** :

   ```bash
   return _satellite.getVar('cart').id
   ```

1. Commande :

   - **Nom** : `order`
   - **Extension** : `Adobe Client Data Layer`
   - **Type d’élément de données** : `Data Layer Computed State`
   - **[Facultatif] chemin d’accès** : `orderContext`

1. Commande Commerce :

   - **Nom** : `commerce order`
   - **Extension** : `Core`
   - **Type d’élément de données** : `Custom Code`
   - **Ouvrez l’éditeur** :

   ```bash
   const order = _satellite.getVar('order');
   const storefront = _satellite.getVar('storefront');
   
   if (order.payments && order.payments.length) {
       payments = order.payments.map(payment => {
           return {
               paymentAmount: payment.total,
               paymentType: payment.paymentMethodCode,
               transactionID: order.orderId.toString(),
           };
       });
   } else {
       payments = [
           {
               paymentAmount: order.grandTotal,
               paymentType: order.paymentMethodCode,
               transactionID: order.orderId.toString(),
           },
       ];
   }
   
   return {
       purchaseID: order.orderId.toString(),
       currencyCode: storefront.storeViewCurrencyCode,
       payments,
   };
   ```

1. Commander l&#39;expédition :

   - **Nom** : `order shipping`
   - **Extension** : `Core`
   - **Type d’élément de données** : `Custom Code`
   - **Ouvrez l’éditeur** :

   ```bash
   const order = _satellite.getVar('order');
   return {
       shippingMethod: order.shipping.shippingMethod,
       shippingAmount: order.shipping.shippingAmount || 0,
   }
   ```

1. ID de promotion :

   - **Nom** : `promotion id`
   - **Extension** : `Core`
   - **Type d’élément de données** : `Custom Code`
   - **Ouvrez l’éditeur** :

   ```bash
   return _satellite.getVar('order').appliedCouponCode
   ```

1. Éléments de la liste de produits :

   - **Nom** : `product list items`
   - **Extension** : `Core`
   - **Type d’élément de données** : `Custom Code`
   - **Ouvrez l’éditeur** :

   ```bash
   const storefrontContext = _satellite.getVar('storefront');
   const cart = _satellite.getVar('cart');
   
   const returnList = [];
   cart.items.forEach(item => {
       const selectedOptions = [];
       item.configurableOptions?.forEach(option => {
           selectedOptions.push({
               attribute: option.optionLabel,
               value: option.valueLabel,
           });
       });
   
       const productListItem = {
           SKU: item.product.sku,
           name: item.product.name,
           quantity: item.quantity,
           priceTotal: item.prices.price.value * item.quantity,
           currencyCode: item.prices.price.currency ? item.prices.price.currency : storefrontContext.storeViewCurrencyCode,
           selectedOptions: selectedOptions,
       };
   
       returnList.push(productListItem);
   });
   return returnList;
   ```

1. Passer une commande :

   - **Nom** : `place order`
   - **Extension** : `Adobe Experience Platform Web SDK`
   - **Type d’élément de données** : `XDM object`
   - **Groupe de champs** : `productListItems`. Par `productListItems`, plusieurs éléments peuvent être précalculés. Sélectionnez **productListItems** > **Remplir le tableau entier**.
   - **Élément de données** : `%product list items%`
   - **Groupe de champs** : `productListItems` > `ProductImageUrl`
   - **ProductImageUrl**: **Value** = `%product image%`
   - **Groupe de champs** : `commerce` > `order`
   - **Identifiant unique** : **Valeur** = `%commerce order%`
   - **Groupe de champs** : `commerce` > `shipping`
   - **Identifiant unique** : **Valeur** = `%order shipping%`
   - **Groupe de champs** : `commerce` > `promotionID`
   - **ID de promotion** : **Valeur** = `%promotion id%`
   - **Groupe de champs** : `commerce` > `purchases` > `value`
   - **value** : **Value** = `1`
   - **Adresse E-Mail Personnelle** : **Valeur** = `%account email%`
   - **Groupe de champs** : `personalEmail` > `address`
   - **Address** : **Value** = `%account email%`

#### Règles 

- **Nom** : `place order`
- **Extension** : `Adobe Client Data Layer`
- **Type d’événement** : `Data Pushed`
- **Événement spécifique** : `place-order`

##### Actions

- **Extension** : `Adobe Experience Platform Web SDK`
- **Type d’action** : `Send event`
- **Type** : `commerce.order`
- **Données XDM** : `%place order%`

## Définition de l’identité dans les événements storefront

Les événements de storefront contiennent des informations de profil basées sur les champs `personalEmail` (pour les événements de compte) et `identityMap` (pour tous les autres événements de storefront). L’extension [!DNL Data Connection] joint et génère des profils en fonction de ces deux champs. Cependant, chaque champ comporte différentes étapes à suivre pour créer des profils :

>[!NOTE]
>
>Si vous disposez d’une configuration précédente qui repose sur différents champs, vous pouvez continuer à les utiliser.

- `personalEmail` - S’applique uniquement aux événements de compte. Suivez les étapes, règles et actions décrites [ci-dessus](#createaccount)
- `identityMap` - S’applique à tous les autres événements du storefront. Voir l’exemple suivant.

### Exemple

Les étapes suivantes indiquent comment configurer un événement `pageView` avec `identityMap` dans [!DNL Data Connection] extension :

1. Configurez l’élément de données avec le code personnalisé pour ECID :

   ![Configurer l’élément de données avec le code personnalisé](assets/set-custom-code-ecid.png)
   _Configurer l’élément de données avec le code personnalisé_

1. Sélectionnez [!UICONTROL Open Editor] et ajoutez le code personnalisé suivant :

   ```javascript
   return alloy("getIdentity").then((result) => {
       var identityMap = {
           ECID: [
           {
               id: ecid,
               primary: true
           }
           ],
           email: [
           {
               id: email,
               primary: false
           }
           ]
       };
     _satelite.setVar("identityMap", identityMap);
   });
   ```

1. Mettez à jour le schéma XDM avec `identityMap` défini comme ECID :

   ![Définir identityMap comme ECID](assets/identity-map-data-element.png)
   _Définir identityMap comme ECID_

1. Définissez des actions de règle qui récupèrent l’ECID :

   ![Récupérer ECID](assets/rule-retrieve-ecid.png)
   _Récupérer ECID_

## Définir l’identité dans les événements back-office

Contrairement aux événements storefront qui utilisent l’ECID pour identifier et lier les informations de profil, les données d’événement back-office sont basées sur SaaS et aucun ECID n’est donc disponible. Pour les événements back office, vous devez utiliser les e-mails pour identifier de manière unique les acheteurs. Dans cette section, vous apprendrez à lier les données d’événement back-office à un ECID à l’aide d’un e-mail.

1. Créez un élément de mappage d’identités.

   ![Mappage d’identité back-office](assets/custom-code-backoffice.png)
   _Créer un mappage d’identités back-office_

1. Sélectionnez [!UICONTROL Open Editor] et ajoutez le code personnalisé suivant :

```javascript
const IdentityMap = {
  "ECID": [
    {
      id:  _satellite.getVar('ECID'),
      primary: true,
    },
  ],
};
 
if (_satellite.getVar('account email')) {
    IdentityMap.email = [
        {
            id: _satellite.getVar('account email'),
            primary: false,
        },
    ];
}
return IdentityMap;
```

1. Ajoutez ce nouvel élément à chaque champ `identityMap`.

   ![Mettre à jour chaque identityMap](assets/add-element-back-office.png)
   _Mettre à jour chaque identityMap_

## Définition du consentement

Lorsque vous installez l’extension [!DNL Data Connection] dans Adobe Commerce, le consentement de la collecte de données est activé par défaut. Le droit d’opposition est géré par le biais du cookie [`mg_dnt`. &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html?lang=fr) Vous pouvez suivre les étapes décrites ici si vous choisissez d’utiliser `mg_dnt` pour gérer le consentement. La documentation de Adobe Experience Platform Web SDK [&#128279;](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?lang=fr) propose plusieurs options supplémentaires pour gérer le consentement.

1. Créez un élément de données **Code personnalisé principal** (`%do not track cookie%`) pour le cookie `mg_dnt` :

   ![Créer l’élément de données ne pas suivre](assets/element-dnt-cookie.png)
   _Créer l’élément de données ne pas suivre_

1. Créez un élément de données **Code personnalisé de base** (`%consent%`) qui renvoie des `out` si le cookie est défini et `in` dans le cas contraire :

   ![Créer un élément de données de consentement](assets/element-consent-dnt-cookie.png)
   _Créer un élément de données de consentement_

1. Configurez l’extension Adobe Experience Platform Web SDK avec `%consent%` élément de données :

   ![Mettre à jour SDK avec le consentement](assets/config-sdk-consent.png)
   _Mettre à jour SDK avec le consentement_

## Avertissements

- Si vous ne suivez pas les étapes pour désactiver la collecte Experience Platform, les événements sont comptabilisés deux fois
- Le fait de ne pas configurer de mappages/événements comme décrit dans cette rubrique peut affecter les tableaux Adobe Analytics
- Vous ne pouvez pas configurer Target avec l’extension [!DNL Data Connection] si la collecte de données est désactivée
