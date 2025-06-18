---
title: Affichage et gestion des journaux
description: Découvrez où trouver et gérer les journaux pour les visuels de produit.
feature: CMS, Media, Integration
badgePaas: label="PaaS uniquement" type="Informative" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."
source-git-commit: b6e190e883087a942630f0a27781654cd2c68781
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---


# Affichage et gestion des journaux

La fonctionnalité Visuels du produit fournit les fichiers journaux suivants dans votre instance Commerce :

- `/var/log/aem-assets-integration.log`
- `/var/log/aem-assets-integration-errors.log`

Demandez à votre administrateur système de vérifier le planning de rotation des fichiers journaux pour ces journaux afin d’éviter qu’ils ne deviennent trop volumineux. Dans certains environnements, les journaux pivotent automatiquement ; dans d’autres, vous devez configurer manuellement la rotation des journaux.  Pour plus d’informations, consultez les rubriques suivantes :

- Pour les installations sur site d’Adobe Commerce, demandez à votre administrateur système de configurer la [rotation des journaux](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/configuration.html?lang=fr#server-settings).
- Pour les projets d’infrastructure cloud d’Adobe Commerce, voir [Afficher et gérer les journaux](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/test/log-locations.html?lang=fr).
