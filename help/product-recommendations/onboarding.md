---
title: Intégration
description: Découvrez les exigences et les plateformes prises en charge dans  [!DNL Product Recommendations].
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---

# Intégration

Le processus d’intégration pour [!DNL Product Recommendations] nécessite l’accès à la ligne de commande du serveur et comprend les étapes suivantes. Si vous n’êtes pas familier avec le fonctionnement depuis la ligne de commande, demandez de l’aide à un développeur ou à un intégrateur système.

- [Workflow de mise en œuvre](implementation-workflow.md)
- [Installation et configuration](install-configure.md)
- [Paramètres](settings.md)
- [Vérifier](verify.md)
- [Environnement d’évaluation](staging-environment.md)

## Conditions requises

- Adobe Commerce 2.4.4+
- PHP 8.1, 8.2
- Compositeur 2

### Plateformes prises en charge

- Adobe Commerce on premise (EE) : 2.4.4+
- Adobe Commerce on Cloud (ECE) : 2.4.4+

## Point d’entrée

[!DNL Product Recommendations] communique via le point d’entrée à l’adresse `https://catalog-service.adobe.io/graphql`.

### Prise en charge de Page Builder

[!DNL Product Recommendations] peut être ajouté à une page en tant que type de contenu Page Builder. Pour ajouter la prise en charge de Page Builder aux recommandations de produits, consultez [Installation et configuration](install-configure.md).

Voir [[!DNL Page Builder] Intégration](page-builder.md) pour obtenir des instructions sur la manière d’ajouter du [!DNL Product Recommendations] dans du contenu [!DNL Page Builder].

### Indexation des prix SaaS

Les clients de Product Recommendations peuvent utiliser l’indexation des prix [SaaS](../price-index/price-indexing.md), qui accélère les mises à jour des prix et la synchronisation.

### Prise en charge B2B {#b2bsupport}

Les vitrines B2B nécessitent souvent une logique complexe qui détermine la visibilité des produits et les prix pour chaque acheteur ou groupe de clients. [!DNL Product Recommendations] désormais [prise en charge](release-notes.md) cette fonctionnalité en respectant les [autorisations de catégorie](https://experienceleague.adobe.com/docs/commerce-admin/catalog/categories/category-permissions.html), [catalogues partagés](https://experienceleague.adobe.com/docs/commerce-admin/b2b/shared-catalogs/catalog-shared.html) et [tarification spécifique au groupe client](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html). Par exemple, si vous avez masqué certaines catégories de votre segment de clients de détail, un acheteur de ce segment n’aura pas de recommandations pour les produits de ces catégories. En outre, lorsque vous définissez un catalogue partagé pour des groupes de clients et des sociétés spécifiques, ces acheteurs ne voient des recommandations que pour les produits auxquels ils ont accès. Tous les produits recommandés reflètent un prix correct spécifique au groupe de clients en fonction du groupe de clients de chaque acheteur.

>[!NOTE]
>
>Les commerçants peuvent personnaliser et étendre les widgets ou les éléments de storefront à l’aide de l’API Storefront [Catalog Service](../catalog-service/overview.md), mais toute personnalisation est hors de portée de l’équipe d’assistance d’Adobe.
