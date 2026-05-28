---
title: Configuration d’AEM Assets pour Commerce Optimizer
description: Découvrez comment configurer l’intégration d’AEM Assets pour  [!DNL Adobe Commerce Optimizer].
feature: CMS, Media, Configuration, Integration
source-git-commit: 42f0e0cb72c6429eb6f08f1922c4171195a78d2b
workflow-type: tm+mt
source-wordcount: '1460'
ht-degree: 0%

---


# Configuration d’AEM Assets pour [!DNL Adobe Commerce Optimizer]

[!BADGE SaaS uniquement]{type=Positive tooltip="S’applique uniquement aux projets Adobe Commerce Optimizer."}

L’intégration AEM Assets pour [!DNL Adobe Commerce Optimizer] permet aux commerçants d’utiliser AEM Assets comme solution centralisée de gestion des ressources numériques pour les images de produits. Ce guide couvre la configuration spécifique à [!DNL Commerce Optimizer].

Contrairement à Adobe Commerce (PaaS) ou Adobe Commerce as a Cloud Service (ACCS), [!DNL Commerce Optimizer] ne dispose pas d’une interface utilisateur de configuration d’administration. Pour activer l’intégration, créez un ticket d’assistance avec vos informations [!DNL Adobe Commerce Optimizer] et AEM Assets. L’assistance Adobe configure l’intégration et enregistre votre client auprès du service d’intégration Assets.

**Préparez AEM Assets avant d’envoyer le ticket.** L’enregistrement du client suppose que le côté AEM est utilisable pour Commerce. Par exemple, après avoir déployé le package AEM Commerce `assets-commerce` afin que les métadonnées et les événements fonctionnent comme expliqué. **L’ouverture d’un ticket avant la configuration d’AEM peut retarder l’intégration.**

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
* Dynamic Media avec OpenAPI activé dans votre environnement AEM Assets (voir [Configuration du projet AEM Assets](configure-aem.md#prerequisites) pour les étapes d’activation).

## Configurer AEM Assets en premier

Suivez les étapes d’AEM Assets **avant** vous [ouvrir un ticket d’assistance](#onboarding) pour l’enregistrement du client. Le modèle d’installation correspond à Adobe Commerce as a Cloud Service. Voir [Configuration du projet AEM Assets pour la prise en charge des métadonnées Commerce](configure-aem.md).

### Étape 1 : déployer le package AEM Commerce

Installez et déployez le package `assets-commerce` dans votre projet AEM afin que les schémas de métadonnées, les événements et l’interface utilisateur de Commerce soient disponibles.

Suivez la procédure complète décrite dans [Installation du package `assets-commerce`](configure-aem.md#step-1-install-the-assets-commerce-package). Avant d’ouvrir un ticket d’assistance, procédez comme suit :

1. Clonez le référentiel Git de Cloud Manager et copiez le code [référentiel AEM Assets Commerce](https://github.com/ankumalh/assets-commerce) dans votre projet.

1. Dans tous les fichiers `filter.xml` et `pom.xml` de votre projet, remplacez toutes les occurrences de &lt;my-app> par le nom de votre application.

1. Validez, poussez, exécutez votre pipeline de déploiement et vérifiez que l’onglet **[!UICONTROL Commerce]** s’affiche dans les propriétés de la ressource.

Voir [Installation du package `assets-commerce`](configure-aem.md#step-1-install-the-assets-commerce-package) pour les captures d’écran de Cloud Manager, les étapes du pipeline et le dépannage si l’onglet **[!UICONTROL Commerce]** est manquant.

### Étape 2 : activation de Dynamic Media avec OpenAPI

Dynamic Media avec les fonctionnalités OpenAPI doit être activé dans votre environnement AEM Assets. Les chemins en libre-service (par exemple, Cloud Manager pour les visuels de produit) et les itinéraires de prise en charge d’Adobe sont décrits sous [Configurer le projet AEM Assets](configure-aem.md#prerequisites).

### Étape 3 : application des métadonnées Commerce et approbation des ressources

Ajoutez des métadonnées Commerce à vos images de produit dans AEM Assets. Pour les définitions de champ, consultez [Contenu du package AEM Commerce](configure-aem.md#aem-commerce-assets-commerce-package-contents).

La ressource doit avoir un statut **approuvé** pour que la synchronisation des données se déclenche. L’enregistrement des métadonnées seul ne déclenche pas l’événement.

### Étape 4 : facultative — configurer un profil de métadonnées Commerce

Si vous choisissez d’utiliser des profils de métadonnées AEM pour rationaliser la création, configurez-les **après** le déploiement du package et la compréhension par votre équipe des champs de Commerce requis (modèle facultatif identique à **Configurer le projet AEM Assets**).

Voir [&#x200B; Configuration d’un profil de métadonnées](configure-aem.md#step-2-optional-configure-a-metadata-profile).

## Restrictions

L’intégration [!DNL Commerce Optimizer] présente les limites suivantes :

### Contraintes liées aux calques

Lisez cette section **avant** vous choisissez un nom de couche de catalogue dans votre ticket d’assistance. Le choix ou le partage de calques sans ce contexte est une cause fréquente de cas d’assistance évitables.

**Utilisez une couche dédiée pour le contenu AEM Assets.** Les payloads envoyés depuis AEM Assets renseignent un catalogue Commerce Optimizer **couche**. Les valeurs de ce calque **remplacent** les attributs de catalogue de base où les champs sont fournis. Lorsque l’intégration omet un champ dans la payload, les valeurs correspondantes dans cette couche peuvent être remplacées par des valeurs vides. Le partage d’une couche avec des workflows Commerce sans rapport ou la réutilisation d’une couche qui stocke déjà des données de produits non liés à AEM-Assets peuvent entraîner des **pertes de données involontaires** ou des remplacements déroutants. Planifiez le choix du calque **avant** ouvrez votre ticket d’assistance et réservez ce nom de calque (par exemple, le **`AEM-Assets`** par défaut) principalement pour la synchronisation des images de produit pilotée par AEM.

>[!IMPORTANT]
>
>L’intégration prend en charge **une source de catalogue par client** : un seul paramètre régional et **une couche nommée**. La configuration de plusieurs calques AEM-Assets ou de plusieurs paramètres régionaux pour le même client n’est pas prise en charge à ce stade.

### Autres contraintes

* **Images uniquement** : à ce stade, l’intégration ne prend pas en charge les vidéos ou d’autres types de médias.
* **Aucune image de catégorie** : la synchronisation des images de catégorie n’est pas disponible. Les images de catégorie d’AEM Assets pour le sélecteur Assets (insertion de l’interface utilisateur) ne sont pas prises en charge.
* **Pas de distinction multisite** : l’intégration ne gère pas le multisite ; une image associée à un produit s’affiche de la même manière sur tous les canaux et politiques.
* **Position/ordre de l’image** : la position et l’ordre de l’image ne sont pas pris en charge.
* **Le produit doit exister** : si le produit n’existe pas dans [!DNL Commerce Optimizer], la couche n’est pas créée pour ce mappage produit-ressource.

## Intégration

Pour intégrer l’intégration d’AEM Assets à [!DNL Commerce Optimizer], vous devez [créer un ticket d’assistance](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket).

L’assistance Adobe utilise les informations figurant dans votre ticket pour enregistrer votre client auprès du service d’intégration d’Assets et configurer l’intégration.

Assurez-vous d’avoir terminé [Configurer AEM Assets en premier](#configure-aem-assets-first) avant d’envoyer le ticket.

Incluez les informations suivantes dans votre ticket de support :

* **[!DNL Adobe Commerce Optimizer]ID de client** (ID d’instance) trouvé dans l’URL [!DNL Commerce Optimizer] ou l’interface utilisateur de Commerce Cloud Manager.
* **ID de programme**.
* **Identifiant d’environnement**.
* **Règle de correspondance** : correspondance par SKU ou [correspondance externe (App Builder)](../synchronize/custom-match.md){target=_blank}.
* **Couche** : nom de la couche de catalogue avec laquelle enregistrer le client (voir **Contraintes liées à la couche**). Spécifiez un nom personnalisé uniquement si vous le souhaitez. Dans le cas contraire, le **`AEM-Assets`** par défaut est utilisé.
* **Paramètres régionaux** : paramètre régional source du catalogue avec lequel enregistrer le client (par exemple, `en-US`). Elle doit correspondre au paramètre régional que vous utilisez dans la vue de catalogue et les données du catalogue de produits.

Une fois que l’assistance Adobe a traité votre ticket, l’intégration est configurée et votre client est enregistré auprès du service d’intégration d’Assets.

Une fois l’intégration terminée :

1. **Enregistrement auprès du service d’intégration d’Assets** : votre client [!DNL Commerce Optimizer] est enregistré auprès du service d’intégration d’Assets à l’aide de votre identifiant client [!DNL Adobe Commerce Optimizer], de votre identifiant de programme AEM, de votre identifiant d’environnement AEM, de la règle correspondante, des paramètres régionaux et du nom de couche fournis dans le ticket.

1. **Abonnement aux événements** : le service d’intégration Assets s’abonne aux éléments suivants :

   * Événements AEM Assets (ressource approuvée, mise à jour, supprimée)
   * Événements de catalogue [!DNL Commerce Optimizer] (produit créé, mis à jour)

Configurez votre [vue de catalogue](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/catalog-view) afin que les données d’image pilotées par AEM du storefront et des API soient visibles :

* **Source du catalogue (paramètres régionaux)** — Sélectionnez les paramètres régionaux que vous avez spécifiés dans votre ticket d&#39;assistance (par exemple **`en-US`**). L’intégration enregistre un paramètre régional par client ; une incohérence empêche les images synchronisées d’apparaître dans la vue de catalogue prévue.
* **Couche Catalogue** — Attribuez la couche **`AEM-Assets`** (ou votre nom de couche personnalisé à partir du ticket) à cette vue Catalogue.

Si le paramètre régional ou le calque n’est pas affecté correctement, les données d’image peuvent **ne pas apparaître** ou se comporter de manière inattendue, même si la synchronisation a réussi en amont.

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
