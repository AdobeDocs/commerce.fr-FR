---
title: Éléments de ligne pour  [!DNL Payment Services]
description: Découvrez les lignes pour et comment afficher les lignes  [!DNL Payment Services]  tableau de bord du commerçant.
feature: Payments, Paas, Saas
role: User
exl-id: f690ff94-f83d-4525-9d52-1dea25a71060
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---

# Éléments de ligne pour [!DNL Payment Services]

Les articles de ligne pour [!DNL Payment Services] sont les articles inclus dans une commande. Ces lignes fournissent des informations telles que :

* Détails du produit
* Quantité
* Prix (taxes, remises et autres informations pertinentes)

Ces informations sont utiles pour le service client, la gestion des commandes et la facturation correcte.

Cette fonctionnalité est activée par défaut pour les [!DNL Payment Services]. Pour afficher les éléments de ligne :

1. Accédez à votre [tableau de bord de vendeur PayPal](https://www.paypal.com/merchant/){target=_blank}.

1. Cliquez sur **Activité** > **Toutes les transactions**.

1. Sélectionnez la commande souhaitée et affichez ses éléments de ligne :

   > Exemple d’éléments de ligne dans la vue du tableau de bord de l’acheteur

   ![Vue Éléments de ligne](assets/paypal-shopper-dashboard-line-items-view.png){width="500" zoomable="yes"}

## Attributs d’éléments de ligne

Les lignes sont générées lorsque la commande est passée via Adobe Commerce et que les informations sont envoyées à PayPal, avec les attributs suivants :

| Attribut | Type de données | Description |
| --- | --- | --- |
| `name` | Chaîne ! | Nom de l’élément. Si un article comporte plusieurs lignes en raison de plusieurs quantités ou d&#39;un problème d&#39;arrondi de taxe, le nom de l&#39;article reste le même pour toutes les lignes, mais le prix affiché peut varier légèrement en raison de l&#39;arrondi. |
| `unit_amount` | Objet ! | Prix ou taux de l&#39;article par unité. Inclut les attributs suivants : `currency_code` et `value`. |
| `tax` | Objet | Taxe article pour chaque unité. Inclut les attributs suivants : `currency_code` et `value`. |
| `quantity` | Chaîne ! | Quantité d&#39;article. Sera un nombre entier. |
| `description` | String | Description détaillée de l&#39;objet. |
| `sku` | String | Unité de gestion des stocks (ou SKU) de l’article. |
| `url` | String | `URL` de l&#39;article acheté. Visible par l&#39;acheteur et utilisée dans les expériences acheteur. |
| `upc` | Objet | Code de produit universel (ou CUP) de l’article. |
| `category` | String | Type de catégorie d&#39;articles. |

### Attributs `unit_amount`

L’objet `unit_amount` contient les attributs suivants :

| Attribut | Type de données | Description |
| --- | --- | --- |
| `currency_code` | Chaîne ! | Code de devise [ISO-4217 à trois caractères](https://developer.paypal.com/api/rest/reference/currency-codes/) qui identifie la devise. |
| `value` | Chaîne ! | Indique la valeur de l’élément. Le `currency_code` détermine le nombre de décimales requis, le cas échéant. |

### Attributs `tax`

L’objet `tax` contient les attributs suivants :

| Attribut | Type de données | Description |
| --- | --- | --- |
| `currency_code` | Chaîne ! | Code de devise [ISO-4217 à trois caractères](https://developer.paypal.com/api/rest/reference/currency-codes/) qui identifie la devise. |
| `value` | Chaîne ! | Indique la valeur de l’élément. Dépend de chaque `currency_code` pour le nombre de décimales requis. |

### Attributs `upc`

L’objet `upc` contient les attributs suivants :

| Attribut | Type de données | Description |
| --- | --- | --- |
| `type` | chaîne ! | Type UPC. |
| `code` | chaîne ! | Code produit UPC de l&#39;article. |

+++Exemple d’éléments de ligne

```json
{
    "name": "Crown Summit Backpack - 1",
    "unit_amount": {
        "currency_code": "USD",
        "value": "38.50"
    },
    "tax": {
        "currency_code": "USD"
        "value": "3.13"
    },
    "quantity": "1",
    "description": "The Crown Summit Backpack is equally at home in a gym locker, study cube or a pup tent, so be sure yours is packed with books,",
    "sku": "24-MB03",
    "url": "https://magento.test/crown-summit-backpack.html",
    "upc": {
        "type": "UPC-A",
        "code": "000003"
    },
    "category": "PHYSICAL_GOODS"
},
{
    "name": "Crown Summit Backpack - 2",
    "unit_amount": {
        "currency_code": "USD",
        "value": "38.50"
    },
    "tax": {
        "currency_code": "USD",
        "value": "3.14"
    },
    "quantity": "1",
    "description": "The Crown Summit Backpack is equally at home in a gym locker, study cube or a pup tent, so be sure yours is packed with books,",
    "sku": "24-MB03",
    "url": "https://magento.test/crown-summit-backpack.html",
    "upc": {
        "type": "UPC-A",
        "code": "000003"
    },
    "category": "PHYSICAL_GOODS"
}
```

+++

Voir [Documentation PayPal pour les développeurs sur les éléments de ligne](https://developer.paypal.com/docs/api/orders/v2/#definition-line_item){target=_blank} pour plus d’informations sur ces champs et leurs limites.

## Gérer les éléments de ligne

Adobe Commerce [calcule la taxe en fonction du montant total de chaque ligne](https://experienceleague.adobe.com/fr/docs/commerce-admin/stores-sales/site-store/taxes/taxes#warning-messages){target=_blank}, ce qui peut entraîner des problèmes d&#39;arrondi si plusieurs quantités du même article sont commandées ou si des prix incluant la taxe sont affichés dans le catalogue. Dans ce cas, la quantité totale peut être fractionnée en deux lignes, mais la quantité sera égale au total des articles commandés.

> Exemple d&#39;éléments de ligne avec des problèmes d&#39;arrondi dans la vue du tableau de bord du commerçant

![Vue Éléments de ligne](assets/line-items-example.png){width="600" zoomable="yes"}

+++Comment Adobe Commerce calcule un problème d’arrondi dans les éléments de ligne

Les lignes de [!DNL Payment Services] équilibrent ce problème d&#39;arrondi de sorte que la valeur de `unit_amount` ou de `unit_tax` corresponde au montant total de la commande. Un élément peut être divisé en deux lignes pour résoudre ce problème d&#39;arrondi :

* Lorsque le problème d&#39;arrondi apparaît sur la `unit_amount`, le commerçant devrait voir une différence de prix sur cette ligne supplémentaire.
* Lorsque le problème d&#39;arrondi apparaît sur la `unit_tax`, aucune différence n&#39;est visible sur les éléments de ligne individuels, car le `tax` n&#39;est pas affiché dans la grille, mais uniquement sous la forme d&#39;un total en bas.

+++
