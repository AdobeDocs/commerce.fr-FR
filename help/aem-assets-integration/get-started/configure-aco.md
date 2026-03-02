---
title: Configuration d’AEM Assets pour Commerce Optimizer
description: Découvrez comment configurer l’intégration d’AEM Assets pour  [!DNL Adobe Commerce Optimizer].
feature: CMS, Media, Configuration, Integration
source-git-commit: bf1d88ef7daec25872678bb27bce0bb7c97fd296
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 0%

---


# Configuration d’AEM Assets pour [!DNL Adobe Commerce Optimizer]

[!BADGE SaaS uniquement]{type=Positive tooltip="S’applique uniquement aux projets Adobe Commerce Optimizer."}

L’intégration AEM Assets pour [!DNL Adobe Commerce Optimizer] permet aux commerçants d’utiliser AEM Assets comme solution centralisée de gestion des ressources numériques pour les images de produits. Ce guide couvre la configuration spécifique à [!DNL Commerce Optimizer].

Contrairement à Adobe Commerce (PaaS) ou Adobe Commerce as a Cloud Service (ACCS), [!DNL Commerce Optimizer] ne dispose pas d’une interface utilisateur de configuration d’administration. Pour activer l’intégration, créez un ticket d’assistance avec vos informations [!DNL Adobe Commerce Optimizer] et AEM Assets. L’assistance Adobe configure l’intégration et enregistre votre client auprès du service d’intégration Assets.

Le diagramme suivant présente une vue d’ensemble de la synchronisation de produit entre [!DNL Adobe Commerce Optimizer] et l’intégration d’AEM Assets.

![AEM Assets vers [!DNL Commerce Optimizer] flux](../assets/aco-asset-sync-architecture.png){width="700"}

Cette intégration comporte deux flux principaux :

* **Depuis AEM Assets** : lorsqu’une ressource est approuvée, rejetée ou supprimée, l’événement se propage par le pipeline Adobe vers le service d’intégration d’Assets. Le service fait correspondre les ressources aux produits à l’aide de `match-by-SKU` (piloté par les métadonnées) ou d’un [mappeur personnalisé (App Builder)](../synchronize/custom-match.md){target=_blank}, puis envoie les mappages de `product-asset` au Commerce Optimizer, où ils sont stockés en tant que couches de produit.

* **De[!DNL Adobe Commerce Optimizer]** : lorsqu’un produit est mis à jour dans [!DNL Commerce Optimizer], l’événement se propage par le biais du pipeline Adobe vers le service d’intégration d’Assets. Le service resynchronise tous les mappages de ressources correspondants avec le [!DNL Adobe Commerce Optimizer].

## Conditions préalables

Avant de configurer l’intégration, vérifiez les points suivants :

* Une instance [!DNL Adobe Commerce Optimizer] active avec des droits de visualisation des produits ou toute licence AEM Assets avec Dynamic Media.
* Accès à un environnement AEM Assets as a Cloud Service.
* [!DNL Commerce Optimizer] et AEM Assets dans la même organisation Adobe IMS.
* Dynamic Media avec OpenAPI activé dans votre environnement AEM Assets.

## Intégration

Pour intégrer l’intégration d’AEM Assets à [!DNL Commerce Optimizer], vous devez [créer un ticket d’assistance](https://experienceleague.adobe.com/fr/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket).

L’assistance Adobe utilise les informations figurant dans votre ticket pour enregistrer votre client auprès du service d’intégration d’Assets et configurer l’intégration.

Incluez les informations suivantes dans votre ticket de support :

* **[!DNL Adobe Commerce Optimizer]ID de client** (ID d’instance) trouvé dans l’URL [!DNL Commerce Optimizer] ou l’interface utilisateur de Commerce Cloud Manager.
* **ID de programme AEM**.
* **Identifiant d’environnement AEM**.
* **Règle de correspondance** : correspondance par SKU ou [correspondance externe (App Builder)](../synchronize/custom-match.md){target=_blank}.
* **Couche** : nom de la couche de catalogue avec laquelle enregistrer le client. Spécifiez un nom personnalisé si nécessaire. Dans le cas contraire, le `AEM-Assets` par défaut est utilisé.
* **Paramètres régionaux** : paramètre régional source du catalogue avec lequel enregistrer le client (par exemple, `en-US`).

>[!IMPORTANT]
>
> L’intégration prend en charge une source par client, c’est-à-dire la combinaison d’un paramètre régional et d’une couche.

Une fois que l’assistance Adobe a traité votre ticket, l’intégration est configurée et votre client est enregistré auprès du service d’intégration d’Assets.

Une fois l’intégration terminée :

1. **Enregistrement auprès du service d’intégration Assets** : votre client [!DNL Commerce Optimizer] est enregistré auprès du service d’intégration Assets à l’aide de l’ID de client [!DNL Adobe Commerce Optimizer], de l’ID de programme AEM, de l’ID d’environnement AEM et du client.

1. **Configuration de l’authentification** : l’authentification du jeton de service IMS est configurée entre [!DNL Commerce Optimizer] et le service d’intégration d’Assets pour une communication sécurisée.

1. **Abonnement aux événements** : le service d’intégration Assets s’abonne aux éléments suivants :

   * Événements AEM Assets (ressource approuvée, mise à jour, supprimée)
   * Événements de catalogue [!DNL Commerce Optimizer] (produit créé, mis à jour)

### Restrictions

L’intégration [!DNL Commerce Optimizer] présente les limites suivantes :

* **Couche unique par commerçant** : l’intégration AEM Assets prend en charge une couche AEM-Assets par commerçant (une source par client). La configuration de plusieurs couches par commerçant n’est pas prise en charge à ce stade.
* **Images uniquement** : l’intégration ne prend pas en charge les vidéos ou d’autres types de médias.
* **Aucune image de catégorie**—La synchronisation des images de catégorie n&#39;est pas disponible. Les images de catégorie d’AEM Assets pour le sélecteur Assets (insertion de l’interface utilisateur) ne sont pas prises en charge.
* **Pas de distinction multisite** : l’intégration ne gère pas les sites multiples ; une image associée à un produit s’affiche de la même manière sur tous les canaux et politiques.
* **Position/ordre de l’image** : la position et l’ordre de l’image ne sont pas pris en charge.
* **Le produit doit exister** : si le produit n’existe pas dans [!DNL Commerce Optimizer], la couche n’est pas créée pour ce mappage produit-ressource.
* **Remplacement du champ de calque** : les valeurs d&#39;un calque remplacent le catalogue de base. Si un champ n’est pas envoyé dans la payload de couche, il peut être remplacé par une valeur vide. Utilisez une couche dédiée pour le contenu AEM Assets ; la réutilisation d’une couche existante à d’autres fins peut entraîner une perte de données involontaire.

### Configuration d’AEM Assets

Le processus d’installation et de configuration d’AEM Assets pour [!DNL Commerce Optimizer] est le même que pour Adobe Commerce as a Cloud Service. Consultez [Configuration du projet AEM Assets pour la prise en charge des métadonnées Commerce](configure-aem.md) pour obtenir des instructions complètes.

Assurez-vous que votre environnement AEM Assets est prêt :

1. **Configuration d’AEM Assets** : configurez le profil de métadonnées Commerce. Voir [&#x200B; Configuration d’un profil de métadonnées](configure-aem.md#configure-a-metadata-profile).

1. **Activation de Dynamic Media** : vérifiez que Dynamic Media avec les fonctionnalités OpenAPI est activé dans votre environnement AEM Assets.

## Configuration d’AEM Assets

Pour activer la synchronisation produit-ressource, configurez votre environnement AEM Assets.

### Étape 1 : activation de Dynamic Media avec OpenAPI

Dynamic Media avec OpenAPI doit être activé dans votre environnement AEM Assets. Les visuels de produit et les nouvelles licences AEM Assets vous permettent de l’activer en libre-service via Cloud Manager. Les licences AEM Assets plus anciennes nécessitent la prise en charge d’Adobe pour l’activer. Voir [Configuration du projet AEM Assets](configure-aem.md#prerequisites) pour connaître les étapes d’activation.

### Étape 2 : Facultatif. Configuration du profil de métadonnées Commerce

Configurez le profil de métadonnées dans AEM Assets pour stocker les métadonnées spécifiques à Commerce.

Consultez [Configuration d’un profil de métadonnées](configure-aem.md#step-2-optional-configure-a-metadata-profile) pour obtenir des instructions détaillées.

### Étape 3 : application de métadonnées aux ressources

Ajoutez des métadonnées Commerce à vos images de produit dans AEM Assets.

Voir le [contenu du package AEM Commerce](configure-aem.md#aem-commerce-assets-commerce-package-contents) pour les définitions de champ et [Configurer un profil de métadonnées](configure-aem.md#step-2-optional-configure-a-metadata-profile) pour les étapes de configuration.

La ressource doit avoir un statut **approuvé** pour que la synchronisation des données se déclenche. L’enregistrement des métadonnées seul ne déclenche pas l’événement.

>[!CAUTION]
>
> Affectez la couche `AEM-Assets` à votre [vue de catalogue](https://experienceleague.adobe.com/fr/docs/commerce/optimizer/setup/catalog-view). Si le calque n’est pas affecté, les données d’image du produit peuvent être écrasées de manière inattendue.

## Synchronisation

Une fois configurée, l’intégration synchronise automatiquement les mappages `product-asset`.

Voir [Correspondance automatique personnalisée](../synchronize/custom-match.md) pour plus d’informations.

### Exemple de workflow Correspondance par SKU

Flux type lors de l’ajout d’une ressource existante à un nouveau produit :

1. Créer le produit dans [!DNL Commerce Optimizer] (via l’API ou l’ingestion de données). Le produit peut exister sans images au départ.

1. Dans AEM Assets, ouvrez la ressource que vous souhaitez mapper au produit.

1. Ajoutez le SKU du produit aux métadonnées **commerce:skus** et attribuez des rôles d’image (par exemple, `thumbnail`, `image`).

1. Valider la ressource à diffuser. Cela déclenche l’événement qu’Assets Integration Service traite.

1. Assets Integration Service envoie le mapping produit-image à [!DNL Commerce Optimizer]. Le produit en [!DNL Commerce Optimizer] est mis à jour avec les images de la ressource.

1. Vérifiez que l’image est visible. Patientez le temps que la synchronisation se termine (généralement en quelques minutes), puis vérifiez le produit dans l’interface utilisateur de [!DNL Commerce Optimizer] (par exemple, Synchronisation des données ou vue de catalogue) ou interrogez les API storefront (Service de catalogue, Recherche en direct, API Storefront GraphQL) pour confirmer que l’image est renvoyée.

## Gestion des rôles d’image

Lorsqu’un produit comporte plusieurs ressources utilisant le même rôle d’image (par exemple, deux ressources avec le rôle `thumbnail`), l’intégration garantit qu’une seule ressource conserve ce rôle afin d’éviter les rôles en double dans la couche de [!DNL Commerce Optimizer] et un comportement de storefront inattendu.

**Comportement :** lorsqu’une mise à jour est envoyée depuis AEM Assets, la ressource la plus récemment mise à jour reçoit le rôle d’image (par exemple, `thumbnail`) et le rôle est supprimé de la ressource précédente qui l’avait. Cela empêche l’affichage de rôles d’image en double dans le storefront.

## Plus comme ceci

* [Visuels du produit](../../optimizer/setup/product-visuals.md)
* [Configuration du projet AEM Assets](configure-aem.md)
* [Correspondance automatique personnalisée](../synchronize/custom-match.md)
* [Présentation de l’intégration d’AEM Assets](../overview.md)
