---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '1468'
ht-degree: 0%
---
Les calques de catalogue vous permettent de modifier les données de produit sans modifier les données source d’origine. Les calques modifient les attributs de produit, tels que le nom, la description, les images, les liens et les métadonnées, en créant un calque par-dessus votre catalogue de base. Vos données de produit d’origine restent intactes, ce qui vous permet de personnaliser les produits en toute sécurité et d’annuler les modifications à tout moment.

![Calques de catalogue](/help/assets/ccdm-shared/setup/catalog-layers.png)

## Accès à l’espace de travail Vues du catalogue

Vous gérez les calques de catalogue à partir de l’espace de travail *Vues du catalogue* en sélectionnant une vue du catalogue. La façon dont vous ouvrez l’espace de travail dépend du produit que vous utilisez :

- **Administrateur Adobe Commerce** (Adobe Commerce as a Cloud Service) : sélectionnez *Catalogue* > **Vues de catalogue**.
- **Adobe Commerce Optimizer Studio** : sélectionnez *Configuration du magasin* > **Vues du catalogue**.

## Fonctionnement des calques de catalogue

Lorsqu’un client consulte votre storefront, le système combine vos données de catalogue de base avec les couches de catalogue actives pour afficher les informations finales sur les produits. Le processus fonctionne comme suit :

1. **Application de couche** : lorsqu’une requête est effectuée avec un identifiant de canal et un identifiant d’environnement, le service de magasin récupère la vue de catalogue appropriée.

1. **Fusion des données** : le système applique des calques de catalogue aux données de produit en fonction de l’ordre de priorité des calques.

1. **Gestion des champs** : les différents types de champs sont traités différemment :

   * **Remplacer les champs** : les champs de texte tels que le nom, la description et les méta-titres sont remplacés par des valeurs de calque et le calque de priorité supérieure est prioritaire.
   * **Fusionner les champs** : les champs de tableau tels que les images, les liens et les attributs sont combinés à partir de plusieurs calques, fournissant ainsi une réponse unifiée.

1. **Résolution de priorité** : le champ Ordre détermine le calque prioritaire. Lorsque plusieurs calques modifient le même champ, le calque portant le numéro d’ordre le plus élevé a la priorité la plus élevée (par exemple, l’ordre 10 est le plus élevé).

## Cas d’utilisation de la couche Catalogue

Les calques de catalogue sont généralement utilisés pour :

* **Optimisation de l’optimisation du moteur de recherche** : remplacez les titres et descriptions des métadonnées de produit en fonction des recommandations de l’IA de [Sites Optimizer](../manage-results/opportunities.md).
* **Campagnes saisonnières** : mettez temporairement à jour les noms, descriptions ou images de produits pour les promotions sans modifier les données sources.
* **Personnalisation régionale** : affichez différentes informations sur les produits en fonction de l&#39;emplacement géographique ou de la langue.
* **Test A/B** : testez différentes présentations de produits pour optimiser les taux de conversion.
* **Gestion multimarque** : personnalisez les attributs de produit pour différentes vues de catalogue de marque.
* **Visuels de produit** : appliquez les images de produit d’AEM Assets sous forme de calque par-dessus votre catalogue de base.

## Couche AEM-Assets

Ce calque contient les images des produits synchronisées à partir d’AEM Assets. Comme les autres calques de catalogue, il est renseigné via l’API [Couches de produit](https://developer.adobe.com/commerce/services/reference/rest/#tag/Product-Layers){target=_blank}. Le service d’intégration Assets transforme les métadonnées des ressources AEM et les URL de diffusion au format API et envoie automatiquement les données lorsque les ressources sont approuvées dans AEM Assets.

L’intégration prend en charge une source par client (un paramètre régional + un calque).

### Fonctionnement de la couche AEM-Assets

1. **Création automatique** : la couche est créée lorsque l’intégration AEM Assets est configurée pour votre instance.

1. **Synchronisation des images** : lorsque des ressources sont approuvées dans AEM Assets, Assets Integration Service transforme les données des ressources et met à jour la couche `AEM-Assets` via l’API Product Layers.

1. **Affectation de calque** : affectez le calque `AEM-Assets` aux vues de catalogue dans lesquelles vous souhaitez que les images AEM Assets apparaissent.

### Affectation de la couche AEM-Assets à une vue de catalogue

>[!CAUTION]
>
> Affectez la couche AEM-Assets à votre vue de catalogue. Si le calque n’est pas affecté, les données d’image du produit sont écrasées de manière inattendue.

Pour afficher des images AEM Assets sur votre storefront :

1. Dans l’espace de travail Vues du catalogue , sélectionnez la vue du catalogue à laquelle vous souhaitez appliquer le calque.

1. Dans la section Calques de catalogue , recherchez le calque **AEM-Assets**.

1. Pour activer le calque pour cette vue de catalogue, activez-le.

1. Cliquez sur **[!UICONTROL Save]** pour appliquer les modifications.

Une fois attribuées, les API Merchandising Services et Storefront GraphQL renvoient à la fois des images de catalogue de base et des images AEM Assets pour les produits.

## Ajout d’une couche de catalogue via l’ingestion de données

Vous pouvez ajouter des couches de catalogue à vos produits pendant le processus d’ingestion de données. Cette méthode est idéale pour les opérations en bloc ou les workflows automatisés. Vous importez des calques de catalogue à l’aide de l’API d’ingestion, mais la [définition de l’ordre](#manage-layer-priorities) des calques s’effectue à l’aide de l’interface utilisateur.

**Conditions Préalables :**

* Informations d’identification d’API avec autorisation d’accès au service d’ingestion de données
* SKU de produit qui existent déjà dans votre catalogue de base

**Étapes :**

1. Préparez les données de la couche au format requis avec les attributs de produit à modifier.

1. Utilisez le point d’entrée de l’API des couches de produit pour ingérer les données de couche.

1. Vérifiez que la couche a bien été ingérée en vérifiant la configuration de la vue de catalogue .

Pour obtenir des spécifications d’API détaillées et des exemples de payload, consultez [Couches de produit](https://developer.adobe.com/commerce/services/reference/rest/#tag/Product-Layers){target=_blank} dans la documentation du développeur.

## Ajout manuel d’un calque de catalogue dans l’interface utilisateur

L’interface utilisateur de la vue Catalogue vous permet de créer et de gérer des calques manuellement, ce qui est particulièrement utile pour les intégrations telles que Sites Optimizer qui génèrent des recommandations optimisées par l’IA. Pour les opérations de calque en masse, utilisez la méthode API d’ingestion de données [ décrite ci-dessus](#add-a-catalog-layer-via-data-ingestion).

S’il n’existe pas de calque Sites Optimizer dans votre vue de catalogue, la fonction de correction automatique de Sites Optimizer en crée automatiquement un et lui affecte la priorité la plus élevée (numéro le plus élevé). Si vous supprimez ce calque, il sera recréé la prochaine fois que la fonction de correction automatique de Sites Optimizer s’exécutera et décalera les calques existants vers des numéros d’ordre inférieurs. Si le calque Sites Optimizer existe déjà avec un autre numéro de commande, la fonction de correction automatique ne modifie pas sa priorité.

**Pour créer un calque manuel :**

1. Dans l’espace de travail **[!UICONTROL Catalog views]**, sélectionnez la vue de catalogue à laquelle vous souhaitez appliquer le calque.

1. Dans la section Calques de catalogue, cliquez sur **Ajouter un calque de catalogue**.

1. Configurez les propriétés du calque :

   * **Nom du calque** : saisissez un nom descriptif pour identifier l&#39;objectif du calque.
   * **Produits** : sélectionnez les produits auxquels cette couche s&#39;applique.
   * **Attributs** : sélectionnez les attributs de produit à modifier (nom, description, images, balises meta, etc.).
   * **Valeurs** : saisissez les nouvelles valeurs pour chaque attribut sélectionné.

1. Cliquez sur **[!UICONTROL Save]** pour créer le calque.

Le nouveau calque est ajouté à la vue Catalogue et se voit attribuer automatiquement le prochain numéro de commande disponible.

## Aperçu des effets de calque


Avant d’activer des calques ou de modifier les priorités, vous pouvez prévisualiser la manière dont ils affectent les données de produit.

**Pour prévisualiser les modifications de calque :**

1. Dans l’espace de travail **[!UICONTROL Catalog views]**, sélectionnez la vue du catalogue avec les calques à prévisualiser.

1. Dans la section Calques de catalogue , sélectionnez un produit spécifique ou utilisez la fonction d’aperçu.

1. Examinez les données de produit combinées montrant comment les calques modifient les valeurs du catalogue de base.

1. Apportez des ajustements au contenu du calque ou à l’ordre de priorité, si nécessaire.

## Gérer l’activation et la suppression des calques

Vous pouvez activer ou désactiver les calques de catalogue sans les supprimer, ce qui vous permet de déterminer à quel moment des personnalisations spécifiques sont appliquées.

**Pour activer ou désactiver un calque :**

1. Dans l’espace de travail **[!UICONTROL Catalog views]**, sélectionnez la vue de catalogue contenant le calque.

1. Dans la section Calques de catalogue, recherchez le calque à activer/désactiver.

1. Cliquez sur le bouton d’activation pour activer ou désactiver le calque.

   * **Actif** : la couche est appliquée aux données du produit.
   * **Inactif** : le calque est conservé, mais pas appliqué aux données du produit.

1. La modification prend effet immédiatement sur votre storefront.

**Pour supprimer un calque :**

Utilisez l’API Data Ingestion pour [supprimer une couche de catalogue](https://developer.adobe.com/commerce/services/reference/rest/#operation/deleteProductLayers){target=_blank}.

## Gérer les priorités de calque

L’ordre dans lequel les calques sont appliqués détermine les valeurs qui apparaissent sur votre storefront lorsque plusieurs calques modifient le même attribut de produit. La gestion des priorités garantit l’affichage des données correctes.

**Présentation de l&#39;ordre de priorité :**

* Chaque calque se voit attribuer un numéro d’ordre (1, 2, 3, etc.)
* Des valeurs plus élevées indiquent une priorité plus élevée et remplacent tous les autres calques
* Lorsque plusieurs calques modifient le même champ, le calque portant le numéro d’ordre le plus élevé est prioritaire
* La priorité s’applique uniquement aux champs de remplacement (nom, description, balises meta)
* Les champs de fusion (images, liens, attributs) combinent les données de tous les calques

**Pour réorganiser les priorités de calque :**

1. Dans l’espace de travail **[!UICONTROL Catalog views]**, sélectionnez la vue du catalogue contenant les calques à réorganiser.

1. Dans la section Calques de catalogue, recherchez le calque à déplacer.

1. Faites glisser et déposez le calque pour modifier sa position ou utilisez les commandes de réorganisation.

1. Le système met automatiquement à jour les numéros de commande en fonction de la nouvelle séquence.

1. Cliquez sur **[!UICONTROL Save]** pour appliquer le nouvel ordre de priorité.

>[!IMPORTANT]
>
>Les modifications apportées à la priorité de calque prennent effet immédiatement et ont une incidence sur ce que les clients voient sur votre storefront. Vérifiez l’aperçu avant d’enregistrer pour vous assurer que les valeurs correctes sont appliquées.

## Bonnes pratiques

Suivez ces recommandations lors de l’utilisation des calques de catalogue :

* **Utilisez des noms descriptifs**—Les calques de nom indiquent clairement leur objectif (par exemple, « Campagne des Fêtes 2025 » ou « Optimisation du référencement — Pages de produits »).

* **Limiter les calques** : bien que le système prenne en charge plusieurs calques, l’utilisation d’un nombre trop élevé peut avoir un impact sur les performances. Consolidez les calques si possible.


* **Logique de priorité du document** : suivez les calques qui ont la priorité pour éviter les remplacements involontaires.

* **Vérifier les calques Sites Optimizer** : lors de l’utilisation du correctif automatique à partir de Sites Optimizer, le système crée les calques avec la priorité la plus élevée. Veillez à ajouter des calques manuels qui remplacent les recommandations de l’IA. En savoir plus sur l&#39;utilisation de [Sites Optimizer](../manage-results/opportunities.md).

* **Surveiller les performances**—Si vous constatez un chargement lent de la page produit, vérifiez la configuration de votre calque et envisagez de consolider les calques.

## Plus comme ceci

* [Vues de catalogue](catalog-view.md) : configurez les vues de catalogue pour différents storefronts.
* [Visuels de produit](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/product-visuals) : utilisez AEM Assets pour les images de produit.
* [Opportunités](../manage-results/opportunities.md)—Découvrez l’optimisation optimisée par l’IA à l’aide des calques de catalogue
* [Clés d&#39;accès restreintes](restricted-access-keys.md)—Protégez une vue de catalogue avec l&#39;authentification par jeton signé
