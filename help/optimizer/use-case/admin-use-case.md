---
title: Cas d’utilisation de Carvelo
description: Découvrez comment utiliser  [!DNL Adobe Commerce Optimizer]  gérer votre catalogue à l’aide de canaux et de politiques, et comment configurer votre storefront en fonction de la configuration de votre catalogue.
hide: true
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: d716dd9d75beb642bfad30271b6ecd3490ee7328
workflow-type: tm+mt
source-wordcount: '1656'
ht-degree: 0%

---

# Cas d’utilisation de Carvelo

>[!NOTE]
>
>Cette documentation décrit un produit en développement à accès anticipé et ne reflète pas toutes les fonctionnalités destinées à une disponibilité générale.

Le cas d’utilisation suivant montre comment utiliser [!DNL Adobe Commerce Optimizer] pour organiser votre catalogue afin de correspondre aux opérations de vente au détail à l’aide d’un seul catalogue de base. Il explique également comment configurer un storefront optimisé par Edge Delivery Services.

## Prérequis

Avant de passer en revue ce cas d’utilisation, assurez-vous d’avoir [configuré votre storefront](../storefront.md).

## Commençons

Dans ce cas d’utilisation, vous utiliserez les éléments suivants :

1. Interface utilisateur de [!DNL Adobe Commerce Optimizer] - Configurez les canaux et les politiques requis pour gérer la configuration opérationnelle complexe du catalogue.

1. Commerce Storefront : effectuez le rendu du storefront avec les données de catalogue configurées dans [!DNL Adobe Commerce Optimizer]’interface utilisateur et les fichiers de configuration, `fstab.yaml` et `config.json` du storefront Commerce.

### ‌Principaux points à retenir

À la fin de cet article, vous pourrez :

- Découvrez les principes de base de [!DNL Adobe Commerce Optimizer] avec son modèle de données de catalogue unique, performant et évolutif.
- Découvrez comment le modèle de données de catalogue s’intègre de manière transparente aux composants storefront indépendants de la plateforme créés par Adobe.
- Découvrez comment utiliser les canaux et politiques Adobe Commerce Optimizer pour créer des vues de catalogue et des filtres d’accès aux données personnalisés, et envoyer les données à un storefront Adobe Commerce optimisé par Edge Delivery.

## Scénario d&#39;affaires - Carvelo Automobile

Carvelo Automobile est un conglomérat automobile fictif avec une configuration opérationnelle complexe.

![Carvelo Automobile](../assets/carvelo.png)

Dans ce diagramme, vous voyez que Carvelo vend des produits automobiles de trois marques. Chaque marque est une entreprise enfant différente :

- Aurora (véhicules électriques)
- Boulon (SUV)
- Cruz (hybride)

Elle vend ces marques par l&#39;intermédiaire de trois concessionnaires :

- Arkbridge
- Kingsbluff
- Celport

Ces concessionnaires appartiennent à deux sociétés mères différentes :

- West Coast Inc. (Arkbridge) (en anglais seulement)
- East Coast Inc. (Kingsbluff, Celport)

Chaque société possède deux registres des prix utilisés pour vendre des produits à un prix spécifique pour différents acheteurs (base, VIP).

- `west_coast_inc` et `vip_west_coast_inc`
- `east_coast_inc` et `vip_east_coast_inc`

Comme vous pouvez le constater, il s’agit d’un cas d’utilisation commerciale très complexe. Avec [!DNL Adobe Commerce Optimizer], un commerçant peut prendre en charge une structure commerciale complexe à l’aide d’un catalogue de base unique pour syndiquer les données sans duplication de catalogue, adapter les tarifs (tarifs de plus de 30 000) et diffuser toutes ces données sur un storefront Edge Delivery Services.

Maintenant que vous disposez d’un aperçu du cas d’utilisation professionnel, voici votre objectif tout au long de ce tutoriel :

>[!BEGINSHADEBOX]

Carvelo souhaite vendre des pièces de ses trois marques (Aurora, Bolt et Cruz) par l&#39;intermédiaire des différents concessionnaires (Akbridge, Kingsbluff et Celport). Carvelo veut s&#39;assurer que les concessionnaires n&#39;ont accès qu&#39;aux pièces et aux prix corrects conformément à leurs accords de licence respectifs.

En fin de compte, Carvelo a deux objectifs principaux :

1. Tenez à jour un site web « mondial », qui comporte tous les SKU des trois marques.
1. Offrez aux concessionnaires un moyen de créer leurs propres vitrines en fonction de la visibilité et des prix uniques des SKU pour chaque SKU de chaque concessionnaire.

>[!ENDSHADEBOX]

Accédez à présent à votre instance [!DNL Adobe Commerce Optimizer].

## 1. Accéder à l’instance de [!DNL Adobe Commerce Optimizer]

Après votre intégration au programme d’accès anticipé, Adobe envoie un e-mail contenant l’URL d’accès à l’instance l[!DNL Adobe Commerce Optimizer] configurée pour vous. Cette instance est préconfigurée avec tout ce dont vous avez besoin pour réussir les étapes décrites dans ce tutoriel, y compris les données de catalogue qui prennent en charge le cas d’utilisation de Carvelo Automobile.

Lorsque vous lancez [!DNL Adobe Commerce Optimizer], les éléments suivants s’affichent :

![[!DNL Adobe Commerce Optimizer] UI](../assets/user-interface.png)

>[!NOTE]
>
>Consultez l’article [présentation](../overview.md) pour en savoir plus sur les différentes parties qui constituent l’interface utilisateur de [!DNL Adobe Commerce Optimizer].

Dans le volet de navigation de gauche, développez la section **[!UICONTROL Catalog]** et cliquez sur **[!UICONTROL Channels]**. Notez que les concessionnaires Arkbridge et Kingsbluff ont déjà créé des canaux :

![Canaux préconfigurés](../assets/existing-channels-list.png)

>[!NOTE]
>
>Pour l’instant, vous pouvez ignorer le canal **global**.

Cliquez sur l’icône d’informations pour consulter les détails du canal.

Les politiques d’Arkbridge sont les suivantes :

- Marque
- Modèle
- Marques de West Coast Inc
- Catégories de pièces Arkbridge

Kingsbluff a les politiques suivantes :

- Marque
- Modèle
- Marques de East Coast Inc
- Catégories de pièces Kingsbluff

Dans la section suivante, vous allez créer un canal et des politiques pour le concessionnaire Celport.

## 2. Créer une politique et un canal

Le directeur du commerce de Carvelo doit mettre en place une nouvelle vitrine pour un concessionnaire appelé *Celport* qui appartient à la société *East Coast Inc*. Celport commercialisera des freins et des suspensions pour les marques Bolt et Cruz.

![Distributeur Celport](../assets/celport-dealer.png)

À l’aide de [!DNL Adobe Commerce Optimizer], le gestionnaire de commerce :

1. Créez une nouvelle politique appelée *Catégories de pièces Celport* pour que Celport vende uniquement des pièces de frein et de suspension.
1. Créez un canal pour le storefront Celport.

   Ce canal utilise votre nouvelle politique *catégories de pièces Celport* et les marques existantes *East Coast Inc* pour s&#39;assurer que Celport ne peut vendre que les marques Bolt et Cruz dans le cadre de l&#39;accord avec East Coast Inc. Le canal Celport utilisera le catalogue de prix `east_coast_inc` pour soutenir les barèmes de prix des produits qui s&#39;alignent sur les accords de licence de la marque.
1. Mettez à jour la configuration du storefront Commerce pour utiliser les données du canal Celport que vous avez créé.

À la fin de cette section, Celport sera opérationnel et prêt à vendre les produits de Carvelo.

### Création d’une politique

Créons une nouvelle politique appelée *Catégories de pièces Celport* pour filtrer les SKU que le concessionnaire Celport vend, qui incluent les pièces de frein et de suspension.

1. Dans le volet de navigation de gauche, développez la section **[!UICONTROL Catalog]** et cliquez sur **[!UICONTROL Policies]**.

1. Cliquez sur **[!UICONTROL Add Policy]**.

   Une nouvelle page s’affiche pour ajouter les détails de la politique.

1. Ajoutez les détails requis :

   **Nom** = *Catégories de pièces Celport*

1. Cliquez sur **[!UICONTROL Add Filter]**.

   Une boîte de dialogue s’affiche pour ajouter des détails de filtre.

1. Ajoutez les détails du filtre :

   - **Attribute** = *part_category*
   - **Opérateur** = **IN**
   - **Valeur Source** = **STATIC**
   - **Valeur** = *freins*, *suspension*

   >[!IMPORTANT]
   >
   >Assurez-vous que le nom d’attribut que vous spécifiez correspond exactement au nom d’attribut de SKU dans le catalogue.

   Pour en savoir plus sur la différence entre une source de valeurs STATIQUE et TRIGGER, voir [types de sources de valeurs](../catalog/policies.md#value-source-types).

1. Dans la boîte de dialogue **[!UICONTROL Filter details]**, cliquez sur **[!UICONTROL Save]**.

1. Pour activer le filtre que vous venez de créer, cliquez sur les points d’action (...) et sélectionnez **Activer**.

1. Cliquez sur **[!UICONTROL Save]**.

   >[!NOTE]
   >
   >Si le bouton **[!UICONTROL Save]** n’est pas actif (bleu), il se peut que le nom de la politique vous manque. Cliquez sur l’icône en forme de crayon en regard de *Nouvelle politique* pour l’ajouter.

1. Revenez à la liste des politiques en cliquant sur la flèche Précédent.

   Votre nouvelle stratégie *Celport part categories* apparaît dans la liste.

### Création d’un canal

Créez un nouveau canal pour le concessionnaire *Celport* et liez les politiques suivantes : *marques East Coast Inc* et *Catégories de pièces Celport*.

1. Dans le volet de navigation de gauche, développez la section **[!UICONTROL Catalog]** et cliquez sur **[!UICONTROL Channels]**.

   ![Canaux](../assets/channels.png)

   Notez les canaux existants : *Arkbridge*, *Kingsbluff* et *Global*.

   ![Page Canaux existants](../assets/existing-channels-list.png)

1. Cliquez sur **[!UICONTROL Add Channel]**.

1. Renseignez les détails du canal :

   - **Name** = *Celport*
   - **Portées** = *en-US* (appuyez sur Entrée)
   - **Politiques** (liste déroulante d’utilisation) = *Marques East Coast Inc*; *Catégories de pièces Celport*; *Marque*; *Modèle*                          

1. Cliquez sur **[!UICONTROL Add]** pour créer le canal.

   La page Canaux se met à jour pour afficher le nouveau canal.

   ![Liste des canaux mise à jour](../assets/updated-channels-list.png)

   >[!NOTE]
   >
   >Si le bouton **[!UICONTROL Add]** n’est pas bleu, assurez-vous que la portée est sélectionnée en plaçant votre curseur dans la section **[!UICONTROL Scopes]** et en appuyant sur **Entrée**.

1. Obtenez l’identifiant du canal Celport.

   Cliquez sur l’icône d’informations du canal Celport sur la page **Canaux**.

   ![Identifiant du canal Celport](../assets/celport-channel-id.png)

   Copiez et enregistrez l’identifiant du canal. Vous avez besoin de cet identifiant lorsque vous mettez à jour la configuration du storefront pour fournir des données à votre nouveau catalogue Celport.

Après avoir créé le canal Celport et les politiques associées, l’étape suivante consiste à configurer le storefront pour créer votre catalogue Celport.

## 3. Mettre à jour votre storefront

La dernière partie de ce tutoriel implique la mise à jour du storefront que [vous avez déjà créé](#prerequisite) pour diffuser des données vers le nouveau catalogue Celport. Dans cette section, vous remplacez l’ID de canal dans votre fichier de configuration de storefront par l’ID de canal pour Celport.

1. Dans votre environnement de développement local, ouvrez le dossier dans lequel vous avez cloné le référentiel GitHub avec vos fichiers de configuration storefront standard.

1. Dans le répertoire racine du dossier, ouvrez le fichier `config.json`.

   +++Code config.json

   ```json
   {
    "public": {
      "default": {
      "commerce-core-endpoint": "https://www.aemshop.net/graphql",
      "commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/Fwus6kdpvYCmeEdcCX7PZg/graphql",
      "headers": {
         "cs": {
            "ac-channel-id": "9ced53d7-35a6-40c5-830e-8288c00985ad",
            "ac-environment-id": "Fwus6kdpvYCmeEdcCX7PZg",
            "ac-price-book-id": "west_coast_inc",
            "ac-scope-locale": "en-US"
           }
         },
         "analytics": {
            "base-currency-code": "USD",
            "environment": "Production",
            "store-id": 1,
            "store-name": "ACO Demo",
            "store-url": "https://www.aemshop.net",
            "store-view-id": 1,
            "store-view-name": "Default Store View",
            "website-id": 1,
            "website-name": "Main Website"
          }
       }
      }
   }
   ```

   Notez que l’en-tête du canal contient les lignes suivantes :

   - `ac-channel-id`:`"9ced53d7-35a6-40c5-830e-8288c00985ad"`
   - `ac-environment-id` : `"Fwus6kdpvYCmeEdcCX7PZg"`
   - `ac-price-book-id` : `"west_coast_inc"`

   +++

1. Remplacez la valeur `ac-channel-id` par l’identifiant de canal Celport que vous avez copié précédemment.
1. Si nécessaire, remplacez la valeur `ac-environment-id` par l’ID du client pour votre instance [!DNL Adobe Commerce Optimizer]. Vous pouvez trouver l’identifiant dans l’e-mail d’intégration du programme d’accès anticipé ou en contactant votre représentant de compte Adobe.

   Assurez-vous que la valeur `commerce-endpoint` correspond au point d’entrée GraphQL de votre instance [!DNL Adobe Commerce Optimizer].

1. Remplacez la valeur `ac-price-book-id` par `"east_coast_inc"`.
1. Enregistrez le fichier.

Lorsque vous enregistrez les modifications, vous mettez à jour la configuration du catalogue pour utiliser le canal Carvelo qui a été configuré pour vendre uniquement des pièces de frein et de suspension.

1. Lancez le storefront pour afficher l’expérience de catalogue spécifique à Celport créée par votre configuration de storefront.

   1. Dans la fenêtre du terminal de votre IDE, démarrez l’aperçu de votre storefront local.

      ```shell
      npm start
      ```

   Le navigateur s’ouvre dans l’aperçu du développement local sur `http://localhost:3000`.

   Si la commande échoue ou si le navigateur ne s’ouvre pas, consultez les [instructions pour le développement local](../storefront.md) dans la rubrique Configuration de Storefront .

   1. Dans le navigateur, recherchez `brakes` et appuyez sur **Entrée**.

      Le storefront se met à jour pour afficher la page de liste de produits affichant les pièces de frein.

   ![Page de liste des produits Freins](../assets/brakes-listing-page.png)

   Cliquez sur une image de pièce de frein pour afficher les détails du produit avec les informations de prix et notez les informations de prix du produit.

1. Recherchez maintenant `tires`, qui est une autre catégorie de composants disponible dans les données de cas d’utilisation de votre instance [!DNL Adobe Commerce Optimizer].

   ![Configuration de storefront avec des en-têtes incorrects](../assets/storefront-configuration-with-incorrect-headers.png)

   Notez qu’aucun résultat n’est renvoyé. Ceci est dû au fait que le canal Celport a été configuré pour vendre uniquement des pièces de frein et de suspension.

1. Testez la mise à jour de votre fichier de configuration de storefront (`config.json`).

   1. Modifiez les valeurs `ac-channel-id` et `ac-price-book`.

      Par exemple, vous pouvez remplacer l’ID de canal par le canal Kingsbluff et l’ID du catalogue par `east_coast_inc`. Vous pouvez voir les catégories de pièces disponibles pour Kingsbluff en examinant la politique *Catégories de pièces Kingsbluff*.

   1. Enregistrez le fichier.

      Lorsque vous enregistrez le fichier, l’aperçu du storefront local se met automatiquement à jour.

   1. Prévisualisez les modifications dans le navigateur à l’aide de la fonction Rechercher pour rechercher des pièces de pneumatique .

      Notez les différents types de pièces disponibles et les prix attribués au canal Kingsbluff.

      En modifiant les valeurs d’en-tête dans le fichier de configuration du storefront et en explorant le storefront mis à jour, vous pouvez voir à quel point il est facile de mettre à jour la vue du catalogue et les filtres de données pour personnaliser l’expérience du storefront.

## C&#39;est ça !

Dans ce tutoriel, vous avez appris comment [!DNL Adobe Commerce Optimizer] pouvez vous aider à organiser votre catalogue pour qu’il corresponde à vos opérations de vente au détail à l’aide d’un seul catalogue de base. Vous avez également appris à configurer un storefront optimisé par Edge Delivery Services.

## Que faire ensuite

Pour découvrir comment utiliser la détection de produit et les recommandations afin de personnaliser l’expérience d’achat de vos clients, consultez la [ présentation du marchandisage ](../merchandising/overview.md).
