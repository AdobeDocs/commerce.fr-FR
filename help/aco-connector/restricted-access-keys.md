---
title: Gestion des clés d’accès restreint pour les catalogues partagés B2B
description: Découvrez comment gérer les clés d’accès restreint utilisées par le connecteur Adobe Commerce Optimizer pour sécuriser les projections de catalogue partagé B2B.
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="PaaS uniquement" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
subfeature_v2:
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
    internal-label: Data Transfer
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
    internal-label: Data management
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
source-git-commit: a3ade1a31d3c2905b601f71bda118de89c43cf59
workflow-type: tm+mt
source-wordcount: '1105'
ht-degree: 0%
---

# Gérer les clés d’accès restreintes pour les catalogues partagés B2B

{type=Caution tooltip="Nécessite l’extension B2B du connecteur Adobe Commerce Optimizer, qui est actuellement en version bêta privée."}

Si vous utilisez [!DNL Adobe Commerce] catalogues partagés B2B avec le [!DNL Adobe Commerce Optimizer Connector B2B extension], l’extension génère et attribue automatiquement la première clé d’accès restreint lors de la création d’une vue de catalogue. Utilisez la page [!UICONTROL Restricted Access Keys] de l’Administration Commerce pour afficher cette clé, ainsi que pour créer, attribuer ou supprimer des clés supplémentaires.

![Clés d’accès restreintes pour les vues de catalogue partagé B2B](assets/restricted-access-keys.png){width="800" zoomable="yes"}

>[!NOTE]
>
>Pour gérer les clés que vous créez manuellement pour des cas d’utilisation non B2B tels que les portails de partenaire, consultez [Clés d’accès restreint](/help/optimizer/setup/restricted-access-keys.md#create-a-restricted-access-key).

## Accès à la page {#access-the-page}

Dans l’administration Commerce, accédez à **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Restricted Access Keys]**.

Vous pouvez attribuer une clé à la vue de catalogue à partir de la grille Catalogue partagé ou de la grille Société. Voir [Attribuer des clés à une vue de catalogue partagée B2B](#assign-keys-to-a-shared-catalog-view).

>[!NOTE]
>
>Pour consulter les champs de cette page, reportez-vous à la section [&#x200B; Gestion des clés d’accès restreint &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/catalog-view-sync/restricted-access-keys){target="_blank"} du *Guide d’administration de Commerce*.—>

## Lorsque vous avez besoin de plus que la clé automatique {#when-you-need-more-than-the-automatic-key}

La clé automatique générée par le [!DNL Adobe Commerce Optimizer Connector B2B extension] couvre la plupart des catalogues partagés B2B sans nécessiter aucune action de votre part. Gérez vous-même les clés dans ces cas :

- **Rotation d’une clé** : créez une clé, affectez-la à la vue de catalogue à côté de la vue existante, confirmez qu’elle fonctionne, puis supprimez l’ancienne clé. La rotation automatique n’est pas encore disponible.
- **Une clé ne parvient pas à lier**—Si [Statut de synchronisation de la vue du catalogue](catalog-view-sync-status.md) affiche une dérive liée à la clé, essayez d’enregistrer à nouveau l’affectation de la vue du catalogue pour réessayer le lien qui a échoué. Si la clé échoue toujours, exécutez [!UICONTROL Reconcile & Repair] pour récupérer la clé ou l’état avant de créer un remplacement. Créez une clé de remplacement uniquement si la clé a expiré ou si l’échec est irrécupérable de manière persistante.
- **Rechercher une clé publique** : sur la page Clés d&#39;accès restreint, sélectionnez **[!UICONTROL View Public Key]** pour afficher et copier la clé publique d&#39;une clé.

Une vue de catalogue peut avoir jusqu’à trois clés affectées à la fois. Lors de la rotation des clés, [!DNL Adobe Commerce Optimizer] accepte les jetons signés par toute clé attribuée non expirée. Il n’existe aucune étape manuelle pour définir une clé « active ».

## Création d’une clé

Sur la page [!UICONTROL Restricted Access Keys], créez une clé en sélectionnant **[!UICONTROL Create Key]**.

Commerce génère une nouvelle paire de clés et contient la clé privée. Le tableau Clés d’accès limité est mis à jour avec une nouvelle entrée de clé indiquant l’ID de clé unique. Utilisez cette [!UICONTROL Key ID] lorsque vous affectez la clé à une vue de catalogue.

La clé publique n’est pas enregistrée auprès de [!DNL Adobe Commerce Optimizer] tant que vous ne l’avez pas affectée à une vue de catalogue. Après enregistrement, l’entrée de table Clé d’accès restreint est mise à jour pour afficher l’affectation du catalogue et la date d’expiration.

## Attribuer des clés à une vue de catalogue projetée à partir du catalogue partagé B2B {#assign-keys-to-a-shared-catalog-view}

Attribuez ou annulez l’attribution des clés de la vue catalogue du compte d’entreprise ou de la page de catalogue partagé, et non de la grille de [!UICONTROL Restricted Access Keys] principale.

Une vue de catalogue doit comporter au moins une clé et peut en contenir trois.

- Si vous essayez d’attribuer une quatrième clé, un message d’erreur s’affiche lorsque vous essayez d’enregistrer la valeur : `A Catalog View can have at most 3 access keys.`
- Si une vue de catalogue ne comporte qu’une seule clé, celle-ci ne peut pas être supprimée ni son affectation annulée.

Pour mettre à jour la configuration de la clé de vue du catalogue, vous pouvez y accéder à partir de la page du compte d’entreprise ou de la page du catalogue partagé.

>[!BEGINTABS]

>[!TAB Gérer les clés d’un compte d’entreprise]

1. Ouvrez la page d’entreprise (**[!UICONTROL Customers]** > **[!UICONTROL Companies]**) à partir de l’Administration de Commerce.

1. Dans [!UICONTROL Action] colonne de la société, sélectionnez [!UICONTROL Edit].

1. Pour afficher la liste des vues de catalogue projetées à partir du catalogue partagé affecté à l’entreprise, développez la section _[!UICONTROL Catalog Views]_.

Cet onglet répertorie les vues de catalogue projetées à partir du catalogue partagé, y compris leurs clés attribuées.

1. Dans la colonne [!UICONTROL Actions] de la vue du catalogue à mettre à jour, sélectionnez **[!UICONTROL Edit Restricted Access Keys]**.

   ![Liste déroulante Modifier les clés d’accès limité affichant les clés affectées à une vue de catalogue](assets/restricted-access-key-selector.png){width="500" zoomable="yes"}

1. Pour attribuer une clé, sélectionnez la liste déroulante **[!UICONTROL Access Keys]** . Sélectionnez ensuite une clé non affectée par le [!UICONTROL key ID], par exemple `#42`. Cliquez ensuite sur [!UICONTROL Done] pour l’affecter à la vue Catalogue.

   Les clés déjà affectées à une autre vue de catalogue sont libellées en conséquence.

1. Pour supprimer un jeton d’accès, supprimez-le du champ [!UICONTROL Access Tokens] en sélectionnant la commande `x` dans le libellé de la clé.

1. Pour enregistrer et appliquer les mises à jour de configuration, sélectionnez **[!UICONTROL Save]**.

>[!TAB Gérer les clés d’un catalogue partagé]

1. Ouvrez la page de catalogue partagé (**[!UICONTROL Catalog]** > **[!UICONTROL Shared catalogs]**) depuis l’interface d’administration de Commerce.

1. Dans [!UICONTROL Action] colonne pour le partagé, choisissez **[!UICONTROL General Settings]** dans le menu [!UICONTROL Select].

1. Pour afficher la liste des vues de catalogue projetées à partir du catalogue partagé, sélectionnez **[!UICONTROL Catalog Views]** dans le menu [!UICONTROL Shared Catalog Information].

La page [!UICONTROL Catalog Views] répertorie l’identifiant de la vue de catalogue, la vue de magasin associée et la clé d’accès pour chaque vue de catalogue.

1. Dans la colonne [!UICONTROL Actions] de la vue du catalogue à mettre à jour, sélectionnez **[!UICONTROL Edit Restricted Access Keys]**.

   ![Liste déroulante Modifier les clés d’accès limité affichant les clés affectées à une vue de catalogue](assets/restricted-access-key-selector.png){width="500" zoomable="yes"}

1. Pour attribuer une clé, sélectionnez la liste déroulante **[!UICONTROL Access Keys]** . Sélectionnez ensuite une clé non affectée à l’aide du titre de clé par défaut, par exemple `#42`. Cliquez ensuite sur [!UICONTROL Done] pour l’affecter à la vue Catalogue.

   Les clés déjà affectées à une autre vue de catalogue sont libellées en conséquence.

1. Pour supprimer un jeton d’accès, supprimez-le du champ [!UICONTROL Access Tokens] en sélectionnant la commande `x` dans le libellé de la clé.

1. Pour enregistrer et appliquer les mises à jour de configuration, sélectionnez **[!UICONTROL Save]**.

>[!ENDTABS]

## Gérer l’expiration et le renouvellement des clés

Vous pouvez configurer la durée de vie par défaut des clés à accès restreint. La valeur détermine la date d’expiration définie lorsque l’extension [!DNL Adobe Commerce Optimizer Connector B2B] génère la clé initiale ou lorsque vous créez une clé manuellement.

La date d’expiration s’affiche dans la colonne [!UICONTROL Expires At] de la page [!UICONTROL Restricted Access Keys].

Pour modifier la durée, accédez à **[!UICONTROL Stores]** > [!UICONTROL Settings] > **[!UICONTROL Configuration]** > **[!UICONTROL Services]** > **[!UICONTROL ACO Restricted Access Keys]**. Sur la page [!UICONTROL Provisioning], mettez à jour le champ **[!UICONTROL Default Key Expiry (days)]** . La durée de vie par défaut de la clé système est initialement définie pour une période prolongée (~100 ans). Veillez à la mettre à jour avec une valeur correspondant à vos politiques de sécurité.

### Renouvellement de clé

Lorsqu’une clé est dans les 10 jours suivant son expiration, la page [!UICONTROL Restricted Access Keys] affiche une icône d’avertissement en regard de son entrée. Si vous ne renouvelez pas la clé avant son expiration, la vue du catalogue devient inaccessible jusqu’à ce que vous attribuiez une nouvelle clé.

Vous pouvez créer et attribuer une nouvelle clé à tout moment, puis supprimer l’ancienne après avoir confirmé que la nouvelle clé fonctionne.

## Limites connues

La rotation automatique des clés n’est pas encore disponible.

>[!MORELIKETHIS]
>
> - [Gérer les clés d’accès restreint](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/catalog-view-sync/restricted-access-keys){target="_blank"} — Référence complète des champs pour cette page, dans le *Guide d’administration de Commerce* —>
> - [Surveillance de la synchronisation des vues du catalogue](catalog-view-sync-status.md) — Surveillez les vues du catalogue protégées par ces clés
> - [Vues de catalogue privé](/help/optimizer/setup/private-catalog-view.md) — Découvrez ce qu’est une vue de catalogue privé gérée par connecteur
> - [Clés d’accès restreint](/help/optimizer/setup/restricted-access-keys.md) — Découvrez comment fonctionne le flux de clés manuel basé sur ACO Studio pour les cas d’utilisation non-B2B
