---
title: Configuration d’AEM Assets pour Commerce Optimizer
description: Découvrez comment configurer l’intégration d’AEM Assets pour  [!DNL Adobe Commerce Optimizer].
feature: CMS, Media, Configuration, Integration
source-git-commit: 0c2e50338cbf286704239b6d1f628180e85a3bef
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 0%

---


# Configuration d’AEM Assets pour [!DNL Adobe Commerce Optimizer]

[!BADGE SaaS uniquement]{type=Positive tooltip="S’applique uniquement aux projets Adobe Commerce Optimizer."}

L’intégration AEM Assets pour [!DNL Adobe Commerce Optimizer] permet aux commerçants d’utiliser AEM Assets comme solution centralisée de gestion des ressources numériques pour les images de produits. Ce guide couvre la configuration spécifique à [!DNL Commerce Optimizer].

Le diagramme suivant présente une vue d’ensemble de la synchronisation de produit entre [!DNL Adobe Commerce Optimizer] et l’intégration d’AEM Assets.

![AEM Assets vers [!DNL Commerce Optimizer] flux](../assets/aco-asset-sync-architecture.png){width="700"}

Cette intégration comporte deux flux d’événements indépendants. Les deux utilisent [](https://developer.adobe.com/events/docs/) pour transférer des événements vers Assets Integration Service, mais chaque direction utilise son propre fournisseur d&#39;événements :

* **D’AEM Assets au service d’intégration d’Assets** : lorsqu’une ressource est approuvée, rejetée ou supprimée, l’événement est diffusé au service d’intégration d’Assets. Le service fait correspondre les ressources aux produits à l’aide de `match-by-SKU` (piloté par les métadonnées) ou d’un [mappeur personnalisé (App Builder)](../synchronize/custom-match.md){target=_blank}, puis envoie les mappages de `product-asset` à [!DNL Commerce Optimizer], où ils sont stockés en tant que couches de produit.

  >[!NOTE]
  >
  >La couche de catalogue `AEM-Assets` utilisée par l’intégration est créée automatiquement lors de l’intégration. Il n’est pas nécessaire de le créer au préalable. Pour en savoir plus sur le fonctionnement des calques de catalogue et le comportement du calque AEM-Assets, consultez [Calque AEM-Assets](../../optimizer/setup/catalog-layer.md#aem-assets-layer).

* **De [!DNL Adobe Commerce Optimizer] à Assets Integration Service** : lorsqu&#39;un produit est mis à jour en [!DNL Commerce Optimizer], l&#39;événement est diffusé au service d&#39;intégration d&#39;Assets. Le service resynchronise tous les mappages de ressources correspondants avec [!DNL Commerce Optimizer].

## Restrictions

L’intégration [!DNL Commerce Optimizer] présente les limites suivantes :

### Contraintes liées aux calques

* Utilisez une couche dédiée pour le contenu AEM Assets.

  Les payloads envoyés depuis AEM Assets renseignent une couche de catalogue Commerce Optimizer. Les valeurs de ce calque remplacent les attributs de catalogue de base où les champs sont fournis. Lorsque l’intégration omet un champ dans la payload, les valeurs correspondantes dans ce calque peuvent être remplacées par des valeurs vides. Le partage d’une couche avec des workflows Commerce sans rapport ou la réutilisation d’une couche qui stocke déjà des données de produits non liés à AEM-Assets peuvent entraîner des **pertes de données involontaires** ou des remplacements déroutants. Réservez le nom du calque (par exemple, le **`AEM-Assets`** par défaut) principalement pour la synchronisation d’images de produit pilotée par AEM.

* L’intégration prend en charge une source de catalogue par client : un seul paramètre régional et un calque nommé. La configuration de plusieurs calques AEM-Assets ou de plusieurs paramètres régionaux pour le même client n’est pas prise en charge à ce stade.

* La réutilisation d’un calque existant ou le partage d’un calque avec des workflows non liés est une cause fréquente de cas de prise en charge évitables.

### Autres contraintes

* **Images uniquement** : à ce stade, l’intégration ne prend pas en charge les vidéos ou d’autres types de médias.
* **Aucune image de catégorie** : la synchronisation des images de catégorie n’est pas disponible. Les images de catégorie d’AEM Assets pour le sélecteur Assets (insertion de l’interface utilisateur) ne sont pas prises en charge.
* **Pas de distinction multisite** : l’intégration ne gère pas le multisite ; une image associée à un produit s’affiche de la même manière sur tous les canaux et politiques.
* **Position/ordre de l’image** : la position et l’ordre de l’image ne sont pas pris en charge.
* **Le produit doit exister** : si le produit n’existe pas dans [!DNL Commerce Optimizer], la couche n’est pas créée pour ce mappage produit-ressource.

## Conditions préalables

Avant de configurer l’intégration, vérifiez les points suivants :

* Une instance [!DNL Adobe Commerce Optimizer] active avec les droits **Visuels de produit** (regroupe Dynamic Media avec des fonctionnalités OpenAPI + [AEM Assets Prime](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-prime)) ou une licence AEM Assets fournie par le client (par exemple, **AEM Assets Ultimate**) avec Dynamic Media activé.
* Accès à un environnement AEM Assets as a Cloud Service.
* [!DNL Commerce Optimizer] et AEM Assets dans la même organisation Adobe IMS.
* Dynamic Media avec OpenAPI activé dans votre environnement AEM Assets (voir [Configuration du projet AEM Assets](configure-aem.md#prerequisites) pour les étapes d’activation).

### Configurer AEM Assets en premier

Pour prendre en charge l’intégration, configurez le projet AEM Assets et les environnements avant de commencer le processus d’intégration d’AEM Assets à [!DNL Commerce Optimizer]. Cela inclut l’activation de Dynamic Media avec les fonctionnalités OpenAPI et la mise à disposition des schémas de métadonnées, des événements et de l’interface utilisateur de Commerce dans votre projet AEM.

* [!BADGE Recommandé]{type=Positive} Dans les versions `2026.5.26309` et ultérieures d’AEM, activez l’intégration à partir de Cloud Manager sans déploiement de code. Suivez [Activation de l’intégration de Commerce (libre-service)](configure-aem.md#enable-aem-commerce-self-service).

* Dans les versions antérieures d’AEM, déployez manuellement le package `assets-commerce`.
Suivez [Installation manuelle du package Assets-Commerce](configure-aem.md#install-the-assets-commerce-package-manually).

>[!TIP]
>
> Vous pouvez vérifier la version actuelle d’AEM dans le menu supérieur droit : **[!UICONTROL Help]** > **[!UICONTROL About AEM]**.

## Intégration

>[!IMPORTANT]
>
>Avant d’envoyer un ticket d’assistance pour activer l’intégration à [!DNL Commerce Optimizer], suivez la procédure de [Configuration d’AEM Assets](#configure-aem-assets-first). La prise en charge nécessite que les environnements et le projet AEM Assets soient configurés pour prendre en charge l’intégration d’AEM Commerce, y compris le déploiement du package `assets-commerce` (ou de l’équivalent en libre-service) pour les métadonnées et les événements. L’ouverture d’un ticket avant la configuration d’AEM peut retarder l’intégration.

Pour intégrer l’intégration d’AEM Assets à [!DNL Commerce Optimizer], l’assistance Adobe doit enregistrer votre instance Adobe Commerce Optimizer auprès du service d’intégration d’Assets et l’abonner à :

* Événements AEM Assets (ressource approuvée, mise à jour, supprimée)
* Événements de catalogue [!DNL Commerce Optimizer] (produit créé, mis à jour)

Pour lancer ce processus, [créez un ticket d’assistance](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) qui contient les informations suivantes :

* **[!DNL Adobe Commerce Optimizer]ID de client** (ID d’instance) trouvé dans l’URL [!DNL Commerce Optimizer] ou l’interface utilisateur de Commerce Cloud Manager.
* **ID de programme AEM et ID d’environnement** que vous configurez lorsque vous [avez configuré AEM Assets](#configure-aem-assets-first) pour l’intégration.
* **Règle de correspondance** : correspondance par SKU ou [correspondance externe (App Builder)](../synchronize/custom-match.md){target=_blank}.
* **Couche** : nom de la couche de catalogue avec laquelle enregistrer le client (voir **Contraintes liées à la couche**). Spécifiez un nom personnalisé uniquement si vous le souhaitez. Dans le cas contraire, le **`AEM-Assets`** par défaut est utilisé.
* **Paramètres régionaux** : paramètre régional source du catalogue avec lequel enregistrer le client (par exemple, `en-US`). Ce paramètre régional doit correspondre à celui que vous utilisez dans la vue de catalogue et les données du catalogue de produits.

### Configuration de la vue du catalogue

Une fois le client [!DNL Commerce Optimizer] enregistré, configurez votre vue de catalogue afin que le storefront et les API affichent les données d’image pilotées par AEM :

* **Sélectionner la source du catalogue (paramètres régionaux)** — Sélectionnez les paramètres régionaux que vous avez spécifiés dans votre ticket d’assistance (par exemple, **`en-US`**). L’intégration enregistre un paramètre régional par client ; une incohérence empêche les images synchronisées d’apparaître dans la vue de catalogue prévue.
* **Attribuer la couche Catalogue** — Attribuez la couche **`AEM-Assets`** (ou votre nom de couche personnalisé à partir du ticket) à cette vue de catalogue.

Si le paramètre régional ou le calque n’est pas affecté correctement, les données d’image n’apparaissent **pas** ou se comportent de manière inattendue, même si la synchronisation a réussi en amont.

## Synchronisation

Une fois configurée, l’intégration synchronise automatiquement les mappages `product-asset`.

Voir [Correspondance automatique personnalisée](../synchronize/custom-match.md) pour plus d’informations.

### Exemple de workflow Correspondance par SKU

Flux type lors de l’ajout d’une ressource existante à un nouveau produit :

1. Créer le produit dans [!DNL Commerce Optimizer] (via l’API ou l’ingestion de données). Le produit peut exister sans images au départ.

1. Dans AEM Assets, ouvrez la ressource que vous souhaitez mapper au produit.

1. Ajoutez le SKU du produit aux métadonnées **commerce:skus** et attribuez des rôles d’image (par exemple, `thumbnail`, `image`).

1. Valider la ressource à diffuser. Cela déclenche l’événement que le service d’intégration d’Assets traite.

1. Le service d’intégration d’Assets envoie le mappage produit-image à [!DNL Commerce Optimizer]. Le produit en [!DNL Commerce Optimizer] est mis à jour avec les images de la ressource.

1. Vérifiez que l’image est visible. Patientez quelques minutes pour que la synchronisation se termine, puis vérifiez le produit dans l’interface utilisateur de [!DNL Commerce Optimizer] ou interrogez les API storefront pour confirmer que l’image est renvoyée.

## Gestion des rôles d’image

Lorsqu’un produit comporte plusieurs ressources utilisant le même rôle d’image (par exemple, deux ressources avec le rôle `thumbnail`), l’intégration garantit qu’une seule ressource conserve ce rôle afin d’éviter les rôles en double dans la couche de [!DNL Commerce Optimizer] et un comportement de storefront inattendu.

**Comportement :** lorsqu’une mise à jour est envoyée depuis AEM Assets, la ressource la plus récemment mise à jour reçoit le rôle d’image (par exemple, `thumbnail`) et le rôle est supprimé de la ressource précédente qui l’avait. Cela empêche l’affichage de rôles d’image en double dans le storefront.

## Plus comme ceci

* [Visuels du produit](../../optimizer/setup/product-visuals.md)
* [Configuration du projet AEM Assets](configure-aem.md)
* [Correspondance automatique personnalisée](../synchronize/custom-match.md)
* [Présentation de l’intégration d’AEM Assets](../overview.md)
