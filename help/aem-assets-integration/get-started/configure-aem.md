---
title: Configuration du projet AEM Assets pour la prise en charge des métadonnées Commerce
description: Découvrez comment synchroniser les ressources entre Adobe Commerce et AEM Assets en déployant le package assets-commerce et en configurant les métadonnées Commerce dans votre projet AEM.
feature: CMS, Media, Integration
exl-id: a5d2cbab-5ea1-446b-8ab2-2c638128a40c
TQID: https://experienceleague.adobe.com/QPlM-eeRjJ0gwmpGO4SSYR4PLtL97O-NeozWorDWtv0
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: da3860b0-d637-47df-bef0-273751180266
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: de02e13e169ab336bac09ebff90c44b3b707efce
workflow-type: tm+mt
source-wordcount: 1775
ht-degree: 1%

---

# Configuration du projet AEM Assets pour la prise en charge des métadonnées Commerce

Lorsque vous utilisez AEM Assets en tant que système de gestion des ressources numériques (DAM) pour Commerce, l’installation du package `assets-commerce` vous permet de gérer les images et les vidéos pour les produits Commerce à partir de l’environnement de création AEM.

Suivez les étapes ci-dessous pour configurer le projet AEM Assets avec le code et les métadonnées de package requis pour gérer les ressources Commerce à partir de l’environnement de création AEM :

1. [En savoir plus sur le contenu du package `assets-commerce`](#aem-commerce-assets-commerce-package-contents)

1. [Suivez les étapes d’installation pour configurer le projet AEM Assets afin de prendre en charge les métadonnées Commerce](#step-1-install-the-assets-commerce-package)

## Contenu du package AEM Commerce assets-commerce

Adobe fournit un `assets-commerce` de code de package AEM Commerce pour ajouter des ressources d’espace de noms et de schéma de métadonnées Commerce à la configuration de l’environnement Experience Manager Assets as a Cloud Service.

Ce code de package ajoute les ressources suivantes à l’environnement de création AEM Assets :

* Un [espace de noms personnalisé](https://github.com/ankumalh/assets-commerce/blob/main/ui.config/jcr_root/apps/commerce/config/org.apache.sling.jcr.repoinit.RepositoryInitializer~commerce-namespaces.cfg.json), `Commerce` pour identifier les propriétés liées à Commerce.

   * Un type de métadonnées personnalisé `commerce:isCommerce` avec le libellé `Eligible for Commerce` pour baliser les ressources Commerce associées à un projet Adobe Commerce.

   * Un `commerce:skus` de type de métadonnées personnalisé et un composant d’interface utilisateur correspondant pour ajouter une propriété **[!UICONTROL Product Data]**. Les données de produit incluent les propriétés de métadonnées pour associer une ressource Commerce aux SKU de produit.

     ![Contrôle personnalisé de l’interface utilisateur des données du produit](../assets/aem-commerce-sku-metadata-fields-from-template.png){width="600" zoomable="yes"}

   * Un type de métadonnées personnalisé `commerce:roles` et `commerce:positions` des attributs pour montrer comment la ressource est visualisée dans Commerce.

   * Métadonnées à plusieurs champs de texte secondaire (_[!UICONTROL Alt texts]_) pour permettre aux éditeurs de saisir un texte secondaire indexé par le code d’affichage de la boutique Commerce. Cela ne modifie pas la manière dont les images de produit sont affectées ou la portée dans le catalogue. Voir [&#x200B; Texte de remplacement dans les métadonnées AEM Assets](#localized-alt-text-in-aem-assets-metadata).

* Formulaire de schéma de métadonnées avec un onglet Commerce contenant les champs `Eligible for Commerce` et `Product Data` pour le balisage des ressources Commerce. Le formulaire fournit également des options pour afficher ou masquer les champs `roles` et `position` de l’interface utilisateur d’AEM Assets.

  Onglet ![Commerce du formulaire de schéma de métadonnées AEM Assets](../assets/assets-configure-metadata-schema-form-editor.png){width="600" zoomable="yes"}

* Un [exemple de ressource Commerce balisée et approuvée](https://github.com/ankumalh/assets-commerce/blob/main/ui.content/src/main/content/jcr_root/content/dam/wknd/en/activities/hiking/equipment_6.jpg/.content.xml) `equipment_6.jpg` pour prendre en charge la synchronisation initiale des ressources. Seules les ressources Commerce approuvées peuvent être synchronisées d’AEM Assets vers Adobe Commerce.

>[!NOTE]
>
> Voir la page [readme](https://github.com/ankumalh/assets-commerce) sur GitHub pour plus d’informations sur le **code du package AEM Commerce**.

## Texte de remplacement dans les métadonnées AEM Assets

Le multichamp _[!UICONTROL Alt texts]_&#x200B;est disponible dans l’éditeur de métadonnées de ressource d’AEM Assets dans l’onglet **[!UICONTROL Commerce]**&#x200B;lorsque vous modifiez une image éligible.

>[!IMPORTANT]
>
> Le comportement d’affichage par magasin s’applique uniquement au texte secondaire. L’intégration d’AEM Assets ne synchronise pas les différentes images des produits par vue de magasin Adobe Commerce. Les images de produit d’AEM continuent à se synchroniser dans Commerce avec le même comportement d’affectation de galerie qu’avant cette version.

Le multichamp contient une ligne par vue de magasin Commerce. Chaque ligne comporte deux entrées :

* **[!UICONTROL Store View Code]** — Identifiant de vue de magasin (par exemple `default` ou `en_US`).

* **[!UICONTROL Alt Text]** : texte secondaire pour cette vue de magasin, limité à 255 caractères.

Sélectionnez **[!UICONTROL Add]** pour ajouter d’autres lignes pour les vues de magasin supplémentaires. Pour supprimer une ligne, sélectionnez l’icône **[!UICONTROL Delete]** de cette ligne pour la supprimer.

![Plusieurs champs Texte de remplacement avec des entrées Code d’affichage de magasin et Texte de remplacement](../assets/commerce-metadata-alt-texts-multifield.png){width="600" zoomable="yes"}

Lors de l’enregistrement, la validation côté client bloque l’envoi si une ligne a un _[!UICONTROL Store View Code]_&#x200B;vide ou si deux lignes utilisent le même code d’affichage du magasin (non-respect de la casse).

Les entrées de texte secondaire sont conservées dans les métadonnées de ressource JCR sous la forme de deux propriétés `String[]` alignées sur l’index :

* `commerce:altTextStoreViews` : Stocker le code d’affichage pour chaque ligne.
* `commerce:altTextValues` : Correspondance du texte secondaire au même index que chaque entrée dans `commerce:altTextStoreViews`.

Lorsque ces ressources se synchronisent avec Adobe Commerce, le texte secondaire d’affichage par magasin est écrit dans la galerie de médias du produit pour les codes d’affichage de magasin correspondants. Le mapping d’images sous-jacent reste inchangé.

## Conditions préalables

Vous avez besoin des ressources et autorisations suivantes pour déployer le code du package `assets-commerce` dans l’environnement AEM Assets as a Cloud Service AEM :

* [Accès au programme et aux environnements AEM Assets Cloud Manager](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager#access-sysadmin-bo) avec les rôles Responsable de programme et de déploiement .

* Un [environnement de développement AEM local](https://experienceleague.adobe.com/fr/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview) et une connaissance du processus de développement local d’AEM.

* Découvrez la structure de projet [AEM et comment déployer &#x200B;](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure) packages de contenu personnalisés à l’aide de Cloud Manager.

* L’**ID d’organisation IMS** pour votre instance Commerce. Votre instance Commerce et votre environnement de création AEM Assets doivent se trouver dans la même organisation IMS.

* Pour activer [Dynamic Media avec les fonctionnalités OpenAPI](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/dynamic-media-open-apis-overview#enable-dynamic-media-open-apis) :

>[!BEGINTABS]

>[!TAB Visuels du produit]

[!BADGE SaaS uniquement]{type=Positive url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."} Dynamic Media avec fonctionnalités OpenAPI est en libre-service pour les visuels de produit optimisés par AEM Assets.

1. Accédez à votre Cloud Manager.

1. Sélectionnez l’environnement souhaité.

1. Activez **Dynamic Media avec les fonctionnalités OpenAPI**.

   Si le bouton **Dynamic Media avec fonctionnalités OpenAPI** n’est pas actif, ouvrez un ticket de support.

>[!TAB Tab]

[!BADGE PaaS uniquement]{type=Informative tooltip="S’applique uniquement à Adobe Commerce sur les projets cloud (infrastructure PaaS gérée par Adobe)."} Sur AEM as a Cloud Service, envoyez un ticket d’assistance Adobe avec les informations suivantes :

* Titre : activez l’OpenAPI Dynamic Media pour intégrer entièrement Adobe Commerce à AEM Assets.

   * Contenu du ticket d’assistance :

      * **[!UICONTROL AEM Program ID]**
      * **[!UICONTROL Adobe Commerce URL]**
      * **[!UICONTROL AEM Environment ID]**
      * **[!UICONTROL IMS Org ID]**

Une fois que vous avez envoyé le ticket d’assistance, Adobe active Dynamic Media avec les fonctionnalités OpenAPI dans votre environnement Cloud Services et partage les informations, telles que l’identifiant du client IMS, pour que vous puissiez poursuivre l’intégration.

>[!ENDTABS]

## Étape 1 : installer le package assets-commerce

1. Accédez à AEM Cloud Manager, sélectionnez un programme, puis [créez des environnements de production et d’évaluation](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/onboarding/journey/create-environments#creating-environments) à intégrer à Adobe Commerce.

1. [Clonez le référentiel Git géré par Adobe](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/sites/administering/site-creation/quick-site/retrieve-access#repo-access) pour le programme sélectionné.

   ![Informations d’identification du référentiel Cloud Manager et commande de clonage](../assets/cloud-manager-repository-info.png){width="600" zoomable="yes"}

   Dans Cloud Manager **Pipelines**, sélectionnez **[!UICONTROL Access Repo Info]** pour ouvrir la **[!UICONTROL Repository Info]**. Copiez la valeur **[!UICONTROL URL]** ou **[!UICONTROL Git command line]**, générez un mot de passe d’accès si nécessaire, puis clonez localement avec votre client Git.

1. À partir de GitHub, téléchargez le code du package à partir du [référentiel AEM Assets Commerce](https://github.com/ankumalh/assets-commerce).

1. À partir de votre [environnement de développement AEM local](https://experienceleague.adobe.com/fr/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview), copiez manuellement le code téléchargé dans le référentiel géré par Adobe existant.

1. Dans tous les fichiers `filter.xml` et `pom.xml` de votre projet, remplacez toutes les occurrences de &lt;my-app> par le nom de votre application.

   >[!NOTE]
   >
   > Vous pouvez également installer le code personnalisé dans la configuration de votre projet AEM Assets sous la forme d’un package **Maven**.

1. Validez les modifications et envoyez votre branche de développement local au référentiel Git de Cloud Manager.

1. Configurez un [pipeline de déploiement](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/sites/administering/site-creation/quick-site/pipeline-setup#create-front-end-pipeline) ou vérifiez que votre pipeline peut déployer les modifications dans l’environnement sélectionné.

   ![Pipelines &#x200B;](../assets/cloud-manager-pipelines.png){width="600" zoomable="yes"}

   Lorsque le pipeline existe, ouvrez le menu d’actions (**...**) pour **[!UICONTROL Run]**, **[!UICONTROL Edit]**, **[!UICONTROL View/Edit variables]** ou d’autres actions, consultez la documentation sur le pipeline Cloud Manager liée ci-dessus.

1. Depuis AEM Cloud Manager, [mettez à jour l’environnement AEM à l’aide du pipeline pour déployer votre code](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code#deploying-code-with-cloud-manager).

1. Accédez à n’importe quelle ressource et modifiez ses propriétés pour valider les modifications :

   * Le schéma de métadonnées par défaut inclut l’onglet **&#x200B;**.

   * Les SKU de produit et les champs `Eligible for Commerce` sont visibles.

### L’onglet Commerce n’est pas visible dans les propriétés

Si l’onglet **&#x200B;**&#x200B;n’apparaît pas dans les propriétés, vous devez effectuer manuellement les étapes suivantes dans l’éditeur de schéma de métadonnées :

1. Accédez à l’éditeur de schéma de métadonnées.

1. Sélectionnez **Modifier** pour modifier le formulaire de schéma de métadonnées par défaut.

1. Créez un onglet **&#x200B;**&#x200B;et sélectionnez-le.

1. Faites glisser et déposez le composant **Product** dans l’onglet **Commerce** et mappez-le à la `commerce:skus` de propriété.

1. Cochez la case **Afficher les rôles** et **Afficher l’ordre**.

1. Faites glisser et déposez un composant **case à cocher** dans l’onglet **Commerce** et mappez-le à l’`commerce:isCommerce` de propriété. Définissez **Oui** et **Non** comme options.

Si vous rencontrez d’autres problèmes, créez un [ticket d’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=fr#submit-ticket) ou contactez votre représentant commercial pour l’intégration AEM Assets pour obtenir de l’aide.

## Étape 2 : Facultatif. Configuration d’un profil de métadonnées

Dans l’environnement de création AEM Assets, définissez les valeurs par défaut des métadonnées de ressources Commerce en créant un profil de métadonnées. Appliquez ensuite le nouveau profil aux dossiers AEM Assets pour utiliser automatiquement ces paramètres par défaut. Cette configuration simplifie le traitement des ressources en réduisant les étapes manuelles.

Lorsque vous configurez le profil de métadonnées, il vous suffit de configurer les composants suivants :

* Ajoutez un onglet Commerce . Cet onglet active les paramètres de configuration spécifiques à Commerce ajoutés par le modèle.

* Ajoutez le champ `Eligible for Commerce` à l’onglet Commerce .

Le composant d’interface utilisateur des données de produit est ajouté automatiquement en fonction du modèle.

### Définition du profil de métadonnées

1. Connectez-vous à l’environnement de création de Adobe Experience Manager.

1. Dans l’espace de travail Adobe Experience Manager , accédez à l’espace de travail Créer une administration de contenu pour AEM Assets en cliquant sur l’icône Adobe Experience Manager .

   ![Création &#x200B;](../assets/aem-assets-authoring.png){width="600" zoomable="yes"}

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

### Application du profil de métadonnées au dossier source des ressources Commerce

1. Sur la page **[!UICONTROL Metadata Profiles]** , sélectionnez le profil d’intégration de Commerce.

1. Dans le menu d’actions, sélectionnez **[!UICONTROL Apply Metadata Profiles to Folders]**.

1. Sélectionnez le dossier contenant les ressources Commerce.

   Créez un dossier Commerce s’il n’existe pas.

1. Sélectionnez **[!UICONTROL Apply]**.

## Étapes suivantes

* [!BADGE PaaS uniquement]{type=Informative tooltip="S’applique uniquement à Adobe Commerce sur les projets cloud (infrastructure PaaS gérée par Adobe)."} [installer les packages Adobe Commerce](configure-commerce.md).

* [!BADGE SaaS uniquement]{type=Positive url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."} [Configurez l’intégration à partir de l’Administration](setup-synchronization.md).
