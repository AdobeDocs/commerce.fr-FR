---
title: Ajouter des fichiers aux produits
description: Découvrez comment joindre des fichiers tels que des PDF, des manuels et des feuilles de données à des produits à l’aide d’attributs de produit de type fichier dans  [!DNL Adobe Commerce as a Cloud Service].
feature: Catalog Management, Products, Integration
role: Admin, Developer
level: Intermediate
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
source-git-commit: 848ba518d170c9a0270b2513fdc8efb6813f6845
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---

# Ajouter des fichiers aux produits

[!DNL Adobe Commerce as a Cloud Service] prend en charge un « fichier » [type d’entrée d’attribut de produit](https://experienceleague.adobe.com/fr/docs/commerce-admin/catalog/product-attributes/attributes-input-types){target="_blank"} qui permet aux commerçants de joindre des fichiers, tels que des PDF, des manuels, des certificats et des feuilles de données, directement aux produits. Les fichiers sont stockés dans le stockage multimédia Amazon S3 et sont accessibles via le storefront à l’aide de GraphQL ou par le biais d’intégrations à l’aide de l’API REST.

Il existe trois façons de charger des fichiers dans les attributs de fichier de produit :

* [Interface utilisateur d’administration](#upload-through-the-admin) - Téléchargez les fichiers manuellement sur la page de modification du produit.
* [API REST](#upload-through-the-rest-api) - Téléchargez des fichiers via l’API REST à l’aide d’URL présignées S3.
* [Import de produit](#upload-through-product-import) - Importez des fichiers en bloc en fournissant des URL externes au format CSV.

## Conditions préalables

Avant de charger des fichiers, vous devez créer un attribut de fichier et l’affecter à un jeu d’attributs.

* [Créer un attribut de fichier](https://experienceleague.adobe.com/fr/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create){target="_blank"} - Définissez **[!UICONTROL Catalog Input Type for Store Owner]** sur **[!UICONTROL File]**.

* [Attribuer l’attribut à un jeu d’attributs](https://experienceleague.adobe.com/fr/docs/commerce-admin/catalog/product-attributes/create/attribute-sets#create-an-attribute-set){target="_blank"} - Faites glisser le nouvel attribut de fichier dans le groupe de votre choix.

* Configurez les types et tailles de fichiers autorisés dans la configuration [Attributs de fichier de produit](https://experienceleague.adobe.com/fr/docs/commerce-admin/config/catalog/product-file-attributes).

## Télécharger des fichiers via l’administrateur

Après avoir [créé un attribut de fichier](https://experienceleague.adobe.com/fr/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create){target="_blank"} et l’avoir affecté à un jeu d’attributs, vous pouvez charger des fichiers directement à partir de la page de modification du produit.

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL Catalog]** > **[!UICONTROL Products]**.

1. Ouvrez le produit que vous souhaitez modifier.

1. Recherchez le champ d’attribut de fichier et cliquez sur **[!UICONTROL Upload]** pour sélectionner un fichier.

![Bouton Télécharger le fichier dans l’Administration](./assets/upload-file.png){width="600" zoomable="yes"}

1. Cliquez sur **[!UICONTROL Save]**.

Pour remplacer un fichier, supprimez le fichier existant, puis chargez-en un nouveau. Le fichier chargé est stocké dans le stockage multimédia Amazon S3.

## Charger via l’API REST

Utilisez le flux d’URL présigné [S3](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/s3-uploads/){target="_blank"} pour charger des fichiers par programmation via l’API REST. Ce processus fonctionne de la même manière pour les attributs de fichier de produit que pour d’autres types de médias tels que les images de catégorie et les fichiers d’attributs du client.

Le processus comporte quatre étapes :

1. Appelez `POST V1/media/initiate-upload` avec le nom de fichier et le `media_resource_type` pour les attributs de fichier de produit.
1. Utilisez l’URL présignée renvoyée pour `PUT` directement le fichier dans Amazon S3.
1. Appelez `POST V1/media/finish-upload` pour confirmer le chargement.
1. Attribuez la clé renvoyée à l’attribut de fichier du produit par `PUT /V1/products/{sku}`, en transmettant la clé en tant que valeur [attribut personnalisé](https://developer.adobe.com/commerce/webapi/rest/modules/custom-attributes/).

## Chargement via l’importation du produit

Vous pouvez joindre des fichiers aux produits en bloc à l’aide de l’API [import](https://developer.adobe.com/commerce/webapi/rest/modules/import/){target="_blank"} ou de l’interface utilisateur d’importation Admin. Les attributs de fichier de produit prennent uniquement en charge l’importation à partir d’URL externes, ce qui suit la même approche que la [méthode 2 pour l’importation d’images de produit](https://experienceleague.adobe.com/fr/docs/commerce-admin/systems/data-transfer/import/data-import-product-images#method-2-import-images-from-external-server){target="_blank"}. Commerce télécharge le fichier à partir de l’URL fournie et l’enregistre dans le stockage multimédia S3.

>[!NOTE]
>
>L’importation de fichiers à partir d’un chemin de serveur local (méthode 1) n’est pas prise en charge dans [!DNL Adobe Commerce as a Cloud Service], car il n’existe aucun accès direct au système de fichiers.

### Indiquez l’URL dans une colonne dédiée

Utilisez le code d’attribut comme en-tête de colonne CSV et l’URL complète comme valeur. Par exemple, si le code d’attribut est `file_upload`, le fichier CSV ressemble à ceci :

```csv
sku,name,file_upload
ADB112,"My Product",https://example.com/files/manual.pdf
```

### Fournissez l’URL en `additional_attributes`

Vous pouvez également inclure l’attribut de fichier dans la colonne `additional_attributes` :

```csv
sku,name,additional_attributes
ADB112,"My Product",file_upload=https://example.com/files/manual.pdf
```

Dans les deux cas, l’URL doit être accessible publiquement et l’extension et la taille du fichier doivent respecter les [limitations configurées](https://experienceleague.adobe.com/fr/docs/commerce-admin/config/catalog/product-file-attributes){target="_blank"}.

## Récupération de fichiers via GraphQL

En [!DNL Adobe Commerce as a Cloud Service], le point d’entrée [Catalog Service GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/){target="_blank"} sert des données de produit. Les attributs du fichier apparaissent dans le champ `attributes` sur `ProductView`, avec la `value` contenant l’URL publique complète du fichier :

```graphql
{
  products(skus: ["ADB112"]) {
    sku
    name
    attributes(roles: []) {
      name
      label
      value
    }
  }
}
```

La réponse inclut l’attribut de fichier avec son URL publique :

```json
{
  "data": {
    "products": [
      {
        "sku": "ADB112",
        "name": "Example product",
        "attributes": [
          {
            "name": "file",
            "label": "FILE",
            "value": "https://<host>/media/catalog/product_file/manual.pdf",
          }
        ]
      }
    ]
  }
}
```

>[!NOTE]
>
>Cette requête nécessite les en-têtes `Magento-Website-Code` et `Magento-Store-View-Code`. Pour plus d’informations, voir la requête [produits du service de catalogue](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/){target="_blank"}.

## Récupérer des fichiers via l’API REST

Lors de la récupération d’un produit par le biais de l’[API REST](https://developer.adobe.com/commerce/webapi/reference/rest/saas/){target="_blank"} (`GET /V1/products/{sku}`), les attributs de fichier apparaissent dans le tableau `custom_attributes` avec le nom de fichier comme valeur :

```json
{
  "custom_attributes": [
    {
      "attribute_code": "file_upload",
      "value": "manual_7aa0b2d63f6d3dbf.pdf"
    }
  ]
}
```
