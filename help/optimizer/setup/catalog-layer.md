---
title: Couche Catalogue
description: Découvrez comment les calques de catalogue vous permettent de modifier les données de produit sans modifier les données source d’origine, afin que vous puissiez les personnaliser en toute sécurité et annuler les modifications à tout moment.
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
source-git-commit: 4a904527af172a5e35b87410135d55484d07ad84
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 0%

---

# Couche Catalogue

Les calques de catalogue vous permettent de modifier les données de produit sans modifier les données source d’origine. Les calques appliquent des modifications à des attributs de produit spécifiques, tels que le nom, la description, les images, les liens et les métadonnées, en créant un calque au-dessus de votre catalogue de base. Vos données de produit d’origine restent intactes, ce qui vous permet de personnaliser les produits en toute sécurité et d’annuler les modifications à tout moment.

![&#x200B; Calques de catalogue &#x200B;](../assets/catalog-layers.png)

## Fonctionnement des calques de catalogue

Lorsqu’un client consulte votre storefront, le système combine vos données de catalogue de base avec les couches de catalogue actives pour afficher les informations finales sur les produits. Voici comment fonctionne le processus :

1. **Application de couche** : lorsqu’une requête est effectuée avec un identifiant de canal et un identifiant d’environnement, le service de magasin récupère la vue de catalogue appropriée.

1. **Fusion des données** : le système applique des calques de catalogue aux données de produit en fonction de l&#39;ordre de priorité des calques.

1. **Gestion des champs** : les différents types de champs sont traités différemment :

   - **Remplacer les champs** : les champs de texte tels que le nom, la description et les méta-titres sont remplacés par les valeurs définies dans le calque, le calque de priorité supérieure étant prioritaire.
   - **Fusionner les champs** : les champs de tableau tels que les images, les liens et les attributs sont combinés à partir de plusieurs calques, fournissant ainsi une réponse unifiée.

1. **Résolution de priorité** : le champ Ordre détermine le calque prioritaire. Lorsque plusieurs calques modifient le même champ, le calque portant le numéro d’ordre le plus bas a une priorité plus élevée (par exemple, l’ordre 1 est le plus élevé).

## Cas d’utilisation de la couche Catalogue

Les calques de catalogue sont généralement utilisés pour :

- **Optimisation de l’optimisation du référencement** : remplacez les titres et descriptions des métadonnées de produit en fonction des recommandations de l’IA de [Sites Optimizer](../manage-results/opportunities.md).
- **Campagnes saisonnières** : mettez temporairement à jour les noms, descriptions ou images de produits pour les promotions sans modifier les données sources.
- **Personnalisation régionale** : affichez différentes informations sur les produits en fonction de l&#39;emplacement géographique ou de la langue.
- **Test A/B** : testez différentes présentations de produits pour optimiser les taux de conversion.
- **Gestion multimarque** : personnalisez les attributs de produit pour différentes vues de catalogue de marque.

## Ajout d’une couche de catalogue via l’ingestion de données

Vous pouvez ajouter des couches de catalogue à vos produits pendant le processus d’ingestion de données. Cette méthode est idéale pour les opérations en bloc ou les workflows automatisés.

>[!NOTE]
>
>Vous importez des calques de catalogue à l’aide de l’API d’ingestion, mais [la définition de l’ordre](#manage-layer-priorities) des calques est effectuée à l’aide de l’interface utilisateur.

**Conditions préalables :**

- Informations d’identification d’API avec autorisation d’accès au service d’ingestion de données
- SKU de produit qui existent déjà dans votre catalogue de base

**Étapes:**

1. Préparez les données de la couche au format requis avec les attributs de produit à modifier.

1. Utilisez le point d’entrée de l’API des couches de produit pour ingérer les données de couche.

1. Vérifiez que la couche a bien été ingérée en vérifiant la configuration de la vue de catalogue .

Pour obtenir des spécifications d’API détaillées et des exemples de payload, voir [Couches de produit](https://developer.adobe.com/commerce/services/reference/rest/#tag/Product-Layers) dans la documentation du développeur.

## Ajout manuel d’un calque de catalogue dans l’interface utilisateur

>[!NOTE]
>
>Cette fonctionnalité n’est pas encore disponible.

L’interface utilisateur de la vue Catalogue vous permet de créer et de gérer manuellement des calques, ce qui est particulièrement utile pour les intégrations telles que Sites Optimizer qui génèrent des recommandations optimisées par l’IA.

>[!NOTE]
>
>Si aucune couche Sites Optimizer n’existe dans votre vue de catalogue, la fonction de correction automatique de Sites Optimizer en crée automatiquement une et lui affecte l’ordre 1 (priorité la plus élevée). Si vous supprimez ce calque, il sera recréé lors de la prochaine exécution de la fonction de correction automatique dans Sites Optimizer et déplacera les calques existants vers des numéros d’ordre inférieurs. Si la couche Sites Optimizer existe déjà avec un autre numéro de commande, la fonction de correction automatique ne modifie pas sa priorité.

>[!TIP]
>
>Pour les opérations de calque en masse, utilisez la méthode API d’ingestion de données [décrite ci-dessus](#add-a-catalog-layer-via-data-ingestion).

**Pour créer un calque manuel, procédez comme suit**

1. Accédez à **Configuration de la boutique** > **Vues du catalogue**.

1. Sélectionnez la vue du catalogue à laquelle appliquer le calque.

1. Dans la section Calques de catalogue, cliquez sur **Ajouter un calque de catalogue**.

1. Configurez les propriétés du calque :

   - **Nom du calque** : entrez un nom descriptif pour identifier l&#39;objectif du calque.
   - **Produits** : sélectionnez les produits auxquels s&#39;applique ce calque.
   - **Attributs** : sélectionnez les attributs de produit à modifier (nom, description, images, balises meta, etc.).
   - **Valeurs** : saisissez les nouvelles valeurs pour chaque attribut sélectionné.

1. Cliquez sur **Enregistrer** pour créer le calque.

Le nouveau calque est ajouté à la vue Catalogue et se voit attribuer automatiquement le prochain numéro de commande disponible.

## Aperçu des effets de calque

>[!NOTE]
>
>Cette fonctionnalité n’est pas encore disponible.

Avant d’activer des calques ou de modifier les priorités, vous pouvez prévisualiser la manière dont ils affectent les données de produit.

**Pour prévisualiser les modifications apportées au calque :**

1. Accédez à **Configuration de la boutique** > **Vues du catalogue**.

1. Sélectionnez la vue du catalogue avec les calques à prévisualiser.

1. Dans la section Calques de catalogue , sélectionnez un produit spécifique ou utilisez la fonction d’aperçu.

1. Examinez les données de produit combinées montrant comment les calques modifient les valeurs du catalogue de base.

1. Apportez des ajustements au contenu du calque ou à l’ordre de priorité, si nécessaire.

## Activer, désactiver ou supprimer des calques

Vous pouvez activer ou désactiver les calques de catalogue sans les supprimer, ce qui vous permet de déterminer à quel moment des personnalisations spécifiques sont appliquées.

**Pour activer ou désactiver un calque, procédez comme suit**

1. Accédez à **Configuration de la boutique** > **Vues du catalogue**.

1. Sélectionnez la vue du catalogue contenant le calque.

1. Dans la section Calques de catalogue, recherchez le calque à activer/désactiver.

1. Cliquez sur le bouton d’activation pour activer ou désactiver le calque.

   - **Actif** : le calque est appliqué aux données du produit.
   - **Inactif** : le calque est conservé, mais pas appliqué aux données du produit.

1. La modification prend effet immédiatement sur votre storefront.

**Pour supprimer un calque, procédez comme suit**

Utilisez l’API Data Ingestion pour [supprimer une couche de catalogue](https://developer.adobe.com/commerce/services/reference/rest/#operation/deleteProductLayers).

## Gérer les priorités de calque

L’ordre dans lequel les calques sont appliqués détermine les valeurs qui apparaissent sur votre storefront lorsque plusieurs calques modifient le même attribut de produit. La gestion des priorités garantit l’affichage des données correctes.

**Présentation de l’ordre de priorité :**

- Chaque calque se voit attribuer un numéro d’ordre (1, 2, 3, etc.)
- L’ordre 1 a la priorité la plus élevée et remplace tous les autres calques
- Lorsque plusieurs calques modifient le même champ, le calque portant le numéro d’ordre le plus bas est prioritaire
- La priorité s’applique uniquement aux champs de remplacement (nom, description, balises meta)
- Les champs de fusion (images, liens, attributs) combinent les données de tous les calques

**Pour réorganiser les priorités des calques :**

1. Accédez à **Configuration de la boutique** > **Vues du catalogue**.

1. Sélectionnez la vue du catalogue contenant les calques à réorganiser.

1. Dans la section Calques de catalogue, recherchez le calque à déplacer.

1. Faites glisser et déposez le calque pour modifier sa position ou utilisez les commandes de réorganisation.

1. Le système met automatiquement à jour les numéros de commande en fonction de la nouvelle séquence.

1. Cliquez sur **Enregistrer** pour appliquer le nouvel ordre de priorité.

>[!IMPORTANT]
>
>Les modifications apportées à la priorité de calque prennent effet immédiatement et peuvent avoir une incidence sur ce que les clients voient sur votre storefront. Vérifiez l’aperçu avant d’enregistrer pour vous assurer que les valeurs correctes sont appliquées (**l’aperçu n’est pas encore disponible**).

## Bonnes pratiques

Suivez ces recommandations lors de l’utilisation des calques de catalogue :

- **Utilisez des noms descriptifs**—Nommez les calques clairement pour indiquer leur objectif (par exemple, « Campagne des Fêtes 2025 » ou « Optimisation du référencement - Pages de produits »).

- **Limiter les calques** : bien que le système prenne en charge plusieurs calques, un nombre trop élevé d’entre eux peut avoir un impact sur les performances. Consolidez les calques si possible.

<!--- **Test before activating**—Always preview layer effects before activating them on your live storefront. !!!REMOVE IF PREVIEW NOT AVAILABLE FOR GA!!!-->

- **Logique de priorité du document** : suivez les calques qui doivent être prioritaires pour éviter les remplacements involontaires.

- **Vérifier les calques Sites Optimizer** : lorsque vous utilisez le correctif automatique de Sites Optimizer, le système crée les calques avec la priorité la plus élevée. Veillez à ajouter des calques manuels susceptibles de remplacer les recommandations de l’IA. En savoir plus sur l&#39;utilisation de [Sites Optimizer](../manage-results/opportunities.md).

- **Surveillance des performances** : si vous constatez un chargement lent des pages produit, passez en revue la configuration des calques et envisagez de les consolider.

## Plus comme ceci

- [Vues du catalogue](catalog-view.md) - Configurez les vues du catalogue pour différents storefronts.
- [Opportunités](../manage-results/opportunities.md) - Découvrez l’optimisation optimisée par l’IA à l’aide des calques de catalogue
