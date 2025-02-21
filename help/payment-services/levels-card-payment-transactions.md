---
title: Traitement de niveau 2 et de niveau 3
description: Niveaux de traitement des paiements par carte dans  [!DNL Payment Services]  transactions.
role: Admin
feature: Payments
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---

# Traitement de niveau 2 et de niveau 3

Il existe trois niveaux de traitement des cartes disponibles via [!DNL Payment Services] :

* Le niveau 1 est le plus courant, nécessite moins d&#39;information et, par conséquent, entraîne généralement des frais d&#39;interchange plus élevés par rapport aux transactions traitées avec des données de niveau 2 ou 3, qui sont généralement liées aux cartes de crédit d&#39;entreprise et d&#39;achat.

* Avec les niveaux 2 et 3, les clients [!DNL Payment Services] au niveau de tarification Interchange Plus (IC++) qui acceptent un grand nombre de transactions par carte d’achat ou par carte d’entreprise peuvent potentiellement bénéficier d’un taux de traitement plus faible en [!DNL Payment Services] permettant d’envoyer davantage d’informations sur une transaction. Si la transaction est admissible, selon les exigences du réseau de cartes, le commerçant peut alors recevoir un taux de traitement inférieur pour une transaction particulière.

>[!NOTE]
>
>Les tarifs des niveaux 2 et 3 s&#39;appliquent uniquement aux transactions Visa et MasterCard. American Express propose uniquement des tarifs de niveau 2. Discover n’offre pas de tarification de niveau 2 ni de niveau 3. Voir [traitement des paiements](https://developer.paypal.com/docs/checkout/advanced/processing/){target=_blank} dans la documentation destinée aux développeurs PayPal pour plus d’informations.

Voir [ Qu’est-ce qu’IC ++?](https://www.paypal.com/us/brc/article/what-is-interchange-plus-plus){target=_blank} dans la documentation PayPal destinée aux développeurs pour plus d&#39;informations.

Les données de traitement de niveaux 2 et 3 permettent aux commerçants de réduire leur prix IC++ s&#39;ils fournissent des détails supplémentaires sur l&#39;achat, ce qui réduit le risque du processeur et présente des avantages :

* Les gros clients paieront moins cher en fournissant ces données de traitement.

* Les clients sont moins susceptibles de se retrouver dans des situations frauduleuses puisque les commandes sont plus informées.

Cependant, les réseaux de cartes, comme Visa et Mastercard, déterminent en fin de compte si une transaction est admissible pour le traitement de niveau 2 ou de niveau 3 :

* Les données de niveau 2 contiennent des informations supplémentaires, telles que le montant de taxe de la commande, le code client ou le numéro de bon de commande.

* Les données de niveau 3 sont des informations plus détaillées sur la vente, ce qui permet de bénéficier de taux d&#39;interchange encore plus bas par rapport au niveau 2. Les données de niveau 3 contiennent des informations telles qu’une description de l’article acheté, la quantité d’unités achetées, l’unité de mesure des articles commandés et d’autres détails spécifiques.

[!DNL Payment Services] collecte ces données et fournit des rapports détaillés sur vos opérations de paiement.

## Opérations de paiement par carte de niveau 2 et de niveau 3 en [!DNL Payment Services]

Pour bénéficier d&#39;un traitement de niveau 2 ou de niveau 3, les commerçants doivent envoyer les informations précédentes, bien que ce soient les réseaux de cartes qui déterminent en fin de compte le niveau auquel une transaction est admissible lors de son traitement.

Pour plus d’informations, consultez la [FAQ sur le traitement des paiements](https://www.paypal.com/us/cshelp/article/ts2278?_ga=1.131773126.875104296.1712843492){target=_blank} dans la documentation PayPal destinée aux développeurs.

Le traitement de niveau 2 et de niveau 3 est désactivé par défaut pour les commerçants [!DNL Payment Services] au niveau du magasin.

Les traitements de niveau 2 et de niveau 3 sont disponibles si vous utilisez déjà la tarification IC++. Pour activer cette fonctionnalité, vous pouvez le faire via l’[interface de ligne de commande (CLI](configure-cli.md).

>[!IMPORTANT]
>
>Pour toute question, veuillez contacter votre gestionnaire de compte [!DNL Payment Services].
