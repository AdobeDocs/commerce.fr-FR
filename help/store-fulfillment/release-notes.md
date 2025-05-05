---
title: Notes de mise à jour de [!DNL Store Fulfillment by Walmart Commerce Technologies]
description: Consultez les notes de mise à jour pour plus d’informations sur toutes  [!DNL Store Fulfillment by Walmart Commerce Technologies]  versions.
role: Admin, User, Leader
feature: Shipping/Delivery, Release Notes
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---

# Notes de mise à jour

Ces notes de mise à jour décrivent la version initiale de [!DNL Store Fulfillment Services by Walmart Commerce Technologies] et incluent les éléments suivants :

![Nouveau](../assets/new.svg) Nouvelles fonctionnalités
![Correction d’un problème](../assets/fix.svg) Correctifs et améliorations
![Problème connu](../assets/bug.svg) Problèmes connus

Voir [Prochaines versions](https://experienceleague.adobe.com/docs/commerce-operations/release/planning/schedule.html?lang=fr) pour en savoir plus sur les plannings de publication et la prise en charge.

Voir [Disponibilité du produit](https://experienceleague.adobe.com/docs/commerce-operations/release/product-availability.html?lang=fr) pour savoir quelles versions d’Adobe Commerce prennent en charge cette extension.

## v1.5.0

*3 août 2023*

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"}[Adobe Commerce versions 2.4.4 à 2.4.6](https://experienceleague.adobe.com/docs/commerce-operations/release/product-availability.html?lang=fr) avec correctifs de sécurité pour 2.4.6-p1, 2.4.5-p3 et 2.4.4-p4

Cette version comprend les mises à jour suivantes :

![Nouveau](../assets/fix.svg) Mise à jour de l’extension pour prendre en charge les [versions du correctif de sécurité Adobe Commerce ](https://experienceleague.adobe.com/docs/commerce-operations/release/notes/security-patches/overview.html?lang=fr) 2.4.6-p1, 2.4.5-p3 et 2.4.4-p4.

![Nouveau](../assets/new.svg)<!-- WMTP-918 --> Ajout de la prise en charge de l’option de configuration [Envoi asynchrone](sales-emails.md) pour les e-mails de ventes. Les commerçants qui effectuent une mise à niveau vers la version 1.5.0 ont la possibilité d’envoyer des e-mails immédiatement (par défaut) ou de manière asynchrone.

![Nouveau](../assets/new.svg)<!-- WMTP-916--> Mise à jour de la configuration [Sources](merchant-store-configuration.md) pour prendre en charge les formats de numéros de téléphone internationaux.

![Nouveau](../assets/new.svg) logique ajoutée pour empêcher les montants de remboursement de dépasser le montant restant ou le montant facturé.

![New](../assets/new.svg)<!-- WMTP-882 --> Remplacement de l’objet `google.map.LatLng` par des littéraux JSON pour prendre en charge la compatibilité avec les versions plus anciennes de [!DNL Google Maps].

![Correction d’un problème](../assets/fix.svg)<!-- WMTP- --> Mise à jour du script qui crée les attributs de produit `[!DNL Available for Store Pickup]` et `[!DNL Available for Home Delivery]` pour éviter les conflits de catégorie d’attributs.

![Correction d’un problème](../assets/fix.svg)<!-- WMTP-915 --> Correction d’un problème de compatibilité qui entraînait une boucle sans fin lors du chargement et de l’enregistrement de certaines entités.

![Correction d’un problème](../assets/fix.svg)<!-- WMTP-921 --> Correction d’un problème qui empêchait le déclenchement de la validation du devis [!DNL Ship to Store] lorsqu’un article était ajouté au panier à partir d’une page de détails du produit (PDP).

![Correction d’un problème](../assets/fix.svg)<!-- WMTP- 932 --> Correction d’un problème de passage en caisse qui permettait aux clients de sélectionner la méthode de livraison à domicile pour les articles non éligibles à la livraison à domicile.

![Problème résolu](../assets/fix.svg) Mises à jour de l’installation :

- &#x200B;<!-- WMTP-880--> Correction d’un problème en raison duquel un code de site web incorrect était renvoyé lors de l’installation de l’extension [!DNL Store Fulfillment].

- &#x200B;<!-- WMTP-878--> Correction d’un problème lié aux entiers de SKU qui nécessitait que le type de données soit converti en type chaîne lors de l’installation.

![Correction d’un problème](../assets/fix.svg)<!-- WMTP-915--> Correction d’un échec provoqué par un code d’erreur d’archivage manquant.

![Correction d&#39;un problème](../assets/fix.svg)<!-- WMTP-932 --> Correction d&#39;un bug lié au rejet partiel lors des opérations de distribution.

![Nouveau](../assets/new.svg)<!-- WMTP-953 --> Mise à jour du point d’entrée Annuler l’API pour utiliser le paramètre de statut comme un objet facultatif.

![Nouveau](../assets/new.svg)<!-- WMTP-960 --> Amélioration des détails de journalisation pour le point d’entrée de l’API Dispense.

## v1.4.0

*13 avril 2023*

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"}

![Nouveau](../assets/fix.svg) [!DNL Store Fulfillment] est désormais [compatible avec les  [!DNL Adobe Commerce] 2.4.4 à 2.4.6](https://experienceleague.adobe.com/docs/commerce-operations/release/product-availability.html?lang=fr).


## v1.3.0

*27 février 2023*

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"}

Cette version comprend la mise à jour suivante :

![Nouveau](../assets/fix.svg)<!-- WMTP-795 --> Ajout de la possibilité de désactiver la solution Store Fulfillment pour un site spécifique en modifiant la portée par défaut du paramètre de configuration système de Site web à Global.

## v1.2.0

*27 septembre 2022*

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"}

Cette version comprend la mise à jour suivante :

![Nouveau](../assets/fix.svg) [!DNL Store Fulfillment] est désormais [compatible avec les  [!DNL Adobe Commerce] 2.4.4 à 2.4.5](https://experienceleague.adobe.com/docs/commerce-operations/release/product-availability.html?lang=fr).


## v1.1.0

*15 juillet 2022*

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"}

Stabilité : Disponibilité générale

![Nouveau](../assets/fix.svg)<!-- WMTP-731 --> Simplification de la [configuration de l’expérience d’enregistrement](check-in-experience-setup.md) pour l’application d’assistance au magasin en ajoutant les sélections de marque et de modèle de voiture par défaut. Dans la version précédente, les commerçants devaient configurer manuellement les sélections de marques et de modèles de voitures.

## v1.0.0

*4 mars 2022*

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"}

Stabilité : Disponibilité générale

## Application Store Assist

Pour plus d’informations sur les nouvelles versions de l’application Store Assist, consultez les informations de l’application dans la boutique [Apple App Store](https://apps.apple.com/us/app/store-assist-by-walmart/id1609281539){target="_blank"} ou [Google Play](https://play.google.com/store/apps/details?id=com.walmart.faas.storeassist){target="_blank"}.
