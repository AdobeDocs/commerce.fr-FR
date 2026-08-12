---
title: Connecter un compte PayPal différent pour un site Web
description: Intégration complète de PayPal à l'échelle du site Web dans l'administrateur pour connecter un compte marchand PayPal différent à un site Web individuel.
role: Admin, User
level: Intermediate
feature: Payments, Checkout, Configuration, Paas, Saas
TQID: 'https://experienceleague.adobe.com/U1zGAU6vYKjk2tc2KXnvyqnYdbA2HKTCNZSKhHdS0Vw'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: bd989d82-1e15-4534-88db-f1f51dd77ffaid: dac87252-6066-4d6e-a9d2-f6d84c323de7
source-git-commit: d754c71e287d7d9ff297dd7d95efbaaae7ffc2fc
workflow-type: tm+mt
source-wordcount: 393
ht-degree: 0%

---

# Connecter un compte PayPal différent pour un site Web

Pour les instances Commerce avec **plusieurs sites web**, vous aurez peut-être besoin de **différents comptes marchands PayPal**. [!DNL Payment Services] permet l’intégration de PayPal **à l’échelle du site web** après l’intégration **globale**.

>[!NOTE]
>
> Cette fonctionnalité ne prend en charge que la connexion de nouveaux comptes.

## Conditions préalables à l’intégration à l’échelle du site web

L’intégration au niveau du site web n’est disponible que lorsque votre boutique répond à ces exigences :

- [Commerce Services Connector](https://experienceleague.adobe.com/en/docs/commerce/user-guides/integration-services/saas) la configuration est terminée.
- Un compte PayPal est connecté à la portée globale (configuration par défaut).

Vous pouvez le confirmer en vérifiant que les champs suivants sont renseignés à l’étendue par défaut :

- [!UICONTROL Payment Services Sandbox ID]
- [!UICONTROL Payment Services Production ID]
- [!UICONTROL PayPal Merchant ID]

Si ces champs sont vides, vous devez d’abord [intégration globale](configure-admin.md). Le bouton **[!UICONTROL Connect different account]** est désactivé jusqu’à ce que vous ayez rempli les conditions préalables.

## Démarrer la connexion au niveau du site web

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**>**[!UICONTROL Sales]**et sélectionnez **[!UICONTROL Payment Methods]**.
1. Dans le sélecteur de portée situé dans le coin supérieur gauche, passez de **[!UICONTROL Default Config]** à la **[!UICONTROL Website]** que vous souhaitez intégrer.
1. Cliquez sur **[!UICONTROL Connect different account]**.

   Si le bouton est désactivé, votre boutique ne remplit pas les [conditions préalables](#prerequisites-global-scope) ci-dessus.

## Terminez la boîte de dialogue modale d’intégration

Une fenêtre contextuelle s’ouvre.

1. Sélectionnez votre **[!UICONTROL Country]** dans la liste déroulante.
1. Choisissez votre type d’intégration : **[!UICONTROL Basic]** ou **[!UICONTROL Advanced]**.
1. Cliquez sur **[!UICONTROL Next]**.

>[!NOTE]
>
> Si vous effectuez une intégration en Hongrie, en Espagne ou en Autriche, vous devez ouvrir et afficher le lien des Conditions générales avant de pouvoir cliquer sur le bouton **[!UICONTROL I Accept]**. Le bouton est désactivé jusqu&#39;à ce que vous ouvriez les conditions générales.

## Se connecter à PayPal

Après avoir été redirigé vers la connexion PayPal, connectez-vous et suivez les étapes d&#39;intégration dans PayPal.

>[!IMPORTANT]
>
> Une fois que vous avez cliqué sur **[!UICONTROL Confirm and Continue]**, votre session pour la portée globale se termine et la connexion au niveau du site web commence. Si vous avez cliqué accidentellement sur **[!UICONTROL Connect different account]**, vous pouvez annuler en sélectionnant **[!UICONTROL Cancel]** ou en cliquant sur l’icône **X** avant de confirmer.

## Terminer et revenir à l’administrateur

1. Après avoir effectué les étapes PayPal, fermez la fenêtre PayPal.
1. Cliquez sur **[!UICONTROL Finish]**, ou sur le **X** dans le coin supérieur droit, pour fermer la fenêtre contextuelle d’intégration.
1. La page de configuration de Commerce s’actualise automatiquement.

## Confirmer le résultat

Une fois la page actualisée, vérifiez les éléments suivants sur la page de configuration de l’étendue du site web :

- Une **[!UICONTROL PayPal Merchant ID]** mise à jour pour ce site web.
- Un libellé de statut affichant le résultat de l’intégration :

| Statut | Signification |
| --- | --- |
| `ACTIVE` | Intégration terminée avec succès |
| `PENDING` | L’intégration est toujours en cours de traitement. |
| `ERROR` | L’intégration n’a pas réussi |

Si un statut de `ERROR` s’affiche, un message d’erreur s’affiche pour expliquer le problème. Vous pouvez relancer le processus d’intégration en cliquant de nouveau sur **[!UICONTROL Connect different account]**.
