---
title: Gestion des restrictions relatives aux cookies
description: Découvrez comment les recommandations de produits gèrent les restrictions de cookie.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# Gestion des restrictions relatives aux cookies

Adobe Commerce et Magento Open Source demandent l’autorisation avant de stocker des données dans des cookies de navigateur. Pour plus d’informations, voir [Mode de restriction des cookies](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html).

Lorsque vous déployez le module `magento/product-recommendations` en production, il commence à collecter les événements d’interaction client sur votre storefront. Comme les données de ces événements peuvent être stockées dans des cookies de navigateur ou un stockage local, la fonctionnalité prend en charge le mode de restriction des cookies en ne collectant pas d’événements avant que l’acheteur n’ait donné son consentement aux cookies.

Cela peut ne pas fonctionner avec les solutions de consentement des cookies tiers. Il incombe à chaque commerçant de s’assurer que la collecte de données n’a pas lieu avant que le consentement des cookies ne soit donné, comme l’exige souvent la loi. Si vous gérez le consentement des cookies avec du code personnalisé, vous pouvez utiliser un cookie de non-suivi appelé `mg_dnt` pour restreindre la collecte de données.

- Nom du cookie :

  ```text
  `const DNT_COOKIE = "mg_dnt";`
  ```

- Définissez le cookie de non-suivi pour désactiver la collecte de données :

  ```text
  `$.mage.cookies.set(DNT_COOKIE, true);`
  ```

- Pour effacer le cookie lorsque l’utilisateur a accepté les cookies :

  ```text
  `$.mage.cookies.clear(DNT_COOKIE);`
  ```
