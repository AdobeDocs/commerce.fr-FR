---
title: Choisir une option Commerce
description: Comparez les architectures Adobe Commerce en fonction de la propriété des transactions, du modèle de déploiement et des besoins de marchandisage.
role: Admin, Developer, Leader, User
feature: Storefront, Integration, Configuration
recommendations: noCatalog
TQID: 'https://experienceleague.adobe.com/5y0IU5nji50eqfFNQHbVDV-R81Mx0I8v5Y0a6nccL-w'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
feature_v2:
  - id: 22bad240-8308-569b-a9d5-578f1ff890ca
    internal-label: Customers
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 6388cf7b-8a81-5248-a1e4-7bb57bbe250f
    internal-label: Install
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: 4c3c267873a68560a885c6376cd1137a7503710a
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%
---

# Choisir une option Commerce

Commencez par identifier le système propriétaire du panier, du passage en caisse, des commandes et des autres transactions. Choisissez ensuite le chemin de marchandisage qui correspond à ce serveur principal.

## Questions pour guider votre décision

Répondez aux questions suivantes pour identifier les options à évaluer. Tenez compte de votre serveur principal de commerce existant, des responsabilités d’infrastructure que vous souhaitez conserver et de la nécessité ou non d’améliorer la découverte et le marchandisage des produits. Adobe Commerce Optimizer offre des fonctionnalités de découverte et de marchandisage. Il ne remplace pas le serveur principal qui gère les transactions.

1. **Voulez-vous qu’Adobe gère la plateforme Commerce en tant que logiciel en tant que service (SaaS) ?**
   - Oui : évaluer Adobe Commerce as a Cloud Service.
   - Non : si vous avez besoin d’Adobe Commerce et souhaitez conserver le contrôle de votre infrastructure cloud ou locale, évaluez Adobe Commerce sur le cloud ou sur site.
1. **Avez-vous besoin d’Adobe Commerce pour gérer le panier, le passage en caisse, les commandes et d’autres transactions ?**
   - Oui : évaluation d’Adobe Commerce sur le cloud ou sur site, ou d’Adobe Commerce as a Cloud Service. Ces options utilisent Commerce Foundation comme serveur principal transactionnel.
   - Non : conserver votre serveur principal transactionnel existant ou tiers. Si vous avez également besoin des fonctionnalités de découverte et de marchandisage d’Adobe, évaluez le Adobe Commerce Optimizer autonome.
1. **Souhaitez-vous utiliser Adobe Commerce Optimizer pour améliorer la découverte et le marchandisage des produits avec votre serveur principal de commerce tiers existant ?**
   - Oui : évaluez le Adobe Commerce Optimizer autonome tout en conservant le serveur principal tiers pour les transactions.
1. **Exploitez-vous déjà Adobe Commerce sur le cloud ou sur site et souhaitez-vous une découverte et un marchandisage plus forts ?**
   - Oui : évaluez le connecteur Adobe Commerce Optimizer pour synchroniser les données de catalogue et de tarification pendant qu’Adobe Commerce continue à gérer les transactions.

Utilisez le tableau de comparaison ci-dessous pour faire correspondre vos réponses à un point de départ. Pour obtenir des diagrammes système détaillés, voir [Options d’architecture](../architecture-options/overview.md).

## Comparer les options de Commerce

| Vos besoins | Point de départ recommandé | Système propriétaire des transactions | Marchandisage et découverte |
| --- | --- | --- | --- |
| Adobe gère la plateforme Commerce en tant que SaaS. | [Adobe Commerce as a Cloud Service](/help/cloud-service/overview.md) | Adobe Commerce as a Cloud Service Foundation | Utilisez les services Commerce configurés pour Adobe Commerce as a Cloud Service. Pour connaître la disponibilité de l’intégration Adobe Commerce Optimizer, consultez la remarque ci-dessous : |
| Vous avez besoin d’Adobe Commerce et souhaitez conserver le contrôle de votre infrastructure cloud ou locale. | [Adobe Commerce sur le cloud ou sur site](https://experienceleague.adobe.com/fr/docs/commerce-admin/start/guide-overview) | Adobe Commerce Foundation | Utilisez les services Commerce pris en charge selon les besoins. |
| Sur Adobe Commerce on Cloud ou on-premise et qui souhaitent adopter Adobe Commerce Optimizer pour la découverte et le marchandisage. | Adobe Commerce avec le connecteur [Adobe Commerce Optimizer](/help/aco-connector/overview.md) | Adobe Commerce reste le système d’enregistrement des transactions. | Le connecteur synchronise les données de catalogue et de prix avec Adobe Commerce Optimizer, ce qui permet de proposer des expériences de découverte et de marchandisage. |
| Disposez d’un serveur principal de commerce tiers et souhaitez découvrir et marchandiser Adobe Commerce Optimizer sans remplacer ce serveur principal. | [Adobe Commerce Optimizer autonome](/help/optimizer/overview.md) | Serveur principal de commerce tiers | Envoyez les données de catalogue et de prix à Adobe Commerce Optimizer. Intégrez le panier, le passage en caisse et d’autres opérations transactionnelles au serveur principal via le maillage API, App Builder ou une intégration directe. |

>[!NOTE]
>
>Une intégration entre Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer figure sur la feuille de route de Commerce. Si vous avez besoin des deux plateformes, prévoyez de les utiliser comme des options d’architecture distinctes pour l’instant. Contactez votre gestionnaire de compte Adobe pour en savoir plus sur le calendrier de l’intégration.

## Conseils connexes

- [Plateformes et services](platform-and-services.md)
- [Options d’architecture](../architecture-options/overview.md)
- [Prise en main](../get-started/get-started-by-role.md)
