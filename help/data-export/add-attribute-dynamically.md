---
title: Ajout dynamique d’attributs de produit
description: Découvrez comment ajouter dynamiquement des attributs de produit personnalisés au flux d’exportation de données pendant le processus de synchronisation des données.
role: Admin, Developer
exl-id: d5ed7497-4be1-440a-a567-81b64fdc54fc
source-git-commit: 37d5699315e34f1504602090fae5201ee51cf470
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---

# Ajout dynamique d’attributs de produit lors de la synchronisation des données

Vous pouvez étendre les attributs de produit sans les enregistrer dans Adobe Commerce en créant un module externe pour ajouter les attributs pendant le processus de synchronisation des données.

>[!NOTE]
>
>La meilleure façon d’étendre les attributs de produit est de les [ajouter à Adobe Commerce](extensibility-and-customizations.md#add-product-attributes-to-adobe-commerce) où vous pouvez les configurer et les gérer à partir de l’administration Commerce. Ne les ajoutez dynamiquement que si vous en avez besoin uniquement pour les services de storefront Commerce et que vous ne souhaitez pas les enregistrer dans Adobe Commerce. Vous avez également la possibilité de gérer les attributs personnalisés à l’aide du [maillage API avec le service de catalogue](../catalog-service/mesh.md) pour étendre le schéma GraphQL du service de catalogue.

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

   ```
   bin/magento saas:resync --feed=products
   ```

## Déclaration des métadonnées d’attribut de produit personnalisé

Si vous créez de manière dynamique un attribut de produit personnalisé et souhaitez l’utiliser pour l’affichage, la recherche ou le filtrage dans les services storefront, ajoutez les métadonnées de l’attribut de produit pour configurer le comportement du storefront.

1. Mettez à jour le [fichier de configuration d’injection de dépendance](https://developer.adobe.com/commerce/php/development/build/dependency-injection-file/) (`di.xml`) pour définir le module externe pour les métadonnées d’attribut de produit.

   ```xml
   <type name="\Magento\CatalogDataExporter\Model\Provider\ProductMetadata">
     <plugin name="product_customer_attributes_metadata" type="Vendor\CatalogDataExporter\Model\Plugin\AddAttributeMetadata"/>
   </type>
   ```

1. Créez le plug-in au `\Magento\CatalogDataExporter\Model\Provider\ProductMetadata` de fournisseur suivant.

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

   ```
   bin/magento saas:resync --feed=productattributes
   ```

