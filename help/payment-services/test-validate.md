---
title: Tester et valider
description: Les tests et la validation permettent de s [!DNL Payment Services] assurer que les fonctions fonctionnent comme prévu et offrent les meilleures options de paiement pour vos clients
exl-id: 95b4615e-73b0-41e8-83e2-e65a0b22f10f
feature: Payments, Checkout, Paas, Saas
source-git-commit: 91a4b8fa7228fb91c8ee0bf0a1623d104f061894
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 0%

---

# Tester et valider

Avant d’exposer [!DNL Payment Services] pour [!DNL Adobe Commerce] et [!DNL Magento Open Source] à vos clientes et clients, il est préférable de les tester dans votre environnement de sandbox _et_ en production. Les tests et la validation permettent de s’assurer que [!DNL Payment Services] fonctions fonctionnent comme prévu et fournissent les meilleures options de paiement pour votre magasin et vos clients.

## Test dans un environnement sandbox

Tester les [!DNL Payment Services] dans un environnement sandbox est une étape de validation importante, même s’il s’agit d’un environnement simulé connecté uniquement au sandbox PayPal, et non à de vraies banques et commerçants.

1. Effectuez un passage en caisse réussi à partir de votre boutique, soit avec les [champs de carte de crédit](payments-options.md#credit-card-fields) ou l&#39;un des [boutons de paiement PayPal](payments-options.md#paypal-smart-buttons). Consultez [Test des informations d’identification](#testing-credentials) pour plus d’informations sur l’utilisation de fausses cartes de crédit pour les tests.
1. Capturez (lorsque votre action de paiement est [définie sur `Authorize and Capture`](onboard.md#set-payment-services-as-payment-method)), [remboursez](refunds.md) ou [annulez](voids.md) la commande qui vient d’être terminée. Vous pouvez également simplement [créer une facture](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice){target="_blank"} pour une commande, si votre action de paiement est définie sur `Authorize` au lieu de `Authorize and Capture`.
1. Dans les 24 à 48 heures, affichez la transaction et d&#39;autres informations dans le [rapport des paiements](payouts.md).
1. Voir les détails de la commande dans l&#39;état [Statut du paiement de la commande](order-payment-status.md).

### Test sur les environnements de développement locaux

Le test des méthodes de paiement PayPal, PayLater et Venmo sur les environnements de développement locaux nécessite que votre environnement soit accessible à partir d&#39;Internet. Ces méthodes de paiement utilisent un [rappel d’expédition côté serveur](https://developer.paypal.com/docs/multiparty/checkout/standard/customize/shipping-module/) qui nécessite que PayPal communique avec votre instance Commerce pour récupérer les options d’expédition et calculer les totaux.

>[!INFO]
>
>Sans une URL accessible sur Internet, le rappel d’expédition ne peut pas fonctionner, ce qui entraîne un flux de passage en caisse différent de celui de la production. Effectuez toujours un test avec une URL accessible pour garantir des résultats précis.

Pour exposer votre environnement local :

1. Utilisez un service de tunneling tel que [ngrok](https://ngrok.com/) pour créer une URL accessible au public pour votre environnement local.

1. Mettez à jour la configuration de votre URL de base Commerce pour qu’elle corresponde à l’URL du groupe :

   ```bash
   bin/magento config:set web/unsecure/base_url https://your-ngrok-url.ngrok.io/
   bin/magento config:set web/secure/base_url https://your-ngrok-url.ngrok.io/
   bin/magento cache:flush
   ```

1. Complétez vos tests avec les méthodes de paiement PayPal, PayLater ou Venmo.

1. Restaurez la configuration de l’URL de base d’origine une fois le test terminé.

Si le temps de réponse du point d&#39;entrée est inférieur à 5 secondes, PayPal affiche un message d&#39;erreur dans le pop-up.

#### Développement local d’Apple Pay

Apple Pay nécessite une configuration supplémentaire pour le développement local. Apple Pay utilise l’enregistrement de domaine pour vérifier que votre site est autorisé à accepter les paiements Apple Pay. Cela signifie qu’Apple doit être en mesure d’accéder à votre domaine pour valider un fichier de vérification de domaine à l’`/.well-known/apple-developer-merchantid-domain-association`.

Pour le développement local, votre environnement doit répondre aux exigences suivantes :

* **accessible au public**, Apple doit pouvoir accéder à votre domaine à partir d’Internet.
* **protocole HTTPS**, Apple Pay ne fonctionne que sur des connexions sécurisées.

L’utilisation d’un service de tunneling tel que [ngrok](https://ngrok.com/) répond aux deux exigences. Après avoir configuré ngrok comme décrit ci-dessus, [enregistrez votre domaine sandbox](https://developer.paypal.com/docs/checkout/apm/apple-pay/#link-registeryoursandboxdomains) avec PayPal en utilisant l’URL **ngrok**.

### Test des informations d’identification

Lors du test et de la validation de votre sandbox , vous devez utiliser de faux numéros de carte de crédit, afin de ne pas créer de frais réels sur un compte de carte de crédit existant.

Utilisez le générateur de cartes de crédit PayPal pour [générer des informations de carte de crédit aléatoires](https://www.paypal.com/us/smarthelp/article/where-can-i-find-test-credit-card-numbers-ts2157) à des fins de test.

Pour tester Apple Pay en mode sandbox :

* Créez un compte de testeur de sandbox [Apple](https://developer.apple.com/apple-pay/sandbox-testing/#create-a-sandbox-tester-account) avec une fausse carte de crédit et de fausses informations de facturation.
* [Enregistrement de vos domaines Sandbox](https://developer.paypal.com/docs/checkout/apm/apple-pay/#link-registeryoursandboxdomains).

>[!NOTE]
>
>Le traitement des paiements par PayPal est parfois lent et le service peut parfois tomber en panne. Cette situation n’est pas une indication de la rapidité et de l’efficacité du traitement des paiements de produits en direct.

## Test en production

Il est vivement recommandé de tester les [!DNL Payment Services] en production, avec des cartes de crédit et des banques réelles, avant de présenter cette fonctionnalité aux acheteurs. Bien que le test des [!DNL Payment Services] dans le sandbox soit important, le test en production est la méthode la plus infaillible pour s’assurer que [!DNL Payment Services] fonctionne comme prévu.

Vous pouvez tester les [!DNL Payment Services] en production de deux manières :

* Choisissez un moment où vous savez qu&#39;aucune commande ne sera passée par les acheteurs.
* Utilisez une boutique en ligne temporairement inaccessible aux acheteurs, mais que vous pouvez tester.

Complétez vos tests de production avec des cartes de crédit et des comptes PayPal réels, en testant l&#39;ensemble du cycle de vie d&#39;un paiement, y compris la capture et le remboursement. En complétant l’ensemble du flux de paiement et de passage en caisse pendant les tests, vous avez une idée précise du fonctionnement de votre fonctionnalité de [!DNL Payment Services] lorsque les acheteurs en direct l’utilisent.

Vous devez également vérifier que les renseignements qui figurent sur les relevés bancaires pour les méthodes de paiement que vous utilisez dans les tests de production sont corrects et attendus (y compris la description de votre entreprise).

### Tester Apple Pay en production

Pour tester Apple Pay en mode production, vous devez [enregistrer vos domaines de production](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain).
