---
title: Livres de prix
description: Découvrez comment gérer les tarifs dans [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et [!DNL Adobe Commerce Optimizer] (infrastructure SaaS gérée par Adobe)."
exl-id: a1849830-3d0e-4df9-ab73-380659c3f9dc
TQID: https://experienceleague.adobe.com/-vL79MMePcUdhE-gPwjFJZStZUtNLKAUxpePm4Fvmfk
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
source-git-commit: cde6d0c92f4c169588164c22c948d1b287873bdd
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 0%
---
# Livres de prix

Les livres de prix définissent les prix des produits pour une source de catalogue sur plusieurs niveaux de client et marchés. Ils prennent en charge un modèle hiérarchique, permettant jusqu’à trois niveaux de livres de prix enfants imbriqués sous chaque livre de prix de base. Chaque catalogue de prix peut référencer un catalogue de prix parent, formant une arborescence pour les sources de catalogue de prix.

![Hiérarchie du catalogue des prix](../assets/price-book-hier.png)

Le livre de prix de base définit la devise pour lui-même et tous ses livres de prix enfants. Les livres de prix enfants héritent de cette devise et ne peuvent pas la remplacer.

## Concepts clés

| Terme | Description |
| ------ | ------------- |
| **Catalogue De Prix** | Regroupement logique qui définit les prix d’une source de catalogue, par exemple une région spécifique ou le niveau client, et qui est utilisé pour gérer les prix des produits. |
| **Tarif de secours** | Classement des prix le plus élevé dans une hiérarchie. Il n&#39;a pas de parent et est le catalogue de prix *uniquement* qui définit la devise pour lui-même et tous ses catalogues de prix descendants.<br/><br/>Si aucun parent n&#39;est défini lors de la création du catalogue de prix (via l&#39;API), un nouveau catalogue de prix de secours est créé. |
| **Catalogue de prix parent** | Un catalogue de prix de niveau supérieur à partir duquel un catalogue de prix enfant peut hériter des prix s&#39;ils ne sont pas explicitement définis dans le catalogue enfant. |
| **Profondeur De Hiérarchie** | Maximum de trois niveaux (de secours -> enfant -> petit-enfant)<br/><br/>non appliqué au moment de l&#39;ingestion. |
| **Devise** | Défini pour le catalogue de prix de secours uniquement. Hérité par tous les livres de prix enfants.<br/><br/>Si la devise n&#39;est pas spécifiée lors de la création du catalogue de prix de secours (via l&#39;API), la devise par défaut est USD. |
| **Prix du produit** | Prix spécifique attribué à un produit (SKU) dans un catalogue de prix particulier. |
| **Remises** | Les remises sont définies dans le prix du produit. Non hérité. |

## Mise en œuvre du catalogue des prix

L’implémentation du catalogue de prix varie en fonction du déploiement de Commerce.

* Dans les instances Adobe Commerce Optimizer avec des serveurs principaux Commerce tiers, les tarifs sont créés à l’aide de l’API REST d’ingestion de données. Vous pouvez les affecter et les gérer à partir de l’espace de travail Vue catalogue dans Commerce Optimizer Studio.

* Dans Adobe Commerce as a Cloud Service avec le modèle de données de catalogue composable (CCDM), les tarifs sont mappés à partir du catalogue Adobe Commerce et des données de tarification. Vous pouvez afficher les tarifs attribués à chaque vue de catalogue à partir de l’Administration Commerce.

* Dans Adobe Commerce sur les déploiements d’infrastructure cloud ou sur site avec le connecteur Adobe Commerce Optimizer, les tarifs sont également mappés à partir du catalogue Adobe Commerce et des données de tarification. Vous pouvez afficher les tarifs attribués à chaque vue de catalogue à partir de l’espace de travail Vue catalogue dans l’instance Commerce Optimizer connectée.

## Ajouter des tarifs

Vous ajoutez des tarifs à [!DNL Adobe Commerce Optimizer] à l’aide de l’API Price Book. Consultez la [documentation pour les développeurs](https://developer.adobe.com/commerce/services/reference/rest/) pour savoir comment créer, mettre à jour et supprimer des tarifs pour [!DNL Adobe Commerce Optimizer].

## Afficher les registres des prix

Après avoir ingéré des tarifs réduits dans [!DNL Adobe Commerce Optimizer], vous pouvez voir la liste des tarifs réduits et leurs identifiants correspondants sur la page **Vue catalogue**.

>[!NOTE]
>
>Une vue de catalogue privée (une avec [!UICONTROL Catalog Protection] activé) ne peut référencer qu’un seul catalogue de prix. Voir [Restriction du catalogue des prix sur les affichages de catalogue privé](private-catalog-view.md#price-book-restriction-on-private-catalog-views).

1. Accédez à _Configuration du magasin_ , puis cliquez sur **[!UICONTROL Catalog views]**.

1. Cliquez sur **[!UICONTROL Create catalog view]**. &#x200B;

   Dans la configuration des détails de la vue du catalogue, sélectionnez l’un des répertoires de prix disponibles.

   ![Noms et ID de catalogue de prix](../assets/price-book-name-ids.png)

## Configurer la disponibilité du catalogue des prix

Indiquez les données de tarification disponibles pour chaque vue du catalogue en configurant la disponibilité du catalogue pour chaque vue.

1. Dans l’espace de travail **Vue du catalogue**, sélectionnez la vue du catalogue que vous souhaitez configurer.

1. Dans la section [!UICONTROL Price Books], sélectionnez les options du catalogue pour configurer les prix disponibles pour les magasins pris en charge par la vue catalogue.

1. Cliquez sur **[!UICONTROL Save]** pour appliquer les modifications à la vue catalogue.
