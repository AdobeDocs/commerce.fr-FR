---
title: Configuration du projet AEM Assets
description: Activez la synchronisation transparente des ressources entre Adobe Commerce et AEM Assets en ajoutant les métadonnées requises pour l’intégration.
feature: CMS, Media, Integration
exl-id: a5d2cbab-5ea1-446b-8ab2-2c638128a40c
source-git-commit: 995fb071953ddad6cb2076207910679905bb0347
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 0%

---

# Configuration du projet AEM Assets pour la prise en charge des métadonnées Commerce

Pour gérer les fichiers de ressources Commerce dans AEM Assets, procédez comme suit pour configurer le projet AEM Assets avec le code standard et les métadonnées nécessaires pour gérer les ressources Commerce à partir de l’environnement de création AEM.

* **Étape 1 :** installez un modèle de projet AEM avec le code standard pour ajouter les ressources d’espace de noms et de schéma de métadonnées Commerce à la configuration de l’environnement Experience Manager Assets as a Cloud Service.
* **Étape 2 :** configurer le profil de métadonnées à appliquer aux fichiers de ressources Commerce

## Ajouter le code standard à votre projet AEM

Adobe fournit un modèle AEM Commerce, `assets-commerce`, pour ajouter des ressources d’espace de noms Commerce et de schéma de métadonnées à la configuration de l’environnement Experience Manager Assets as a Cloud Service. Déployez ce code dans votre environnement en tant que package **Maven**. Configurez ensuite les métadonnées Commerce dans l’environnement de création AEM Assets pour terminer la configuration.

Le modèle standard ajoute les ressources suivantes à l’environnement de création AEM Assets :

* Un [espace de noms personnalisé](https://github.com/ankumalh/assets-commerce/blob/main/ui.config/jcr_root/apps/commerce/config/org.apache.sling.jcr.repoinit.RepositoryInitializer~commerce-namespaces.cfg.json), `Commerce` pour identifier les propriétés liées à Commerce.

   * Un type de métadonnées personnalisé `commerce:isCommerce` avec le libellé `Eligible for Commerce` pour baliser les ressources Commerce associées à un projet Adobe Commerce.

   * Un `commerce:skus` de type de métadonnées personnalisé et un composant d’interface utilisateur correspondant pour ajouter une propriété **[!UICONTROL Product Data]**. Les données de produit incluent les propriétés de métadonnées pour associer une ressource Commerce aux SKU de produit.

     ![Contrôle personnalisé de l’interface utilisateur des données du produit](../assets/aem-commerce-sku-metadata-fields-from-template.png){width="600" zoomable="yes"}

   * Un type de métadonnées personnalisé `commerce:roles` et `commerce:positions` des attributs pour montrer comment la ressource est visualisée dans Commerce.

* Formulaire de schéma de métadonnées avec un onglet Commerce contenant les champs `Eligible for Commerce` et `Product Data` pour le balisage des ressources Commerce. Le formulaire fournit également des options pour afficher ou masquer les champs `roles` et `position` de l’interface utilisateur d’AEM Assets.

  Onglet ![Commerce du formulaire de schéma de métadonnées AEM Assets](../assets/assets-configure-metadata-schema-form-editor.png){width="600" zoomable="yes"}

* Un [exemple de ressource Commerce balisée et approuvée](https://github.com/ankumalh/assets-commerce/blob/main/ui.content/src/main/content/jcr_root/content/dam/wknd/en/activities/hiking/equipment_6.jpg/.content.xml) `equipment_6.jpg` pour prendre en charge la synchronisation initiale des ressources. Seules les ressources Commerce approuvées peuvent être synchronisées d’AEM Assets vers Adobe Commerce.

>[!NOTE]
>
> Voir la page [readme](https://github.com/ankumalh/assets-commerce) pour plus d&#39;informations sur le modèle AEM Commerce **&#x200B;**.

### Conditions préalables

Vous avez besoin des ressources et autorisations suivantes pour déployer le package `commerce-assets` dans l’environnement AEM Assets as a Cloud Service AEM :

* [Accès au programme et aux environnements AEM Assets Cloud Manager](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager#access-sysadmin-bo) avec les rôles Responsable de programme et de déploiement .

* Un [environnement de développement AEM local](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview) et une connaissance du processus de développement local d’AEM.

* Découvrez la structure de projet [AEM et comment déployer ](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure) packages de contenu personnalisés à l’aide de Cloud Manager.

### Installation du package `commerce-assets`

1. Dans AEM Cloud Manager, créez des environnements de production et d’évaluation pour votre projet AEM Assets, si nécessaire.

1. Configurez un pipeline de déploiement, si nécessaire.

1. À partir de GitHub, téléchargez le code à partir du fichier standard AEM Commerce [&#128279;](https://github.com/ankumalh/assets-commerce).

1. À partir de votre [environnement de développement AEM local](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview), installez le code personnalisé dans la configuration de votre environnement AEM Assets sous la forme d’un package Maven ou en copiant manuellement le code dans la configuration du projet existant.

1. Validez les modifications et envoyez votre branche de développement local au référentiel Git de Cloud Manager.

1. Depuis AEM Cloud Manager, [déployez votre code pour mettre à jour l’environnement AEM](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code#deploying-code-with-cloud-manager).

## Facultatif. Configuration d’un profil de métadonnées

Dans l’environnement de création AEM Assets, définissez les valeurs par défaut des métadonnées de ressources Commerce en créant un profil de métadonnées. Appliquez ensuite le nouveau profil aux dossiers AEM Assets pour utiliser automatiquement ces paramètres par défaut. Cette configuration simplifie le traitement des ressources en réduisant les étapes manuelles.

Lorsque vous configurez le profil de métadonnées, il vous suffit de configurer les composants suivants :

* Ajoutez un onglet Commerce . Cet onglet active les paramètres de configuration spécifiques à Commerce ajoutés par le modèle
* Ajoutez le champ `Eligible for Commerce` à l’onglet Commerce .

Le composant d’interface utilisateur des données de produit est ajouté automatiquement en fonction du modèle.

### Définition du profil de métadonnées

1. Connectez-vous à l’environnement de création de Adobe Experience Manager.

1. Dans l’espace de travail Adobe Experience Manager , accédez à l’espace de travail Créer une administration de contenu pour AEM Assets en cliquant sur l’icône Adobe Experience Manager .

   ![Création AEM Assets](../assets/aem-assets-authoring.png){width="600" zoomable="yes"}

1. Ouvrez les outils d’administration en sélectionnant l’icône en forme de marteau.

   ![L’administrateur de création AEM gère les profils de métadonnées](../assets/aem-manage-metadata-profiles.png){width="600" zoomable="yes"}

1. Ouvrez la page de configuration du profil en cliquant sur **[!UICONTROL Metadata Profiles]**.

1. **[!UICONTROL Create]** un profil de métadonnées pour l’intégration de Commerce.

   ![L’administrateur de création AEM ajoute des profils de métadonnées](../assets/aem-create-metadata-profile.png){width="600" zoomable="yes"}

1. Ajoutez un onglet pour les métadonnées Commerce.

   1. Sur la gauche, cliquez sur **[!UICONTROL Settings]**.

   1. Cliquez sur **[!UICONTROL +]** dans la section d’onglet, puis spécifiez le **[!UICONTROL Tab Name]**, `Commerce`.

1. Ajoutez le champ `Eligible for Commerce` au formulaire.

   ![L’administrateur de création AEM ajoute des champs de métadonnées au profil](../assets/aem-edit-metadata-profile-fields.png){width="600" zoomable="yes"}

   * Cliquez sur **[!UICONTROL Build form]**.

   * Faites glisser le champ `Single Line text` vers le formulaire.

   * Ajoutez le texte `Eligible for Commerce` pour le libellé en cliquant sur **[!UICONTROL Field Label]**.

   * Dans l’onglet Paramètres , ajoutez le texte du libellé à **Libellé du champ**.

   * Définissez le texte d’espace réservé sur `yes`.

   * Dans le champ **[!UICONTROL Map to Property]** , copiez et collez la valeur suivante :

     ```terminal
     ./jcr:content/metadata/commerce:isCommerce
     ```

1. Facultatif. Pour synchroniser automatiquement les ressources Commerce approuvées lors de leur chargement dans l’environnement AEM Assets, définissez la valeur par défaut du champ _[!UICONTROL Review Status]_&#x200B;de l’onglet `Basic` sur `approved`.

1. Enregistrez la mise à jour.

#### Application du profil de métadonnées au dossier source des ressources Commerce

1. Sur la page [!UICONTROL &#x200B; Metadata Profiles], sélectionnez le profil d’intégration de Commerce.

1. Dans le menu d’actions, sélectionnez **[!UICONTROL Apply Metadata Profiles to Folders]**.

1. Sélectionnez le dossier contenant les ressources Commerce.

   Créez un dossier Commerce s’il n’existe pas.

1. Cliquez sur **[!UICONTROL Apply]**.

## Étape suivante

[!BADGE PaaS uniquement]{type=Informative tooltip="S’applique uniquement à Adobe Commerce sur les projets cloud (infrastructure PaaS gérée par Adobe)."} [installer les packages Adobe Commerce](configure-commerce.md)
