---
title: Prise en main de  [!DNL Catalog Service]
description: Découvrez comment accéder à et  [!DNL Catalog Service]  intégrer aux applications frontales et aux services tiers.
role: Admin, Developer
exl-id: ee178e67-519d-4283-8de8-2634ae1f347a
TQID: https://experienceleague.adobe.com/KBdWesEoKJu-qWsY-Ny1Om-msUkyUPfUTQWftEqSg1g
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 586
ht-degree: 0%

---

# Prise en main du [!DNL Catalog Service]

Une fois le [!DNL Catalog Service] activé, vous pouvez accéder au service et l’utiliser pour récupérer les données du catalogue, telles que les informations sur les produits et les catégories, à partir de votre instance Adobe Commerce. Le service est disponible sous la forme d’une API GraphQL à laquelle vous pouvez accéder à partir de l’administration Commerce ou de toute application frontale prenant en charge les requêtes GraphQL.

{{aco-merchandising-services}}

## Accès au service

Le [!DNL Catalog Service] est disponible sous la forme d’une API GraphQL à laquelle vous pouvez accéder à partir de l’administration Commerce ou de toute application frontale prenant en charge les requêtes GraphQL. Le service est disponible dans les environnements SaaS et PaaS.

[!BADGE PaaS uniquement]{type=Informative url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."}

| Environnement | Point d’entrée |
| ------------ | ----------: |
| **Test** | `https://catalog-service-sandbox.adobe.io/graphql` |
| **Production** | `https://catalog-service.adobe.io/graphql` |

[!BADGE SaaS uniquement]{type=Positive url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."}

| Environnement | Point d’entrée |
| ----------- | --------:|
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

Si vous utilisez le storefront d’Adobe Commerce sur Edge Delivery Services, ajoutez le point d’entrée du service de catalogue à la configuration du storefront. Pour plus d’informations, consultez la documentation de [&#128279;](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/?lang=fr#storefront-configuration).

Pour les autres intégrations, consultez la documentation de configuration du projet pour plus d’informations sur la configuration des intégrations entre les sources de données de service et d’arrière-plan.

### Configuration du pare-feu

Pour autoriser le [!DNL Catalog Service] à travers un pare-feu, ajoutez des `commerce.adobe.io` à la liste autorisée.

## Service de catalogue et maillage API

Le [maillage API pour Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/gateway/overview/) permet aux développeurs d’intégrer des API privées ou tierces et d’autres interfaces aux produits Adobe à l’aide d’Adobe IO.

Pour plus d’informations sur l’installation et la configuration[&#128279;](mesh.md) consultez la rubrique [!DNL Catalog Service]  et Maillage API .

## Surveillance et dépannage de l’exportation des données

Commerce Admin fournit des outils pour surveiller et résoudre les problèmes d’exportation des données de Commerce vers les services connectés :

- **[Tableau de bord de gestion des données](https://experienceleague.adobe.com/fr/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)** : surveillez la synchronisation des données entre le [!DNL Catalog Service] et votre instance Adobe Commerce. Le tableau de bord affiche le statut de synchronisation global et répertorie tous les produits synchronisés.

- **[Page Statut de synchronisation des flux de données](https://experienceleague.adobe.com/fr/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status)** : suivez le statut d’exportation de tous les flux de données pour garantir la cohérence des données. Cette page vous avertit des problèmes qui se produisent pendant le processus d’exportation afin que vous puissiez les résoudre rapidement. Un statut « Succès » indique que les données ont été exportées et seront disponibles dans les services Commerce connectés une fois le processus de synchronisation des données terminé.

>[!NOTE]
>
>Si la page Statut de la synchronisation des flux de données n’est pas disponible dans les déploiements Commerce Admin for Commerce on Cloud ou on-premise, suivez les [&#x200B; instructions d’installation de l’extension &#x200B;](https://experienceleague.adobe.com/fr/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status#install-the-extension) pour l’activer.
