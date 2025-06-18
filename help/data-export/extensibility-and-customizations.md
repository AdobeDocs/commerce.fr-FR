---
title: Extension et personnalisation des données de flux d’exportation SaaS
description: Découvrez comment étendre et personnaliser les données  [!DNL SaaS Data Export]  flux.
role: Admin, Developer
exl-id: 694bd281-12c5-415c-a251-b4251e2edea7
source-git-commit: ff5c717dbdd638e114bccc3f6dec26f4be269194
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---

# Extension et personnalisation des données de flux d’exportation SaaS

L’extension [!DNL Commerce Data Export] permet d’exporter des données de l’application [!DNL Commerce] vers les services Commerce tels que Live Search, Catalog Service et Product Recommendations. Si nécessaire, vous pouvez étendre et personnaliser les données de flux pour inclure des données d’attribut supplémentaires ou modifier les données collectées.

Après avoir ajouté des données d’attribut, elles sont accessibles à partir du champ [attributes](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/#productviewattribute-type) dans le schéma GraphQL pour le service storefront.

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

Voir [Créer des attributs de produit](https://experienceleague.adobe.com/fr/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create) dans le *Guide d’administration d’Adobe Commerce*.

#### Créer l’attribut de produit par programmation

Ajoutez un attribut de produit par programmation en créant un correctif de données qui implémente le `DataPatchInterface` et instanciez une copie de la classe `EavSetup Factory` dans le constructeur pour configurer les options d’attribut.

Lorsque vous définissez les options d’attribut, tous les paramètres d’attribut, à l’exception de `type`, `label` et `input`, sont facultatifs. Définissez les paramètres supplémentaires suivants et tous les autres paramètres qui diffèrent des paramètres par défaut.

- **`user_defined`=`1`** : exportation de l’attribut vers les services storefront lors de la synchronisation des données.
- **`used_in_product_listing`=`1`** : rend l’attribut accessible dans la requête de base de données de liste de produits.

Pour plus d&#39;informations sur la création de patchs de données, voir [Developer data and schema patchs](https://developer.adobe.com/commerce/php/development/components/declarative-schema/patches/) dans le *PHP Developer Guide*.

### Ajout dynamique de l’attribut de produit

Pour plus d’informations sur la création dynamique d’attributs de produit sans introduire de nouveaux attributs EAV, voir [Ajouter un attribut de manière dynamique](add-attribute-dynamically.md).
