---
title: Sécurité et conformité
description: Examinez les exigences de sécurité et de conformité de votre site.
feature: Payments, Checkout, Compliance
redirect_from: https://experienceleague.adobe.com/docs/commerce/payment-services/security.html
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 0%

---

# Sécurité et conformité

La sécurité est la plus grande préoccupation en [!DNL Payment Services] et aucune information réglementée par Private Card Industry (PCI) n&#39;est transmise à travers votre [!DNL Payment Services].

## Sécurité de Commerce

[!DNL Adobe Commerce] et [!DNL Magento Open Source] prennent en charge plusieurs fonctionnalités de sécurité.

Consultez [Sécurité](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/security){target="_blank"} dans le guide d’utilisation principal pour passer en revue les bonnes pratiques de sécurité et apprendre à gérer les sessions d’administration et les informations d’identification, à implémenter CAPTCHA et à gérer les restrictions de site web.

## Conformité PCI

L&#39;industrie des cartes de paiement (PCI) a établi un ensemble d&#39;exigences pour les entreprises qui acceptent le paiement par carte de crédit sur Internet. En plus de maintenir un environnement sécurisé, les commerçants qui manipulent les informations de carte de crédit client sont tenus de respecter certaines directives standard.

Pour plus d’informations, consultez [Instructions de conformité PCI](https://experienceleague.adobe.com/en/docs/commerce-admin/start/compliance/payments/compliance-pci){target="_blank"}.

Les commerçants peuvent remplir un [questionnaire d&#39;auto-évaluation (SAQ)](https://www.pcisecuritystandards.org/pci_security/completing_self_assessment){target="_blank"}, qui est un outil d&#39;auto-validation pour évaluer la sécurité des données des titulaires de carte.

### Champs de carte de crédit

Avec les champs de carte de crédit, aucune donnée réglementée par PCI n’est transmise à vos services. Vous n’avez pas à stocker ni à gérer ces données, ce qui réduit considérablement les problèmes de conformité PCI.

### 3DS

PCI 3-D Secure (3DS) permet l&#39;authentification de l&#39;acheteur auprès de son émetteur de carte de crédit lors des achats par carte de crédit en ligne. Cette couche de sécurité supplémentaire contribue à prévenir la fraude en ligne et est requise dans le cadre des réglementations de conformité de l’Union européenne (UE).

[!UICONTROL Payment Services] fournit des fonctionnalités 3DS pour permettre aux commerçants de se conformer aux réglementations de l&#39;UE et de protéger les clients et les commerçants contre les activités frauduleuses dans leurs magasins.

Si vous êtes un commerçant dans l’UE ou en Grande-Bretagne où la conformité 3DS est requise, vous devez activer manuellement la 3DS (elle est `Off` par défaut) dans [Paramètres](settings.md#credit-card-fields).

>[!IMPORTANT]
>
>L&#39;exigence des 3DS s&#39;applique aux opérations dans lesquelles l&#39;entreprise et la banque du titulaire de la carte sont situées dans l&#39;[Espace économique européen](https://www.efta.int/eea) (EEE) et en Grande-Bretagne. Les commerçants des États-Unis n&#39;ont pas besoin de 3DS, mais peuvent l&#39;activer pour leurs transactions si vous le souhaitez.

Les commandes passées pour l&#39;acheteur par le commerçant/le personnel du magasin ne sont pas configurées avec des mesures de conformité 3DS.

>[!MORELIKETHIS]
>
> * Voir [3DS dans Paramètres](settings.md#3ds) pour plus d’informations.
> * Voir [Tester les cartes](https://developer.paypal.com/docs/checkout/advanced/customize/3d-secure/test/) dans la documentation PayPal destinée aux développeurs pour plus d’informations sur les cartes de crédit spécifiques pour les tests 3DS.

### Coffre de cartes

Lorsqu’un acheteur [met en chambre forte ou « enregistre » ses informations de carte de crédit](vaulting.md) pour des achats futurs dans vos magasins, des informations de carte de crédit minimales sont partagées avec l’acheteur (les quatre derniers chiffres, la date d’expiration de la carte et la marque de la carte). Les informations de carte de crédit sont stockées auprès du fournisseur de paiement. Lorsqu’une carte expire ou qu’ils n’ont plus besoin des informations enregistrées, ils peuvent supprimer ce jeton afin que les informations ne soient plus stockées par le fournisseur de services de paiement.

Pour plus d’informations, consultez [chambre forte de carte de crédit](vaulting.md).

### Boutons de paiement PayPal

Avec les boutons de paiement PayPal, aucune donnée réglementée PCI n&#39;est transmise à vos services. Vous n’avez pas à stocker ni à gérer ces données, ce qui réduit considérablement les problèmes de conformité PCI.

Pour des raisons de sécurité, PayPal ne transmet pas l&#39;adresse de facturation lors du passage en caisse. Le pays, l&#39;adresse e-mail et le nom sont les seules informations de facturation utilisées. Vous pouvez éventuellement activer le paiement PayPal de votre site pour renvoyer l&#39;adresse de facturation complète en contactant PayPal et en effectuant un processus de vérification.

PayPal a également une protection intégrée contre la fraude qui utilise l&#39;apprentissage automatique pour vous aider à lutter contre la fraude. Pour plus d&#39;informations, consultez la [documentation sur la protection des vendeurs](https://www.paypal.com/us/webapps/mpp/security/seller-protection) de PayPal.

## Protection contre la fraude

Vous pouvez activer la protection automatique contre la fraude pour les services de paiement avec l’extension [Signifyd](https://commercemarketplace.adobe.com/signifyd-module-connect.html). Voir [Protection contre la fraude Signifyd](fraud-protection.md) pour plus d’informations.

PayPal propose d&#39;autres options de [protection contre la fraude](https://www.paypal.com/us/cshelp/article/what-is-fraud-protection-help1014){target=_blank} dans sa documentation destinée aux développeurs :

* Consultez [Protection antifraude avancée](https://www.paypal.com/us/enterprise/fraud-protection-advanced#fraud-protection-advanced){target=_blank} pour plus d’informations.
* Pour plus d’informations, consultez la section [Protection de refacturation](https://www.paypal.com/us/cshelp/article/what-is-chargeback-protection-help608){target=_blank}.
