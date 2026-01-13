---
title: Notes de mise à jour de l’intégration AEM Assets
description: Consultez les notes de mise à jour pour plus d’informations sur toutes les versions de l’intégration AEM Assets.
feature: CMS, Media, Release Notes
exl-id: 0d639565-812f-481a-afd6-6e6fa54ed70e
source-git-commit: 4f95ca25da819d5c8dfa99e1380edf672f3e0249
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 0%

---

# Notes de mise à jour de l’intégration AEM Assets

Ces notes de mise à jour décrivent toutes les versions de l’intégration AEM Assets et incluent :

![Nouveau](../assets/new.svg) Nouvelles fonctionnalités
![Correction d’un problème](../assets/fix.svg) Correctifs et améliorations
![Problème connu](../assets/bug.svg) Problèmes connus

Pour les modifications et correctifs de fonctionnalités publiés en dehors de la version standard de mise à jour des fonctionnalités, consultez les sections _Mises à jour de service hébergées_ .

Pour en savoir plus sur les prochaines versions, la prise en charge des produits et les versions d’Adobe Commerce qui prennent en charge l’extension d’intégration d’AEM Assets, consultez les rubriques Adobe Commerce [Calendrier des versions](https://experienceleague.adobe.com/en/docs/commerce-operations/release/planning/schedule) et [Disponibilité du produit](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability).

## Mises à jour des services hébergés

Ces notes de mise à jour décrivent les modifications et correctifs de fonctionnalités qui se sont produits et ont été publiés en dehors des versions standard des fonctionnalités pour le service hébergé.

+++Mises à jour des services hébergés

_1 septembre 2025_

![Nouveau problème](../assets/new.svg) Mise à jour des points d’entrée [correspondance automatique personnalisée](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/synchronize/custom-match){target=_blank} avec un nouvel attribut `asset_matches`.

_1 février 2025_

![Nouvel événement](../assets/new.svg) Désormais, les commerçants peuvent synchroniser les images des produits et des catégories.

+++

## v1.2.11

_15 janvier 2026_

[!BADGE pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce version 2.4.5 et versions ultérieures.

![Correction d’un problème](../assets/fix.svg)<!-- Issue ACAP-1180 --> Améliorations générales de la page de modification du produit. Désormais, les pages s’affichent correctement lorsque l’intégration d’AEM Assets est activée.

## v1.2.10

_12 janvier 2026_

[!BADGE pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce version 2.4.5 et versions ultérieures.

![Correction d’un problème](../assets/fix.svg)<!-- Issue ACAP-1178 --> Correction d’un problème en raison duquel les attributs personnalisés du produit ne pouvaient pas être mis à jour via l’API REST lorsque le produit avait une image et que l’intégration d’AEM Assets était activée. Désormais, les attributs personnalisés du produit se mettent correctement à jour via l’API REST.

![Correction d’un problème](../assets/fix.svg)<!-- Issue ACAP-1172 --> Correction d’un problème où les images de produit masquées n’étaient pas affichées comme masquées dans l’interface utilisateur d’administration sur la page de modification du produit. Désormais, le statut de visibilité des images s’affiche correctement.

![Correction d’un problème](../assets/fix.svg)<!-- Issue ACAP-1170 --> Correction d’un problème où les images de produits d’AEM Assets n’étaient pas synchronisées avec Adobe Commerce en raison d’une erreur de désérialisation. Désormais, tous les attributs d’image (`image`, `small_image` et `swatch_image`) se synchronisent correctement.

## v1.2.7

_6 novembre 2025_

[!BADGE pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce version 2.4.5 et versions ultérieures.

![Correction d’un problème](../assets/fix.svg)<!-- Issue ACAP-1169 --> Correction d’un problème en raison duquel les miniatures de produit s’affichaient de manière incohérente après l’activation de l’intégration d’AEM Assets sur les pages **Mini panier**, **panier** et **passage en caisse**. Désormais, les images du produit s’affichent de manière cohérente sur toutes les pages, même après actualisation de la page.

## v1.2.6

_24 octobre 2025_

[!BADGE pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce version 2.4.5 et versions ultérieures.

![Correction d’un problème](../assets/fix.svg)<!-- Issue ACAP-1163 --> Correction d’un problème en raison duquel les demandes consécutives de mise à jour en masse de produits pouvaient laisser l’indicateur de suivi de statut bloqué, empêchant le traitement correct des mises à jour suivantes. Désormais, le statut est réinitialisé même si une erreur se produit.

## v1.2.5

_2 octobre 2025_

[!BADGE pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce version 2.4.5 et versions ultérieures.

![Correction d’un problème](../assets/fix.svg)<!-- Issue ACAP-1161 --> Correction d’un problème en raison duquel la mise à jour de la position d’un mapping d’image existant dans l’administration Adobe Commerce entraînait une erreur de type PHP.

## v1.2.4

_17 octobre 2025_

[!BADGE pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce version 2.4.5 et versions ultérieures.

![Correction d’un problème](../assets/fix.svg)<!-- Issue ACAP-1155 --> Amélioration de la stabilité globale des attributs personnalisés. Les attributs personnalisés se mettent désormais correctement à jour lors de l’utilisation d’API asynchrones.

![Problème résolu](../assets/fix.svg)<!-- Issue ACAP-1074 --> Désormais, la [synchronisation produit-ressource](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/store-urls#configure-the-base-url){target=_blank} n’échoue pas lorsqu’une URL de lien de base est définie.

## v1.2.3

_2 octobre 2025_

[!BADGE pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce version 2.4.5 et versions ultérieures.

![Correction d’un problème](../assets/fix.svg)<!-- Issue ACAP-1135 --> Correction d’un problème lié à la mise à jour des attributs de produit. Les attributs de produit se mettent désormais à jour comme prévu et une erreur appropriée est renvoyée au lieu d’une réponse 200 en cas d’échec des mises à jour.

## v1.2.2

_18 septembre 2025_

[!BADGE pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce version 2.4.5 et versions ultérieures.

![Problème résolu](../assets/fix.svg)<!-- Issue ACAP-1110 --> Amélioration de la stabilité globale des images sur les pages de mini panier, de panier et de passage en caisse. Les images de ces pages se chargent désormais correctement.

## v1.2.0

_7 août 2025_

[!BADGE pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce version 2.4.5 et versions ultérieures.

![Nouveau problème](../assets/new.svg)<!-- Issue ACAP-1018 --> Désormais, les commerçants peuvent choisir la source des ressources images et médias en sélectionnant un [Propriétaire de la visualisation](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/setup-synchronization){target=_blank} lors de la configuration de l’intégration Assets à partir de l’administration.

![Nouveau problème](../assets/new.svg)<!-- Issue ACAP-1078 --> Mise à jour des points d’entrée [correspondance automatique personnalisée](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/synchronize/custom-match){target=_blank} avec un nouvel attribut `asset_matches`. Cette modification vous permet d’implémenter votre propre logique de correspondance pour renvoyer toutes les ressources associées à une `productSku` spécifique.

## v1.1.2

_1 juin 2025_

[!BADGE pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce version 2.4.5 et versions ultérieures.

![Nouveau problème](../assets/new.svg)<!-- Issue ACAP-1041 --> Ajout de la prise en charge d’Adobe Commerce 2.4.8 et de PHP 8.4.

## v1.1.0

_23 avril 2025_

[!BADGE pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce version 2.4.5 et versions ultérieures.

![Nouveau problème ](../assets/new.svg)<!-- Issue ACAP-955 --> désormais, il est possible d’utiliser une [URL de domaine personnalisée](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/setup-synchronization#optional-configure-the-custom-domain-url) au lieu de l’URL de diffusion AEM. Si un commerçant définit un **Nom de domaine personnalisé** dans son tableau de bord AEM, il est nécessaire d’ajouter cette **URL de domaine personnalisé** dans Commerce.

![Correction d’un problème](../assets/fix.svg)<!-- Issue ACAP-987 --> Amélioration des journaux globaux pour les processus de synchronisation AEM Assets.

## v1.0.22

_12 mars 2025_

[!BADGE pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce version 2.4.5 et versions ultérieures.

![Nouveau problème](../assets/new.svg)<!-- Issue ACAP-xx --> Désormais, le [identifiant du client IMS du sélecteur Assets](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/setup-synchronization) est requis par le sélecteur Assets pour activer le mappage des images AEM Assets avec les catégories de produits et le contenu généré par Page Builder.

## v1.0.20

_1 février 2025_

[!BADGE pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce version 2.4.5 et versions ultérieures.

![Nouvelle](../assets/new.svg)<!-- Issue ACAP-xx --> Mise à jour de la disponibilité générale.
