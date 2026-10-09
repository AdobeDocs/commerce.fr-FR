---
title: Affichage et gestion des journaux
description: Découvrez où trouver et gérer les journaux de l’intégration AEM Assets pour Commerce.
feature: CMS, Media, Integration
badgePaas: label="PaaS uniquement" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."
exl-id: 9c6c8694-6ded-4cc8-a3ab-d1dfb50e3583
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: ddbd0f6e-b569-5a04-8a70-55058777c373
    internal-label: CMS
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 76e77db86adecdbd3be76040970c0d0899c34cdc
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%
---
# Affichage et gestion des journaux

L’intégration d’AEM Assets fournit les fichiers journaux suivants dans votre instance Commerce :

- `/var/log/aem-assets-integration.log`
- `/var/log/aem-assets-integration-errors.log`

Pour obtenir une vue centrée sur les ressources des ressources synchronisées dans l’administration, y compris la recherche, les filtres et les résumés des erreurs de synchronisation, consultez [Affichage de l’état de synchronisation d’AEM Assets](sync-status.md).

Demandez à votre administrateur système de vérifier le planning de rotation des fichiers journaux pour ces journaux afin d’éviter qu’ils ne deviennent trop volumineux. Dans certains environnements, les journaux pivotent automatiquement ; dans d’autres, vous devez configurer manuellement la rotation des journaux.  Pour plus d’informations, consultez les rubriques suivantes :

- Pour les installations sur site d’Adobe Commerce, demandez à votre administrateur système de configurer la [rotation des journaux](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/next-steps/configuration#server-settings).
- Pour les projets d’infrastructure cloud d’Adobe Commerce, voir [Afficher et gérer les journaux](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/test/log-locations).
