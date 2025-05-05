---
title: Rapport des paiements
description: Utilisez le rapport Paiements pour une transparence totale sur le montant des paiements, le volume traité et la création de rapports détaillés au niveau des transactions pour le rapprochement financier.
role: User
level: Intermediate
feature: Payments, Checkout
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1303'
ht-degree: 0%

---

# Rapport des paiements

[!DNL Payment Services] for [!DNL Adobe Commerce] and [!DNL Magento Open Source] vous offre des rapports complets afin que vous puissiez obtenir une vue claire des transactions, des commandes et des paiements de votre magasin.

Il existe deux vues de rapports Paiements disponibles pour vous permettre d’afficher des informations détaillées sur tous vos paiements :

* **[Vue de visualisation des données des paiements](#payouts-data-visualization-view)** : graphique disponible sur l’Accueil des services de paiement qui est une représentation visuelle des montants agrégés par jour à partir de la vue Rapport des paiements
* **[vue Rapport des paiements](#payouts-report-view)** : rapport disponible dans Paiements qui affiche des informations détaillées sur les paiements pour toutes les transactions

Les vues Paiements affichent des informations complètes sur les paiements en un coup d&#39;œil, ce qui vous permet d&#39;obtenir une transparence totale quant au montant des paiements, au volume traité et à la création de rapports détaillés sur le niveau des transactions pour le rapprochement financier.

Vous pouvez [télécharger les transactions de paiement](#download-transactions) au format .csv pour les utiliser dans les logiciels de comptabilité ou de gestion des commandes existants.

>[!NOTE]
>
>Les rapports de paiements affichent uniquement les commandes capturées (l’action de paiement est définie sur [`Authorize and Capture`](https://experienceleague.adobe.com/docs/commerce/payment-services/get-started/production.html#set-payment-services-as-payment-method)) ou [marquées comme `Invoiced`](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice).

## Vue de visualisation des données des paiements

La vue de visualisation des données des paiements est disponible dans la page d’accueil des services de paiement. Il s’agit d’une représentation visuelle des montants agrégés par jour à partir du tableau détaillé [vue du rapport des paiements](#payouts-report-view).

Dans la barre latérale _Admin_, accédez à **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** pour afficher le graphique de visualisation des données des crédits par rapport aux débits et les moyennes glissantes au fil du temps.

![Visualisation des données de disposition dans l’administration](assets/payouts-report.png){width="800" zoomable="yes"}

Cliquez sur **[!UICONTROL View Report]** pour accéder au tableau détaillé [vue du rapport des paiements](#payouts-report-view).

### Personnaliser la période des transactions

Par défaut, 30 jours de transactions s’affichent.

Dans la vue de visualisation des données des paiements, vous pouvez personnaliser la période des transactions de paiement que vous souhaitez afficher en sélectionnant une période :

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**. La vue de visualisation des données des paiements est visible dans la section Paiements .
1. Cliquez sur le filtre du sélecteur de **[!UICONTROL Range]**.
1. Sélectionnez la période applicable : 30 jours, 15 jours ou 7 jours.
1. Affichez les informations sur les transactions pour les dates spécifiées.

### Informations sur les transactions

Les montants des transactions pour une période sélectionnée sont affichés à gauche de la vue de visualisation des données Paiements. Les dates de la période sélectionnée s’affichent au bas de l’affichage. S&#39;il n&#39;y a pas eu de paiements à une date donnée, cette date n&#39;apparaîtra pas.

La vue de visualisation des données des paiements comprend les informations suivantes.

| Données | Description |
| ------------ | -------------------- |
| [!UICONTROL Transaction amount] | Fourchette de montants pour les transactions dans une période spécifiée ; données sur l’axe Y (gauche) |
| Période | Période de l’intervalle spécifié ; données sur l’axe X (bas) |
| Crédit | Paiements pour la période spécifiée |
| Débit | Débits (remboursements) pour la période spécifiée |
| Moyenne glissante | Représentation du paiement moyen pour chaque date dans la période spécifiée |
| Net pour la plage | Montant net du paiement pour la période spécifiée (plage) |

## Vue du rapport des paiements

La vue Rapport des paiements est disponible dans la vue Paiements des Services de paiement. Il comprend toutes les informations disponibles sur les paiements pour vos magasins.

Dans la barre latérale _Admin_, accédez à **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** > _[!UICONTROL Payouts]_>**[!UICONTROL View Report]**&#x200B;pour afficher la vue détaillée du rapport tabulaire des paiements.

![Transactions de paiement dans l’administrateur](assets/payouts-report-new.png){width="800" zoomable="yes"}

Vous pouvez configurer cette vue, conformément aux sections de cette rubrique, pour présenter au mieux les données que vous souhaitez afficher.

Voir les ID de commande et de transaction Commerce liés, les montants des transactions, le mode de paiement par transaction, etc., dans cet état.

Vous pouvez [télécharger les transactions de paiement](#download-transactions) au format .csv pour les utiliser dans les logiciels de comptabilité ou de gestion des commandes existants.

>[!NOTE]
>
>Les données affichées dans ce tableau sont triées par défaut par ordre décroissant (`DESC`) à l’aide de la `TRANS DATE` . La `TRANS DATE` correspond à la date et à l&#39;heure auxquelles la transaction a été initiée.

### Sélectionner la source de données

Dans la vue Rapport des paiements, vous pouvez sélectionner la source de données (**[!UICONTROL Live]** ou **[!UICONTROL Sandbox]**) pour laquelle vous souhaitez afficher les résultats du rapport.

![Sélection des sources de données](assets/datasource.png){width="300" zoomable="yes"}

Si _[!UICONTROL Live]_&#x200B;est la source de données sélectionnée, vous pouvez afficher les informations de rapport pour les magasins en mode de production. Si&#x200B;_[!UICONTROL Sandbox]_ est la source de données sélectionnée, vous pouvez afficher les informations de rapport stockées en mode sandbox.

Les sélections de sources de données fonctionnent comme suit :

* Si aucun magasin n’est en mode réel, la sélection de la source de données est définie par défaut sur _[!UICONTROL Sandbox]_.
* Si vous disposez de magasins (un ou plusieurs) en mode réel, la sélection de la source de données est définie par défaut sur _[!UICONTROL Live]_.
* Les exportations de rapports respectent toujours la sélection de la source de données.

Pour sélectionner l&#39;origine de données de l&#39;état Statut du paiement de la commande :

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** > _[!UICONTROL Payouts]_>**[!UICONTROL View Report]**.
1. Cliquez sur **[!UICONTROL Data source]** et sélectionnez **[!UICONTROL Live]** ou **[!UICONTROL Sandbox]**.

   Les résultats du rapport sont régénérés en fonction de la source de données sélectionnée.

### Afficher les transactions

Par défaut, 30 jours de transactions s’affichent.

Le nombre de lignes renvoyées dans une recherche, ou affichées dans les 30 jours de transactions par défaut, s&#39;affiche au-dessus de la grille de la vue Paiements à côté du filtre du calendrier des dates de transaction.

Faites défiler l&#39;écran vers la gauche et la droite pour afficher les [informations pour chaque transaction de paiement](#column-descriptions) dans l&#39;état quotidien, y compris la date de transaction, l&#39;ID référence, le numéro de facture et les détails du mode de paiement.

#### Personnaliser la période des transactions

Dans la vue Rapport des paiements, vous pouvez personnaliser le délai des transactions de paiement que vous souhaitez afficher en saisissant des dates spécifiques ou en sélectionnant une période dans le sélecteur de date :

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** > _[!UICONTROL Payouts]_>**[!UICONTROL View Report]**.
1. Cliquez sur le filtre du sélecteur de calendrier _[!UICONTROL Transaction dates]_.
1. Sélectionnez la période applicable.
1. Affichez les statuts des paiements dans la grille pour les dates spécifiées.

### Afficher et masquer les colonnes

Par défaut, la vue Rapport des paiements affiche la plupart des colonnes d’informations disponibles. Vous pouvez toutefois personnaliser les colonnes affichées dans le rapport.

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Payouts]_>**[!UICONTROL View Report]**.
1. Cliquez sur l’icône _Paramètres de colonne_ (![icône des paramètres de colonne](assets/column-settings.png){width="20" zoomable="yes"}).
1. Pour personnaliser les colonnes du rapport, cochez ou décochez les colonnes de la liste.

   La vue Rapport des paiements affiche immédiatement toutes les modifications que vous avez effectuées dans le menu Paramètres des colonnes. Les préférences de colonne sont enregistrées et restent actives si vous quittez la vue du rapport.

### Transactions de téléchargement

Vous pouvez télécharger un fichier .csv contenant toutes les transactions visibles dans la grille de la vue Paiements.

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** > _[!UICONTROL Payouts]_>**[!UICONTROL View Report]**.
1. [Personnaliser la période pour vos transactions](#customize-transactions-timeframe).
1. Cliquez sur l’icône _Télécharger_ (![icône Télécharger](assets/icon-download.png){width="20" zoomable="yes"}).

Vos paiements sont téléchargés au format .csv.

### Descriptions des colonnes

Les rapports de paiement contiennent les informations suivantes.

| Colonne | Description |
| ------------ | -------------------- |
| [!UICONTROL Provider] | Prestataire de paiement |
| [!UICONTROL Provider trans] | ID de transaction |
| [!UICONTROL Trans date] | Date et heure auxquelles la transaction a été initiée |
| [!UICONTROL Type] | Type de transaction : *[!UICONTROL PAYMENT]*, *[!UICONTROL BONUS]*, *[!UICONTROL CHARGEBACK]*, *[!UICONTROL CORRECTION]*, *[!UICONTROL CURRENCY_CONVERSATION]*, *[!UICONTROL DEPOSIT]*, *[!UICONTROL DISBURSEMENT]*, *[!UICONTROL DISPUTE]*, *[!UICONTROL FEES]*, *[!UICONTROL HOLD]*, *[!UICONTROL HOLD_RELEASE]*, *[!UICONTROL INCENTIVES]*, *[!UICONTROL OTHERS]*, *[!UICONTROL RECOUP]*, *[!UICONTROL REFUND]*, *[!UICONTROL REVERSAL]*, *[!UICONTROL WITHDRAWAL]*, <br>,, <br>Voir [Types de transaction](#transaction-types) pour plus d’informations. |
| [!UICONTROL Status] | Statut actuel de la transaction : *[!UICONTROL SUCCESS]*, *[!UICONTROL DENIED]*, *[!UICONTROL PENDING]* |
| [!UICONTROL Code] | Code transaction qui indique soit Crédit (*CR*) soit Débit (*DR*) |
| [!UICONTROL Reference ID] | ID de transaction d&#39;origine auquel cet événement est associé |
| [!UICONTROL Invoice] | Identifiant de la facture (un par commande) de la transaction |
| [!UICONTROL Commerce order] | ID de commande Commerce <br> <br>Pour afficher les [informations de commande](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/orders) associées, cliquez sur l’ID. |
| [!UICONTROL Commerce trans] | ID de transaction Commerce |
| [!UICONTROL Pay method] | Type de carte de crédit (*[!UICONTROL BANK]*, *[!UICONTROL PAYPAL]*, *[!UICONTROL CREDIT_CARD]*) et fournisseur de carte associé (tel que *Visa* ou *MasterCard*) |
| [!UICONTROL TRANS AMT] | Montant de la transaction |
| [!UICONTROL CUR] | Unité monétaire du montant de la transaction |
| [!UICONTROL PENDING] | Montant à décaisser |
| [!UICONTROL CUR] | Unité monétaire du montant en attente |
| [!UICONTROL SELLER AMT] | Montant des fonds transférés à ou depuis un <br> client <br>Les fonds qui sortent du compte vendeur affichent un tiret (-) préfixe. |
| [!UICONTROL CUR] | Unité monétaire du montant vendeur |
| [!UICONTROL PARTNER FEE] | Frais de partenaire associés à la transaction <br> <br>Les fonds qui sortent du compte de frais du partenaire affichent un préfixe tiret (-). |
| [!UICONTROL CUR] | Unité monétaire pour les frais de partenaire |
| [!UICONTROL PROV FEES] | Frais associés au <br> de transaction <br>Les fonds qui sortent du compte de frais du fournisseur affichent un préfixe tiret (-). |
| [!UICONTROL CUR] | Unité monétaire pour les frais du fournisseur |
| [!UICONTROL FEE %] | Pourcentage du montant de la transaction facturé en tant que frais |
| [!UICONTROL FIXED FEE] | Montant fixe des frais du prestataire |
| [!UICONTROL CHBK FEE] | Frais de refacturation associés au <br> de transaction <br>Un préfixe tiret (-) indique que les frais de refacturation ont été inversés. |
| [!UICONTROL CUR] | Unité monétaire des frais de rétrofacturation |
| [!UICONTROL HOLD AMT] | Montant mis en attente ou libéré des <br> en attente <br>Un préfixe tiret (-) indique que des fonds bloqués sont libérés. |
| [!UICONTROL CUR] | Unité monétaire du montant du blocage |
| [!UICONTROL RECOUP AMT] | Montant récupéré à partir du compte de récupération <br> <br>Les fonds qui sortent du compte de récupération affichent un préfixe tiret (-). |
| [!UICONTROL CUR] | Unité monétaire du montant de la récupération |

### Types de transactions

Ces types de transactions peuvent être notés dans les transactions de paiement.

| Rapport | Description |
| ------------ | -------------------- |
| [!UICONTROL PAYMENT] | Argent transféré entre un acheteur et un vendeur pour une commande |
| [!UICONTROL AUTH] | Transactions d&#39;autorisation et d&#39;annulation d&#39;autorisation |
| [!UICONTROL BONUS] | — |
| [!UICONTROL CHARGEBACK] | Transactions de contrepassation des frais de refacturation et des frais de refacturation |
| [!UICONTROL CORRECTION] | — |
| [!UICONTROL CURRENCY_CONVERSION] | — |
| [!UICONTROL DEPOSIT] | — |
| [!UICONTROL DISBURSEMENT] | — |
| [!UICONTROL DISPUTE] | — |
| [!UICONTROL FEES] | Frais de partenaire, frais de paiement et transactions de contrepassation des frais |
| [!UICONTROL HOLD] | — |
| [!UICONTROL HOLD_RELEASE] | — |
| [!UICONTROL INCENTIVES] | — |
| [!UICONTROL OTHERS] | — |
| [!UICONTROL RECOUP] | Récupérations sur comptes bancaires ou pertes |
| [!UICONTROL REFUND] | — |
| [!UICONTROL REVERSAL] | — |
| [!UICONTROL WITHDRAWAL] | — |
