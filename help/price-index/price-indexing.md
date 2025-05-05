---
title: Indexation des prix SaaS
description: Utilisation de l'indexation des prix SaaS pour améliorer les performances
seo-title: Adobe SaaS Price Indexing
seo-description: Price indexing give performance improvements using SaaS infrastructure
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%

---

# Indexation des prix SaaS

L&#39;indexation des prix SaaS optimise les performances du site en déchargeant les tâches gourmandes en ressources (comme l&#39;indexation et le calcul des prix) de l&#39;application Commerce vers l&#39;infrastructure cloud Adobe. Cette approche permet aux commerçants de mettre rapidement à l&#39;échelle leurs ressources afin d&#39;accélérer les délais d&#39;indexation des prix et de fournir plus rapidement des mises à jour de prix au storefront et aux services Commerce connectés.

Le diagramme suivant montre le flux de données d’indexation sur les services SaaS lorsque Commerce utilise le processus [indexation des prix](https://experienceleague.adobe.com/fr/docs/commerce-operations/configuration-guide/cli/manage-indexers) inclus dans l’application Commerce :

![ Flux de données par défaut ](assets/old_way.png)

Lorsque l&#39;indexation des prix SaaS est activée, le flux de données change. L&#39;indexation des prix est effectuée à l&#39;aide de l&#39;exportation des données SaaS de [Commerce](../data-export/data-synchronization.md).

![Flux de données d&#39;indexation des prix SaaS](assets/new_way.png)

Tous les commerçants peuvent bénéficier de l&#39;indexation des prix SaaS, mais les commerçants qui ont des projets avec les caractéristiques suivantes peuvent réaliser les plus grands gains :

* **Changements de prix constants**-Les commerçants qui ont besoin de changements répétés à leurs prix pour atteindre des objectifs stratégiques tels que des promotions fréquentes, des remises saisonnières ou des réductions d&#39;inventaire.
* **Plusieurs sites web et/ou groupes de clients**-commerçants avec des catalogues de produits partagés sur plusieurs sites web (domaines/marques) et/ou groupes de clients.
* **De nombreux prix uniques sur plusieurs sites web ou groupes de clients**-Marchands avec des catalogues de produits partagés complets qui contiennent des prix uniques sur plusieurs sites web ou groupes de clients. Par exemple, les commerçants B2B qui ont des prix prénégociés ou des marques avec différentes stratégies de tarification.

## Utiliser l&#39;indexation des prix SaaS

L&#39;indexation des prix SaaS est activée automatiquement lorsque vous installez les services Adobe Commerce. Il prend en charge le calcul des prix pour tous les types de produits Adobe Commerce intégrés.

### Conditions requises

* Adobe Commerce 2.4.4+

### Conditions préalables

* L’un des services Commerce suivants doit être installé avec la dernière version de l’extension Commerce :

   * [Service de catalogue](../catalog-service/overview.md)
   * [Recherche en direct](../live-search/overview.md)
   * [Recommandations de produit](../product-recommendations/guide-overview.md)


>[!NOTE]
>
>Si nécessaire, l’indexeur de prix par défaut dans l’application Commerce peut être désactivé à l’aide de la [Carte catalogue](catalog-adapter.md).

## Synchroniser les prix avec l&#39;indexation des prix SaaS

Après avoir activé l’indexation des prix SaaS pour Adobe Commerce, mettez à jour les prix sur le Storefront et dans les services Commerce en synchronisant les nouveaux flux :

```bash
bin/magento saas:resync --feed=scopesCustomerGroup
bin/magento saas:resync --feed=scopesWebsite
bin/magento saas:resync --feed=prices
```

### Prix des types de produits personnalisés

Les calculs de prix sont pris en charge pour les types de produits personnalisés tels que le prix de base, le prix spécial, le prix de groupe, le prix de règle de catalogue, etc.

Si vous disposez d’un type de produit personnalisé qui utilise une formule spécifique pour calculer le prix final, vous pouvez étendre le comportement du flux de prix du produit.

1. Créez un plug-in sur la classe `Magento\ProductPriceDataExporter\Model\Provider\ProductPrice`.

   ```xml
   <config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:noNamespaceSchemaLocation="urn:magento:framework:ObjectManager/etc/config.xsd">
       <type name="Magento\ProductPriceDataExporter\Model\Provider\ProductPrice">
           <plugin name="custom_type_price_feed" type="YourModule\CustomProductType\Plugin\UpdatePriceFromFeed" />
       </type>
   </config>
   ```

1. Créez une méthode avec la formule personnalisée :

   ```php
   class UpdatePriceFromFeed
   {
       /**
       * @param ProductPrice $subject
       * @param array $result
       * @param array $values
       *
       * @return array
       */
       public function afterGet(ProductPrice $subject, array $result, array $values) : array
       {
           // Override the output $result with your data for the corresponding products (see original method for details) 
           return $result;
       }
   }
   ```

