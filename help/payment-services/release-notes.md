---
title: Notes de mise à jour de [!DNL Payment Services]
description: Consultez les notes de mise à jour pour plus d’informations sur toutes  [!DNL Payment Services]  versions.
exl-id: 104aa2c7-7735-4ac2-8ed1-a03cd9911273
feature: Payments, Release Notes
source-git-commit: 7dabfc6c26ef77beec0ce9bab4c5c6d09a4d8827
workflow-type: tm+mt
source-wordcount: '4160'
ht-degree: 0%

---


# Notes de mise à jour

Ces notes de mise à jour décrivent la version initiale de [!DNL Payment Services] et incluent les éléments suivants :

![Nouveau](../assets/new.svg) Nouvelles fonctionnalités
![Correction d’un problème](../assets/fix.svg) Correctifs et améliorations
![Problème connu](../assets/bug.svg) Problèmes connus

Pour les modifications et correctifs de fonctionnalités publiés en dehors de la version standard de mise à jour des fonctionnalités, consultez les sections _Mises à jour de service hébergées_ .

Pour en savoir plus sur les prochaines versions, la prise en charge des produits et les versions d’Adobe Commerce qui prennent en charge l’extension [!DNL Payment Services], consultez les rubriques Adobe Commerce [Calendrier des versions](https://experienceleague.adobe.com/en/docs/commerce-operations/release/planning/schedule) et [Disponibilité du produit](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability).

## Mises à jour des services hébergés

Ces notes de mise à jour décrivent les modifications et correctifs de fonctionnalités qui se sont produits et ont été publiés en dehors des versions standard des fonctionnalités pour le service hébergé.

+++Mises à jour des services hébergés

_25 avril 2025_

![Nouvel événement ](../assets/new.svg)<!-- Issue PAY-6051 --> Désormais, [!DNL Payment Services] tableau de bord affiche à la fois la version actuelle de l’extension et la version du tableau de bord.

_30 août 2024_

![Nouvel événement](../assets/new.svg)<!-- Issue PAY-5658 --> Désormais, les commerçants peuvent filtrer les transactions en fonction des Détails de paiement dans le [rapport des transactions](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/transactions.html) pour obtenir des données plus détaillées et plus précises sur les modes de paiement.

_15 juillet 2024_

![Nouvel événement](../assets/new.svg)<!-- Issue PAY-5571 --> Désormais, les commerçants peuvent filtrer les transactions par e-mail du client Commerce dans le [rapport de transactions](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/transactions.html). Saisissez l’e-mail du client pour filtrer les transactions de cet e-mail spécifique.

_9 juillet 2024_

![Nouvel événement](../assets/new.svg)<!-- Issue PAY-5488 --> Désormais, les commerçants peuvent afficher l’ID client Commerce dans une colonne du [rapport des transactions](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/transactions.html) pour faciliter l’identification des transactions qu’un client particulier a passées. En outre, les commerçants peuvent filtrer le rapport des transactions en fonction de cet ID client Commerce pour les commandes associées.

_5 mars 2024_

![Correction d’un problème](../assets/fix.svg)<!-- Issue PAY-5252 --> Désormais, les commerçants peuvent copier les données des grilles du tableau de bord en sélectionnant le contenu d’une seule cellule.

_10 octobre 2023_

![Nouvel événement](../assets/fix.svg)<!-- Issue PAY-4888 --> Désormais, les commerçants peuvent filtrer les transactions par carte de crédit et de débit selon les quatre derniers chiffres du numéro de carte dans le [Rapport des transactions](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/transactions.html).

_12 juillet 2023_

![Correction d’un problème](../assets/fix.svg)<!-- Issue PAY-4587 --> Un problème introduit dans la version [!DNL Payment Services] 2.1.0 qui empêchait les vides d’autorisation placés par les versions d’extension précédentes est désormais résolu. Les commerçants qui utilisent n&#39;importe quelle version de [!DNL Payment Services] peuvent annuler les autorisations.

_9 juin 2023_

![Nouveau](../assets/new.svg)<!-- Issue PAY-4288 --> Désormais, les commerçants peuvent [configurer _uniquement_ les boutons de paiement PayPal](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options.html#use-only-paypal-payment-buttons) et _pas_ utiliser l&#39;option de paiement par carte de crédit PayPal. Cela permet aux commerçants de fournir diverses options de paiement, y compris des boutons de paiement Venmo et PayPal, et d&#39;utiliser un fournisseur de carte de crédit existant au lieu de l&#39;option de paiement par carte de crédit PayPal.

![Nouveau](../assets/new.svg)<!-- Issue PAY-4050 --> Ajout d&#39;une [vue de visualisation des données](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/order-payment-status.html#order-payment-status-data-visualization-view), qui s&#39;affiche sur l&#39;Accueil du service de paiement, pour l&#39;état Statut du paiement des commandes.

![Correction du problème](../assets/fix.svg)<!-- Issue PAY-4486--> Auparavant, le bouton PayPal PayLater n’apparaissait pas dans le passage en caisse pour les commerçants britanniques. Ce problème est résolu.

![Problème résolu](../assets/fix.svg)<!-- Issue PAY-4485--> Les vues de visualisation des données du rapport apparaissent désormais sur [!DNL Payment Services]’Accueil lorsque [!DNL Payment Services] est désactivé.

_25 janvier 2023_

![Problème connu](../assets/bug.svg)<!-- Issue PAY-4102 --> Les nouvelles installations de [!DNL Payment Services] ne peuvent pas configurer les services Commerce, ce qui rend les [!DNL Payment Services] inutilisables. Pour résoudre ce problème, mettez à jour votre extension [!DNL Payment Services] vers la version 1.5.3.

_12 septembre 2022_

![Nouveau](../assets/new.svg)<!-- Issue PAY-3705 --> Le `increment_id` peut désormais être utilisé pour rapprocher les paiements dans les systèmes ERP externes. Il est propagé aux [`custom_id` _et_ `invoice_id`](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/data.html#reconcile-with-erp-system), visibles dans le webhook PayPal et dans les détails de l’activité du commerçant pour un paiement.

_31 août 2022_

![Correction d’un problème](../assets/fix.svg)<!-- Issue PAY-3629 --> Lorsqu’un nouveau commerçant accède pour la première fois à la page d’accueil de [!DNL Payment Services], celle-ci se charge désormais immédiatement pour afficher le contenu, au lieu d’exiger une actualisation de page.

_9 août 2021_

![Nouveau](../assets/new.svg)<!-- Issue PAY-3420 --> Apple Pay est désormais disponible en tant que bouton intelligent PayPal. Cette [option de paiement](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-options.html#apple-pay-button) permet aux clients d’utiliser la fonction d’identifiant tactile sur leur appareil iOS ou macOS pour sélectionner Apple Pay. Apple Pay traite le paiement à l’aide des informations de paiement par carte de crédit et de débit stockées sur l’appareil.

_28 juin 2021_

![Nouveau](../assets/new.svg)<!-- Issue PAY-1720 --> Les litiges relatifs aux commandes en magasin sont désormais disponibles dans [l&#39;état Statut du paiement de la commande](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/order-payment-status.html#view-disputes). Vous pouvez résoudre les litiges en accédant directement au Centre de résolution PayPal à partir de [!DNL Payment Services].

![Nouveau](../assets/new.svg)<!-- Issue PAY-2854 --> Les améliorations de l’expérience utilisateur de [!DNL Payment Services]’accueil incluent la possibilité de modifier une configuration au niveau de l’héritage actuel, ainsi que des améliorations de l’affichage de l’en-tête et de la navigation.

![Nouveau](../assets/new.svg)<!-- Issue PAY-2854 --> des avertissements s’affichent désormais lorsque vous passez du mode sandbox au mode production et lorsque vous tentez de quitter une vue avec des mises à jour qui n’ont pas été enregistrées.

![Nouveau](../assets/new.svg)<!-- Issue PAY-2761 --> Vous pouvez désormais personnaliser les données qui s&#39;affichent dans l&#39;état [Statut du paiement des commandes](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/order-payment-status.html#show-and-hide-columns) et l&#39;état [Paiements](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/payouts.html#show-and-hide-columns) en affichant ou en masquant les colonnes à l&#39;aide du contrôle Paramètres des colonnes.

+++

>[!NOTE]
>
> Les versions se produisent fréquemment pour fournir de nouvelles fonctionnalités et de nouveaux correctifs si nécessaire. Le planning de publication n’est pas fixe.

## v2.12.1

_18 septembre 2025_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Problème résolu](../assets/fix.svg)<!-- PAY-6164 --> Désormais, [!DNL Payment Services] utilise la devise de base pour les méthodes d’expédition disponibles dans le **rappel d’expédition côté serveur (SSSC) PayPal**.

![Correction d’un problème](../assets/fix.svg)<!-- PAY-6267 --> le bloc **Adresse de livraison** est masqué sur la page de passage en caisse lorsque l’option **Récupération en magasin (ISPU)** est sélectionnée.

![Problème résolu](../assets/fix.svg)<!-- PAY-6271 --> Désormais, [!DNL Payment Services] affiche les détails de carte de crédit enregistrés à partir de PayPal PayFlow dans la section **Compte client** > **Modes de paiement stockés**.

## v2.12.0

_20 août 2025_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg)<!-- PAY-6022 --> [Fastlane](https://experienceleague.adobe.com/en/docs/commerce/payment-services/payments-checkout/payments-options) offre un achat plus rapide lors des passages en caisse des invités.

![Nouveau](../assets/new.svg)<!-- PAY-6168 --> Ajout de la mutation [`addProductsToNewCart`](https://developer.adobe.com/commerce/webapi/graphql/payment-services-extension/mutations/) à [!DNL Payment Services] pour permettre des transitions plus fluides et une meilleure réutilisation du panier.

![Nouveau](../assets/new.svg)<!-- PAY-6169 --> Ajout de la mutation [`setCartAsInactive`](https://developer.adobe.com/commerce/webapi/graphql/payment-services-extension/mutations/) à [!DNL Payment Services] pour améliorer la gestion du cycle de vie des devis.

![Nouveau](../assets/new.svg)<!-- PAY-6227 --> lors de la commande avec PayPal, [!DNL Payment Services] ignore le pop-up de confirmation de commande pour accélérer le processus d&#39;achat.

![Nouveau](../assets/new.svg)<!-- PAY-6234 --> Ajout d&#39;une nouvelle fonctionnalité pour l&#39;option de paiement [Payer plus tard](https://experienceleague.adobe.com/en/docs/commerce/payment-services/payments-checkout/payments-options). Désormais, le configurateur de messagerie BNPL offre plus de flexibilité pour afficher les messages BNPL à payer plus tard sur les pages de passage en caisse des clients.

![Problème résolu](../assets/fix.svg)<!-- PAY-5505 --> Désormais, [!DNL Payment Services] définit le devis comme inactif lorsqu’un pop-up Google Pay ou PayPal est fermé dans la page du produit.

![Problème résolu](../assets/fix.svg)<!-- PAY-5754 --> [!DNL Payment Services] n&#39;autorise plus la création de commandes à partir de devis vides.

## v2.11.1

_14 mars 2025_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Correction d’un problème](../assets/fix.svg)<!-- PAY-5849 --> Correction d’un problème qui affectait [Éléments de ligne](line-items.md) lors de la passage en caisse. Désormais, [!DNL Payment Services] a amélioré la fiabilité du processus de passage en caisse pour les **lignes**. Si vous rencontrez un problème similaire, contactez votre représentant commercial [!DNL Payment Services] pour obtenir de l’aide.

## v2.11.0

_13 mars 2025_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures


![Nouveau](../assets/new.svg)<!-- PAY-5938 --> Désormais, [!DNL Payment Services] permet aux commerçants de gérer les paramètres de paiement afin de maximiser la flexibilité de leur entreprise. Cette version améliore la possibilité de joindre [plusieurs comptes PayPal](https://experienceleague.adobe.com/en/docs/commerce/payment-services/configure/settings#use-multiple-paypal-accounts) pour les régions et les marques prises en charge par un commerçant. Notre équipe des ventes peut fournir un lien d’intégration pour configurer votre site web et les portées d’affichage de la boutique.

![Nouveau](../assets/new.svg)<!-- PAY-5968 --> Désormais, [!DNL Payment Services] met à jour la configuration d’administration avec les valeurs **ID de vendeur PayPal** et **Statut de vendeur PayPal**. Ces valeurs offrent aux commerçants une meilleure visibilité sur le statut de leur compte PayPal.

![Correction d’un problème](../assets/fix.svg)<!-- PAY-5816 --> Restauration de la fonctionnalité de commande normale dans [!DNL Payment Services] en résolvant un problème qui provoquait des erreurs dans tous les emplacements de commande avec la version v2.9.0.

![Correction d’un problème](../assets/fix.svg)<!-- PAY-5825 --> Correction d’un problème en raison duquel le mini-panier Apple Pay utilisait une URL de totaux estimés incorrecte pour les clients connectés. Désormais, [!DNL Payment Services] assure des calculs totaux précis.

![Correction d’un problème](../assets/fix.svg)<!-- PAY-5826 --> Amélioration de la fiabilité de la gestion des commandes en résolvant un problème qui provoquait une erreur HTTP 500 lors du changement du statut du devis en `inactive`.

![Correction d’un problème](../assets/fix.svg)<!-- PAY-5849 --> Correction d’un problème en raison duquel `LineItemProvider` générait des exceptions pour les quantités décimales inférieures à 1. Désormais, [!DNL Payment Services] offre une meilleure prise en charge des quantités fractionnelles.

![Correction d’un problème](../assets/fix.svg)<!-- PAY-5868 --> Correction d’une erreur de montant de carte cadeau lors du passage en caisse. [!DNL Payment Services] garantit désormais des valeurs précises pendant le processus de passage en caisse.

![Problème résolu](../assets/fix.svg)<!-- PAY-5911 --> Erreurs résolues lors de la création de l&#39;expédition pour les commandes passées à l&#39;aide de méthodes de paiement en ligne non [!DNL Payment Services], ce qui améliore la fiabilité globale.

![Problème résolu](../assets/fix.svg)<!-- PAY-5954 --> [!DNL Payment Services] offre désormais une expérience de passage en caisse plus fluide en résolvant un problème où Apple Pay n’avait pas passé de commande lorsqu’une autre carte de crédit avait été sélectionnée dans le portefeuille.

![Problème résolu](../assets/fix.svg)<!-- PAY-5971 --> [!DNL Payment Services] ne redirige plus les clients vers la page de révision des commandes lorsqu’Apple Pay échoue, ce qui évite les perturbations inutiles lors du passage en caisse.

## v2.10.3

_24 février 2025_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Problème résolu](../assets/fix.svg)<!-- PAY-xxxx --> Amélioration de la stabilité globale et des performances.

![Correction d’un problème](../assets/fix.svg)<!-- PAY-xxxx --> Améliorations et optimisations générales. Correction de bugs critiques dans la version v2.10.2.

## v2.10.2

_21 février 2025_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Problème connu](../assets/bug.svg)<!-- PAY-xxxx --> contient des bogues critiques qui peuvent affecter la stabilité et les performances. Adobe recommande d’effectuer une mise à niveau vers la version v2.10.3 au lieu d’utiliser cette version (v2.10.2).

## v2.10.1

_5 février 2025_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg)<!-- PAY-5813 --> Ajout de la prise en charge d’Adobe Commerce 2.4.8 et de PHP 8.4.

## v2.10.0

_13 décembre 2024_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg)<!-- PAY-5702 --> [!DNL Payment Services] prend désormais en charge les points d’entrée GraphQL pour le stockage en chambre forte sans achat, ce qui permet aux clients d’enregistrer leurs modes de paiement sans effectuer de transaction.

![Nouveau](../assets/fix.svg)<!-- PAY-5789 --> [!DNL Payment Services] prend désormais en charge l’authentification sécurisée [3D avec Google Pay](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/payment-services/security-compliance/security#3ds), ce qui renforce la sécurité pour les commerçants et les clients lors des transactions de paiement.

![Correctif](../assets/fix.svg)<!-- PAY-5703 --> [!DNL Payment Services] permet aux clients de [enregistrer leurs cartes directement dans leur **Mon compte**](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/payment-services/payments-checkout/vaulting), ce qui améliore la commodité et simplifie les paiements futurs. `Vault without purchase functionality might not be 100% compatible with Adobe Commerce 2.4.4 due to a known issue with` [`GraphQL authorization mechanisms`](https://developer.adobe.com/commerce/webapi/graphql/usage/authorization-tokens/).

![Correction](../assets/fix.svg)<!-- PAY-5762 --> correction d’un problème en raison duquel les codes de coupon n’étaient pas appliqués sur la page de révision de la commande lorsque celle-ci était lancée à partir de la page des détails du produit (PDP).

![Correctif](../assets/fix.svg)<!-- PAY-5792 --> [!DNL Payment Services] affiche désormais les descriptions et les adresses de facturation des cartes [voûtées sur la page de passage en caisse](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/payment-services/payments-checkout/vaulting), ce qui offre aux clients une plus grande visibilité sur leurs modes de paiement enregistrés.

![Correctif](../assets/fix.svg)<!-- PAY-5793 --> [!DNL Payment Services] permet aux commerçants de stocker l&#39;adresse de facturation des cartes voûtées directement à partir de la page de passage en caisse, assurant ainsi des informations de paiement exactes et complètes.

## v2.9.0

_7 novembre 2024_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg)<!-- PAY-5629 --> [!DNL Payment Services] prend désormais en charge une **URL SDK mise à niveau pour Apple Pay**, ce qui améliore l’intégration pour les commerçants utilisant Apple Pay. Cette fonctionnalité est compatible avec macOS 14 et versions ultérieures. Les appareils exécutant des versions antérieures de macOS n’afficheront pas cette fonctionnalité.

![Nouveau](../assets/new.svg)<!-- PAY-5630 --> Mise à jour des pages **Passage en caisse**, **Produit**, **Panier** et **MiniCart** afin de prendre en charge l’URL de SDK **mise à niveau pour Apple Pay**, ce qui améliore l’expérience utilisateur des commerçants qui proposent Apple Pay comme option de paiement.

![Nouveau](../assets/new.svg)<!-- PAY-5635 --> Amélioration des estimations d’expédition **basées sur l’adresse Apple Pay**, ce qui permet aux clients d’afficher des coûts d’expédition précis lors du passage en caisse.

![Correction](../assets/fix.svg)<!-- PAY-5661 --> Correction de divers problèmes de **[!DNL Payment Services]lors du passage en caisse**, ce qui améliorait la fiabilité du processus de paiement pour les commerçants et les acheteurs.

![Correctif](../assets/fix.svg)<!-- PAY-5692 --> Correction d’un problème en raison duquel le **prénom et nom du client** n’était pas ajouté à la commande lors de l’utilisation des **boutons intelligents pour un passage en caisse express**.

![Correction](../assets/fix.svg)<!-- PAY-5712 --> Correction d’un problème en raison duquel les commerçants **ne pouvaient pas effectuer le paiement à l’aide de l’option de paiement de passage en caisse avec sous-total nul** lorsque le montant total était gratuit.

## v2.8.1

_13 septembre 2024_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Correction](../assets/fix.svg)<!-- PAY-5644 --> correction d’un problème lié au cache des paramètres SDK lors de l’utilisation de plusieurs portées dans [!DNL Payment Services]. La configuration de SDK est désormais mise en cache séparément pour chaque portée au lieu d’être sous une seule clé. Cela garantit que le cache de chaque portée est invalidé indépendamment, ce qui améliore la fiabilité lors de la gestion de plusieurs portées.

## v2.8.0

_13 septembre 2024_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg)<!-- PAY-5499 --> [!DNL Payment Services] prend désormais en charge l’envoi d’informations de numéro de suivi à PayPal lorsqu’un [numéro de suivi est saisi](track-shipment.md) dans Adobe Commerce.

![Correctif](../assets/fix.svg)<!-- PAY-5626 --> [!DNL Payment Services] a optimisé le processus de demande au registre des commerçants lorsque les clients visitent la page de passage en caisse de Commerce. Auparavant, des demandes distinctes étaient effectuées pour chaque mode de paiement (champs hébergés, Google Pay, Apple Pay et boutons intelligents). Cette amélioration réduit le nombre d’appels et améliore les performances et l’efficacité pendant le processus de passage en caisse.

![Correctif](../assets/fix.svg)<!-- PAY-5645 --> [!DNL Payment Services] empêche désormais l’ouverture de la fenêtre contextuelle PayPal/Google Pay si l’acheteur n’a pas accepté les conditions générales personnalisées créées par le vendeur sur la page de passage en caisse.

![Correctif](../assets/fix.svg)<!-- PAY-5648 -->  [!DNL Payment Services] a résolu un problème lié à la répartition par ligne de la taxe sur le portail PayPal. Si la taxe est associée aux frais d&#39;expédition d&#39;une commande, la taxe sera incluse dans les frais d&#39;expédition et sera visible de cette manière dans les détails de ligne affichés sur le portail PayPal.

## v2.7.0

_2 août 2024_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg)<!-- PAY-4844 --> [!DNL Payment Services] prend désormais en charge [les données d’élément de ligne au niveau de la commande](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/payment-services/payments-checkout/manage/line-items). Cette fonctionnalité permet aux commerçants de voir des informations détaillées sur les articles d’une commande, telles que les détails du produit, la quantité et le prix (y compris la taxe de vente, les remises et d’autres informations pertinentes).

![Nouveau](../assets/new.svg)<!-- PAY-5380 --> [!DNL Payment Services] améliore l’expérience [Configuration dans l’administration](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/payment-services/configure/configure-admin#general-configuration) pour les commerçants afin de faciliter et d’intuitionner le processus d’intégration. Cette fonctionnalité permet aux commerçants de réinitialiser leurs identifiants [!DNL Payment Services].

![Nouveau](../assets/new.svg)<!-- PAY-5255 --> [!DNL Payment Services] comprend une [notification d’échec de paiement](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/point-of-purchase/checkout/checkout-payment-failed-emails). Cette fonctionnalité fournit des notifications en temps quasi réel des échecs de paiement aux commerçants, de sorte que les commandes peuvent être enregistrées en contactant l’acheteur et en améliorant potentiellement la résolution des problèmes.

![Correctif](../assets/fix.svg)<!-- PAY-5469 --> Correction d’un problème en raison duquel la fenêtre contextuelle de Google Pay **était bloquée par Safari**. Les acheteurs peuvent désormais effectuer leurs transactions de paiement Google Pay sur Safari.

![Correctif](../assets/fix.svg)<!-- PAY-5492 --> Correction d’un problème qui survenait lorsqu’un commerçant ajoutait des conditions générales personnalisées à la page de passage en caisse. Lors d’un passage en caisse [express](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options#standard-vs-advanced-payments-experience) un acheteur peut désormais accepter les présentes conditions générales pour effectuer le passage en caisse sans problème.

![Correctif](../assets/fix.svg)<!-- PAY-5532 --> Amélioration des fonctionnalités de collecte en magasin (ISPU) avec **InstantPurchase**. Les **méthodes de livraison ISPU** ne s’affichent plus lorsqu’un acheteur passe une commande avec **InstantPurchase**.

![Correctif](../assets/fix.svg)<!-- PAY-5606 --> Correction d’un problème dans le sélecteur de pays de la **Page de configuration** qui se produisait lorsque le pays du commerçant était défini sur **Allemagne**.

## v2.6.0

_4 juin 2024_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg)<!-- PAY-4877 --> Désormais, [!DNL Payment Services] prend en charge les fonctionnalités de tarification [L2/L3](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/levels-card-payment-transactions.html). Cette fonctionnalité est uniquement disponible pour les clients [!DNL Payment Services] pour lesquels le prix IC++ est activé. Si vous souhaitez utiliser des données de traitement L2/L3 pour [!DNL Payment Services], contactez votre gestionnaire de compte [!DNL Payment Services].

![Correctif](../assets/fix.svg)<!-- PAY-5455 -->[!DNL Payment Services] permet d’activer Apple Pay directement à partir de l’extension sans télécharger et héberger le fichier d’association de domaine [](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain).

## v2.5.0

_23 avril 2024_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Correctif](../assets/fix.svg)<!-- Issue PAY-5396 -->[!DNL Payment Services] prend désormais en charge les [instructions d’Adobe Commerce pour le paramètre `--db-prefix`](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/advanced#install-from-the-command-line) pour les versions 2.4.7 et ultérieures d’Adobe Commerce.

## v2.4.3

_16 avril 2024_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Correction](../assets/fix.svg)<!-- Issue PAY-5106 --> Correction d’un problème qui renseignait incorrectement les totaux des montants des commandes lors du passage en caisse entre PayPal et Adobe Commerce. Désormais, les commerçants peuvent s’assurer que les totaux des montants des commandes sont corrects lors de la commande.

## v2.4.2

_1 avril 2024_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg)<!-- Issue xxx --> Ajout de la prise en charge d’Adobe Commerce 2.4.7.

## v2.4.1

_4 avril 2024_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Correctif](../assets/fix.svg)<!-- PAY-5322 --> Correction d’un problème de compatibilité PCI avec les versions plus récentes d’Adobe Commerce. Désormais, [!DNL Payment Services] est adapté aux exigences de passage en caisse dans Adobe Commerce en tant qu’option de paiement.

![Fix](../assets/fix.svg)<!-- PAY-5323 --> PayLater et Venmo s’affichent correctement dans Adobe Commerce. Correction d’une erreur qui empêchait l’administrateur d’afficher les options de basculement PayLater et Venmo.

## v2.4.0

_20 mars 2024_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg)<!-- PAY-4868 --> les commerçants peuvent [configurer Google Pay tout au long de l’expérience d’achat](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options.html) comme les autres boutons de paiement dans [!DNL Payment Services] via l’administrateur.

![Nouveau](../assets/new.svg)<!-- PAY-4381 --> [Payment Services prend en charge Google Pay via GraphQL](https://developer.adobe.com/commerce/webapi/graphql/payment-services/) ce qui permet aux commerçants de bénéficier d’une expérience Commerce découplée grâce au mode de paiement Google Pay.

![Nouveau](../assets/new.svg)<!-- PAY-4878 --> Désormais, la fonctionnalité de passage en caisse de base [!DNL Payment Services] est proposée aux commerçants Adobe Commerce et Magento Open Source.[!DNL Payment Services] peut maintenant soutenir les commerçants ayant des entreprises dans n&#39;importe laquelle des 200 régions du monde.[!DNL Payment Services] paiement de base fournit des options de débit/crédit, PayPal, Venmo (le cas échéant) et PayLater (le cas échéant) dans une intégration en libre-service.

![Correctif](../assets/fix.svg)<!-- PAY-5291 --> La réception de la confirmation de paiement pour certaines transactions peut être retardée. Dans ce cas, les commerçants peuvent désormais obtenir un statut de paiement mis à jour pour une commande. [Payment Services détecte le statut en attente d&#39;une transaction de paiement](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/order-payment-status.html) dans une commande en détectant les transactions en attente et en surveillant de manière proactive ces transactions et en mettant à jour le moment où le statut en attente a été capturé.

## v2.3.4

_1er mars 2024_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg)<!-- PAY-5244 --> Correction de la compatibilité d’extraction asynchrone.

![Correctif](../assets/fix.svg)<!-- PAY-5253 --> Correction d’une erreur qui empêchait la suppression d’un jeton de coffre n’appartenant pas à [!DNL Payment Services].

## v2.3.3

_14 février 2024_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg)<!-- PAY-5048 --> Ajout de la prise en charge de PHP 8.3

![Correctif](../assets/fix.svg)<!-- PAY-5048 --> Correction d’une erreur avec l’indicateur `is_deleted`. Désormais, les commandes n’échouent pas en raison du statut de `Rejected` envoyé à partir de l’extension.

## v2.3.2

_26 janvier 2024_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Correctif](../assets/fix.svg)<!-- PAY-5183 --> Correction de problèmes de performances de REST/GraphQL. Désormais, le bouton de carte de crédit s’affiche lors de la récupération via l’API.

## v2.3.1

_7 décembre 2023_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg)<!-- PAY-5047 --> La marque de carte de crédit/débit ou le type de mode de paiement est désormais disponible aux emplacements suivants :
- la page des commandes client sur le storefront
- e-mail de confirmation de commande envoyé à l’acheteur
- dans la vue [Détails de la commande](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/order-management/orders/order-processing.html#view-an-order) dans l’Administration Commerce.

## v2.3.0

_1er décembre 2023_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg)<!-- PAY-4381 --> [Les services de paiement prennent désormais en charge l’intégration de GraphQL](https://developer.adobe.com/commerce/webapi/graphql/payment-services/). Avec la prise en charge par GraphQL des boutons de paiement PayPal, des champs hébergés et d’Apple Pay[!DNL Payment Services] prend désormais en charge une configuration Commerce découplée.

## v2.2.1

_27 septembre 2023_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Correction d’un problème](../assets/fix.svg)<!-- Issue PAY-4870 --> Correction d’un problème qui renseignait incorrectement le nouvel attribut d’en-tête dans Storefront lors de l’envoi de la version de l’extension avec la dernière version. Auparavant, avec la version `1.3.0` du connecteur Commerce Services, vous ne pouviez pas étendre le `User-Agent header` à partir de l’extension [!DNL Payment Services].

## v2.2.0

_30 août 2023_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg)<!-- PAY-4638 --> Ajout d’une [intégration à Signifyd](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/security-compliance/fraud-protection.html), qui fournit des services automatisés de protection contre la fraude.

![Nouveau](../assets/new.svg)<!-- PAY-3981 --> [Promotion d’Apple Pay en tant qu’option de paiement distincte](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options.html?lang=en#apple-pay-button) en dehors des boutons de paiement PayPal, afin d’accroître la visibilité de l’option de paiement pour les acheteurs et de permettre aux commerçants de contrôler l’emplacement et le style d’Apple Pay.

![Nouveau](../assets/new.svg)<!-- PAY-4002 --> Amélioration de l’expérience utilisateur lors du passage en caisse des champs de carte de crédit, y compris des améliorations du style, telles que l’ajout d’icônes de paiement, pour réduire la charge cognitive de l’acheteur et augmenter les conversions.

![Nouveau](../assets/new.svg)<!-- PAY-4002 --> Ajout d&#39;une fonctionnalité pour permettre aux commerçants de [trier l&#39;ordre de leurs options de paiement](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/configure/settings.html#payment-buttons) afin de prioriser certaines options de paiement. Cette fonctionnalité encourage un taux de conversation de passage en caisse plus élevé.

![Nouveau](../assets/new.svg)<!-- PAY-4035 --> Les commerçants peuvent désormais surveiller efficacement l&#39;intégrité de leurs magasins et identifier tout problème de transaction à l&#39;aide du nouveau [Rapport des transactions](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/transactions.html) disponible sur la page d&#39;accueil de l&#39;administrateur[!DNL Payment Services]. Le rapport présente également des données sur les taux d’autorisation des transactions et les tendances négatives des transactions.

## v2.1.0

_9 juin 2023_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg)<!-- Issue xxx --> Ajout de la prise en charge d’Adobe Commerce 2.4.7-bêta1.

![Nouveau](../assets/new.svg)<!-- Issue xxx --> Ajoutée [disponibilité dans les pays suivants et les devises associées](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/overview.html#availability) : Australie, France, Royaume-Uni.

![Nouveau](../assets/new.svg)<!-- Issue PAY-4296 --> Ajout de [ressources étendues pour les rôles d’administrateur](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/configure/settings.html#configure-roles) afin de garantir que les utilisateurs administrateurs puissent créer et gérer des commandes pour les clients et puissent voir[!DNL Payment Services] dans le menu Ventes.

![Nouveau](../assets/new.svg)<!-- Issue PAY-4236 --> Ajouté [annulation automatique pour les commandes qui génèrent des erreurs lors du passage en caisse](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/checkout.html#order-auto-voided-if-error).

![Nouveau](../assets/new.svg)<!-- Issue PAY-4183 --> Fonctionnalité créée pour [afficher le bouton d’option de paiement par carte de crédit/débit](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options.html#debit-or-credit-card-button) sur la page de passage en caisse.

## v2.0.0

_10 mars 2023_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg)<!-- Issue PAY-4152 --> Ajout de la prise en charge de PHP 8.2 et Adobe Commerce 2.4.6. Non compatible avec PHP 7.x.

## v1.6.1

_10 mars 2023_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Correctif](../assets/fix.svg)<!-- Issue PAY-4226 --> Correction d’un problème qui empêchait les nouveaux commerçants [!DNL Payment Services] d’utiliser le passage en caisse dans l’administrateur.[!DNL Payment Services] utilisait auparavant l’ID de client Commerce, qui n’existe pas pour les nouveaux clients.

![Correction](../assets/fix.svg)<!-- Issue PAY-4205 --> correction d’un problème en raison duquel le statut de l’adresse de livraison spécifiée était remplacé par le statut dans les paramètres de taxe par défaut lors du passage en caisse à l’aide de l’option [PayPal](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options.html#paypal-smart-buttons). Désormais, les clients peuvent faire expédier leurs commandes vers un état autre que celui configuré par défaut dans les paramètres fiscaux du commerçant.

![Correction](../assets/fix.svg)<!-- Issue PAY-4202 --> Correction d’un problème qui empêchait les clients d’utiliser le stockage par carte pour terminer un achat ou de supprimer un mode de paiement stocké pour un magasin [à l’aide de l’action de paiement `Authorize and Capture`](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/production.html#set-payment-services-as-payment-method). Auparavant, une erreur « Identifiant de coffre du fournisseur introuvable » s’affichait lorsque le client tentait d’utiliser ou de modifier ses cartes de crédit protégées.

## v1.6.0

_17 février 2023_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.0 et ultérieures

![Nouveau](../assets/new.svg)<!-- Issue PAY-3540 --> Ajout de la fonction de conformité [PCI 3DS pour les commerçants qui effectuent des transactions dans l’Union européenne (UE) et en Grande-Bretagne](security.md#3ds). Cette couche de sécurité supplémentaire, qui exige que les acheteurs s&#39;authentifient auprès de leur émetteur de carte de crédit, aide à prévenir la fraude en ligne et fait partie des règlements de conformité de l&#39;Union européenne (UE).

![Nouveau](../assets/new.svg)<!-- Issue PAY-3609 --> Ajout de la possibilité d’[activer le coffre de cartes dans l’administrateur](vaulting.md#use-vaulting-in-the-admin). Cela permet aux commerçants de créer une commande pour les clients de l’administrateur à l’aide de leurs méthodes de paiement voûtées.

## v1.5.4

_29 janvier 2023_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.0 et ultérieures

![Correction d’un problème](../assets/fix.svg)<!-- Issue PAY-4110 --> Correction d’un problème qui empêchait les acheteurs de passer une commande à l’aide de boutons de paiement sur la page du produit, le mini panier et le panier. Les acheteurs peuvent désormais passer des commandes avec succès.

## v1.5.3

_25 janvier 2023_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.0 et ultérieures

![Correction d’un problème](../assets/fix.svg)<!-- Issue PAY-4102 --> Publication d’un correctif pour un problème connu rétrocompatible. Cette version verrouille la version de l’extension d’ID de service sur la dernière version stable, ce qui permet aux nouvelles installations de [!DNL Payment Services] de configurer les services Commerce.

## v1.5.2

_2 décembre 2022_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.0 et ultérieures

![Correction d’un problème](../assets/fix.svg)<!-- Issue PAY-3992 --> Amélioration de la facturation dans [!DNL Payment Services] lorsqu’un mode de paiement est refusé.

![Problème résolu](../assets/fix.svg)<!-- Issue PAY-3999 -->[!DNL Payment Services] affiche désormais correctement les boutons de paiement PayPal pour les commerçants à l’aide du modèle personnalisé [Fire Checkout](https://commercemarketplace.adobe.com/swissup-firecheckout.html){target=_blank} pour la page de paiement. Auparavant, le mini-art affichait les boutons par intermittence.

## v1.5.1

_23 novembre 2022_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.0 et ultérieures

![Nouveau](../assets/new.svg)<!-- Issue PAY-3923 -->[!DNL Payment Services] inclut désormais le numéro de version dans l’en-tête de l’agent utilisateur afin que les requêtes puissent suivre, filtrer ou rendre obsolètes les points d’entrée inutilisés.

![Problème résolu](../assets/fix.svg)<!-- Issue PAY-3968 -->[!DNL Payment Services] affiche désormais correctement les données de commande lorsqu’une commande est passée à partir de la page produit à l’aide des boutons de paiement.

## v1.5.0

_18 novembre 2022_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.0 et ultérieures

![Nouveau](../assets/new.svg)<!-- Issue PAY-3880 --> Un acheteur peut désormais [enregistrer) ses informations de carte de crédit lors du passage en caisse](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/vaulting.html) pour les utiliser lors d’un achat ultérieur pour le même magasin ou un autre magasin dans le même compte marchand.

![Nouveau](../assets/new.svg)<!-- Issue PAY-3950 --> les commerçants peuvent désormais activer la fonctionnalité [Commerce d’achat instantané](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/point-of-purchase/checkout-instant-purchase.html) pour leurs magasins afin que les acheteurs puissent (utiliser [les informations de carte de crédit voûtées](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/vaulting.html)) accélérer le passage en caisse.

## v1.4.1

_14 octobre 2022_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.0 et ultérieures

![Correction](../assets/fix.svg)<!-- Issue PAY-3766 --> Lorsque le mode de paiement d’un client est refusé, le message d’erreur visible est plus explicite. Il conseille au client de saisir à nouveau les informations de paiement et d&#39;essayer à nouveau, d&#39;essayer un autre mode de paiement ou de contacter sa banque au sujet de la transaction refusée.

## v1.4.0

_30 septembre 2022_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.0 et ultérieures

![Nouveau](../assets/new.svg)<!-- Issue PAY-784 -->[!DNL Payment Services] offre désormais la possibilité de configurer un compte marchand pour [utiliser plusieurs comptes professionnels PayPal](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/configure/settings.html#use-multiple-paypal-accounts). Cela permet au commerçant d’exploiter vos magasins dans plusieurs pays à l’aide de différentes devises ou d’utiliser Adobe Commerce pour une partie de votre entreprise.

![Nouveau](../assets/new.svg)<!-- Issue PAY-3231 --> Les commerçants peuvent [ajouter un [!UICONTROL Soft Descriptor]](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/configure/settings.html#add-soft-descriptor) à des sites web ou à une configuration d’affichages de magasin individuels qui s’affiche sur les relevés bancaires de transaction du client pour délimiter les marques, les magasins ou les lignes de produits.

![Nouveau](../assets/new.svg)<!-- Issue PAY-3707 --> [Activez ou désactivez les champs de carte de crédit et les boutons de paiement PayPal](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/configure/settings.html#configure-payment-options) pour les paramètres de paiement en [!DNL Payment Services].

![Problème résolu](../assets/fix.svg)<!-- Issue PAY-3546 --> Lorsqu’un client clique sur **[!UICONTROL Edit cart]**, la page redirige vers la page du panier et affiche les articles mis à jour au lieu d’afficher un panier vide.

## v1.3.1

_6 septembre 2022_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.0 et ultérieures

![Problème résolu](../assets/fix.svg)<!-- Issue PAY-3663 --> Désormais, lorsque la boutique d’un commerçant capture une commande autorisée avec une devise non globale, le processus de capture se termine et aucune erreur ne s’affiche.

## v1.3.0

_9 août 2022_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.0 et ultérieures

![Nouvelle](../assets/new.svg)<!-- Issue PAY-XX --> Mise à jour de disponibilité générale - [!DNL Payment Services] est désormais [prise en charge par [!DNL Adobe Commerce] et [!DNL Magento Open Source] versions 2.4.0 à 2.4.5](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability).

![Problème résolu](../assets/fix.svg)<!-- Issue PAY-x --> Apple Pay est désormais compatible avec le navigateur Safari v15.5 pour mobiles et ordinateurs de bureau.

## v1.2.0

_29 juin 2022_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.0 et ultérieures

![Problème connu](../assets/bug.svg)<!-- Issue PAY-x --> Apple Pay est incompatible avec le navigateur Safari v15.5 pour mobiles et ordinateurs de bureau. Lors de l’utilisation de Safari version 15.5, vous ne pouvez pas terminer le passage en caisse avec Apple Pay.

![Problème résolu](../assets/fix.svg)<!-- Issue PAY-3264 --> Auparavant, lorsqu’un utilisateur connecté sélectionnait une adresse de facturation/d’expédition autre que l’adresse par défaut pour son compte, le passage en caisse échouait. Désormais, l’adresse de facturation/d’expédition sélectionnée est envoyée (au lieu de l’adresse enregistrée par défaut) et le passage en caisse est terminé avec succès.

![Problème résolu](../assets/fix.svg)<!-- Issue PAY-3314 --> Si vous désactivez les boutons de paiement PayPal pour le passage en caisse, aucune erreur ne s&#39;affiche.

![Problème résolu](../assets/fix.svg)<!-- Issue PAY-3330 --> Les paiements n’échouent plus lors du passage en caisse lorsqu’un utilisateur invité saisit un numéro de téléphone qui comprend des tirets.

![Correction d’un problème](../assets/fix.svg)<!-- Issue PAY-3338 PAY-2502 --> lorsque les informations d’identification des services Commerce ne sont pas valides[!DNL Payment Services] vous avertit désormais en affichant une erreur d’informations d’identification dans l’Accueil [!DNL Payment Services] de l’administrateur.

![Problème connu](../assets/bug.svg)<!-- Issue PAY-0 --> [!DNL Payment Services] est incompatible avec `commerce-data-export` v101.20 et les versions ultérieures, ce qui le rend incompatible avec l’extension [[!DNL Channel manager] ](https://experienceleague.adobe.com/docs/commerce-channels/channel-manager/guide-overview.html).

## v1.1.0

_31 mars 2022_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.0 et ultérieures

![Nouvelle](../assets/new.svg)<!-- Issue PAY-2127 --> Mise à jour de la disponibilité générale - [!DNL Payment Services] est désormais [prise en charge par les versions 2.4.0 à 2.4.4 [!DNL Adobe Commerce]  [!DNL Magento Open Source]  ](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability).

![Nouveau](../assets/new.svg)<!-- Issue PAY-2682 --> L&#39;extension [!DNL Payment Services] pour [!DNL Adobe Commerce] et [!DNL Magento Open Source] est maintenant disponible pour les commerçants canadiens. Les commerçants peuvent afficher la configuration des paiements en [français](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/overview.html?lang=fr#carte-de-cr%C3%A9dit-et-devises-accept%C3%A9es) ou [anglais](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/overview.html#accepted-credit-cards-and-currencies).

![Nouveau](../assets/new.svg)<!-- Issue PAY-2681 --> [!DNL Payment Services] prend en charge les [dollars canadiens (CAD)](introduction.md#accepted-credit-cards-and-currencies) pour les cartes de crédit et les transactions PayPal.

![Nouveau](../assets/new.svg)<!-- Issue PAY-2680 --> Les commerçants peuvent [embarquer [!DNL Payment Services]](onboard.md) une extension en anglais ou en français.

![Nouveau](../assets/new.svg)<!-- Issue PAY-2678 --> Les commerçants peuvent désormais consulter les rapports financiers, tant les rapports [État du paiement des commandes](order-payment-status.md) que [Rapports des paiements](payouts.md), en dollars canadiens (CAD).

![Problème résolu](../assets/fix.svg)<!-- Issue PAY-2710 -->[!DNL Payment Services] est désormais compatible avec [PHP 8.1](https://www.php.net/releases/8.1/en.php).

![Correction d’un problème](../assets/fix.svg)<!-- Issue PAY-3017 --> Amélioration de l’alerte du mode Sandbox pour afficher les alertes appropriées avec plusieurs magasins.

![Correction d’un problème](../assets/fix.svg)<!-- Issue PAY-2742 --> Vous pouvez désormais activer et désactiver les méthodes de paiement disponibles, telles que Venmo, au niveau de la vue du magasin. Auparavant, vous pouviez uniquement configurer les modes de paiement par site web.

![Correction d&#39;un problème](../assets/fix.svg)<!-- Issue PAY-2277 --> Vous pouvez désormais de manière sélective [activer ou désactiver les boutons de paiement PayPal individuels](configure-admin.md#payment-buttons).

![Problème résolu](../assets/fix.svg)<!-- Issue PAY-2561 --> les produits précédemment supprimés n’apparaissent pas dans le panier sur la page _Vérifier la commande_.

![Problème connu](../assets/bug.svg)<!-- Issue PAY-2842 --> Testez les transactions de carte de crédit [peuvent échouer avec PayPal](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-cc-sandbox-failure.html) lors du traitement des paiements dans un environnement Sandbox.

## v1.0.0

_29 novembre 2021_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.0 et ultérieures

![Nouvelle](../assets/new.svg)<!-- Issue PAY-2127 --> Version à disponibilité générale—[[!DNL Payment Services]](https://commercemarketplace.adobe.com/magento-payment-services.html) est désormais prise en charge par les versions 2.4.0 à 2.4.3-p1 de [!DNL Adobe Commerce] et [!DNL Magento Open Source].

![Nouveau](../assets/new.svg)<!-- Issue PAY-124 --> l’extension [!DNL Payment Services] pour [!DNL Adobe Commerce] et [!DNL Magento Open Source] peut être installée pour des instances [[!DNL Adobe Commerce] sur l’infrastructure cloud](install.md#adobe-commerce-on-cloud-infrastructure) ou [On-premise](install.md#on-premises). Ces méthodes nécessitent l’utilisation d’une interface de ligne de commande.

![Nouveau](../assets/new.svg)<!-- Issue PAY-1986 --> [!DNL Payment Services] prend en charge un [compte sandbox](sandbox.md) qui permet aux commerçants d’évaluer l’extension en mode test.

![Nouveau](../assets/new.svg)<!-- Issue PAY-666 --> Les commerçants peuvent [configurer l’extension des services de paiement](configure-admin.md) avec des comportements de paiement de base, tels que l’utilisation de [`Authorize and Capture`](production.md#set-payment-services-as-payment-method) le changement entre les environnements de sandbox ou de production.

![Nouveau](../assets/new.svg)<!-- Issue PAY-780 --> Vos acheteurs peuvent passer en caisse avec [!DNL Payment Services] ou via [création manuelle de commande](create-order.md).

![Nouveau](../assets/new.svg)<!-- Issue PAY-1856 --> des rapports complets, via les rapports [Statut du paiement des commandes](order-payment-status.md) et [Paiements](payouts.md), sont disponibles pour les [!DNL Payment Services] afin de vous donner une vue claire des commandes de votre magasin et des paiements associés.

![Nouveau](../assets/new.svg)<!-- Issue PAY-311 --> [!DNL Payment Services] prend en charge une tarification échelonnée flexible, basée sur le volume de traitement total, adaptée à tout commerçant.

![Nouveau](../assets/new.svg)<!-- Issue PAY-1443 --> Vous pouvez facilement [personnaliser l&#39;apparence](payments-options.md) des boutons de paiement PayPal et des champs de carte de crédit pour l&#39;extension [!DNL Payment Services].

![Problème connu](../assets/bug.svg)<!-- Issue PAY-2473 --> l’utilisation de [clés de compositeur incorrectes](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-install.html) lors de l’installation de l’extension empêche l’utilisateur de [s’authentifier](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys) avec les `MAGEID` correctes.

![Problème connu](../assets/bug.svg)<!-- Issue PAY-2474 --> [!DNL Payment Services] rapports [peuvent ne pas se synchroniser immédiatement](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-report-info-delayed.html).

![Problème connu](../assets/bug.svg)<!-- Issue PAY-2475 --> Votre [compte sandbox PayPal](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-paypal-acct.html) pour [!DNL Payment Services] ne peut pas être vérifié si vous créez ce compte lors de l’intégration.
