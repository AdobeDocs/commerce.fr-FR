---
title: Configurer votre storefront
description: 'Découvrez comment configurer votre storefront [!DNL Adobe Commerce Optimizer] '
role: Developer
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et  [!DNL Adobe Commerce Optimizer]  (infrastructure SaaS gérée par Adobe)."
exl-id: 2b4c9e98-a30c-4a33-b356-556de5bd721a
source-git-commit: 0cd9749574460374a8fe875f1eff54f2a4a8d614
workflow-type: tm+mt
source-wordcount: '1397'
ht-degree: 0%

---

# Configurer votre storefront

Ce guide vous guide tout au long de la configuration d’un storefront pour votre instance [!DNL Adobe Commerce Optimizer] à l’aide d’Adobe Edge Delivery Services. Votre storefront comprend du code standard, un exemple de contenu et une assistance pour les pages de détails du produit et la découverte de produits (recherche et filtrage).

**Délai d’exécution estimé :** entre 30 et 45 minutes

## Conditions préalables

* **Compte GitHub** qui peut créer des référentiels et qui est configuré pour le développement local (github.com).
* **[!DNL Adobe Commerce Optimizer]instance** avec des exemples de données et des vues de catalogue et des politiques configurées
   * Voir [Ajouter des données d’exemple](get-started.md#add-sample-data) pour obtenir des instructions de configuration.

### Données d’instance requises

Avant de commencer, collectez les informations suivantes à partir de votre instance [!DNL Adobe Commerce Optimizer] :

* **Identifiant client** (également appelé identifiant d’instance)
   * Disponible à partir de la page [Détails de l’instance](get-started.md#manage-instances)
* **point d’entrée GraphQL** pour votre instance
   * Disponible à partir de la page [Détails de l’instance](get-started.md#manage-instances)
* **Identifiant de la vue Catalogue** pour la vue Catalogue globale
   * Disponible à partir de la page [Détails du catalogue](./setup/catalog-view.md#manage-catalog-view)
* **Paramètres régionaux Source** pour la vue de votre catalogue
   * La valeur par défaut pour les données d’exemple est `en-US`

>[!NOTE]
>
>Les clients disposant d’un accès d’évaluation peuvent trouver le point d’entrée GraphQL dans l’e-mail de bienvenue reçu lors de la création de votre instance. Les instances d’évaluation sont préconfigurées avec des exemples de données, des vues de catalogue et des politiques.

## Étapes de configuration

1. **[Créer votre projet de storefront](#create-your-storefront-project)**-Utilisez l’outil [Créateur de site](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator) pour créer un projet de storefront avec un code standard, un exemple de contenu et un fichier de configuration.

1. **[Personnaliser la configuration storefront](#customize-the-storefront-configuration)**-Mettez à jour le fichier `config.json` dans votre référentiel pour vous connecter à votre instance [!DNL Adobe Commerce Optimizer].

1. **[Vérification de la configuration](#verify-your-setup)** (10 minutes)
   * Prévisualiser votre site storefront
   * Tester les pages de détails du produit et la fonctionnalité de recherche

## Créer votre projet storefront

L’outil Créateur de site crée un projet de storefront complet avec les composants suivants :

* **Site** : page de destination de storefront avec du contenu standard
* **Code** : référentiel contenant des fichiers sources standard.
* **Contenu** : environnement de création de documents avec des fichiers de contenu de site.
* **Configuration Commerce** : fichier `config.json` pour une configuration spécifique à l&#39;instance

### Étape 1 : générer votre projet

1. Ouvrez l’outil [Créateur de site](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator)

   ![[!DNL Site Creator tool]](./assets/storefront-setup-site-creator.png){width="700" zoomable="yes"}

1. Sélectionnez **Créer un site (code et contenu)**.

1. Effectuez la configuration du site :

   * **Organisation/nom d’utilisateur GitHub** : saisissez votre nom d’utilisateur ou d’organisation GitHub
   * **Nom du site** : choisissez un nom explicite pour votre storefront
   * **Point d’entrée Commerce GraphQL (facultatif)** : saisissez le point d’entrée GraphQL de votre instance [!DNL Adobe Commerce Optimizer]

1. Cliquez sur **Créer un site** pour créer le référentiel GitHub avec le code standard du storefront.

   Lorsque le référentiel est créé, le créateur du site se met à jour et vous invite à installer l’application de synchronisation du code.

### Étape 2 : installer l’application de synchronisation du code

1. Cliquez sur **[!UICONTROL Install AEM Code Sync App]** pour ouvrir le programme d’installation de la synchronisation du code dans un nouvel onglet.

1. Configurez l’application de synchronisation du code :
   * Sélectionnez votre organisation GitHub, puis cliquez sur **[!UICONTROL Configure]**.
   * Dans l’interface de synchronisation du code, cliquez sur **[!UICONTROL Only select repositories]**.
   * Cliquez sur le menu **[!UICONTROL Select repositories]**, puis choisissez le référentiel de code storefront que vous avez créé.
   * Cliquez sur **[!UICONTROL Save]** pour enregistrer votre référentiel.

1. Revenez à la fenêtre du navigateur dans laquelle le créateur du site est ouvert, puis cliquez sur **Créer un site**.

   Le créateur du site copie le contenu standard du storefront dans l’environnement de création de documents. Ce processus prend entre 1 et 2 minutes.

### Étape 3 : enregistrer les liens de votre projet

1. Dans la section Détails du site , passez en revue les liens de votre projet de storefront :

   ![[!DNL Storefront setup complete]](./assets/storefront-setup-complete.png){width="700" zoomable="yes"}

   Utilisez ces liens pour gérer le code, le contenu et la configuration de votre storefront.

1. Copiez et enregistrez ces liens pour référence ultérieure : cliquez sur **[!UICONTROL Copy].

## Configuration de votre storefront

Mettez à jour la configuration de storefront pour vous connecter à votre instance [!DNL Adobe Commerce Optimizer].

1. Ouvrez le fichier `config.json` dans votre référentiel de code standard.

   `https://github.com/<username or org>/<repo name>/config.json`

1. Recherchez la section `cs` (Catalog Service) dans la configuration.

1. Remplacez les valeurs d’espace réservé par les valeurs de votre instance. Voir [Conditions préalables](#prerequisites).

   ```json
   "cs": {
      "AC-View-ID": "{catalogViewId}",
      "AC-Source-Locale": "en-US",
      "AC-Price-Book-ID": "{priceBookId}"
   }
   ```

   >[!NOTE]
   >
   >Pour trouver l&#39;ID du catalogue des prix, vérifiez les [détails de configuration de la vue de catalogue](./setup/catalog-view.md) dans Adobe Commerce Optimizer pour afficher les catalogues des prix attribués. Si aucun catalogue des prix n’est affecté, vous pouvez supprimer cet en-tête du fichier de configuration. Ajoutez-le à nouveau lorsqu&#39;un catalogue a été affecté à la vue Catalogue.

1. Enregistrez le fichier de configuration.

   La propagation des modifications de configuration peut prendre quelques minutes. Si vous ne voyez pas immédiatement les données, attendez 2 à 3 minutes avant de procéder au dépannage.

## Vérification de la configuration

Testez votre storefront pour vous assurer qu’il est correctement connecté à votre instance [!DNL Adobe Commerce Optimizer].

### Étape 1 : afficher votre page d’accueil storefront

1. Accédez à votre URL d’aperçu en direct :

   `https://main--{SITE}--{ORG}.aem.live`

   Remplacez `{ORG}` et `{SITE}` par le nom de votre organisation et de votre site GitHub.

1. **Critères de réussite** : vous devriez voir la page d’accueil du storefront avec du contenu standard.

   ![[!DNL ACO storefront site with boilerplate]](./assets/aco-storefront-site-boilerplate.png){width="700" zoomable="yes"}

### Étape 2 : test des pages de détails du produit

Affichez la page des détails du produit par défaut pour vérifier que les données du produit se chargent correctement.

1. Accédez à un exemple de page de produit :
   `https://main--{SITE}--{ORG}.aem.live/products/placeholder/{sku}`

   Utilisez n’importe quel SKU de vos données d’exemple, par exemple :
   `https://main--{SITE}--{ORG}.aem.live/products/placeholder/aur-flu-tir-std-2017`

   Pour le storefront par défaut, vous pouvez utiliser la valeur `placeholder` dans l’itinéraire pour afficher le produit. Lorsque vous commencez à personnaliser votre storefront, vous pouvez personnaliser le code de storefront pour définir le chemin d’accès à la page des détails du produit en fonction des itinéraires de produit définis dans votre catalogue.

   >[!TIP]
   >
   >Affichez les SKU disponibles à partir de la page [Synchronisation des données](./setup/data-sync.md) dans votre instance [!DNL Adobe Commerce Optimizer].

1. **Critères de réussite** : la page doit afficher :
   * Nom, description et prix du produit
   * Images du produit
   * Fonctionnalité Ajouter au panier
   * Données extraites de votre instance [!DNL Adobe Commerce Optimizer]

   ![[!DNL Default product detail page showing a product from the sample data]](./assets/storefront-boilerplate-product-page.png){width="700" zoomable="yes"}

### Étape 3 : tester la fonctionnalité de recherche par défaut

Testez les fonctionnalités du produit par défaut, notamment la recherche et le filtrage.

1. Sur la page d’accueil du storefront, cliquez sur l’icône de loupe dans l’en-tête.

1. Saisissez la chaîne de recherche `tires` et appuyez sur **Entrée**.

1. **Critères de réussite** : vous devriez voir :
   * Page de résultats de recherche avec produits pneumatiques
   * Options de filtrage dans la barre latérale
   * Listes de produits avec images et prix

   ![[!DNL View search results page]](./assets/storefront-with-aco-search-results-page.png){width="675" zoomable="yes"}

1. Cliquez sur n&#39;importe quel produit de pneu pour voir sa page détaillée.

   ![[!DNL View product details page]](./assets/storefront-with-aco-pdp-page.png){width="675" zoomable="yes"}

## Dépannage

Si vous rencontrez des problèmes lors de la configuration, utilisez la console Inspecteur de page web pour rechercher des erreurs. Essayez également d’effacer le cache de votre navigateur ou utilisez un autre navigateur.

Suivez les conseils suivants pour vérifier les problèmes courants :

### Problèmes courants

| Problème | Symptômes | Solution |
|-------|----------|----------|
| **Échec de l’installation de la synchronisation du code** | Impossible de terminer la configuration de la synchronisation du code | <ul><li>Vérifiez que vous disposez d’un accès administrateur à votre organisation GitHub.</li><li>Essayez d’utiliser un référentiel personnel au lieu d’une organisation.</li><li>Vérifiez les autorisations GitHub et réessayez.</li></ul> |
| **Site non chargé** | Erreurs 404 ou de connexion | <ul><li>Vérifiez le format de l’URL de votre site : `https://main--{SITE}--{ORG}.aem.live`</li><li>Vérifiez que l’application de synchronisation du code est correctement installée.</li><li>Assurez-vous que le référentiel est public ou correctement configuré.</li></ul> |
| **Aucune donnée de produit affichée** | Les pages de produits affichent des espaces réservés ou des erreurs | <ul><li>Vérifiez vos valeurs de configuration dans `config.json`</li><li>Dans l’instance [!DNL Adobe Commerce Optimizer], vérifiez la page Synchronisation des données pour vous assurer que les exemples de produits sont chargés. Si aucun produit n’est disponible, rechargez les données d’exemple ou ajoutez un produit à l’aide de l’[API Data Ingestion](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/using-the-api/#make-your-first-request). Patientez quelques minutes pour que les modifications de configuration se propagent.</li><li>Essayez de récupérer les détails du produit à l’aide de la requête [products](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/use-cases/#return-product-details) du service de marchandisage en utilisant les mêmes en-têtes que ceux configurés dans le fichier `config.json`. Si vous pouvez récupérer les données, il s’agit probablement d’un problème lié à la configuration de la vue de catalogue ou d’une erreur d’index.</li></ul> |
| **La recherche ne renvoie aucun résultat** | Page de résultats de recherche vide | <ul><li>Vérifiez que vous pouvez récupérer les résultats de la recherche de produit à l’aide des services de marchandisage [requête productSearch](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/use-cases/#product-search) en utilisant les mêmes en-têtes configurés dans le fichier `config.json`. Si vous pouvez récupérer les données, il s’agit probablement d’un problème lié à la configuration de la vue de catalogue ou d’une erreur d’index.</li><li>Vérifiez que l’ID de vue de catalogue dans le fichier `config.json` correspond à l’ID de vue de catalogue dans [!DNL Adobe Commerce Optimizer].</li><li>Dans Adobe Commerce Optimizer, vérifiez la configuration des politiques, des paramètres régionaux et des tarifs que vous avez utilisés dans la configuration de l’en-tête du storefront.</li><li>Vérifiez que les [paramètres de métadonnées d’attribut](https://developer.adobe.com/commerce/services/reference/rest/#operation/createProductMetadata) sont correctement définis pour la recherche.</li></ul> |

### Liste de contrôle de validation

Avant de passer aux étapes suivantes, vérifiez que votre storefront fonctionne correctement en vérifiant les éléments suivants :

![Liste de contrôle](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) Les valeurs de configuration correspondent aux paramètres de votre instance<br>
![Liste de contrôle](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) la page d’accueil de Storefront se charge sans erreur<br>
![&#x200B; Liste de contrôle &#x200B;](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) au moins une page de détails du produit affiche des informations complètes<br>
![Liste de contrôle](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) la fonctionnalité de recherche renvoie des résultats pertinents<br>
![Liste de contrôle](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) Les images du produit se chargent correctement<br>
![Liste de contrôle](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) Les valeurs de configuration correspondent aux paramètres de votre instance<br>

### Obtenir de l’aide

Si les problèmes persistent :

* Consultez la [documentation du storefront Adobe Commerce](https://experienceleague.adobe.com/developer/commerce/storefront/)
* Consultez le guide du développeur de Adobe Commerce Optimizer [&#128279;](https://developer.adobe.com/commerce/services/optimizer/)
* Consultez les [ressources d’assistance Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/overview)

## Étapes suivantes

Après avoir configuré et vérifié votre storefront, vous pouvez :

1. **[Installez Sidekick](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/#install-and-configure-sidekick)**-Extension de navigateur pour modifier, prévisualiser et publier du contenu directement à partir de votre site web.

2. **[Configurer un environnement de développement local](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/#set-up-local-environment)**—Créez un environnement local pour personnaliser le code et le contenu de votre storefront.

### Apprendre et explorer

* **[Complétez le cas d&#39;utilisation complet](./use-case/admin-use-case.md)**—En savoir plus sur la configuration de storefront et la gestion des catalogues à l&#39;aide de [!DNL Adobe Commerce Optimizer].

* **[Explorer la personnalisation du storefront](https://experienceleague.adobe.com/developer/commerce/storefront/setup/)**—Découvrez les options de configuration et de configuration avancées.

* **[Utilisez les listes déroulantes Commerce pour personnaliser l’expérience storefront](https://experienceleague.adobe.com/developer/commerce/storefront/dropins/all/introduction/)**-ajoutez des composants préconfigurés pour améliorer votre expérience storefront.

* **Migrer vers le service de configuration de storefront** : après avoir créé votre storefront initial, vous pouvez migrer la configuration pour utiliser le service de configuration qui prend en charge les cas d’utilisation avancés tels que la configuration et les recouvrements sans réponse. Pour plus d’informations, consultez la documentation du [Service de configuration](https://www.aem.live/docs/config-service-setup) dans le Adobe Experience Manager.

>[!MORELIKETHIS]
>
> Consultez la [documentation du storefront Adobe Commerce](https://experienceleague.adobe.com/developer/commerce/storefront/) pour en savoir plus sur la mise à jour du contenu du site et l’intégration aux composants frontend Commerce et aux données principales.
