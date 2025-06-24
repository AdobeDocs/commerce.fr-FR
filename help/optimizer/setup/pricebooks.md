---
title: Livres de prix
description: Découvrez comment gérer les tarifs dans  [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
source-git-commit: 553490762ef10e43ccce1654acec59aeb83bb5f9
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---

# Livres de prix

Cet article décrit comment définir et affecter des tarifs aux vues de catalogue avec des contrôles appropriés de la gouvernance des données.

Consultez la [documentation pour les développeurs](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/api-reference/#tag/Price-Books) pour savoir comment ingérer des informations de catalogue des prix d’un système tiers dans [!DNL Adobe Commerce Optimizer] à l’aide de l’API Price Book.

Grâce aux livres de tarification, vous pouvez définir des sources de catalogue de tarification afin de gérer les prix des produits sur différents niveaux de client et marchés. Les livres de prix prennent en charge un modèle hiérarchique, permettant jusqu&#39;à trois niveaux de livres de prix enfants imbriqués sous chaque livre de prix de base. Chaque catalogue de prix peut référencer un catalogue de prix parent, formant une arborescence pour les sources de catalogue de prix.

Le livre de prix de base définit la devise pour lui-même et tous ses livres de prix enfants. Les livres de prix enfants héritent de cette devise et ne peuvent pas la remplacer.

## Concepts clés

| Terme | Description |
|------|-------------|
| **Prix catalogue** | Regroupement logique qui définit la source du catalogue des prix ; par exemple, une région spécifique ou le niveau client et qui est utilisé pour gérer les prix des produits. |
| **Livre de prix de secours** | Classement des prix le plus élevé dans une hiérarchie. Il n&#39;a pas de parent et est le *seul* catalogue de prix qui définit la devise pour lui-même et tous ses catalogues de prix descendants.<br/><br/>Si aucun parent n&#39;est défini lors de la création du catalogue des prix (via l&#39;API), un nouveau catalogue des prix de secours est créé. |
| **Catalogue de prix parent** | Un catalogue de prix de niveau supérieur à partir duquel un catalogue de prix enfant peut hériter des prix s&#39;ils ne sont pas explicitement définis dans le catalogue enfant. |
| **Profondeur de hiérarchie** | 3 niveaux maximum (secours → enfant → petit-enfant)<br/><br/>non appliqués au moment de l’ingestion. |
| **Devise** | Défini uniquement sur le catalogue de prix de secours. Hérité par tous les enfants, les livres de prix.<br/><br/>Si la devise n’est pas spécifiée lors de la création du catalogue de prix de secours (via l’API), la devise par défaut est USD. |
| **Prix du produit** | Prix spécifique attribué à un produit (SKU) dans un catalogue de prix particulier. |
| **Remises** | Les remises sont définies dans le prix du produit. Non hérité. |
