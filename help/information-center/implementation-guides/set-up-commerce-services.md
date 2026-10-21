---
title: Configuration des services Commerce
description: Découvrez comment connecter Adobe Commerce aux services de marchandisage et Magento Open Source aux services de paiement à l’aide du connecteur de services Commerce.
role: Admin, Developer
feature: Integration, Configuration
recommendations: noCatalog
autotag-review: '2026-10-20T11:14:04.410Z'
TQID: 'https://experienceleague.adobe.com/yyUDw1y5CYHxdLlC3bNo0DKK0byamPAKUjK-wwxVEX4'
product_v2:
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
subfeature_v2:
  - id: a1d22079-48b9-5e69-9ee6-eb236068ef34
    internal-label: Search
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%
---

# Configuration des services Commerce

Les projets sur site et d’infrastructure cloud d’Adobe Commerce se connectent à des services tels que [!DNL Catalog Service], [!DNL Live Search], [!DNL Product Recommendations] et [!DNL Payment Services] via le connecteur de services Commerce. Sur [!DNL Adobe Commerce as a Cloud Service], cette connexion est configurée automatiquement.

Magento Open Source utilise le connecteur de services Commerce pour [!DNL Payment Services]. [!DNL Catalog Service], [!DNL Live Search] et [!DNL Product Recommendations] nécessitent Adobe Commerce et ne sont pas disponibles pour Magento Open Source.

>[!NOTE]
>
>Adobe Commerce Optimizer fournit des fonctionnalités de catalogue et de marchandisage en mode natif, au lieu d’utiliser des services [!DNL Live Search], [!DNL Catalog Service] et [!DNL Product Recommendations] distincts. La synchronisation de son catalogue ne nécessite pas le connecteur de services Commerce. D’autres intégrations sur le serveur principal Commerce, telles que [!DNL Payment Services] et [!DNL Data Connection], nécessitent toujours le connecteur . Voir [Activation de Adobe Commerce Optimizer](enable-aco.md) pour la configuration d’Optimizer.


## Prise en main

1. Consultez la documentation de [Commerce Services Connector](/help/landing/saas.md) pour obtenir et configurer vos clés API.

1. Consultez les [Guides des services &#x200B;](/help/landing/home.md) pour connaître les services individuels disponibles via le connecteur.

## Conseils connexes

- [Configuration des paiements](configure-payments.md)
- [Connecter AEM Assets](connect-aem-assets.md)
- [Intégration à Adobe Experience Platform](integrate-aep.md)
