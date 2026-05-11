---
title: Intégration
description: Découvrez les exigences et les plateformes prises en charge dans  [!DNL Product Recommendations].
exl-id: 7b8a1117-b6d5-4e5d-bb97-09f76a024cbd
TQID: https://experienceleague.adobe.com/FLrOFe-Lwe7i3dOwCISflVGEv2MIkXmmE-NqTvpaY-0
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 418
ht-degree: 0%

---

# Intégration

>[!IMPORTANT]
>
>**Product Recommendations n’est pas un service conforme à la loi HIPAA.** N’activez ni n’utilisez les recommandations de produits dans les mises en œuvre d’Adobe Commerce qui utilisent l’offre conforme à la loi HIPAA ou qui traitent des informations de santé protégées (ISP). Product Recommendations fait partie des services SaaS de Commerce actuellement classés comme non conformes à la loi HIPAA.
>
>Pour plus d’informations sur les fonctionnalités Adobe Commerce prêtes pour la loi HIPAA et les services qui ne doivent pas être utilisés avec les ISP, voir [ Préparation de la loi HIPAA pour Adobe Commerce ](https://experienceleague.adobe.com/en/docs/commerce-admin/start/compliance/hipaa-ready-service/overview) et [ Opérations ](https://experienceleague.adobe.com/en/docs/commerce-admin/start/compliance/hipaa-ready-service/operations#adobe-commerce-services).

Le processus d’intégration pour [!DNL Product Recommendations] nécessite l’accès à la ligne de commande du serveur et comprend les étapes suivantes. Si vous n’êtes pas familier avec le fonctionnement depuis la ligne de commande, demandez de l’aide à un développeur ou à un intégrateur système.

- [Workflow de mise en œuvre](implementation-workflow.md)
- [Installation et configuration](install-configure.md)
- [Paramètres](settings.md)
- [Vérifier](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/verify/)
- [Environnement d’évaluation](staging-environment.md)

## Conditions requises

- Adobe Commerce 2.4.4+
- PHP 8.1, 8.2, 8.3 ou 8.4
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
