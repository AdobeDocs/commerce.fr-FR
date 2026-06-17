---
title: Ajout dynamique d’attributs de produit
description: Découvrez comment ajouter dynamiquement des attributs de produit personnalisés au flux d’exportation de données pendant le processus de synchronisation des données.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: d5ed7497-4be1-440a-a567-81b64fdc54fc
TQID: https://experienceleague.adobe.com/SZWtLSvxb-w-968f4wqWrPTBn1c9IEuthvhIv86Pvss
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088bid: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 267
ht-degree: 0%

---

# Ajout dynamique d’attributs de produit

Vous pouvez étendre les attributs de produit sans les enregistrer dans [!DNL Adobe Commerce] en créant un module externe pour ajouter les attributs pendant le processus de synchronisation des données.

>[!NOTE]
>
>La meilleure façon d’étendre les attributs de produit est de les [ajouter à [!DNL Adobe Commerce]](extensibility-and-customizations.md#add-product-attributes-to-adobe-commerce) where you can configure and manage them from the Commerce Admin. Only add them dynamically if you need them solely for Commerce storefront services and do not want to register them in [!DNL Adobe Commerce]. You also have the option to manage custom attributes using [[!DNL API Mesh] avec le [!DNL Catalog Service]](../catalog-service/mesh.md) pour étendre le schéma de [!DNL GraphQL] [!DNL Catalog Service].

## Ajouter des attributs de produit

Créez un module externe qui ajoute un `customer_attribute` à la classe `Magento\CatalogDataExporter\Model\Provider\Product\Attributes`.

1. Mettez à jour le [fichier de configuration d’injection de dépendance](https://developer.adobe.com/commerce/php/development/build/dependency-injection-file/) (`di.xml`) pour définir le module externe.

   ```xml
   <type name="Magento\CatalogDataExporter\Model\Provider\Product\Attributes">
     <plugin name="product_customer_attributes" type="Vendor\CatalogDataExporter\Model\Plugin\AddAttribute"/>
   </type>
   ```

1. Créez le plug-in .

   ```php
    <?php
    declare(strict_types=1);
   
    namespace Vendor\CatalogDataExporter\Model\Plugin;
   
    use Magento\CatalogDataExporter\Model\Provider\Product\Attributes;
   
    class AddAttribute {
   
         /**
          * @param Attributes $subject
          * @param array $result
          * @param $arguments
          * @return array
          * @throws \Zend_Db_Statement_Exception
          */
          public function afterGet(Attributes $subject, array $result, $arguments): array
          {
              $additionalAttributes = [];
              $attributeCode = 'customer_attribute';
              foreach ($result as $product) {
                  if (!isset($product['productId']) || !isset($product['storeViewCode'])) {
                      continue;
                  }
                  // HINT: if needed, do filtration by "storeViewCode" and or "productId"
   
                  $productId = $product['productId'];
                  $storeViewCode = $product['storeViewCode'];
   
                  $newKey = \implode('-', [$product['storeViewCode'], $product['productId'], $attributeCode]);
                  if (isset($additionalAttributes[$newKey])) {
                      continue;
                  }
                  $additionalAttributes[$newKey] = [
                      'productId' => $productId,
                      'storeViewCode' => $storeViewCode,
                      'attributes' => [
                          'attributeCode' => $attributeCode,
                          // provide single or multiple values for the attribute
                          'value' => [
                              rand(1, 42)
                          ]
                      ]
                  ];
   
              }
   
              return array_merge($result, $additionalAttributes);
          }
    }
   ```

   Après avoir ajouté le module externe, les modifications sont synchronisées avec les services storefront connectés lors de la prochaine synchronisation planifiée. Pour envoyer les mises à jour immédiatement, utilisez la commande CLI suivante pour lancer manuellement le processus de synchronisation.

   ```shell
   bin/magento saas:resync --feed=products
   ```

## Déclaration des métadonnées d’attribut de produit personnalisé

Si vous créez de manière dynamique un attribut de produit personnalisé et souhaitez l’utiliser pour l’affichage, la recherche ou le filtrage dans les services storefront, ajoutez les métadonnées de l’attribut de produit pour configurer le comportement du storefront.

1. Mettez à jour le [fichier de configuration d’injection de dépendance](https://developer.adobe.com/commerce/php/development/build/dependency-injection-file/) (`di.xml`) pour définir le module externe pour les métadonnées d’attribut de produit.

   ```xml
   <type name="Magento\CatalogDataExporter\Model\Provider\ProductMetadata">
     <plugin name="product_customer_attributes_metadata" type="Vendor\CatalogDataExporter\Model\Plugin\AddAttributeMetadata"/>
   </type>
   ```

1. Créez le plug-in pour les `Magento\CatalogDataExporter\Model\Provider\ProductMetadata` de fournisseur suivantes.

   Vérifiez `ProductAttributeMetadata` les champs obligatoires dans `vendor/magento/module-catalog-data-exporter/etc/et_schema.xml`.

   ```php
    <?php
    declare(strict_types=1);
   
    namespace Vendor\CatalogDataExporter\Model\Plugin;
   
    use Magento\CatalogDataExporter\Model\Provider\ProductMetadata;
   
    class AddAttributeMetadata {
   
         /**
          * @param ProductMetadata $subject
          * @param array $result
          * @param $arguments
          * @return array
          * @throws \Zend_Db_Statement_Exception
          */
         public function afterGet(ProductMetadata $subject, array $result, $arguments): array
         {
              $result[] = [
                'id' => '123',
                // provide storeCode, websiteCode and storeViewCode applicable for your AC instance
                'storeCode' => 'default',
                'websiteCode' => 'base',
                'storeViewCode' => 'default',
                // specify the customer attribute code - should be the same as used in the products attributes plugin
                'attributeCode' => 'customer_attribute',
                // only product attributes are supported
                'attributeType' => 'catalog_product',
                // specify the data type
                'dataType' => 'int',
                'multi' => false,
                'label' => 'Customer Attribute',
                'frontendInput' => 'select',
                'required' => false,
                'unique' => false,
                'global' => true,
                'visible' => true,
                'searchable' => true,
                'filterable' => true,
                // This value must be set to true to export it to the storefront services
                'visibleInCompareList' => true,
                'visibleInListing' => true,
                'sortable' => true,
                'visibleInSearch' => true,
                'filterableInSearch' => true,
                'searchWeight' => 1.0,
                'usedForRules' => true,
                'boolean' => false,
                'systemAttribute' => false,
                'numeric' => false,
                // specify the list of attribute options
                'attributeOptions' => [
                    'option1',
                    'option2',
                    'option3'
                ]
             ];
   
              return $result;
         }
      }
   ```

   Après avoir ajouté le module externe, les modifications sont synchronisées avec les services storefront connectés lors de la prochaine synchronisation planifiée. Pour envoyer les mises à jour immédiatement, utilisez la commande CLI suivante pour lancer manuellement le processus de synchronisation.

   ```shell
   bin/magento saas:resync --feed=productAttributes
   ```

>[!MORELIKETHIS]
>
> * [Extension et personnalisation des flux d’exportation de données SaaS](extensibility-and-customizations.md)
> * [Synchroniser les flux à l’aide de l’interface de ligne de commande Commerce](data-export-cli-commands.md)
> * [Fonctionnement de la synchronisation ](sync-overview.md) — Découvrez les modes de synchronisation et la resynchronisation planifiée ou manuelle.
> * [Consulter les journaux et résoudre les problèmes](troubleshooting/logging.md)
