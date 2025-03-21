---
title: Notes de mise à jour
description: Dernières informations de mise à jour pour l [!DNL Data Connection] extension d’Adobe Commerce.
feature: Personalization, Integration, Release Notes
exl-id: f3b92632-947d-40cd-89b7-24ed0680be51
source-git-commit: e92f6c2b748683fbe1a358680b03eefb27fe0093
workflow-type: tm+mt
source-wordcount: '1118'
ht-degree: 2%

---

# Notes de mise à jour

>[!IMPORTANT]
>
>Le connecteur Experience Platform a été renommé [!DNL Data Connection].

Ces notes de mise à jour contiennent des mises à jour de l’extension [!DNL Data Connection] et incluent :

![Nouveau](../assets/new.svg) - Nouvelles fonctionnalités
![Correctif](../assets/fix.svg) - Correctifs et améliorations
![Bug](../assets/bug.svg) - Problèmes connus

Pour connaître les modifications de fonctionnalités et les correctifs liés aux extensions utilisées par l’extension [!DNL Data Connection], voir **Mises à jour de service prises en charge**.

Voir [Prochaines versions](https://experienceleague.adobe.com/en/docs/commerce-operations/release/planning/schedule) pour en savoir plus sur les plannings de publication et la prise en charge.

Consultez la documentation destinée aux développeurs pour [découvrir quelles versions de Commerce prennent en charge ce module](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability).

## Mises à jour de service prises en charge

Ces notes de mise à jour décrivent les modifications de fonctionnalités et les correctifs liés aux extensions utilisées par l’extension [!DNL Data Connection].

+++Mises à jour de service prises en charge

_2 août 2024_

![Corriger](../assets/fix.svg) - Correction du montant total des paiements lorsque le total de la commande est configuré pour inclure les taxes.
![Nouveau](../assets/new.svg) - Ajout d’un champ `taxAmount` pour commander des événements d’achat.
![Nouveau](../assets/new.svg) - Ajout de la possibilité d’ajouter des données personnalisées aux événements. Pour obtenir un [exemple](https://github.com/adobe/commerce-events/blob/main/examples/events/custom-event-override.md), reportez-vous à la section suivante.

_24 janvier 2024_

![Nouveau](../assets/new.svg) - Mise à jour de l’extension `data-services-b2b` pour inclure un nouvel événement de demande d’approvisionnement appelé [deleteRequisitionList](events.md#deleterequisitionlist) pour les commerçants B2B.

_16 novembre 2023_

![Correctif](../assets/fix.svg) - Correction d’un problème en raison duquel un message d’erreur s’affichait incorrectement lorsque vous passiez une commande comportant plusieurs adresses d’expédition.
![Corriger](../assets/fix.svg) - Correction d’un problème dans l’événement [productPageView](events.md#productpageview) en raison duquel le champ d’événement `productListItems.priceTotal` ne convertissait pas le prix après le changement de devise dans la vue du magasin.
![Correctif](../assets/fix.svg) - Correction d’un problème dans le champ d’événement `productListItems` en raison duquel le code de devise n’était pas mis à jour lorsque le commerçant a basculé sur la vue de la boutique.

_10 octobre 2023_

![Nouveau](../assets/new.svg) - Ajout de nouveaux événements de statut de commande : [Commande facturée](events-backoffice.md#orderinvoiced), [Retour d&#39;article de commande initié](events-backoffice.md#orderitemsreturninitiated) et [Retour d&#39;article de commande terminé](events-backoffice.md#orderitemreturncompleted).
![Correctif](../assets/fix.svg) - Correction d’un problème en raison duquel les modifications de configuration de devise n’étaient pas reflétées dans les événements après l’actualisation du cache.
![Correctif](../assets/fix.svg) - Correction d’une erreur qui empêchait l’affichage du message de confirmation de commande si le placement de commande asynchrone était activé.
![Nouveau](../assets/new.svg) - Ajout de données à l’événement [addToRequisitionList](events.md#addtorequisitionlist) pour les produits simples sur la page Affichage des catégories.
![Correctif](../assets/fix.svg) - Correction d’un problème dans les données `selectedOptions` de l’événement [addToRequisitionList](events.md#addtorequisitionlist) lorsque des produits sont ajoutés à partir de la page de confirmation de commande.
![Nouveau](../assets/new.svg) - Ajout de données de produit à l&#39;événement [addToRequisitionList](events.md#addtorequisitionlist) lorsque des produits sont ajoutés à la liste de demandes d&#39;approvisionnement à partir de la page de vue Catégorie.
![Nouveau](../assets/new.svg) - Événement ajouté [addToRequisitionList](events.md#addtorequisitionlist) lorsque des produits configurables sont ajoutés à la liste de demandes d&#39;approvisionnement à partir de la page d&#39;affichage des produits.
![Nouveau](../assets/new.svg) - Ajout d&#39;événements [addToRequisitionList](events.md#addtorequisitionlist) et [removeFromRequisitionList](events.md#removefromrequisitionlist) lorsque la quantité de produits est augmentée et/ou diminuée à partir d&#39;une liste de demandes d&#39;approvisionnement.

_10 juin 2023_

![Correctif](../assets/fix.svg) - Correction d’un problème en raison duquel `orderId` n’était pas transmis dans le contexte en raison de préfixes dans l’identifiant de commande Commerce.
![Correctif](../assets/fix.svg) - Mise à jour des configurations de la politique de sécurité du contenu.

_30 mars 2023_

![Nouveau](../assets/new.svg) - Ajout d’une extension appelée `data-services-b2b` qui inclut [des événements de liste de demandes](events.md#b2b-events) pour les commerçants B2B.
![Nouveau](../assets/new.svg) - Ajout du champ `uniqueIdentifier` aux événements [rechercher](events.md#search-events). Ce nouveau champ permet aux commerçants de faire des références croisées entre les demandes de recherche et les réponses de recherche.

_12 octobre 2022_

![Nouveau](../assets/new.svg) - Ajout de deux [événements storefront](events.md), `openCart` et `removeFromCart`, au SDK et au collecteur d’événements storefront Adobe Commerce.
![Nouveau](../assets/new.svg) - Ajout de la prise en charge d’un [storefront AEM](overview.md#aem-support).

+++

## 3.3.0

_21 mars 2025_

[!BADGE Compatibilité ]{type=Informative tooltip="Compatibilité"}

![Nouveau](../assets/new.svg) Ajout de la prise en charge de PHP 8.4.

## 3,2,1

_17 janvier 2025_

[!BADGE Compatibilité ]{type=Informative tooltip="Compatibilité"}

![Nouveau](../assets/new.svg) - Ajout de l’extension [conforme à la loi HIPAA](hipaa-readiness.md) à [!DNL Data Connection] afin que les commerçants puissent partager [!DNL Commerce] données d’événement back-office avec Experience Platform et respecter la loi HIPAA.
![Correctif](../assets/fix.svg) - Correction d’un problème en raison duquel l’extension [!DNL Data Connection] remplaçait les données `eventForwarding` et définissait l’indicateur `HIPAA` pour tous les clients. Désormais, l’extension définit uniquement l’indicateur pour les clients HIPAA.

## 3.2.0

_7 octobre 2024_

[!BADGE Compatibilité ]{type=Informative tooltip="Compatibilité"}

![Nouveau](../assets/new.svg) - Possibilité de créer des [attributs de commande personnalisés](custom-attributes.md) pour les données de back-office.
![Nouveau](../assets/new.svg) - Ajout d’un nouveau tableau [Attributs de commande personnalisés](connect-data.md#data-customization) pour vous aider à afficher les attributs personnalisés configurés dans [!DNL Commerce] et envoyés à Experience Platform.
![Nouveau](../assets/new.svg) - Possibilité de [collecter et envoyer des enregistrements de profil](connect-data.md#send-customer-profile-data) et des données à Experience Platform.

## 3.2.0-bêta3

_27 août 2024_

[!BADGE Compatibilité ]{type=Informative tooltip="Compatibilité"}

![Nouveau](../assets/new.svg) - Si vous participez à la version bêta, assurez-vous que votre fichier `composer.json` comporte les éléments suivants au niveau racine : ` "minimum-stability": "beta"`. Ajoutez également des `composer require "magento/customers-connector: ^1.2.0"` pour envoyer les profils client de votre instance Commerce à SaaS.
![Nouveau](../assets/new.svg) - Cette version contient les correctifs publiés dans 3.1.1, 3.1.2, 3.1.3 et 3.1.4.

## 3.1.4

_9 août 2024_

[!BADGE Compatibilité ]{type=Informative tooltip="Compatibilité"}

![Correctif](../assets/fix.svg) - Mise à jour du métapaquet `experience-platform-connector` pour supprimer les autres exportateurs et indexeurs de données inutilisés.

## 3.1.3

_2 juillet 2024_

[!BADGE Compatibilité ]{type=Informative tooltip="Compatibilité"}

![Correctif](../assets/fix.svg) - Mise à jour du métapaquet `experience-platform-connector` pour supprimer les exportateurs de données et les indexeurs inutilisés.

## 3.1.2

_5 juin 2024_

[!BADGE Compatibilité ]{type=Informative tooltip="Compatibilité"}

![Correctif](../assets/fix.svg) - Correction d’un problème en raison duquel un format de date incorrect était utilisé lors du lancement d’une [synchronisation historique](connect-data.md#specify-order-history-date-range).
![Correctif](../assets/fix.svg) - Correction d’un problème où l’événement [startCheckout](events.md#startcheckout) n’était pas envoyé sur Adobe Commerce 2.4.7.

## 3.1.1

_4 avril 2024_

[!BADGE Compatibilité ]{type=Informative tooltip="Compatibilité"}

![Nouveau](../assets/new.svg) - Ajout de la prise en charge de PHP 8.3 pour toutes les extensions [!DNL Data Connection].
![Nouveau](../assets/new.svg) - Ajout d’un article sur l’[intégration](mobile-sdk-epc.md) de Adobe Experience Platform Mobile SDK à Commerce.

## 3.2.0-beta2

_4 mars 2024_

[!BADGE Compatibilité ]{type=Informative tooltip="Compatibilité"}

![Nouveau](../assets/new.svg) - Si vous participez à la version bêta, assurez-vous que votre fichier `composer.json` comporte les éléments suivants au niveau racine : ` "minimum-stability": "beta"`. Ajoutez également des `composer require "magento/customers-connector: ^1.2.0"` pour envoyer les profils client de votre instance Commerce à SaaS.
![Nouveau](../assets/new.svg) - Possibilité d’[ajouter des attributs personnalisés](custom-attributes.md).
![Nouveau](../assets/new.svg) - Possibilité de [collecter et envoyer des enregistrements de profil](connect-data.md#send-customer-profile-data) et des données à Experience Platform.

## 3.1.0

_16 novembre 2023_

[!BADGE Compatibilité ]{type=Informative tooltip="Compatibilité"}

![Nouveau](../assets/new.svg) - Le connecteur Experience Platform a été renommé [!DNL Data Connection].
![Correctif](../assets/fix.svg) - Possibilité de consigner la réponse d’erreur si Adobe IMS ne peut pas générer le jeton d’accès.
![Correctif](../assets/fix.svg) - Ajout d’un message de notification si vous tentez de synchroniser les commandes historiques mais que vous n’avez pas spécifié d’informations d’identification de compte.

## 3.0.0

_10 octobre 2023_

[!BADGE Compatibilité ]{type=Informative tooltip="Compatibilité"}

Il s’agit d’une version majeure. [Modifiez](install.md#update-the-data-connection) le fichier racine composer.json de votre projet.

![Nouveau](../assets/new.svg) - Disponibilité générale pour [envoyer l’ordre historique](connect-data.md#send-historical-order-data) les données et le statut à Experience Platform.
![Nouveau](../assets/new.svg) - Ajout de la prise en charge d’OAuth 2.0 lorsque vous [configurez](connect-data.md#connect-commerce-data-to-adobe-experience-platform) l’extension [!DNL Data Connection].
![Nouveau](../assets/new.svg) - Fin de la prise en charge d’Adobe Commerce 2.4.3.

## 2.3.0

_27 juin 2023_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"}

![Nouveau](../assets/new.svg) - Possibilité de [désactiver l’envoi d’événements de storefront](connect-data.md#data-collection) à Experience Platform.
![Correctif](../assets/fix.svg) - Mise à jour des configurations de la politique de sécurité du contenu.
![Correctif](../assets/fix.svg) - Correction de la prise en charge des événements back-office sur la version 2.4.7 de Commerce.
![Nouveau](../assets/new.svg) - Ajout d’un message de notification concernant l’invalidation du cache lorsque vous enregistrez les modifications apportées au formulaire d’extension [!DNL Data Connection].

## 3.0.0-beta1 (interne uniquement)

_13 juin 2023_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"}

![Nouveau](../assets/new.svg) - (Beta) Possibilité d’[envoyer les données et le statut de l’ordre historique](connect-data.md#beta-send-historical-order-data) à Experience Platform.

## 2.2.0

_30 mars 2023_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"}

![New](../assets/new.svg) - Regroupement des dépendances `commerce-data-export` et `saas-export` avec l’extension `experience-platform-connector`. Auparavant, vous deviez installer ces dépendances séparément. Ces dépendances, ainsi que la configuration du commerçant, permettent le traitement côté serveur des [événements back-office](events-backoffice.md).
![Nouveau](../assets/new.svg) - Ajout d’un nouvel événement back-office appelé [`orderShipmentCompleted`](events-backoffice.md#ordershipmentcompleted).

## 2.1.1

_28 février 2023_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"}

![Nouveau](../assets/new.svg) - Ajout de la prise en charge de PHP 8.2 pour toutes les extensions [!DNL Data Connection].

## 2.1.0

_17 janvier 2023_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"}

![Nouveau](../assets/new.svg) - Mise à jour de l’[[!DNL Data Connection] extension Admin](connect-data.md) afin que vous puissiez spécifier votre propre SDK Web AEP (alliage).
![Correctif](../assets/fix.svg) Modification de l’utilisation de `identityMap` au lieu de `personID` lors de la définition de l’identité principale pour toutes les données poussées vers Edge.

## 2.0.1

_10 novembre 2022_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"}

![Correctif](../assets/fix.svg) - Désormais, le contexte Adobe Experience Platform n’est défini qu’une fois le collecteur d’événements Storefront et le SDK d’événements Storefront chargés avec succès.

## 2.0.0

_12 octobre 2022_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"}

![Nouveau](../assets/new.svg) - Possibilité de spécifier votre propre SDK Web AEP lors de la [connexion](connect-data.md) de votre instance Adobe Commerce à Experience Platform.
![Correctif](../assets/fix.svg) - Mise à jour de l’exigence de portée du train de données afin que les identifiants du train de données soient limités au site web plutôt qu’à la révision.

## 1.0.0

_9 août 2022_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"}

![Nouveau](../assets/new.svg) - Version mise à disposition générale.
