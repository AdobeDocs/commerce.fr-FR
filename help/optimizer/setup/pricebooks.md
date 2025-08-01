---
title: Livres de prix
description: Découvrez comment gérer les tarifs dans  [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
exl-id: a1849830-3d0e-4df9-ab73-380659c3f9dc
source-git-commit: 502d8d21ff052f4ecb212176459b38ce51f85dfc
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---

# Livres de prix

Les livres de prix vous permettent de définir les prix de produit pour une source de catalogue sur différents niveaux de client et marchés. Les livres de prix prennent en charge un modèle hiérarchique, permettant jusqu&#39;à trois niveaux de livres de prix enfants imbriqués sous chaque livre de prix de base. Chaque catalogue de prix peut référencer un catalogue de prix parent, formant une arborescence pour les sources de catalogue de prix.

Le livre de prix de base définit la devise pour lui-même et tous ses livres de prix enfants. Les livres de prix enfants héritent de cette devise et ne peuvent pas la remplacer.

Consultez la [documentation destinée aux développeurs](https://developer.adobe.com/commerce/services/reference/rest/) pour savoir comment créer, mettre à jour et supprimer des tarifs à l’aide de l’API Price Book pour les [!DNL Adobe Commerce Optimizer].

## Concepts clés

| Terme | Description |
|------|-------------|
| **Prix catalogue** | Regroupement logique qui définit les prix d’une source de catalogue, par exemple une région spécifique ou le niveau client, et qui est utilisé pour gérer les prix des produits. |
| **Livre de prix de secours** | Classement des prix le plus élevé dans une hiérarchie. Il n&#39;a pas de parent et est le *seul* catalogue de prix qui définit la devise pour lui-même et tous ses catalogues de prix descendants.<br/><br/>Si aucun parent n&#39;est défini lors de la création du catalogue des prix (via l&#39;API), un nouveau catalogue des prix de secours est créé. |
| **Catalogue de prix parent** | Un catalogue de prix de niveau supérieur à partir duquel un catalogue de prix enfant peut hériter des prix s&#39;ils ne sont pas explicitement définis dans le catalogue enfant. |
| **Profondeur de hiérarchie** | Maximum de trois niveaux (Fallback -> Enfant -> Petit-enfant)<br/><br/>non appliqué au moment de l’ingestion. |
| **Devise** | Défini pour le catalogue de prix de secours uniquement. Hérité par tous les livres de prix enfants.<br/><br/>Si la devise n’est pas spécifiée lors de la création du catalogue de prix de secours (via l’API), la devise par défaut est USD. |
| **Prix du produit** | Prix spécifique attribué à un produit (SKU) dans un catalogue de prix particulier. |
| **Remises** | Les remises sont définies dans le prix du produit. Non hérité. |
