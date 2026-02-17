---
title: Performances
description: L’espace de travail  [!DNL Live Search]  performances fournit insight dans les termes de recherche utilisés par les acheteurs.
exl-id: 07a63df8-b981-4913-841a-7e81ec634281
source-git-commit: 5978a400d985e3099962af8bcefdd6f29f687d67
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

# Performances

L’espace de travail *Performances* fournit insight dans les termes de recherche utilisés par les acheteurs. Ces informations peuvent être utilisées pour identifier les tendances, augmenter les clics publicitaires et améliorer le taux de conversion. L’espace de travail Performances fournit un instantané des mesures de recherche pour une période spécifique et inclut les rapports suivants :

* Recherches uniques
* Zéro résultat
* Résultats populaires

![Performances](assets/performance-unique-searches.png)

Vous pouvez également consulter le [Tableau de bord de gestion des données](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html?lang=fr) pour plus d’informations sur la synchronisation des données.

>[!NOTE]
>
>L’espace de travail des performances est mis à jour toutes les 12 heures.

## Affichage d’un rapport

1. Pour saisir la **Période**, cliquez sur le calendrier (![Calendrier](assets/btn-calendar.png)) et effectuez l’une des opérations suivantes :

   * Pour spécifier une seule date, double-cliquez sur la date dans le calendrier.
   * Pour spécifier une plage de dates, cliquez sur la première et la dernière date du calendrier.

>[!NOTE]
>
>La plage de dates ne peut pas dépasser un an.

## Descriptions des champs

| Données de capture instantanée | Description | Exemple de calcul |
|--- |--- |--- |
| Recherches uniques | Nombre total de recherches uniques pour la période spécifiée. Les recherches multiples effectuées par le même acheteur, même si pour la même requête, sont considérées comme uniques si elles sont envoyées à plus d’une heure d’intervalle. | **Exemple:**<br /> Recherches:<br />- « pantalon » à 10:00h<br />- « pantalon » à 10:30h (dans l&#39;heure → non unique)<br />- « pantalon » à 12:00h (après 1 heure → unique)<br />- « chemise » à 1:00h <br /><br />**Total recherches uniques = 3** |
| Taux de clics | Pourcentage de recherches qui se terminent par un clic de l’acheteur sur un produit. Par exemple, le taux de clic publicitaire est de 50 % si l’acheteur recherche « pantalon » et « chemise », puis clique sur un résultat de la recherche « chemise ». | **Formule :**<br /> Taux de clics = Recherches avec ≥1 clic ÷ Nombre total de recherches uniques <br /><br />**Exemple :**<br /> Nombre total de recherches uniques = 4<br />Recherches avec au moins un clic = 2<br /><br />CTR = 2 ÷ 4 = **50 %** |
| Taux de conversion | Pourcentage de produits achetés par l’acheteur par rapport au nombre de produits sur lesquels l’acheteur clique pendant la période spécifiée. Par exemple, le taux de conversion de l’interaction est de 100 % si l’acheteur consulte six produits dans la fenêtre contextuelle, clique sur un produit et effectue un achat. <br /><br />Le taux de conversion n’est pas affecté par le nombre de consultations d’un produit donné. Par exemple, le taux de conversion reste le même si l’acheteur utilise la recherche, mais ne clique sur aucun produit. | **Formule :**<br /> Taux de conversion = Total des produits achetés ÷ Total des produits ayant fait l’objet d’un clic <br /><br />**Exemple 1:**<br /> Produits ayant fait l’objet d’un clic = 5<br />Produits achetés = 2<br /><br />CVR = 2 ÷ 5 = **40 %**<br /><br />**Exemple 2 (agrégation sur 5 heures) :**<br /> Clics par heure : 4, 5, 6, 10, 2<br />Achats par heure : 1, 3, 0, 4, 1<br /><br />Total des clics = 4 + 5 + 6 + 10 + 2 = 27<br />Total des achats = 1 + 3 + 0 + 4 + 1 = 9CVR = 9 ÷ 27 = <br /><br />33,33 %**&#x200B;** |
| Taux de résultats nuls | Pourcentage de recherches uniques qui ne renvoie aucun résultat pour la période spécifiée. Par exemple, le taux de zéro des résultats est de 66,67 % si l&#39;acheteur recherche « fjjajfjf » deux fois (sans résultats) et « pants » une fois (avec résultats). | **Formule:**<br /> Taux de résultats nul = Recherches uniques sans résultats ÷ Nombre total de recherches uniques <br /><br />**Exemple:**<br /> Nombre total de recherches uniques = 3<br />Recherches sans résultats = 2<br /><br />Taux de résultats nul = 2 ÷ 3 = **66,67 %** |
| Moy. position de clic | Position relative du taux de clics publicitaires moyen en fonction des recherches uniques pour la période spécifiée. | **Formule:**<br /> Position moyenne des clics = Somme des positions des clics ÷ Nombre total de clics <br /><br />**Exemple:**<br /> Clics aux positions : 1, 3, 2<br /><br />Position moyenne des clics = (1 + 3 + 2) ÷ 3 = **2** |

| Rapports | Description |
|--- |--- |
| Recherches uniques | Répertorie les requêtes de recherche uniques utilisées au cours de la période spécifiée. Les données du rapport sont calculées de la même manière que les données d’instantané de recherche unique. Si un acheteur saisit deux fois la même requête de recherche, mais à plus d’une heure d’intervalle, la recherche est considérée comme deux recherches uniques. <br />**Limite du rapport :** les 500 premiers termes lors de la génération du fichier CSV. |
| Zéro résultat | Répertorie les requêtes de recherche qui ne renvoient aucun résultat et le nombre de fois où elles ont été utilisées au cours de la période spécifiée. <br />**Limite du rapport :** les 500 premiers termes lors de la génération du fichier CSV. |
| Résultats populaires | Répertorie les noms des produits qui ont reçu le plus de vues au cours de la période spécifiée. Les résultats populaires sont calculés en fonction des impressions uniquement et ne sont pas affectés par le nombre de clics ou le chiffre d’affaires généré. <br />**Limite du rapport :** les 500 premiers termes lors de la génération du fichier CSV. |
