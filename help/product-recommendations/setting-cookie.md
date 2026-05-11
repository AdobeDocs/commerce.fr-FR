---
title: Gestion des restrictions relatives aux cookies
description: Découvrez comment les recommandations de produits gèrent les restrictions des cookies et la conformité en matière de confidentialité.
exl-id: 7e7342db-b903-4105-93c0-e4022c81673b
TQID: https://experienceleague.adobe.com/qqgwO4KI4koSBcYu9mdrjb6AQFW4guxk6dfLDBEwVb8
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 454
ht-degree: 0%

---

# Gestion des restrictions relatives aux cookies

Adobe Commerce et Magento Open Source demandent l’autorisation avant de stocker des données dans des cookies de navigateur. Pour plus d’informations, voir [Mode de restriction des cookies](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html?lang=fr).

## Gestion des restrictions liées aux cookies par les recommandations de produits

Lorsque vous déployez le module `magento/product-recommendations` en production, il commence à collecter les événements d’interaction client sur votre storefront. Ces données peuvent être stockées dans des cookies de navigateur ou un stockage local pour alimenter les algorithmes de recommandation.

>[!IMPORTANT]
>
>Les recommandations de produits respectent désormais le mode de restriction des cookies en ne collectant ni ne stockant aucune donnée dans des cookies ou un stockage local lorsque les restrictions des cookies sont activées. Cela inclut les données comportementales utilisées pour les recommandations personnalisées.

### Données affectées par les restrictions relatives aux cookies

Les données des recommandations de produits suivantes ne sont pas collectées lorsque le mode de restriction des cookies est activé :

- **Données comportementales** : consultations de produits, actions de mise en panier, achats et autres interactions d’acheteurs.
- **Données de session** : informations sur la session client et interactions des unités de recommandation.
- **Données Personalization** : données utilisées pour les types de recommandations tels que « Récemment consultés » et « Les plus achetés ».

### Impact sur les types de recommandations

Lorsque le mode de restriction des cookies est activé et que les acheteurs n’ont pas accepté les cookies, certains types de recommandations peuvent ne pas s’afficher ou n’afficher que des résultats limités :

- **Produits récemment consultés** : nécessite des données de session stockées dans des cookies/un stockage local.
- **Recommandé pour vous** : nécessite des données comportementales pour la personnalisation.
- **Acheté ceci, acheté cela** : nécessite des données d’historique d’achat.

>[!NOTE]
>
>Les types de recommandations qui ne reposent pas sur des données comportementales, tels que « Les plus consultés » et « Similarité visuelle », continueront à fonctionner normalement même si les restrictions de cookies sont activées.

## Solutions de consentement des cookies tiers

Il se peut que Product Recommendations ne s’intègre pas automatiquement aux solutions de consentement des cookies tiers. Il incombe au commerçant de s&#39;assurer que la collecte de données est conforme aux lois et règlements applicables en matière de protection des renseignements personnels.

Si vous utilisez une solution de consentement des cookies personnalisée, vous pouvez implémenter le mécanisme de cookie de non-suivi pour contrôler la collecte de données.

### Mise en œuvre des cookies de non-suivi

Vous pouvez utiliser le cookie `mg_dnt` pour contrôler par programmation la collecte de données :

#### Nom du cookie

```javascript
const DNT_COOKIE = "mg_dnt";
```

#### Désactiver la collecte de données

Définissez le cookie de non-suivi lorsque les utilisateurs refusent les cookies :

```javascript
$.mage.cookies.set(DNT_COOKIE, true);
```

#### Activer la collecte de données

Effacez le cookie de non-suivi lorsque les utilisateurs acceptent les cookies :

```javascript
$.mage.cookies.clear(DNT_COOKIE);
```

## Test du mode de restriction des cookies

Pour tester le comportement des recommandations de produits avec les restrictions de cookie :

1. Activez le mode de restriction des cookies dans votre configuration Adobe Commerce.
1. Visitez votre storefront sans accepter les cookies.
1. Vérifiez que les unités de recommandation affichent le contenu de secours approprié.
1. Acceptez les cookies et vérifiez que les recommandations commencent à collecter des données.

## Respect de la confidentialité

La collecte de données des recommandations de produits n’inclut pas les informations d’identification personnelle (PII). Tous les identifiants d’utilisateur, tels que les ID de cookie et les adresses IP, sont rendus anonymes. Pour plus d’informations, consultez la [Politique de confidentialité d’](https://www.adobe.com/privacy/policy.html).

>[!TIP]
>
>Pour les clients du secteur de la santé qui utilisent l’extension HIPAA des services de données, une configuration supplémentaire peut être requise. Pour plus d’informations, consultez la section [Préparation du HIPAA](../data-connection/hipaa-readiness.md).
