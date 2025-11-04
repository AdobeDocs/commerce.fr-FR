---
title: Ajouter une classe de taxe, un jeu d'attributs et des attributs de stock
description: Découvrez comment étendre les données de flux de produits afin d’inclure des attributs pour la classification fiscale, le jeu d’attributs et les paramètres d’inventaire avancés
role: Admin, Developer
badgePaas: label="PaaS uniquement" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/
source-git-commit: dd8f518028c9f2025606e6620fc20156fceac9ce
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---

# Ajouter une classe de taxe, un jeu d&#39;attributs et des attributs de stock

Le module Attributs de produit supplémentaires d’Adobe Commerce étend les flux de données de produit. Elle comprend des attributs de produit supplémentaires issus des configurations de produit Adobe Commerce :

* [Classification fiscale](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/taxes/tax-class)
* [Jeu d’attributs](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/create/attribute-sets)
* [Inventaire](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/configuration/product-options#advanced-product-options)

Une fois installé, le module fonctionne automatiquement. Il capture et exporte les attributs supplémentaires lors de la synchronisation du produit. Aucune configuration supplémentaire n’est requise.

## Principaux avantages

* **Amélioration automatique** : enrichit les flux de produits avec la classe de taxe, le jeu d’attributs et les attributs de stock.
* **Intégration transparente** : fournit un contexte essentiel pour les systèmes et services externes
* **Configuration zéro** : fonctionne immédiatement après l&#39;installation
* **Mises à jour en temps réel** : synchronise automatiquement les modifications du produit

## Fonctionnalités et attributs exportés

Le module ajoute trois attributs supplémentaires à vos flux de données de produit existants :

* `ac_tax_class`
* `ac_attribute_set`
* `ac_inventory`

### &#x200B;1. Informations sur la classe d&#39;imposition (`ac_tax_class`)

**Objectif** : fournit des informations de classification fiscale pour chaque produit

**Format des données** : valeur de chaîne contenant le nom de la classe de taxe

**Exemple de sortie** :

```json
{
  "attributes": [
    {
      "code": "ac_tax_class",
      "values": ["Taxable Goods"]
    }
  ]
}
```

**Cas d’utilisation** :

Lorsque vous exportez des données de classe de taxe vers les services de catalogue Commerce, ces données sont disponibles pour les applications qui prennent en charge :

* Déclaration de conformité fiscale
* Intégration avec les services externes de calcul des taxes
* Catégorisation des produits pour les systèmes comptables

### &#x200B;2. Informations sur le jeu d’attributs (`ac_attribute_set`)

**Objectif** : identifie le jeu d’attributs affecté à chaque produit

**Format des données** : valeur de chaîne contenant le nom du jeu d’attributs.

**Exemple de sortie** :

```json
{
  "attributes": [
    {
      "code": "ac_attribute_set",
      "values": [
        "Default"
      ]
    }
  ]
}
```

**Cas d’utilisation** :

Lorsque vous exportez des données de jeu d’attributs vers les services de catalogue Commerce, cela active des fonctionnalités avancées de gestion des produits dans les systèmes externes. Ces fonctionnalités incluent :

* Identification du modèle de produit
* Gestion et organisation des catalogues
* Intégration de systèmes tiers nécessitant un contexte de jeu d’attributs

### &#x200B;3. Données d&#39;inventaire avancées (`ac_inventory`)

**Objectif** : fournit des paramètres de gestion des stocks pour chaque produit

**Format de données** : chaîne codée en JSON contenant la configuration de l’inventaire

**Champs inclus** :

* `manageStock` (booléen) : indique si la gestion des stocks est activée
* `cartMinQty` (flottant) : quantité minimale autorisée dans le panier
* `cartMaxQty` (flottant) : quantité maximale autorisée dans le panier
* `backorders` (chaîne) : politique de backorder. La valeur est l’une des suivantes :
   * `"no"` : aucun reliquat autorisé
   * `"allow"` : Autoriser une quantité inférieure à 0
   * `"allow_notify"` : Autoriser une quantité inférieure à 0 et informer le client
* `enableQtyIncrements` (booléen) : indique si les incréments de quantité sont activés
* `qtyIncrements` (flottant) : valeur d’incrément de quantité requise

**Exemple de sortie** :

```json
{
  "attributes": [
    {
      "code": "ac_inventory",
      "values": [
        "{\"manageStock\":true,\"cartMinQty\":2,\"cartMaxQty\":42,\"backorders\":\"no\",\"enableQtyIncrements\":false,\"qtyIncrements\":2}"
      ]
    }
  ]
}
```

**Cas d’utilisation** :

Lorsque vous exportez des données d’inventaire vers les services de catalogue Commerce, cela active des fonctionnalités avancées de gestion des stocks dans les systèmes externes. Ces fonctionnalités incluent :

* Intégration du système Inventory management
* Règles de validation du panier
* Optimisation du processus d’exécution des commandes
* Personnalisation de l’expérience client

## Amélioration du flux d’exportation des données

Le module Attributs de produit supplémentaires améliore les flux de produits existants. Il intègre automatiquement les nouvelles données d’attribut.

* **Flux de produits** (`products`) : amélioré avec les trois attributs supplémentaires

   * Ajoute les attributs `ac_tax_class`, `ac_attribute_set` et `ac_inventory` à chaque enregistrement de produit
   * Ne modifie pas les données de produit d’origine
   * Maintient la rétrocompatibilité avec les consommateurs d’aliments existants.

* **Flux d’attributs de produit** (`productAttributes`) : amélioré avec des métadonnées d’attribut pour les nouveaux attributs

   * Enregistre automatiquement les métadonnées des trois nouveaux attributs dans le flux de `productAttributes`
   * Fournit des détails de configuration des attributs (types de données, paramètres de visibilité, etc.)
   * Aide les systèmes externes à comprendre le nouveau schéma d’attribut.

## Installation de l’extension

**Conditions requises**

* PHP 8.1, 8.2, 8.3 ou 8.4
* Adobe Commerce 2.4.4+
* [Extension Adobe Commerce Data Export](manage-extension.md#update-a-module-to-a-specific-version), version 103.4.11 ou ultérieure
* Accès à [repo.magento.com](https://repo.magento.com)

  Pour générer des clés et obtenir les droits nécessaires, voir [&#x200B; Obtenir vos clés d’authentification &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys). Pour les installations cloud, consultez le guide [Commerce sur les infrastructures cloud](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/authentication-keys).
* Accès à la ligne de commande du serveur applicatif Adobe Commerce.

### Etapes d&#39;installation

Ajoutez le module `adobe-commerce/module-extra-product-attributes` à l’aide du compositeur :

```shell
composer require adobe-commerce/module-extra-product-attributes
```

Pour obtenir des instructions d’installation détaillées, consultez les guides suivants :

* [Installation de l’extension sur Adobe Commerce sur une infrastructure cloud](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure-store/extensions)
* [Installation de l’extension Adobe Commerce sur site](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/extensions)

## Synchronisation des données de produit

Après le redéploiement, l’instance Adobe Commerce exporte automatiquement les données supplémentaires lors de la synchronisation du produit. Vous pouvez également utiliser les commandes de l’interface de ligne de commande `resync` pour effectuer une synchronisation immédiate.

```shell
# Resync the products feed (includes the new attributes)
bin/magento saas:resync --feed=products
```

```shell
# Resync the product attributes feed (includes new attribute metadata)
bin/magento saas:resync --feed=productAttributes
```

## Dépannage

**Attributs supplémentaires manquants dans les produits :**

* Vérifiez que le module est correctement installé et activé
* Exécutez les commandes de resynchronisation pour actualiser les données du produit.
* Vérifiez que les produits ont des affectations de classe de taxe et de jeu d&#39;attributs valides

**Les données d’inventaire semblent incorrectes :**

* Vérifiez que les paramètres d’inventaire sont correctement configurés dans l’administration.
* Rechercher des remplacements d’inventaire spécifiques au site web
* Vérifiez que le module [Inventory management](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/guide-overview) fonctionne correctement

Pour plus d’informations, consultez le [Guide Inventory management](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/guide-overview) dans la *Documentation pour les commerçants Adobe Commerce*.

**Problèmes de performances :**

* Surveiller les performances du processus d’exportation après l’installation
* Envisagez de planifier des resynchronisations pendant les périodes de faible trafic

### Journalisation et débogage

Le module consigne les erreurs et les avertissements d’exportation dans le système de journalisation Commerce standard. Si vous rencontrez des problèmes lors de la synchronisation du produit, vérifiez les journaux d’exportation des données.

Pour plus d’informations, voir [Vérification des journaux et dépannage](troubleshooting-logging.md).

