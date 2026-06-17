---
title: Extension et personnalisation des données de flux d’exportation SaaS
description: Découvrez comment étendre et personnaliser les données  [!DNL SaaS Data Export]  flux.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: 694bd281-12c5-415c-a251-b4251e2edea7
TQID: https://experienceleague.adobe.com/T71zNl7WOrqzEsz4H8A8arx--q6w1B0h33CF2Q0VI4A
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 815
ht-degree: 0%

---

# Extension et personnalisation des données de flux d’exportation SaaS

L’extension [!DNL Commerce Data Export] permet d’exporter des données de l’application [!DNL Commerce] vers les services Commerce tels que Live Search, Catalog Service et Product Recommendations. Si nécessaire, vous pouvez étendre et personnaliser les données de flux pour inclure des données d’attribut supplémentaires ou modifier les données collectées.

Après avoir ajouté des données d’attribut, elles sont accessibles à partir du champ [attributes](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/#productviewattribute-type) dans le schéma GraphQL pour les services de storefront.

>[!NOTE]
>
>L’ajout ou la modification des données de flux peut avoir un impact sur les performances et la logique de traitement du serveur principal Commerce. Testez le code personnalisé avant de fusionner en production. Au lieu d’ajouter des données au serveur principal, utilisez le maillage API pour étendre le schéma GraphQL du service de catalogue . Pour plus d’informations sur la configuration, voir [Service de catalogue et maillage API](../catalog-service/mesh.md).

## Étendre les données d’attributs système dans le flux de produits

Le flux de produits comprend des attributs système par défaut qui sont requis pour le traitement des produits ou généralement utilisés par les consommateurs. Vous pouvez inclure des attributs système supplémentaires dans le flux de produits en les ajoutant au flux.

Pour terminer cette tâche, mettez à jour le module `magento/catalog-data-exporter` pour ajouter les attributs système supplémentaires au [fichier de configuration de l’injection de dépendance](https://developer.adobe.com/commerce/php/development/build/dependency-injection-file/) (`di.xml`).

Ajoutez les attributs à la ou aux requête(`Magento\CatalogDataExporter\Model\Query\ProductAttributeQuery`) d’attributs de produit.

**Exemple**

```xml
    <type name="Magento\CatalogDataExporter\Model\Query\ProductAttributeQuery">
        <arguments>
            <argument name="systemAttributes" xsi:type="array">
                <item name="news_from_date" xsi:type="string">news_from_date</item>
                ...
                <item name="some_system_attribute_code">some_system_attribute_code</item>
            </argument>
        </arguments>
    </type>
```

## Ajout d’attributs de produit à Adobe Commerce

L’équipe de développement peut ajouter des attributs de produit accessibles à partir du champ [attributs de produit](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/#output-fields) en utilisant l’une des méthodes suivantes :

- Ajoutez l’attribut à Adobe Commerce pour l’inclure dans les données de flux `products` exportées vers les services de storefront Commerce.
- Ajoutez l’attribut de manière dynamique pendant le processus de synchronisation des flux à l’aide d’un module externe.

### Ajouter l’attribut à Adobe Commerce

Vous pouvez ajouter un attribut de produit à partir de l’administration Commerce ou par programmation à l’aide d’un module PHP personnalisé pour définir l’attribut et mettre à jour Adobe Commerce. L’ajout de l’attribut à partir de l’administration Commerce est la méthode la plus simple, car vous pouvez ajouter l’attribut et toutes les métadonnées requises en même temps. Le nouvel attribut et ses propriétés de métadonnées sont automatiquement exportés vers les services SaaS lors de la prochaine synchronisation planifiée.

#### Créer l’attribut de produit à partir de l’administrateur

1. Créez l’attribut à partir de la page de configuration des attributs de produit ([!UICONTROL Stores] > *[!UICONTROL Attributes]* > [!UICONTROL Product]) dans l’administration de Commerce.

1. Ajoutez l’attribut à un jeu d’attributs selon vos besoins.

Voir [Créer des attributs de produit](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create) dans le *Guide d’administration d’Adobe Commerce*.

#### Créer l’attribut de produit par programmation

Ajoutez un attribut de produit par programmation en créant un correctif de données qui implémente le `DataPatchInterface` et instanciez une copie de la classe `EavSetup Factory` dans le constructeur pour configurer les options d’attribut.

Lorsque vous définissez les options d’attribut, tous les paramètres d’attribut, à l’exception de `type`, `label` et `input`, sont facultatifs. Définissez les paramètres supplémentaires suivants et tous les autres paramètres qui diffèrent des paramètres par défaut.

- **`user_defined`=`1`** : exportation de l’attribut vers les services storefront lors de la synchronisation des données.
- **`used_in_product_listing`=`1`** : rend l’attribut accessible dans la requête de base de données de liste de produits.

Pour plus d&#39;informations sur la création de patchs de données, voir [Developer data and schema patchs](https://developer.adobe.com/commerce/php/development/components/declarative-schema/patches/) dans le *PHP Developer Guide*.

### Ajout dynamique de l’attribut de produit

Pour plus d’informations sur la création dynamique d’attributs de produit sans introduire de nouveaux attributs EAV, voir [Ajouter dynamiquement des attributs de produit](add-attribute-dynamically.md).

## Présentation du schéma de flux (`et_schema.xml`) {#feed-schema-overview}

Chaque structure de données de flux est déclarée dans `etc/et_schema.xml` à l’aide d’un simple DSL XML. Le framework lit ce fichier pour déterminer les champs à collecter et les classes de fournisseur PHP à appeler.

```xml
<record name="Product">
  <field name="sku" type="ID" />
  <field name="name" type="String" />
  <field name="attributes" type="Attribute" repeated="true"
         provider="Magento\CatalogDataExporter\Model\Provider\Product\Attributes">
    <using field="productId" />
    <using field="storeViewCode" />
  </field>
</record>
```

Éléments clés :

- `<record>` : définit l’entité de flux.
- `<field>` - déclare un champ de données ; l’attribut `provider` pointe vers une classe PHP implémentant `DataProcessorInterface` qui récupère les données
- `repeated="true"` - le champ est un tableau d’objets .
- `<using>` - Paramètres d’entrée transmis du contexte de l’enregistrement parent au fournisseur

>[!IMPORTANT]
>
>L’ajout d’un nouveau champ à `et_schema.xml` ne modifie que ce que [!DNL Adobe Commerce] collecte localement. Le service SaaS de réception doit également être mis à jour pour accepter et traiter le nouveau champ avant qu’il n’ait un effet sur le storefront.

## Observer les données après envoi {#observe-data-after-submission}

[!DNL SaaS Data Export] distribue l’événement `data_sent_outside` après chaque envoi par lots réussi à un service SaaS. Utilisez cet événement pour la journalisation d’audit, les déclencheurs webhook ou la collecte de mesures.

**Event:** `data_sent_outside`

**Données disponibles :**

| Clé | Description |
|---|---|
| `timestamp` | Horodatage Unix de l’envoi |
| `type` | Nom du flux (par exemple, `products`, `prices`) |
| `data` | Payload de flux envoyée |

**Exemple d’observateur :**

```php
<?php
namespace My\Module\Observer;

use Magento\Framework\Event\Observer;
use Magento\Framework\Event\ObserverInterface;

class DataSentOutsideObserver implements ObserverInterface
{
    public function execute(Observer $observer): void
    {
        $feedName = $observer->getData('type');
        $timestamp = $observer->getData('timestamp');
        $data = $observer->getData('data');

        // Custom logic: audit logging, webhook, metrics
    }
}
```

Enregistrez l’observateur dans `etc/events.xml` :

```xml
<event name="data_sent_outside">
    <observer name="my_module_data_sent_outside"
              instance="My\Module\Observer\DataSentOutsideObserver" />
</event>
```

Pour obtenir des informations générales sur les événements et les observateurs, voir [Événements et observateurs](https://developer.adobe.com/commerce/php/development/components/events-and-observers){target="_blank"} dans la documentation destinée aux développeurs Adobe Commerce.

## Filtrer les données avant envoi

Utilisez le point d’extension `Magento\SaaSCommon\Model\DataFilter` pour supprimer les champs sensibles ou ignorer des entités spécifiques avant l’envoi des données au service SaaS. Cela s’avère utile pour les exigences de conformité telles que le RGPD ou PCI, où certains champs ne doivent pas quitter l’instance Commerce.

Implémentez l’interface et connectez-la via une préférence d’identifiant dans `etc/di.xml` :

```xml
<preference for="Magento\SaaSCommon\Model\DataFilter"
            type="My\Module\Model\MyDataFilter" />
```

>[!NOTE]
>
>Le filtrage est appliqué après la collecte des données. Si `PERSIST_EXPORTED_FEED=1` est défini, le tableau de flux stocke la payload non filtrée avant le filtrage.

>[!MORELIKETHIS]
>
> - [Ajouter dynamiquement un attribut de produit](add-attribute-dynamically.md)
> - [Ajouter une classe de taxe, un jeu d’attributs et des métadonnées d’inventaire](add-tax-attribute-set-inventory-attributes.md)
> - [Fonctionnement de la synchronisation](sync-overview.md)
