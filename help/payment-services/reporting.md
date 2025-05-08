---
title: Création de rapports
description: Utilisez le rapport Transactions pour obtenir une visibilité sur les taux d'autorisation des transactions et les tendances des transactions.
role: User
level: Intermediate
exl-id: dd1d80f9-5983-4181-91aa-971522eb56fa
source-git-commit: 4482c1f93a424c73497b88c707d0ab93a694c957
workflow-type: tm+mt
source-wordcount: '1270'
ht-degree: 0%

---

# Création de rapports

[!DNL Payment Services] for [!DNL Adobe Commerce] and [!DNL Magento Open Source] vous offre des rapports complets afin que vous puissiez obtenir une vue claire des transactions, des commandes et des paiements de votre magasin.

![Rapport des transactions](assets/transactions-report.png){width="700" zoomable="yes"}

Le rapport des transactions offre une visibilité sur les taux d’autorisation des transactions et les tendances négatives des transactions afin que vous puissiez surveiller efficacement l’intégrité de votre magasin et identifier et résoudre de manière préventive les problèmes de transaction.

Voir les transactions individuelles pour les commandes passées sur le storefront et leurs modes de paiement, résultat, codes réponse de paiement, etc.

Les informations fournies dans le rapport des transactions sont destinées uniquement aux commerçants. Ne partagez pas ces informations avec des clients ou d&#39;autres fraudeurs potentiels. Les informations sur les transactions peuvent être utilisées pour contourner les contrôles de sécurité ou passer des commandes qui entraînent des imputations.

Vous pouvez télécharger l&#39;état des transactions au format .csv pour l&#39;utiliser dans les logiciels de comptabilité ou de gestion des commandes existants.

>[!NOTE]
>
>Vous ne pouvez pas afficher les rapports financiers si vous n’avez pas [intégré et activé le mode réel](production.md#enable-live-payments) par [!DNL Payment Services].

## Vue du rapport des transactions

La vue Rapport des transactions est disponible dans la vue Transactions des Services de paiement. Il comprend toutes les informations disponibles sur les transactions de votre ou vos boutique(s).

Dans la barre latérale _Admin_, accédez à **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** > _[!UICONTROL Transactions]_>**[!UICONTROL View Report]**&#x200B;pour afficher la vue du rapport de transactions tabulaire détaillé.

![Vue du rapport des transactions](assets/transactions-report-view.png){width="800" zoomable="yes"}

Vous pouvez configurer cette vue, conformément aux sections de cette rubrique, pour présenter au mieux les données que vous souhaitez afficher.

Voir les ID de commande Commerce et de transaction PayPal liés, les montants des transactions, le mode de paiement par transaction et plus encore, le tout dans ce rapport.

Tous les modes de paiement n’offrent pas la même granularité d’informations. Par exemple, les transactions par carte de crédit fournissent des codes de réponse, AVS et CCV, ainsi que les quatre derniers chiffres de la carte dans le rapport Transactions ; les boutons de paiement PayPal n’en fournissent pas.

Vous pouvez [télécharger des transactions](#download-transactions) au format .csv pour les utiliser dans les logiciels de comptabilité ou de gestion des commandes existants.

>[!WARNING]
>
> Le rapport des transactions n’inclut aucune capture effectuée en dehors de [!DNL Payment Services].

### Sélectionner la source de données

Dans la vue Rapport des transactions , vous pouvez sélectionner la source de données (**[!UICONTROL Live]** ou **[!UICONTROL Sandbox]**) pour laquelle vous souhaitez afficher les résultats du rapport.

![Sélection des sources de données](assets/datasource.png){width="300" zoomable="yes"}

Si _[!UICONTROL Live]_&#x200B;est la source de données sélectionnée, vous pouvez afficher les informations de rapport pour vos magasins qui utilisent [!DNL Payment Services] en mode production. Si&#x200B;_[!UICONTROL Sandbox]_ est la source de données sélectionnée, vous pouvez afficher les informations de rapport pour votre mode sandbox.

Les sélections de sources de données fonctionnent comme suit :

* Si aucun magasin n’utilise [!DNL Payment Services] en mode de production, la sélection de la source de données est définie par défaut sur _[!UICONTROL Sandbox]_.
* Si des magasins (un ou plusieurs) utilisent [!DNL Payment Services] en mode de production, la sélection de la source de données est définie par défaut sur _[!UICONTROL Live]_.
* Les exportations de rapports respectent toujours la sélection de la source de données.

Pour sélectionner la source de données de votre rapport [!UICONTROL Transactions] :

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Transactions]_>**[!UICONTROL View Report]**.
1. Cliquez sur **[!UICONTROL Data source]** et sélectionnez **[!UICONTROL Live]** ou **[!UICONTROL Sandbox]**.

   Les résultats du rapport sont régénérés en fonction de la source de données sélectionnée.

### Personnaliser la période

Dans la vue Rapport de transactions , vous pouvez personnaliser la période des transactions que vous souhaitez afficher en sélectionnant des dates spécifiques. Par défaut, 30 jours de transactions sont affichés dans la grille.

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Transactions]_>**[!UICONTROL View Report]**.
1. Cliquez sur le filtre du sélecteur de calendrier **[!UICONTROL Transaction dates]**.
1. Sélectionnez la période applicable.
1. Affichez les transactions pour les dates spécifiées dans la grille.

### Filtrer les informations du rapport

Dans la vue Rapport des transactions , vous pouvez filtrer les statuts et les résultats à afficher en sélectionnant des critères de filtrage.

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Transactions]_>**[!UICONTROL View Report]**.
1. Cliquez sur le sélecteur de **[!UICONTROL Filter]**.
1. Activez/désactivez les options de _[!UICONTROL Transaction Result]_&#x200B;pour afficher les résultats du rapport pour les transactions de commande sélectionnées uniquement.
1. Activez/désactivez les options de _[!UICONTROL Payment Method]_&#x200B;pour afficher les résultats du rapport pour le type de paiement utilisé pour la transaction.
1. Activez/désactivez les options de _[!UICONTROL Payment Detail]_&#x200B;pour afficher des informations supplémentaires sur le type de paiement utilisé, le cas échéant.
1. Saisissez un _Montant minimum de commande_ ou _Montant maximum de commande_ pour afficher les résultats de l&#39;état dans cette fourchette de montant de commande.
1. Saisissez un _[!UICONTROL Order ID]_&#x200B;pour rechercher une transaction spécifique.
1. Découvrez le _[!UICONTROL Card Last Four]_&#x200B;permettant de rechercher une carte de crédit ou de débit spécifique.
1. Saisissez un _[!UICONTROL Customer ID]_&#x200B;pour afficher toutes les transactions d&#39;un client spécifique.
1. Saisissez le _[!UICONTROL Customer Email]_&#x200B;de filtrage des transactions pour cet e-mail.
1. Cliquez sur **[!UICONTROL Hide filters]** pour masquer le filtre.

### Afficher et masquer les colonnes

Par défaut, le rapport Transactions affiche toutes les colonnes d’informations disponibles. Vous pouvez toutefois personnaliser les colonnes affichées dans votre rapport.

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Transactions]_>**[!UICONTROL View Report]**.
1. Cliquez sur l’icône **[!UICONTROL Column settings]** ![icône des paramètres de colonne](assets/column-settings.png){width="20" zoomable="yes"}.
1. Pour personnaliser les colonnes affichées dans le rapport, cochez ou décochez les colonnes de la liste.

   Le rapport Transactions affiche immédiatement toutes les modifications que vous avez apportées dans le menu Paramètres de colonne . Les préférences de colonne sont enregistrées et restent actives si vous quittez la vue du rapport.

### Mise à jour des données d’un rapport

La vue Rapport de transactions affiche un horodatage _[!UICONTROL Last updated]_&#x200B;indiquant la dernière fois que les informations du rapport ont été mises à jour. Par défaut, les données du rapport de transactions sont automatiquement actualisées toutes les trois heures.

Vous pouvez également forcer manuellement une actualisation des données du rapport pour afficher les informations de rapport les plus récentes.

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Transactions]_>**[!UICONTROL View Report]**.
1. Cliquez sur l’icône _Actualiser_ (![icône d’actualisation](assets/refresh-button-med.png){width="20" zoomable="yes"}).

   Les données du rapport de transactions sont actualisées, une confirmation *[!UICONTROL Update complete]* s’affiche et les dernières informations sont présentes dans la grille.

### Transactions de téléchargement

Vous pouvez télécharger un fichier .csv avec toutes les transactions visibles dans la grille d’affichage des transactions, que vous consultiez les 30 jours de transactions par défaut ou un délai personnalisé.

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > **[!UICONTROL Transactions]**.
1. Si vous souhaitez afficher les transactions pour une période autre que les 30 derniers jours, [personnalisez la période pour vos statuts](#customize-dates-timeframe).
1. Cliquez sur l’icône _Télécharger_ ![icône de téléchargement](assets/icon-download.png){width="20" zoomable="yes"}.

Vos transactions sont téléchargées au format .csv.

### Descriptions des colonnes

Les rapports de transactions contiennent les informations suivantes.

| Colonne | Description |
| ------------ | -------------------- |
| [!UICONTROL Order ID] | ID de commande Commerce (contient uniquement des valeurs pour les transactions réussies et est vide pour les transactions rejetées)<br> <br>Pour afficher les [informations de commande](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/orders){target="_blank"} associées, cliquez sur l’ID. |
| [!UICONTROL PayPal Transaction ID] | Identifiant de transaction fourni par le fournisseur de paiement ; contient uniquement des valeurs pour les transactions réussies et un tiret pour les transactions rejetées. Vous pouvez cliquer sur cet ID pour accéder à la page des détails de la transaction PayPal. |
| [!UICONTROL Customer ID] | ID de client Commerce d’une commande<br> <br>Voir la rubrique [Informations sur le client](https://experienceleague.adobe.com/en/docs/commerce-admin/customers/customer-accounts/account-create){target="_blank"} pour plus d’informations. |
| [!UICONTROL Transaction Date] | Date et heure de la transaction |
| [!UICONTROL Payment Method] | Type de paiement utilisé pour la transaction avec des informations sur la marque et le type de carte. Voir [types de carte](https://developer.paypal.com/docs/api/orders/v2/#definition-card_type) pour plus d’informations ; disponible pour les versions 1.6.0 et ultérieures des services de paiement |
| [!UICONTROL Payment Detail] | Fournit des informations supplémentaires sur le type de paiement utilisé pour la transaction, le cas échéant. |
| [!UICONTROL Card Last Four] | Quatre derniers chiffres des cartes de crédit ou de débit utilisées pour la transaction |
| [!UICONTROL Result] | Résultat de la transaction : *[!UICONTROL OK]* (transaction réussie), *[!UICONTROL Rejected by Payment Provider]* (rejeté par PayPal), *[!UICONTROL Rejected by Bank]* (rejeté par la banque qui a émis la carte) |
| [!UICONTROL Response Code] | Code d&#39;erreur indiquant le motif du rejet par le fournisseur de paiement ou la banque. Voir la liste des codes de réponse possibles et leur description pour [`Rejected by Bank` statut](https://developer.paypal.com/docs/api/orders/v2/#definition-processor_response) et [`Rejected by Payment Provider` statut](https://developer.paypal.com/api/rest/reference/orders/v2/errors/). |
| [!UICONTROL AVS Code] | Code du service de vérification d&#39;adresse ; informations de réponse du processeur pour les demandes de paiement. Pour plus d’informations, voir [liste des codes et descriptions possibles](https://developer.paypal.com/docs/api/orders/v2/#definition-processor_response). |
| [!UICONTROL CVV Code] | Code de valeur de vérification de carte pour les cartes de crédit et de débit ; voir [liste des codes et descriptions possibles](https://developer.paypal.com/docs/api/orders/v2/#definition-processor_response) pour plus d’informations. |
| [!UICONTROL Amount] | Montant de commande de la transaction |
| [!UICONTROL Currency] | Devise utilisée pour la commande dans la transaction |
| [!UICONTROL Type] | [Action de paiement](../payment-services/production.md#set-payment-services-as-payment-method) pour la transaction : `Authorize` ou `Authorize and Capture` |

### Codes de réponse d’erreur

La colonne _Code de réponse_ affiche un code d’erreur ou de succès spécifique lié à la transaction. Voici quelques codes d’erreur courants qui peuvent s’afficher :

* `PAYMENT_DENIED`—La transaction a été refusée par PayPal parce qu&#39;on la soupçonnait d&#39;être une fraude.
* `INTERNAL_SERVER_ERROR` : la transaction a été refusée par PayPal et une erreur de serveur PayPal est survenue. La transaction peut être reprise.
* `INSTRUMENT_DECLINED` : le client a été refusé par PayPal pour le mode de paiement sélectionné. La transaction peut être retentée avec un autre mode de paiement.
* `9500`—La banque associée a refusé l&#39;opération parce qu&#39;elle était soupçonnée d&#39;être frauduleuse.
* `5120` — La transaction a été refusée par la banque associée parce que le client n&#39;avait pas suffisamment de fonds pour effectuer le paiement.
* `5650` — La transaction a été refusée par la banque associée parce que la banque exige une authentification forte du client ([3DS](security.md#3ds)).

Des codes de réponse d’erreur détaillés pour les transactions ayant échoué sont disponibles pour les transactions postérieures au 1er juin 2023. Des données de rapport partielles apparaîtront pour les transactions effectuées avant le 1er juin 2023.
