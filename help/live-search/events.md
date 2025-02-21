---
title: Événements [!DNL Live Search]
description: Découvrez comment les événements collectent des données pour  [!DNL Live Search].
feature: Services, Eventing
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---

# Événements [!DNL Live Search]

[!DNL Live Search] utilise des événements pour alimenter les algorithmes de recherche tels que « Les plus consultés » et « Affiché ceci, Affiché cela ». Tandis que l’exemple de thème Luma [Commerce](https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/design/themes/themes#the-default-theme) met en œuvre des événements prêts à l’emploi, les implémentations découplées et autres implémentations personnalisées doivent mettre en œuvre des événements en fonction de leurs propres besoins.

Ce tableau décrit les événements utilisés par [!DNL Live Search] [stratégies de classement](rules-add.md#intelligent-ranking).

| Stratégie de classement | Événements | Page |
| --- | --- | --- |
| Les plus consultés | `page-view`<br>`product-view` | Page des détails du produit |
| Les plus achetés | `page-view`<br>`complete-checkout` | Panier/Passage en caisse |
| Les plus ajoutés au panier | `page-view`<br>`add-to-cart` | Page des détails du produit<br>page de liste des produits<br>panier<br>liste de souhaits |
| A consulté ceci, a consulté cela | `page-view`<br>`product-view` | Page des détails du produit |

>[!NOTE]
>
>La collecte de données à des fins de [!DNL Live Search] n’inclut pas les informations d’identification personnelle (PII). Tous les identifiants d’utilisateur, tels que les ID de cookie et les adresses IP, sont strictement anonymisés. [En savoir plus](https://www.adobe.com/privacy/experience-cloud.html).

## Événements de tableau de bord requis

Certains événements sont nécessaires pour renseigner le tableau de bord [Recherche en direct](performance.md)

| Zone du tableau de bord | Événements | Joindre le champ |
| ------------------- | ------------- | ---------- |
| Recherches uniques | `page-view`, `search-request-sent`, `search-response-received` | `searchRequestId` |
| Aucun résultat de recherche | `page-view`, `search-request-sent`, `search-response-received` | `searchRequestId` |
| Taux de résultats nuls | `page-view`, `search-request-sent`, `search-response-received` | `searchRequestId` |
| Recherches populaires | `page-view`, `search-request-sent`, `search-response-received` | `searchRequestId` |
| Moy. position de clic | `page-view`, `search-request-sent`, `search-response-received`, `search-results-view`, `search-product-click` | `searchRequestId` |
| Taux de clic publicitaire | `page-view`, `search-request-sent`, `search-response-received`, `search-results-view`, `search-product-click` | `searchRequestId`, `sku`, `parentSku` |
| Taux de conversion | `page-view`, `search-request-sent`, `search-response-received`, `search-results-view`, `search-product-click`, `product-view`, `add-to-cart`, `place-order` | `searchRequestId`, `sku`, `parentSku` |

### Contextes requis

Tous les événements nécessitent les contextes `Page` et `Storefront`. Cela doit se produire au niveau de la page ou de la couche d’application du storefront, plutôt que lors de la génération d’événements individuels (par exemple, dans un storefront PHP, le conteneur d’applications PHP est chargé de les définir au moment de l’exécution).

## Utilisation

Voici un exemple d’implémentation de l’événement `search-request-sent` :

```javascript
const mse = window.magentoStorefrontEvents;

/* set in application container */
// mse.context.page(pageCtx);
// mse.context.setStorefrontInstance(storefrontCtx);

/* set before firing event */
mse.context.setSearchInput(searchInputCtx);
mse.publish.searchRequestSent("search-bar");
```

## Avertissements

- Les bloqueurs de publicités et les paramètres de confidentialité peuvent empêcher la capture d’événements et peuvent entraîner la sous-déclaration des mesures d’engagement et de chiffre d’affaires [mesures](performance.md). En outre, certains événements peuvent ne pas être envoyés en raison de problèmes de page ou de réseau liés aux clients qui quittent la page.
- Les implémentations découplées doivent mettre en œuvre des événements pour optimiser le marchandisage intelligent.

>[!NOTE]
>
>Si le [Mode de restriction des cookies](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html) est activé, Adobe Commerce ne collecte pas de données comportementales tant que l’acheteur n’a pas consenti à l’utilisation de cookies. Si le Mode de restriction des cookies est désactivé, Adobe Commerce collecte des données comportementales par défaut.
