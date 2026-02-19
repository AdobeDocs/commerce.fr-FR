---
title: Configuration de l’intégration
description: Découvrez comment connecter votre projet Adobe Commerce et vos projets Experience Manager Assets pour activer la synchronisation des ressources entre ces deux systèmes.
feature: CMS, Media
exl-id: 3533d010-926f-4d78-935c-98a9b7040d27
source-git-commit: d59c9d179018318d7a0ab1685d8e9e172eefa3ed
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 0%

---

# Configuration de l’intégration

Configurez l’intégration en connectant Commerce à l’instance AEM Assets et en sélectionnant la stratégie correspondante pour la synchronisation des ressources.

Après avoir identifié le projet AEM Assets, sélectionnez la règle correspondante pour synchroniser les ressources entre Adobe Commerce et AEM Assets.

* **[!UICONTROL Match by product SKU]** : règle par défaut qui associe le SKU dans les métadonnées de ressource au [SKU de produit Commerce](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/glossary#sku) pour s’assurer que les ressources sont associées aux produits appropriés.

* **[!UICONTROL Custom match]** : règle de correspondance pour les scénarios plus complexes ou pour les besoins spécifiques de l&#39;entreprise qui nécessitent une logique de correspondance personnalisée. L’implémentation d’une correspondance personnalisée nécessite le développement d’un code personnalisé dans Adobe Developer App Builder pour définir la manière dont les ressources sont associées aux produits. Plus de détails bientôt disponibles...

Pour la configuration initiale, utilisez la règle par défaut *Correspondance par sku de produit*.

## Conditions requises

Avant de configurer l’intégration AEM Assets, vérifiez que vous avez effectué les étapes suivantes :

* [Configuration du projet AEM Assets](configure-aem.md)

* [!BADGE PaaS uniquement]{type=Informative tooltip="S’applique uniquement à Adobe Commerce sur les projets cloud (infrastructure PaaS gérée par Adobe)."} [Installez les packages Adobe Commerce](configure-commerce.md) pour ajouter l’extension et générer les informations d’identification et les connexions requises pour utiliser l’extension.

### Autorisations IMS et utilisateur

Pour utiliser le sélecteur de ressources et fournir une configuration plus fluide dans Commerce, les autorisations suivantes sont requises :

>[!BEGINTABS]

>[!TAB  ACCS ]

[!BADGE SaaS uniquement]{type=Positive tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."}

L’authentification IMS est activée par défaut. Ajoutez l’utilisateur au profil de produit **Utilisateurs OpenAPI AEM Assets DM - diffusion** dans le [Adobe Admin Console](https://adminconsole.adobe.com/) pour accorder l’accès à la couche de diffusion AEM Assets.

![Profil de produit Admin Console pour la diffusion AEM Assets](../assets/aem-assets-delivery-product-profile.png){width="600" zoomable="yes"}

>[!TAB  PaaS ]

[!BADGE PaaS uniquement]{type=Informative tooltip="S’applique uniquement à Adobe Commerce sur les projets cloud (infrastructure PaaS gérée par Adobe)."}

1. [Activez Adobe IMS pour Commerce](https://experienceleague.adobe.com/docs/commerce-admin/start/admin/ims/adobe-ims-config.html){target=_blank} en suivant les instructions du *Guide d’administration de Commerce*.

1. [Ouvrez un ticket d’assistance](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#support-cases) pour demander un identifiant client IMS personnalisé pour le sélecteur de ressources.

1. Ajoutez l’utilisateur au profil de produit **Utilisateurs OpenAPI AEM Assets DM - diffusion** dans le [Adobe Admin Console](https://adminconsole.adobe.com/) pour accorder l’accès à la couche de diffusion AEM Assets.

>[!ENDTABS]

## Configurer la connexion

1. Ouvrez la configuration de l’intégration AEM Assets à partir de l’Administration Commerce.

   1. Accédez à **[!UICONTROL Store]** > Configuration > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

      ![L’intégration AEM Assets active l’intégration](../assets/aem-assets-view.png){width="600" zoomable="yes"}

>[!INFO]
>
> L’intégration d’AEM Assets ne prend en charge la configuration qu’à la portée globale (par défaut). La configuration au niveau du site web n’est pas prise en charge. Lorsque vous tentez de configurer l’intégration au niveau du site web, le système ignore les paramètres au niveau du site web et utilise plutôt les valeurs de configuration globales.

1. [!BADGE PaaS uniquement]{type=Informative tooltip="S’applique uniquement à Adobe Commerce sur les projets cloud (infrastructure PaaS gérée par Adobe)."} Saisissez le **[!UICONTROL Asset Selector IMS Client ID]**.

   Cet identifiant est requis pour activer le sélecteur de ressources et remplir automatiquement la fonction pour les champs ID de programme et ID d’environnement . Voir [IMS et autorisations utilisateur](#ims-and-user-permissions) pour obtenir cet identifiant. Pour plus d’informations sur le sélecteur de ressources, voir [Sélection manuelle des ressources](../synchronize/asset-selector-integration.md).

1. Sélectionnez l’environnement AEM Assets **[!UICONTROL Program ID]** et **[!UICONTROL Environment ID]** dans les menus déroulants.

   Les listes déroulantes sont automatiquement renseignées en fonction de la session IMS de l’utilisateur. Pour utiliser cette fonctionnalité, vérifiez que vous disposez des autorisations appropriées [IMS et utilisateur](#ims-and-user-permissions).

   Si les listes déroulantes ne sont pas disponibles, vous pouvez saisir manuellement les identifiants à partir de l’URL AEM Cloud Manager : `https://author-p[Program ID]-e[EnvironmentID].adobeaemcloud.com/`

   Modifiez les valeurs de configuration en supprimant la sélection de *[!UICONTROL Use system value]*.

1. [!BADGE PaaS uniquement]{type=Informative tooltip="S’applique uniquement à Adobe Commerce sur les projets cloud (infrastructure PaaS gérée par Adobe)."} sélectionnez les [[!UICONTROL Commerce integration]](configure-commerce.md#add-the-integration-to-the-commerce-environment) d’authentification des requêtes entre Commerce et le service de correspondance des ressources.

1. Définissez **[!UICONTROL Synchronization enabled]** sur `Yes` pour permettre à Commerce d’accepter les mises à jour entrantes en provenance d’AEM Assets.

   Après avoir activé l’intégration, des options de configuration supplémentaires sont disponibles pour spécifier les critères de correspondance des ressources.

1. Sélectionnez l’une des règles de correspondance de ressources pour la synchronisation des ressources dans la liste déroulante **[!UICONTROL Asset matching rule]** .

   * Sélectionnez **[!UICONTROL Match by SKU]** pour [correspondance automatique par défaut](../synchronize/default-match.md),
   * Sélectionnez **[!UICONTROL Custom match]** pour [correspondance automatique personnalisée](../synchronize/custom-match.md) (nécessite [Adobe Developer App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder).)

1. Ajoutez le [nom du champ de métadonnées AEM Assets](configure-aem.md#configure-metadata) défini pour les SKU de produit Commerce dans le champ **[!UICONTROL Match by product SKU attribute name]**, `commerce:skus` par défaut.

1. Sélectionnez **[!UICONTROL Save Config]** pour appliquer des mises à jour et lancer la synchronisation des ressources.

   La mise à jour de la configuration déclenche le processus de synchronisation initial, ce qui permet à Commerce d’accepter les mises à jour entrantes provenant d’AEM Assets. Le temps nécessaire à la synchronisation dépend du volume de ressources et de configurations spécifiques. L’intégration tire parti de processus automatisés afin de réduire le temps nécessaire à la synchronisation.

### SLA de synchronisation

L’intégration garantit les niveaux de performances de synchronisation suivants :

* `< 5 minutes for 99% of updates`

* `< 30 minutes for 99.9% of updates`

Cela permet de s’assurer que les pages produit affichent toujours les images les plus récentes, en préservant la précision et l’attrait visuel du contenu du storefront.

### Configuration du propriétaire de la visualisation

Le paramètre **Propriétaire de la visualisation** détermine le système qui diffuse les images de produit dans l’intégration :

* Adobe Commerce - Utilise des images hébergées dans Commerce.

* AEM Assets - Utilise des images synchronisées à partir d’AEM.

L’administrateur affiche les images disponibles pour ce propriétaire, tandis que le reste des images est grisé et affiché avec un libellé **masqué**.

Voir la rubrique [Définition des détails de l’image](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/digital-assets/product-image#set-image-details){target=_blank} pour plus d’informations sur le comportement d’affichage des images.

>[!TIP]
>
> Lors d’une migration de Commerce vers AEM Assets, définissez le **Propriétaire de la visualisation** sur Commerce afin d’éviter la rupture des liens d’image. Une fois tous les produits synchronisés avec AEM Assets, basculez vers le propriétaire d’AEM Assets pour terminer la transition. Cela garantit la disponibilité continue des images tout au long du processus.

1. Accédez à **[!UICONTROL Store]** > Configuration > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

   ![Fonction du propriétaire de la visualisation d’intégration AEM Assets](../assets/visualization-owner-detail.png){width="400" zoomable="yes"}

1. Sélectionnez la source **Propriétaire de la visualisation** pour afficher les images.

1. Cliquez sur **[!UICONTROL Save Config]** pour appliquer les mises à jour et lancer la synchronisation des ressources.

### Facultatif. Configuration de l’URL du domaine personnalisé

Si le projet AEM Assets as a Cloud Service a été configuré avec un [nom de domaine personnalisé](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name){target=_blank}, vous devez ajouter le nom de domaine à la configuration du magasin Commerce afin que l’intégration AEM Assets pour Commerce puisse l’utiliser.

1. Accédez à **[!UICONTROL Store]** > Configuration > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

   ![L’intégration AEM Assets active l’intégration](../assets/aem-assets-view.png){width="700" zoomable="yes"}

1. Ajoutez l’**URL de domaine personnalisé** au champ **[!UICONTROL Asset Custom Domain]** .

1. Cliquez sur **[!UICONTROL Save Config]** pour appliquer les mises à jour et lancer la synchronisation des ressources.

## Étape suivante

* **Configurer votre storefront Commerce** : pour utiliser AEM Assets avec le storefront Commerce optimisé par Edge Delivery Services, effectuez la configuration de storefront décrite dans la rubrique [Intégration d’AEM Assets](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/) dans la *documentation du storefront Adobe Commerce*.

* Configurez les [règles correspondantes](../synchronize/default-match.md) entre Adobe Commerce et l’intégration AEM Assets.

* [Gérer les ressources Commerce](../manage-assets.md).
