---
title: Données disponibles
description: Utilisez les données des rapports financiers pour réconcilier les rapports avec les systèmes autres que Commerce.
role: User
level: Intermediate
exl-id: dbf41ce9-01f9-45d0-b651-e4c499e83822
feature: Payments, Checkout, Data Import/Export, Paas, Saas
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# Données disponibles

Certaines données sur les commandes et les paiements vous sont accessibles afin que vous puissiez coordonner les rapports financiers d’Adobe Commerce entre les systèmes externes.

## Réconcilier avec le système ERP

Vous pouvez réconcilier les rapports financiers Adobe Commerce avec votre système de planification des ressources de l&#39;entreprise (ERP) autre qu&#39;Adobe à l&#39;aide de l&#39;ID d&#39;incrément associé à une commande spécifique.

Lorsque Payment Services envoie la commande Commerce à PayPal, l&#39;ID d&#39;incrément est inclus comme `custom_id` _et_ dans le `invoice_id` (qui contient également une chaîne aléatoire après le `increment_id`).

Les identifiants sont facilement accessibles dans les détails de l’activité du commerçant pour un paiement et dans le webhook PayPal.

Les `invoice_id` et `custom_id` sont affichés près du bas des détails de l’activité du commerçant pour un paiement :

![`custom_id` dans les détails de l’activité du commerçant](assets/merchant-activity-ids.png){width="600" zoomable="yes"}

`custom_id` et `invoice_id` dans les détails sur le webhook de PayPal :

```json
   ...
   {
    "id": "4E855005GK253170H",
    "intent": "AUTHORIZE",
    "status": "COMPLETED",
    "payment_source": {
        ...
    },
    "purchase_units": [
        {
            ...
            "custom_id": "000001322",
            "invoice_id": "000001322-c01bd7c3-920f-4542-a900-738082177e92",
            ...
            "payments": {
                "authorizations": [
                    {
                       ...
                        "invoice_id": "000001322-c01bd7c3-920f-4542-a900-738082177e92",
                        "custom_id": "000001322",
                        ...
                    }
                ],
                "captures": [
                    {
                        ...
                        "invoice_id": "000001322-c01bd7c3-920f-4542-a900-738082177e92",
                        "custom_id": "000001322",
                        ...
                    }
                ]
            }
        }
    ],
    "payer": {
        ...
    },
    "create_time": "2022-09-12T14:59:01Z",
    "update_time": "2022-09-12T14:59:45Z",
    "links": [
        ...
    ]
}
   ...
```

Consultez la documentation des API REST de PayPal pour plus d’informations :

* [`purchase_unit`, où `custom_id` et `invoice_id` résident](https://developer.paypal.com/docs/api/orders/v2/#definition-purchase_unit)
* [Afficher les détails de la commande](https://developer.paypal.com/docs/api/orders/v2/#orders_get)
