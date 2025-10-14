---
title: Ajout d’attributs personnalisés aux commandes
description: Découvrez comment ajouter des attributs de commande personnalisés à vos données de back-office et envoyer ces attributs à Experience Platform.
role: Admin, Developer
feature: Personalization, Integration
exl-id: dcd0b9e7-8d36-4bde-b226-ac19e83f00e4
source-git-commit: 5b1387e18e059c938aca600cc31951a3f5289e7e
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 2%

---

# Ajout d’attributs personnalisés aux commandes

Dans cet article, vous apprendrez à ajouter des attributs personnalisés aux événements back-office. Les attributs personnalisés vous permettent de capturer des informations de données riches afin d’améliorer les analyses et de créer davantage d’expériences personnalisées pour vos clientes et clients.

>[!NOTE]
>
>Découvrez comment [ajouter des identités personnalisées](custom-identities.md) aux profils.

Les attributs personnalisés sont pris en charge à deux niveaux :

- Niveau de commande
- Niveau d’article de commande

>[!NOTE]
>
>Adobe [!DNL Commerce] prend en charge les attributs personnalisés ayant un type de données de chaîne, booléen ou date.

L’ajout d’attributs personnalisés aux événements de back-office nécessite que vous :

1. Créez un projet dans votre installation [!DNL Commerce].
1. Mettez à jour votre schéma afin que les nouveaux attributs personnalisés puissent être correctement ingérés dans Experience Platform.
1. Dans l’interface d’administration, vérifiez que les attributs personnalisés sont capturés et envoyés à Experience Platform.

>[!IMPORTANT]
>
>La structure de répertoires et les exemples de code ci-dessous illustrent comment implémenter des attributs personnalisés. La structure et le code de répertoire réels requis dépendent de la configuration et de l’environnement de votre magasin.

## Étape 1 : créer la structure de répertoires

1. Accédez au répertoire `app/code` de votre installation [!DNL Commerce] et créez un répertoire de modules. Par exemple : `Magento/AepCustomAttributes`. Ce répertoire contient les fichiers nécessaires aux attributs personnalisés.
1. Dans le répertoire du module, créez un sous-répertoire appelé `etc`. Le répertoire `etc` contient les fichiers `module.xml`, `query.xml`, `di.xml` et `et_schema.xml`.

## Étape 2 : définir les dépendances et la version de configuration

Créez un fichier `module.xml` qui définit les dépendances et la version de configuration. Par exemple :

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:Module/etc/module.xsd">
    <module name="Magento_AepCustomAttributes">
        <sequence>
            <module name="Magento_SalesOrderDataExporter"/>
        </sequence>
    </module>
</config>
```

## Étape 3 : récupérer les données de commande client

Créez un fichier `query.xml` qui récupère les données des commandes client. Par exemple :

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:Module:Magento_QueryXml:etc/query.xsd">
  <query name="salesOrdersV2">
    <source name="sales_order">
      <link-source name="sales_order_inventory_source" link-type="inner">
        <attribute name="inventory_source_code" alias="inventory_source" />
        <using glue="and">
          <condition attribute="order_id" operator="eq" type="identifier">entity_id</condition>
         </using> 
        </link-source>
    </source>
  </query>
  </config>
```

## Étape 4 : Configurez l’injection de dépendance

Créez un fichier `di.xml` qui configure l’injection de dépendance. Par exemple :

```xml
  <?xml version="1.0"?>
  <config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:ObjectManager/etc/config.xsd">
      <type name="Magento\AepCustomAttributes\Model\Provider\CustomAttribute">
          <arguments>
              <argument name="usingField" xsi:type="string">commerceOrderId</argument>
          </arguments>
      </type>
      <type name="Magento\AepCustomAttributes\Model\Provider\OrderItemCustomAttribute">
          <arguments>
              <argument name="usingField" xsi:type="string">entityId</argument>
          </arguments>
      </type>
      <type name="Magento\DataServices\Model\ProductContext">
          <plugin name="product-context-plugin" type="Magento\AepCustomAttributes\Plugin\Model\ProductContext"/>
      </type>
  </config>
```

## Étape 5 : définir les services utilisés pour l’injection de dépendance

Créez un fichier `et_schema.xml` qui définit les services utilisés pour l’injection de dépendance. Par exemple :

```xml
  <?xml version="1.0"?>
  <config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:module:Magento_DataExporter:etc/et_schema.xsd">
      <record name="OrderV2">
          <field name="additionalInformation" type="CustomAttribute" repeated="true" provider="Magento\AepCustomAttributes\Model\Provider\CustomAttribute">
              <using field="commerceOrderId"/>
          </field>
      </record>
      <record name="OrderItemV2">
          <field name="additionalInformation" type="CustomAttribute" repeated="true" provider="Magento\AepCustomAttributes\Model\Provider\OrderItemCustomAttribute">
              <using field="entityId"/>
          </field>
      </record>
  </config>
```

## Etape 6 : Créer un répertoire pour les fichiers PHP

Au même niveau que le répertoire `etc`, créez un répertoire appelé `Module/Provider`. Ce répertoire contient les fichiers PHP `OrderCustomAttributes` et `OrderItemCustomAttributes`.

## Étape 7 : définir OrderCustomAttributes

Créez un fichier `OrderCustomAttributes.php` qui définit les attributs personnalisés d’ordre. Par exemple :

```php
declare(strict_types=1);

namespace Magento\AepCustomAttributes\Model\Provider;

use Magento\Framework\Serialize\Serializer\Json;

class CustomAttribute
{
  /**
   * @var Json
   */
  private Json $jsonSerializer;

  /**
   * @var string
   */
  private string $usingField = '';

  /**
   * @param string $usingField
   * @param Json $jsonSerializer
   */
  public function __construct(
      string $usingField,
      Json $jsonSerializer
  ) {
      $this->usingField = $usingField;
      $this->jsonSerializer = $jsonSerializer;
  }

  /**
   * @param array $values
   * @return array
   */
  public function get(array $values): array
  {
      $output = [];

      /**
       * Entity IDs
       */
      $ids = array_column($values, $this->usingField);

      foreach ($this->flatten($values) as $row) {
          $info = \is_string($row['additionalInformation']) ? $row['additionalInformation'] : '{}';
          $unserializedData = $this->jsonSerializer->unserialize($info) ?? [];

          if (isset($row)) {
              $unserializedData['order_channel'] = 'order_channel';
              $unserializedData['order_status'] = 'order_status';

              $additionalInformation = [];
              foreach ($unserializedData as $name => $value) {
                  $additionalInformation[] = [
                      'name' => $name,
                      'value' => \is_string($value) ? $value : $this->jsonSerializer->serialize($value)
                  ];
              }
              foreach ($additionalInformation as $information) {
                  $output[] = [
                      'additionalInformation' => $information,
                      $this->usingField => $row[$this->usingField],
                  ];
              }
          }
      }
      return $output;
  }

  /**
   * @param $values
   * @return array
   */
  private function flatten($values): array
  {
      if (isset(current($values)[0])) {
          return array_merge([], ...array_values($values));
      }
      return $values;
  }
}
```

## Étape 8 : définir OrderItemCustomAttributes

Créez un fichier `OrderItemCustomAttributes.php` qui définit les attributs personnalisés de l’élément de commande. Par exemple :

```php
declare(strict_types=1);

namespace Magento\AepCustomAttributes\Model\Provider;

use Magento\Framework\Serialize\Serializer\Json;

class OrderItemCustomAttribute
{
  /**
   * @var Json
   */
  private Json $jsonSerializer;

  /**
   * @var string
   */
  private string $usingField = '';

  /**
   * @param Json $jsonSerializer
   * @param string $usingField
   */
  public function __construct(
      Json $jsonSerializer,
      string $usingField
  ) {
      $this->jsonSerializer = $jsonSerializer;
      $this->usingField = $usingField;
  }

  /**
   * Getting additional attributes data.
   *
   * @param array $values
   * @return array
   */
  public function get(array $values): array
  {
      $output = [];
      $values = $this->flatten($values);

      foreach ($values as $row) {
          $info = \is_string($row['additionalInformation']) ? $row['additionalInformation'] : '{}';
          $unserializedData = $this->jsonSerializer->unserialize($info) ?? [];
          $unserializedData['product_brand'] = implode(',', ['label 1', 'label 2']);

          $additionalInformation = [];
          foreach ($unserializedData as $name => $value) {
              $additionalInformation[] = [
                  'name' => $name,
                  'value' => \is_string($value) ? $value : $this->jsonSerializer->serialize($value)
              ];
          }
          foreach ($additionalInformation as $information) {
              $output[] = [
                  'additionalInformation' => $information,
                  $this->usingField => $row[$this->usingField],
              ];
          }
      }
      return $output;
  }

  /**
   * @param $values
   * @return array
   */
  private function flatten($values): array
  {
      if (isset(current($values)[0])) {
          return array_merge([], ...array_values($values));
      }
      return $values;
  }
}
```

## Étape 9 : créer un répertoire pour le fichier productContext

Au même niveau que le répertoire `etc`, créez un répertoire appelé `Plugin/Module`. Ce répertoire contient le fichier `ProductContext.php`.

## Étape 10 : définir la classe ProductContext

Créez un fichier appelé `ProductContext.php`qui définit la classe `ProductContext`. Par exemple :

```php
<?php>
namespace Magento\AepCustomAttributes\Plugin\Model;
use Magento\Catalog\Model\Product;
use Magento\DataServices\Model\ProductContext as Subject;
use Magento\Framework\App\ResourceConnection;

class ProductContext
{
    private ?array $brandCache = [];
    public function __construct(
        private ResourceConnection $resourceConnection ) {
    }  

    public function afterGetContextData(Subject $subject, array $result Product $product)
    {
        $brand = $product->getCustomAttribute('cust_attr1');
        if (!empty($brand) && $brand->getValue()) {
            $result['brands'] = ['brand_label_1', 'brand_label_2'];
            }
            return $result;
      }
  }
```

## Étape 11 : Enregistrement du module

Au même niveau que le répertoire `etc`, créez un fichier `registration.php` qui enregistre le module. Par exemple :

```php
<?php>
declare(strict_types=1);

use \Magento\Framework\Component\ComponentRegistrar;

ComponentRegistrar::register(
    ComponentRegistrar::MODULE,
    'Magento_AepCustomAttributes',
    __DIR__
);
```

## Étape 12 : étendre votre schéma XDM existant

Pour vous assurer que les nouveaux attributs de commande personnalisés peuvent être ingérés par votre schéma [!DNL Commerce] dans Experience Platform, vous devez étendre le schéma afin d’inclure ces champs personnalisés.

Pour savoir comment étendre un schéma XDM existant afin d’inclure ces champs personnalisés, consultez l’article [Créer et modifier des schémas dans l’interface utilisateur](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/ui/resources/schemas#custom-fields-for-standard-groups) dans la documentation d’Experience Platform. Le champ ID de client est généré dynamiquement. Cependant, la structure des champs doit ressembler à l’exemple fourni dans la documentation d’Experience Platform.

>[!IMPORTANT]
>
>Les attributs personnalisés XDM doivent correspondre aux attributs envoyés depuis [!DNL Commerce].

Pour `commerce.order`, ajoutez un champ pour le niveau Commande :

![Niveau de commande](assets/order-level.png)

Pour `productListItems`, ajoutez des champs pour le niveau Article de commande :

![Niveau article de commande](assets/order-item-level.png)

## Étape 12 : confirmer que les données sont capturées

Consultez l’onglet [&#x200B; Personnalisation des données &#x200B;](connect-data.md#data-customization) dans l’interface d’administration pour confirmer que les données d’attribut personnalisé sont capturées et envoyées à Experience Platform.

### Dépannage

Si le message s’`No custom order attributes found.` dans l’onglet **[!UICONTROL Data Customization]** , confirmez ce qui suit :

1. Vous avez rempli les conditions préalables pour activer l’extension [Data Connector](overview.md#prerequisites).
1. Vous avez configuré [attributs de commande personnalisés](#add-custom-order-attributes).
1. Au moins un événement de commande a été généré.
