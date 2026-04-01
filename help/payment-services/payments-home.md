---
title: Accueil
description: ' [!DNL Payment Services]  Utilisez l’Accueil dans l’Administration pour l’intégration (y compris ACCS), ouvrez le rapport des transactions, gérez les points d’entrée Commandes et paiements sur PaaS et accédez à Apprentissage, Aide et Paramètres.'
role: Admin, User
level: Intermediate
exl-id: d7a4c87f-33cb-446a-b442-3cdf05b518a2
feature: Payments, Checkout, Paas, Saas
source-git-commit: e4aede88f8470f79e5987afcb7311bf6ef44c16e
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 1%

---

# Page de départ [!DNL Payment Services]

[!DNL Payment Services] pour Adobe Commerce et Magento Open Source fournit une vue d’accueil avec les informations dont vous avez besoin pour configurer et utiliser l’extension. Les options situées en haut de la page d’Accueil dépendent de votre déploiement : Adobe Commerce sur le cloud ou sur site (PaaS), ou [!DNL Adobe Commerce as a Cloud Service] ou [!DNL Adobe Commerce Optimizer] (SaaS).

Dans la barre latérale _Admin_, accédez à **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** :

>[!BEGINTABS]

>[!TAB Adobe Commerce sur le cloud et sur site]

![Vue d’accueil](assets/home-view.png){width="700" zoomable="yes"}

>[!TAB Adobe Commerce as a Cloud Service et Commerce Optimizer]

Jusqu’à ce que vous ayez terminé l’intégration, **[!UICONTROL Home]**’affiche **[!UICONTROL ACCS Onboarding Required]**. La notification contient des liens pour [configurer le service Sandbox](sandbox.md#enable-sandbox-testing) (avec un compte de traitement PayPal de test) ou pour [activer les paiements en direct](production.md#enable-live-payments) si vous avez déjà effectué un test dans un autre environnement :

![Intégration ACCS requise sur les services de paiement - Page d&#39;accueil](assets/payment-services-home-accs-onboarding.png){width="700" zoomable="yes"}

Une fois l’intégration terminée (ou sur une instance déjà configurée), **[!UICONTROL Home]** affiche les **[!UICONTROL Transactions]** avec les **[!UICONTROL View Report]** pour le rapport tabulaire, ainsi que les zones **[!UICONTROL Learn]** et **[!UICONTROL Help]** :

![Payment Services Home sur SaaS](assets/payment-services-home-saas.png){width="700" zoomable="yes"}

>[!ENDTABS]

Dans cette vue d’accueil, vous pouvez accéder à _Accueil_, _En savoir_ sur les [!DNL Payment Services], configurer l’extension _Paramètres_ ou obtenir _Aide_. Utilisez **[!UICONTROL View Report]** (SaaS) ou les points d’entrée **[!UICONTROL Orders]** et **[!UICONTROL Payouts]** (Adobe Commerce sur le cloud et sur site) pour ouvrir le compte rendu des performances. Voir [Compte rendu des performances](reporting.md).

## Accueil

[!BADGE PaaS uniquement]{type=Informative url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."}

| Champ | Description |
|---|---|
| [!UICONTROL Orders] | Ces rapports vous permettent de consulter rapidement le statut du paiement de vos commandes et d’identifier les problèmes potentiels. |
| [!UICONTROL Payouts] | Les rapports Paiements affichent des informations complètes sur les paiements en un coup d&#39;œil, ce qui vous permet d&#39;obtenir une transparence totale sur le montant des paiements, le volume traité et des rapports détaillés sur le niveau des transactions pour le rapprochement financier. |

[!BADGE SaaS uniquement]{type=Positive url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."}

| Champ | Description |
|---|---|
| [!UICONTROL Transactions] | Affiche le rapport des transactions, qui vous aide à comprendre le résultat de transactions spécifiques. Cliquez sur **[!UICONTROL View Report]** pour ouvrir la grille des transactions (par exemple, les ID de transaction de commande et PayPal, le mode de paiement, le résultat et les codes réponse). Voir [Vue du rapport des transactions](reporting.md#transactions-report-view). |

## Apprendre

| Champ | Description |
|---|---|
| [!UICONTROL Read documentation] | Consultez la dernière documentation destinée aux utilisateurs et aux développeurs pour en savoir [!DNL Payment Services]. |
| [!UICONTROL How to onboard] | Trouvez tout ce dont vous avez besoin pour configurer et commencez à utiliser la fonctionnalité [!DNL Payment Services]. |
| [!UICONTROL Understand financial reports] | Explication détaillée des rapports sur la gestion des flux de trésorerie en [!DNL Payment Services]. |

## Aide

| Champ | Description |
|---|---|
| [!UICONTROL Visit help center] | Le Centre d’aide [!DNL Adobe Commerce] contient des articles de la base de connaissances sur [!DNL Payment Services]. |
| [!UICONTROL Get support] | Consultez le portail d’assistance [!DNL Adobe Commerce] pour obtenir de l’aide sur [!DNL Payment Services]. |

## Paramètres

Dans la vue d’accueil, cliquez sur **[!UICONTROL Settings]**. Voir [[!DNL Payment Services] configuration](configure-admin.md) pour plus d’informations.

Le pied de page de la zone Services de paiement affiche les libellés de version **Services de paiement** et **Tableau de bord des services de paiement** par exemple, lorsque vous collectez des détails pour l’assistance.
