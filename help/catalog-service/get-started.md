---
title: Prise en main de  [!DNL Catalog Service]
description: Découvrez comment accéder à et  [!DNL Catalog Service]  intégrer aux applications frontales et aux services tiers.
role: Admin, Developer
source-git-commit: 3a6a81fa03f13c24ac08041c39452c553aa54f55
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---


# Prise en main du [!DNL Catalog Service]

Une fois le [!DNL Catalog Service] activé, vous pouvez accéder au service et l’utiliser pour récupérer les données du catalogue, telles que les informations sur les produits et les catégories, à partir de votre instance Adobe Commerce. Le service est disponible sous la forme d’une API GraphQL à laquelle vous pouvez accéder à partir de l’administration Commerce ou de toute application frontale prenant en charge les requêtes GraphQL.

## Accès au service

Le [!DNL Catalog Service] est disponible sous la forme d’une API GraphQL à laquelle vous pouvez accéder à partir de l’administration Commerce ou de toute application frontale prenant en charge les requêtes GraphQL. Le service est disponible dans les environnements SaaS et PaaS.


[!BADGE PaaS uniquement]{type=Informative url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."}

| Environnement | Point d’entrée |
|------------ | ----------: |
| **Test** | `https://catalog-service-sandbox.adobe.io/graphql` |
| **Production** | `https://catalog-service.adobe.io/graphql` |

[!BADGE SaaS uniquement]{type=Positive url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."}

| Environnement | Point d’entrée |
| ------------ | --------:|
| Test | `https://na1-sandbox.api.commerce.adobe.com/{{tenant-id}}/graphql` |
| Production (pas encore disponible) | `https://na1.api.commerce.adobe.com/{{tenant-id}}/graphql` |

**Structure d’URL pour les points d’entrée SaaS**

```text
https://<region>-<environment>.api.commerce.adobe.com/<tenantId>/graphql
```

- `<region>` est la région cloud dans laquelle votre instance est déployée.
- `<environment>` est le type d’environnement, par exemple `sandbox`. Si l’environnement est en production, cette valeur est omise.
- `<tenantId>` est l’identifiant unique de l’instance spécifique de votre organisation dans Adobe Experience Cloud.

Pour plus d’informations sur l’utilisation de l’API GraphQL Catalog Service, consultez le guide [Catalog Service for Adobe Commerce](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/) dans la documentation *Adobe Commerce Developer*.


## Intégration à un storefront découplé ou à des services tiers

Pour une intégration à un storefront découplé, vous devez mettre à jour la configuration du storefront pour permettre la communication entre le storefront et le [!DNL Catalog Service] afin de récupérer les données de produit et de catégorie.

Si vous utilisez le storefront d’Adobe Commerce sur Edge Delivery Services, vous ajoutez le point d’entrée du service de catalogue à la configuration du storefront. Pour plus d’informations, consultez la documentation de [Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/?lang=fr#storefront-configuration).

Pour les autres intégrations, consultez la documentation de configuration du projet pour plus d’informations sur la configuration des intégrations entre les sources de données de service et d’arrière-plan.


### Configuration du pare-feu

Pour autoriser le [!DNL Catalog Service] à travers un pare-feu, ajoutez des `commerce.adobe.io` à la liste autorisée.

## Service de catalogue et maillage API

Le [maillage API pour Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/gateway/overview/) permet aux développeurs d’intégrer des API privées ou tierces et d’autres interfaces aux produits Adobe à l’aide d’Adobe IO.

Pour plus d’informations sur l’installation et la configuration[[!DNL Catalog Service]  consultez la rubrique ](mesh.md) et Maillage API .

## Utiliser le tableau de bord de gestion des données

Utilisez le [tableau de bord de gestion des données](https://experienceleague.adobe.com/fr/docs/commerce-admin/systems/data-transfer/data-dashboard) pour surveiller la synchronisation des données entre le [!DNL Catalog Service] et votre instance Adobe Commerce. Le tableau de bord fournit des informations sur le processus de transfert de données, notamment le statut des exportations de données et une liste de produits synchronisés.
