---
source-git-commit: a3ade1a31d3c2905b601f71bda118de89c43cf59
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 27%
---

# Supprimer les extensions en conflit

Si l’une des extensions suivantes est installée, désinstallez-la avant d’installer le [!DNL Adobe Commerce Optimizer Connector for B2B] :

* [!DNL Adobe Commerce Live Search] (`magento/live-search`)
* [!DNL Adobe Commerce Product Recommendations] (`magento/product-recommendations`)
* [!DNL Adobe Commerce Catalog Service] (`magento/catalog-service`, `magento/catalog-service-installer`)
* **[!UICONTROL Data Management Dashboard]** (`magento-catalog-sync-admin`)

Les données associées à ces extensions sont toujours disponibles dans la base de données Commerce. Cependant, il n’est pas exporté vers [!DNL Commerce Optimizer] lorsque le connecteur est activé. Pour implémenter les fonctionnalités de recherche et de marchandisage d’Adobe Commerce fournies par ces extensions après l’activation du connecteur, configurez-les à partir de l’[[!DNL Commerce Optimizer] interface utilisateur d’administration](https://experienceleague.adobe.com/fr/docs/commerce/optimizer/overview#quick-tour).

>[!IMPORTANT]
>
>Si vous ne supprimez pas ces extensions avant d’activer le connecteur, les écrans de configuration sont rompus, les données en double sont [!DNL Commerce Optimizer] et des erreurs d’authentification 401 ou 403 se produisent.