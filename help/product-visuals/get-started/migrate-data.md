---
title: Migrer des fichiers multimédias vers AEM
description: Migrez les fichiers multimédias depuis Adobe Commerce ou une source externe dans la gestion des ressources numériques AEM Assets.
feature: CMS, Media, Integration
source-git-commit: b6e190e883087a942630f0a27781654cd2c68781
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 0%

---


# Migrer des fichiers multimédias vers la gestion des ressources numériques AEM Assets

Adobe Commerce et Adobe Experience Manager (AEM) fournissent des fonctionnalités intégrées pour rationaliser la migration des fichiers multimédias de Commerce vers AEM Assets **système de gestion des ressources numériques (DAM)**. Vous pouvez également migrer des fichiers multimédias provenant d’autres sources.

## Conditions préalables

| Catégorie | Exigence |
|----------|-------------|
| **Configuration requise** | <ul><li>Environnement AEM as a Cloud Service configuré avec AEM Assets</li><li>Capacité de stockage suffisante</li><li>Bande passante réseau pour les transferts de fichiers volumineux</li></ul> |
| **Accès et autorisations requis** | <ul><li>Accès des administrateurs à AEM Assets as a Cloud Service</li><li>Accès au système source où sont stockés les fichiers multimédias (Adobe Commerce ou système externe)</li><li>Autorisations appropriées pour accéder aux services de stockage dans le cloud</li></ul> |
| **Compte d’espace de stockage** | <ul><li>Compte de stockage Blob AWS S3 ou Azure</li><li>Configuration de conteneur/compartiment privé</li><li>Informations d’identification d’authentification</li></ul> |
| **Contenu Source** | <ul><li>Fichiers multimédias organisés prêts pour la migration</li><li>Fichiers image et vidéo dans des <a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/file-format-support#image-formats">formats pris en charge par AEM Assets</a>.</li><li>Nettoyer les ressources dupliquées</li></li> |
| **Préparation des métadonnées** | <ul><li><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/aem-asset-management/getting-started/aem-assets-configure-aem">Profil de métadonnées AEM Assets configuré pour les ressources Commerce</a></li><li>Valeurs de métadonnées mappées pour chaque ressource</li><li>Éditeur de fichier CSV (par exemple, Microsoft Excel)</li></ul> |

## Bonnes pratiques de migration

1. Traitez les ressources avant la migration en supprimant le contenu inutilisé et en double.

1. Organisez les ressources de manière logique par taille, format ou cas d’utilisation.

1. Envisagez de diviser les migrations importantes en lots plus petits.

1. Planifiez les importations gourmandes en ressources pendant les heures creuses.

1. Validez le mappage des métadonnées avant l’importation complète.

## Workflow de migration

Suivez le workflow de migration pour exporter des fichiers multimédias depuis Adobe Commerce ou un autre système externe et les importer dans la gestion des ressources numériques d’AEM Assets.

### Étape 1 : Exporter le contenu de la source de données existante

[!BADGE PaaS uniquement]{type=Informative tooltip="S’applique uniquement à Adobe Commerce sur les projets cloud (infrastructure PaaS gérée par Adobe)."}

Pour les commerçants Adobe Commerce, le **module de stockage à distance** peut faciliter l’importation et l’exportation de fichiers multimédias. Ce module permet aux entreprises de stocker et de gérer des fichiers multimédias à l’aide de services de stockage à distance tels qu’AWS S3. Pour configurer le stockage distant de votre instance Commerce, consultez [Configurer le stockage distant](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/storage/remote-storage/remote-storage-aws-s3) dans le **Guide de configuration de Commerce**.

Si des fichiers multimédias sont stockés en dehors d’Adobe Commerce, chargez-les directement vers l’une des [sources de données](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/bulk-import-assets-view#prerequisites) prises en charge par AEM as a Cloud Service.

### Étape 2 : créer un fichier CSV pour le mappage des métadonnées

Après avoir exporté les fichiers multimédias, créez un fichier CSV pour mapper ces ressources avec les métadonnées nécessaires à l’automatisation. Le fichier CSV doit inclure des champs pour **product**, **position** et **role mapping**, pour garantir l’alignement avec le [profil de métadonnées AEM Assets](configure-aem.md#configure-a-metadata-profile).

Pour chaque fichier multimédia que vous prévoyez de migrer, saisissez les valeurs des champs de métadonnées inclus dans le [profil de métadonnées AEM Assets pour les ressources Commerce](configure-aem.md) comme décrit dans le tableau suivant.

| Métadonnées | Description | Valeur |
|-------|-------------|--------|
| assetPath | Chemin d’accès complet où la ressource sera stockée dans le référentiel AEM Assets.<br><br>Utilisez le chemin d’accès pour créer des sous-dossiers afin d’organiser les ressources Commerce, par exemple les `content/dam/commerce/<brand>/<type>`. | `/content/dam/commerce/<sub-folder>/..<filename>` |
| commerce:positions | Position/ordre de la ressource dans les galeries de produits | Plusieurs valeurs numériques séparées par des barres verticales (voir le fichier csv) |
| commerce:isCommerce | Indicateur signalant si la ressource est utilisée dans Commerce | `Yes` |
| commerce:sku | SKU de produit associés à cette ressource | Plusieurs valeurs de chaîne séparées par une barre verticale (voir le fichier csv) |
| commerce:roles | Les rôles ou types d’images pour la ressource (par exemple, `thumbnail`, `main image`, `swatch`) | Plusieurs valeurs séparées par des points-virgules (par exemple, « miniature ; image ; image_échantillon ; image_petite ») |

+++Code CSV

Utilisez cet exemple de code CSV pour créer le fichier dans un éditeur de code ou une tableur telle que Microsoft Excel.

```csv
assetPath,commerce:positions{{Number: multi}},commerce:isCommerce{{String}},commerce:skus{{String: multi}},commerce:roles{{String: multi}}
/content/dam/commerce/sample1.jpg,1,Yes,sku1,thumbnail; image; swatch_image; small_image
/content/dam/commerce/sample2.jpg,1|1|1,Yes,sku1|sku2|sku3,thumbnail; image; swatch_image; small_image|image|image; small_change
```

+++

### Étape 3 : Importer en bloc Assets dans AEM Assets

Après avoir créé le fichier de mappage de métadonnées, utilisez l’outil d’importation en bloc AEM Assets pour importer vos ressources.

Voici un aperçu général de l’utilisation de l’outil.

1. [Connectez-vous à votre environnement de création AEM Assets as a Cloud Service](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/aem-users#login-aem).

1. Dans la vue Outils Experience Manager, sélectionnez **[!UICONTROL Assets]** > **[!UICONTROL Bulk Import]**.

   ![Création AEM Assets](../assets/aem-assets-bulk-import-selection.png){width="600" zoomable="yes"}

1. Dans les configurations d’importation en bloc, sélectionnez **[!UICONTROL Create]** pour ouvrir le formulaire de configuration.

   ![Création AEM Assets](../assets/aem-assets-bulk-import-configuration.png){width="600" zoomable="yes"}

1. Configurez et enregistrez la configuration.

   Vous aurez besoin de :

   * Informations d’authentification pour la source de données
   * Le dossier cible dans AEM Assets où seront stockés les fichiers importés
   * Facultatif. Informations sur les types MIME, la taille de fichier et d’autres paramètres permettant de personnaliser la configuration de l’importation
   * Chemin d’accès au fichier CSV de mappage de métadonnées que vous avez chargé dans l’instance d’espace de stockage.

   Pour obtenir des instructions détaillées, consultez [Configuration de l’outil d’importation en bloc](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/add-assets#configure-bulk-ingestor-tool) dans le *Guide de l’utilisateur d’AEM Assets as a Cloud Service*.

1. Après avoir enregistré la configuration, utilisez les outils d’importation en bloc pour tester et exécuter l’opération d’importation.

>[!MORELIKETHIS]
>
> [ Démonstration vidéo de l’outil d’importation en bloc ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/add-assets#asset-bulk-ingestor)
> &#x200B;> [Conseils, bonnes pratiques et restrictions](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/add-assets#tips-limitations)
> &#x200B;> [Chargement ou ingestion de ressources à l’aide d’API](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/admin/developer-reference-material-apis#asset-upload)
