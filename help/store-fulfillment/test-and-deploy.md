---
title: Tester et déployer la Store Fulfillment
description: Testez le plan pour vérifier la fonctionnalité Store Fulfillment. Les tests couvrent l'API de synchronisation des stocks, le workflow d'exécution de bout en bout pour les commandes annulées, la gestion des utilisateurs de l'application Store Fulfillment et l'expérience d'enregistrement du client.
role: User, Admin
level: Intermediate
feature: Shipping/Delivery, User Account, Roles/Permissions
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '2661'
ht-degree: 0%

---

# Tester et déployer la Store Fulfillment pour Adobe Commerce

Une fois le processus d’intégration terminé dans votre environnement de développement, vous pouvez lancer le processus pour tester et déployer la solution Store Fulfillment dans votre environnement de production.

**Conditions préalables**

Avant de tester ou de synchroniser des informations, des magasins ou des commandes, vérifiez que vous avez terminé les tâches suivantes :

- Fin de la [configuration générale](enable-general.md) pour les services Store Fulfillment.

- [Ajouter et valider les informations d’identification de compte et de connexion pour votre sandbox et vos environnements de production](connect-set-up-service.md#configure-store-fulfillment-account-credentials)

- Vérifiez que l’[intégration Adobe Commerce](connect-set-up-service.md#configure-store-fulfillment-account-credentials) pour la solution Store Fulfillment est disponible et autorisée.

## Préparation du test

La configuration de la connexion doit être terminée avant de pouvoir créer des ordres de test ou effectuer des tests d’intégration. Avant de procéder aux tests, vous devez également vérifier que les données de votre boutique sont synchronisées.

1. Synchroniser les sources de Store Fulfillment.

   - Accédez à **[!UICONTROL Stores > Sources]**.

   - Sélectionnez **[!UICONTROL Synchronize Store Fulfillment Sources]**.

1. Dans la grille de magasin, vérifiez que les magasins ont été marqués comme `Synced` avant de créer des ordres de test.

## Exemple de plan de test

Les détaillants valident les fonctionnalités de base de la solution Store Fulfillment au cours des phases de configuration et de test d&#39;un déploiement. Cet exemple de plan de test fournit un point de départ pour les tests. Ajoutez d’autres scénarios en fonction de vos besoins.

>[!NOTE]
>
>Après avoir terminé l’intégration initiale de la solution Store Fulfillment ou mis à jour une installation existante, testez toujours l’application dans un environnement hors production avant de la déployer en production.

Cet exemple de plan de test couvre les domaines fonctionnels suivants :

| Domaine Fonctionnel | Fonction | Rôle |
|-------------------------------------|------------------------------------------|----------------------------------|
| Synchronisation des stocks et des commandes | Synchronisation de l’API d’inventaire | Administrateur Adobe Commerce |
| De bout en bout | Workflows d’annulation de commande | Client, administrateur, associé de magasin |
| Admin | Autorisations de l&#39;application Store Fulfillment | Admin |
| Adobe Commerce Frontend | Types de produits | Client, Administrateur |
| Formulaire D&#39;Extraction</br>D&#39;Archivage Frontend | Expérience d’enregistrement | Client, Administrateur |
| Application d’assistance de magasin | Order</br>Pick</br>Stage</br>and Handoff | Associé de magasin |

### Synchronisation des API d’inventaire

Cette section du plan de test couvre la synchronisation des stocks et des commandes afin de vérifier que les mises à jour des sources de prélèvement et des stocks sont correctement synchronisées entre Adobe Commerce et la solution Store Fulfillment.

**Domaine fonctionnel** : Synchronisation des stocks et des commandes</br>
**Rôle :** Admin</br>
**Type de test :** Tous positifs

<table>
<thead>
<tr>
<th>Fonction</th>
<th>Scénario de test</th>
<th>Résultats attendus</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>Ajouter une source de stock en retrait</strong></td>
<td>Enregistrez une nouvelle source de stock en retrait.</td>
<td>La synchronisation en temps réel envoie les détails de la source au service Walmart GIF dans les 5 minutes.</td>
</tr>
<tr>
<td><strong>Mettre à jour la source de stock de prélèvement existante</strong></td>
<td>Enregistrez les mises à jour sur une source de stock de prélèvement existante.</td>
<td>L’opération de synchronisation en temps réel envoie les détails au Walmart GIF dans les 5 minutes</td>
</tr>
<tr>
<td><strong>Origine du stock de prélèvement </br><code>Is Synced</code> statut</strong></td>
<td>Enregistrez les mises à jour sur une source de stock de prélèvement existante.</td>
<td>Après une opération réussie, la colonne <code>Is Synced</code> de la page Gérer Source est mise à jour de <code>No</code> à <code>Yes</code>.</td>
</tr>
<tr>
<td><strong>Processus de réservation de stock modifié</strong></td>
<td>Créer et soumettre une nouvelle commande pour un produit.</td>
<td>La quantité commercialisable pour le produit diminue en conséquence.</td>
</tr>
<tr>
<td><strong>Notification push de nouvelle commande, synchronisation de l'API : commande client</strong></td>
<td>Le client envoie une commande de retrait de magasin.</td>
<td><ul><li>Dans la vue Commande d’administration, un utilisateur <strong>Adobe Commerce Admin</strong> voit que l’état de synchronisation de la commande a été mis à jour sur . <code>Sent</code></li><li>Le journal des détails de la commande inclut le message <code>Order was sent to BOPIS solution for sync, it's not yet acknowledged yet.</code></li></ul></td>
</tr>
<tr>
<td><strong>Notification push de nouvelle commande, synchronisation de l’API : l’administrateur envoie la commande</strong></td>
<td>Un administrateur Adobe Commerce <strong>Admin</strong> envoie un ordre de retrait.</td>
<td><ul><li>Dans la vue Commande d’administration, l’état de synchronisation des commandes est mis à jour sur <code>Sent</code>.</li><li>Le journal des détails de la commande inclut le message <code>Order was sent to BOPIS solution for sync, it's not yet acknowledged yet.</code></li></ul></td>
</tr>
<tr>
<td><strong>Notification push de nouvelle commande, file d'attente des exceptions<strong></td>
<td>Identifiez plusieurs produits virtuels et téléchargeables dans l’administration Adobe Commerce qui peuvent être exécutés par Adobe Commerce sans nécessiter d’interaction avec le service Fulfillment (FaaS).</td>
<td>Ces produits sont retirés ou marqués de manière appropriée dans l'exportation pour éviter un conflit en aval avec les FaaS.</td>
</tr>
</tbody>
</table>

### Workflows d’annulation de commande

Cette section du plan de tests comprend des scénarios permettant de tester le workflow de bout en bout pour les commandes annulées via Adobe Commerce.

**Domaine fonctionnel :** Adobe Commerce Admin</br>
**Rôle :** de bout en bout (administrateur, associé de magasin, client)</br>
**Type de résultat du test :** positif pour tous les scénarios

<table style="table-layout:fixed">
<tr>
<th>Fonction</th>
<th>Scénario</th>
<th>Résultats Attendus</th>
</tr>
<tr>
<td><strong>Annulation complète de la commande</strong></td>
<td><ol>
<li>Passer une commande.</li>
<li>Patientez jusqu’à ce que la commande soit synchronisée.</li>
<li>Vérifier la création de la facture (si autorisée et saisie) réception de l’e-mail de facture.</li>
<li>Créez un avoir avec tous les produits commandés à partir de la vue Facture.</li>
</ol>
</td>
<td>
<ul>
<li>Historique des commandes mis à jour avec <code>We refunded $X online. Transaction ID: transactionID</code> et <code>Received Cancel acknowledgment from the BOPIS solution.</code></li>
<li>Le statut de la commande est <code>Closed</code>. (Nous avons défini la RÉVISION DES PAIEMENTS maintenant.)</li>
<li>Avoir créé dans Adobe Commerce. (Attendez que cron fonctionne.)</li>
<li>Si tous les articles ont été prélevés, l’<code>DISPLAY COMMENT HISTORY</code> Prêt pour le prélèvement <code>Order is ready for pickup</code>’affiche (<code>CUSTOMER NOTIFIED</code> indicateur est <code>true</code>).</li>
<li>Si tous les articles ne sont pas sélectionnés, l'email d'annulation et l'HISTORIQUE DES COMMENTAIRES AFFICHÉS s'affichent <code>Order has been canceled - all items were not available</code></li>
<li><code>CUSTOMER NOTIFIED</code> l'indicateur est <code>true</code>.)</li>
</ul>
</td>
</tr>
<tr><td><strong>Annulation partielle de la commande<strong></td>
<td>
<ol>
<li>Commandez avec au moins deux produits.</li>
<li>Patientez jusqu’à ce que la commande soit synchronisée.</li>
<li>Vérifiez que la facture a été créée (si autorisée et capturée) et que l’e-mail de facture a été reçu.</li>
<li>Patientez deux heures pour le règlement de la transaction.</li>
<li>Créez un avoir avec seulement une partie des produits commandés depuis la vue Facture.</li>
</td>
<td>
<ul>
<li>Mise à jour de l'historique des commandes : <code>We refunded $X online. Transaction ID: transactionID</code></li>
<li>Mise à jour de l'historique des commandes : <code>Order notified as partly canceled at: Date and Hour</code></li>
<li>E-mail de remboursement de réception de commande : <code>$x amount was refunded</code></li>
<li>Le statut de la commande est <code>Processing</code>.</li>
<li>Avoir créé dans Adobe Commerce (Attendez que cron fonctionne).</li>
<li>Si certains articles n'ont pas été prélevés, vérifiez que l'e-mail [!UICONTROL Ready for Pickup] contenant la section Prélèvement ou remboursement nul s'affiche. <code>DISPLAY COMMENT HISTORY</code> affiche des <code>Order is ready for pickup, but some items not available.</code>.</li>
<li><code>CUSTOMER NOTIFIED</code> l'indicateur est <code>true</code>.</li>
</ul>
</td>
</tr>
<td><strong>Prêt pour ramassage</br></br>Annulation complète</br>(tous les produits sont définis comme ramassés avec 0 qté)</strong></td>
<td>
<ol>
<li>Passez la commande.</li>
<li>Patientez jusqu’à ce que la commande soit synchronisée.</li>
<li>Vérifiez que la facture a été créée (si autorisée et capturée) et que l’e-mail de facture a été reçu.</li>
<li>Accédez au Postman et exécutez la demande Prêt pour le retrait avec tous les produits définis comme <code>picked</code> avec <code>0 qty</code>.</li>
</ol>
</td>
<td>
<ul>
<li>Historique des commandes mis à jour : <code>We refunded $X offline</code></li>
<li>Le statut de la commande est <code>CLOSED</code>.
<li>L'avoir est créé. (Attendez que cron fonctionne.)</li>
<li>E-mail de remboursement reçu : <code>$x amount was refunded</code></li>
<li>E-mail d'annulation de commande envoyé.</li>
</ul>
</td>
</tr>
<tr>
<td><strong>Prêt pour retrait - Annulation partielle</strong></br></br><strong>(Certains produits sont prélevés et d’autres le sont avec <code>0 qty</code>)</strong>
</td>
<td>
<ol>
<li>Passez la commande.</li>
<li>Patientez jusqu’à ce que la commande soit synchronisée.</li>
<li>Vérifiez que la facture a été créée (si autorisée et capturée) et que l’e-mail de facture a été reçu.</li>
<li>Accédez au Postman et exécutez la demande Prêt pour le prélèvement avec une partie des produits définis comme étant prélevés avec une quantité de 0 et le reste d'entre eux prélevés.</li>
</ol>
</td>
<td>
<ul>
<li><code>Your order is ready for pickup</code> avec des tables [!UICONTROL Ready for Pickup Items] et [!UICONTROL Canceled Items]. </li>
<li>Le statut de la commande est PRÊT POUR LE RETRAIT. </li>
<li>Historique des commandes mis à jour : <code>We refunded $X offline.</code>
<li>Historique des commandes mis à jour : <code>Order notified as partly canceled at: Date and hour</code>
<li>E-mail de remboursement reçu : <code>$x amount was refunded</code>
<li>L'avoir est créé. (Attendez que cron fonctionne.)</li>
</ul>
</td>
</tr>
<tr>
<td><strong>Prêt pour le retrait - Annulation partielle</br></br>Certains produits sont prélevés et d’autres le sont avec <code>0 qty</code>)</strong>
</td>
<td><ol>
<li>Passez la commande.</li>
<li>Patientez jusqu’à ce que la commande soit synchronisée.</li>
<li>Vérifiez que la facture a été créée (si autorisée et capturée) et que l’e-mail de facture a été reçu.</li>
<li>Accédez au Postman et exécutez la demande Prêt pour le prélèvement avec une partie des produits définis comme étant prélevés avec une quantité de 0 et le reste d'entre eux prélevés.</li>
</ol>
</td>
<td><ul>
<li><code>Your order is ready for pickup</code> avec des tables [!UICONTROL Ready for Pickup Items] et [!UICONTROL Canceled Items]. </li>
<li>Le statut de la commande est PRÊT POUR LE RETRAIT. </li>
<li>Historique des commandes mis à jour : <code>We refunded $X offline.</code>
<li>Historique des commandes mis à jour : <code>Order notified as partly canceled at: Date and hour</code>
<li>E-mail de remboursement reçu : <code>$x amount was refunded</code>
<li>L'avoir est créé. (Attendez que cron fonctionne.)</li>
</ul>
</td>
</tr>
<tr>
<td><strong>Distribué (pendant la délivrance) </br></br>Annulation complète (tous les produits sont définis comme rejetés)</strong>
</td>
<td>
<ol>
<li>Passez la commande.</li>
<li>Patientez jusqu’à ce que la commande soit synchronisée.</li>
<li>Vérifiez que la facture a été créée (si autorisée et capturée) et que l’e-mail de facture a été reçu.</li>
<li>Accédez au Postman et exécutez la demande Prêt pour le prélèvement avec tous les produits définis comme prélevés.</li>
<li>Ouvrez votre boîte aux lettres, recherchez l'e-mail Prêt pour le retrait . Cliquez ensuite sur **[!UICONTROL Confirm Arrival]**.</li>
<li>Archivez-vous.</li>
<li>Accédez à Postman et exécutez la demande Distribué avec tous les produits définis comme rejetés.</li>
</ol>
<td><ul>
<li>Historique des commandes mis à jour : <code>We refunded $X offline.</code></li>
<li>E-mail de remboursement reçu : <code>$x amount was refunded</code></li>
<li>Statut défini sur <code>CLOSED</code>.</li>
<li>Avoir créé. (Attendez que cron fonctionne.)</li>
</ul>
</td>
</tr>
<tr>
<td><strong>Distribué (pendant la distribution)</br></br>Annulation partielle</br>(Certains produits sont distribués ; certains sont rejetés.)</strong>
</td>
<td>
<ol>
<li>Passez la commande.</li>
<li>Patientez jusqu’à ce que la commande soit synchronisée.</li>
<li>Vérifiez que la facture a été créée (si autorisée et capturée) et que l’e-mail de facture a été reçu.</li>
<li>Accédez à Postman, puis exécutez la demande Prêt pour le prélèvement avec tous les produits définis comme prélevés.</li>
<li>Ouvrez votre boîte aux lettres. Recherchez l’e-mail Prêt pour le retrait et sélectionnez <code>Confirm Arrival</code>.</li>
<li>Archivez-vous.</li>
<li>Accédez au Postman, puis exécutez la demande de distribution avec certains produits définis sur distribué et d’autres sur rejeté.</li>
</ol>
</td>
<td>
<li>Historique des commandes mis à jour : <code>We refunded $X offline</code></li>
<li><code>Order notified as partly canceled at: Date and Hour</code>
<li>E-mail de remboursement reçu : <code>$x amount was refunded</code>
<li>Statut de la commande défini sur <code>Ready for pickup Dispensed</code>
<li>Avoir créé. (Attendez que cron fonctionne.)</li>
</td>
</tr>
<tr>
<td> <strong>Nouveau RMA après le retour (complet)</strong>
</td>
<td>
<ol>
<li>Passez la commande.</li>
<li>Patientez jusqu’à ce que la commande soit synchronisée.</li>
<li>Si l’option Autoriser et capturer est configurée, vérifiez que la facture a été créée et que le client a reçu l’e-mail de facture.</li>
<li>Choisissez tous les produits avec Postman.</li>
<li>Archivez-vous.</li>
<li>Délivrez-vous.</li>
<li>Accédez à la commande, puis sélectionnez <strong>[!UICONTROL Create returns]=
<li>Créez le RMA.</li>
</ol>
</td>
<td>
<ul>
<li>Le retour client a été créé et s'affiche sous l'onglet <strong>[!UICONTROL Returns]</b> dans la vue Commande.</li>
<li>Le client a reçu un e-mail de confirmation RMA.</li>
</ul>
</td>
</tr>
<tr>
<td><strong>Nouveau RMA après renvoi — Partiel</strong>
</td>
<td>
<ol>
<li>Passez la commande.</li>
<li>Patientez jusqu’à ce que la commande soit synchronisée.</li>
<li>Vérifiez que la facture a été créée (si autorisée et capturée) et que l’e-mail de facture a été reçu.</li>
<li>Choisissez tous les produits avec Postman.</li>
<li>Archivez-vous.</li>
<li>Délivrez-vous.</li>
<li>Dans l’ordre, sélectionnez  <strong>[!UICONTROL Create returns]</strong></li>
<li>Créer le retour client avec une partie des produits commandés.</li>
</ol>
<td>
<ul>
<li>RMA créé et affiché sous l'onglet <strong>[!UICONTROL Returns]</strong> dans la vue Commande.</li>
<li>Le client a reçu l'e-mail de confirmation RMA.</li>
<li>Après avoir créé RMA, obtenez l'autorisation RMA : auprès de l'administrateur, accédez à <strong>[!UICONTROL Sales > Returns]</strong>. Sélectionnez le RMA que vous avez créé et autorisez-le.</li>
<li>Vérifiez que le client a reçu l'e-mail de confirmation d'autorisation RMA.</li>
<li>Vérifiez que le remboursement a été ajouté à l'historique des transactions et des commandes.</li>
</ul>
</td>
</tr>
</table>


### Autorisations de l&#39;application Store Fulfillment

Cette section du plan de test traite de la gestion des comptes pour les utilisateurs de l’application Store Fulfillment.

- Vérifiez qu’un associé de magasin peut s’authentifier avec un nouveau compte utilisateur créé à partir de l’administrateur Adobe Commerce.
- Vérifiez que les mises à jour apportées aux comptes existants ont bien été appliquées.

**Domaine fonctionnel :** Adobe Commerce Admin</br>
**Rôle :** administrateur, associé au magasin</br>
**Type de test :** Tous positifs

<table style="table-layout:auto">
<tr>
<th>Fonction</th>
<th>Scénario</th>
<th>Résultats Attendus</th>
</tr>
<tr>
<td><strong>Gestion des comptes d’utilisateurs - Créer un compte</strong></br></br>
</td>
<td>
<ol>
<li><strong>Admin</strong> — Connectez-vous à Adobe Commerce Admin</li>
<li>Accédez à <strong>[!UICONTROL System] &gt; Autorisations d’application Store Fulfillment &gt; Tous les utilisateurs d’application Store Fulfillment</strong></li>
<li><strong>Ajoutez un nouvel utilisateur.</strong></li>
</ol>
<td>
<ul>
<li>Compte créé.</li>
<li>Le nouveau compte utilisateur s’affiche dans le tableau de bord [!UICONTROL Store Fulfillment Users].</li>
<li><strong>Store Associate</strong> connectez-vous à l’application Store Assist avec un nouveau compte utilisateur.</li>
</ul>
</td>
</tr>
<tr>
<td><strong>Gestion des comptes d’utilisateurs - Mettre à jour le compte d’utilisateur existant</strong>
</td>
<td>
<ol>
<li>Connectez-vous à l’administration Adobe Commerce à l’aide du compte utilisateur administrateur.</li>
<li>Accédez à <strong>[!UICONTROL System] &gt; Autorisations d’application Store Fulfillment &gt; Tous les utilisateurs d’application Store Fulfillment</strong>.</li>
<li>Dans la liste Compte utilisateur , ouvrez un compte utilisateur actif existant en sélectionnant <strong>[!UICONTROL Edit]</strong>.
<li>Désactivez le compte en remplaçant <strong>[!UICONTROL Is Active]</strong> par <strong>Non</strong>.</li>
</ol>
</td>
<td>
<ul>
<li>Dans le tableau de bord <strong>[!UICONTROL Store Fulfillment App Users]</strong>, le statut du compte mis à jour est passé à <strong>[!UICONTROL Inactive]</strong>.</li>
<li>Store Associate ne peut pas se connecter à l’application Store Assist avec les identifiants du compte inactif.</li>
</ul>
</td>
</tr>
</table>

## Types de produits Adobe Commerce

Les scénarios de test pour les types de produits Adobe Commerce vérifient que les clients voient les informations correctes sur le produit, le stock et la méthode de livraison pour différents types de produits :

- [!UICONTROL Configurable]
- [!UICONTROL Grouped]
- [!UICONTROL Virtual]
- [!UICONTROL Bundle products] dans le storefront Adobe Commerce.

**Domaine fonctionnel :** Adobe Commerce Frontend</br>
**Rôle : Utilisateur De L’Application D’Assistance De La Boutique** (Store Associate)</br>
**Type de test :** Tous positifs

<table style="table-layout:auto">
<tr>
<th>Fonction</th>
<th>Scénario</th>
<th>Commentaires</th>
</tr>
<tr>
<td><strong>Produits configurables</strong>
</td>
<td>
<ul>
<li>Vérifiez que l’utilisateur ne peut voir que ces options configurables, que la source est activée, que le stock est affecté et qu’il y a des articles en stock. Vérifiez les produits enfants.</li>
<li>Vérifiez que lors de la sélection d’un autre magasin, les options qui ne sont pas disponibles apparaissent barrées.</li>
<li>Vérifiez que si l’utilisateur sélectionne un magasin différent, les options configurables ne sont pas sélectionnées.</li>
<li>Vérifiez que si un produit configurable se trouve déjà dans le panier et qu’un utilisateur sélectionne un autre magasin, le produit s’affiche comme en rupture de stock.</li>
</ul>
</td>
<td></td>
</td>
</tr>
<tr>
<td><strong>Produits groupés</strong>
</td>
<td>
<ul>
<li>Vérifiez que les boutons Méthodes de diffusion et [!UICONTROL Add to cart] sont désactivés pour le client lorsque tous les produits enfants ont
<code>qty</code> défini sur <code>0</code>.</li>
<li>Vérifiez que les méthodes de diffusion sont activées pour le client lorsqu'au moins un des produits enfants a <code>qty</code> défini sur <code>0.</code></li>
<li>Vérifiez que [!UICONTROL Store Pickup Delivery] méthode n’est visible et active que pour les produits dont le [!UICONTROL Available for Store Pickup] est activé. (Vérifier le produit enfant.)</li>
</ul>
</td>
<td></td>
</tr>
<tr>
<td><strong>Produits virtuels</strong>
</td>
<td>
Vérifiez que les produits virtuels n'offrent pas la méthode de diffusion [!UICONTROL In-store Pickup].
<td></td>
</td>
</tr>
<tr>
<td><strong>Regrouper les produits</strong>
</td>
<td>
<ul>
<li>Vérifiez que si au moins un produit enfant a [!UICONTROL Available for Store Pickup] désactivé, l'option de livraison en retrait de la boutique n'est pas disponible pour le client.</li>
<li>Vérifiez que si au moins un produit enfant a [!UICONTROL Available for Home Delivery] désactivé, l'option Diffusion à domicile n'est pas disponible pour le client.</li>
<li>Vérifiez si au moins un des produits enfants d’une offre groupée est en rupture de stock. Le lot (produit parent) s’affiche également
comme [!UICONTROL Out of stock].</li>
</ul>
</td>
<td></td>
</tr>
<tbody>
</table>

## Expérience d’enregistrement

Cette section du plan de test couvre l’expérience d’enregistrement pour les commandes de retrait de la boutique pour les fonctionnalités suivantes :

- Autre contact de prélèvement : vérifiez le workflow d&#39;ajout d&#39;un [!UICONTROL Alternate Pickup Contact] et de sélection d&#39;un [!UICONTROL Preferred Contact] sur les commandes de prélèvement en magasin.

- Formulaire d&#39;enregistrement : vérifiez le workflow de soumission d&#39;une demande d&#39;enregistrement pour les commandes de retrait du magasin.

**Domaines fonctionnels :** Passage en caisse, formulaire d’enregistrement pour les commandes de retrait en magasin</br>
**Rôle :** administrateur, client, associé de magasin</br>
**Type de test :** Tous positifs

### Autre contact de retrait


**Domaine fonctionnel :** Passage en caisse</br>
**Rôle :** client</br>
**Type de test :** Tous positifs

<table style="table-layout:auto">
<tr>
<th>Fonction</th>
<th>Scénario</th>
<th>Résultats Attendus</th>
</tr>
<tr>
<td><strong>Autre contact de retrait</br>
Archiver<strong>
</td>
<td>
Un client passe une commande avec l’option Prise en charge en magasin .</td>
<td>Pendant le processus de passage en caisse, le client voit l’option [!UICONTROL Alternate Pickup Contact] à l’étape Expédition .
</td>
</tr>
<tr>
<td><strong>Autre contact préféré pour l'enlèvement, enregistrer</strong>
<td>
Un client passe une commande avec l’option Prise en charge en magasin . Lors du passage en caisse, le client ajoute un [!UICONTROL Alternate Pickup Contact].</td>
<td>Pendant le processus de passage en caisse, le client voit l’option [!UICONTROL Preferred Contact] à l’étape d’expédition.</td>
</td>
</tr>
<tr>
<td><strong>Autres coordonnées de retrait, enregistrer</strong>
</td>
<td>
Un client passe une commande avec l’option Prise en charge en magasin . Lors du passage en caisse, le client sélectionne [!UICONTROL Alternate Pickup Contact] à l’étape d’expédition.
</td>
<td>Le client voit des options de saisie pour saisir les coordonnées : [!UICONTROL First name], [!UICONTROL Last name], [!UICONTROL Phone] et [!UICONTROL Email].</td>
</tr>
<tr>
<td><strong>Autre retrait, enregistrer l'e-mail</strong>
</td>
<td>Un client passe une commande avec l’option Prise en charge en magasin . Lors du passage en caisse, le client sélectionne [!UICONTROL Alternate Pickup Contact] à l’étape d’expédition, ajoute les coordonnées et soumet la commande.</td>
<td>Le client et l'autre contact reçoivent un e-mail d'enregistrement pour la commande.</td>
</tr>
<td><strong>Autre prélèvement, détail de la commande</strong></td>
<td>Un client passe une commande avec l’option Prise en charge en magasin . Lors du passage en caisse, le client sélectionne [!UICONTROL Alternate Pickup Contact] à l’étape d’expédition, ajoute les coordonnées et soumet la commande.</td>
<td>L’administrateur voit les informations de contact supplémentaires sur la commande enregistrée.</td>
</tr>
<tr>
<td><strong>Autre contact de retrait, vue de commande Store Associate</strong>
</td>
<td>Un client passe une commande avec l’option Prise en charge en magasin . Lors du passage en caisse, le client sélectionne [!UICONTROL Alternate Pickup Contact] à l’étape d’expédition, ajoute les coordonnées et soumet la commande.</td>
<td>L'associé du magasin peut voir les coordonnées supplémentaires sur la commande dans FaaS/ChaaS.</td>
</td>
</tr>
</tbody>
</table>

### Formulaire d&#39;enregistrement


**Domaine fonctionnel :** Formulaire d&#39;enregistrement</br>
**Rôle :** client</br>
**Type de test :** Tous positifs

<table style="table-layout:auto">
<tr>
<th>Fonction</th>
<th>Scénario</th>
<th>Résultats Attendus</th>
</tr>
<tr>
<td><strong>Action d'archivage—Soumettre la demande</strong>
</td>
<td>Sur le formulaire d’enregistrement, un client remplit tous les champs obligatoires et soumet la demande.</td>
<td>Le client reçoit une réponse de succès.</td>
</tr>
<tr>
<td><strong>Action d'archivage—Affichage des détails de la demande</strong></td>
<td>Un client a soumis avec succès une demande d’enregistrement.</td>
<td>Le statut de la commande est mis à jour dans le système FaaS et l’associé du magasin peut voir les détails de la demande d’enregistrement dans la FaaS.
</td>
</tr>
<tr>
<td><strong>Action Archiver : soumettre la demande une seule fois</strong></td>
<td>Après l’envoi d’une demande d’enregistrement pour une commande, un client sélectionne le lien pour s’enregistrer une seconde fois.</td>
<td>Dans le formulaire d’enregistrement, le client ne voit pas d’option permettant de modifier ou de renvoyer le formulaire.</td>
</tr>
<tr>
<td><strong>Action d'enregistrement - Confirmer l'arrivée</strong></td>
<td>Une commande de retrait en magasin est marquée prête pour le retrait dans la FaaS. Le client reçoit un e-mail Prêt pour le retrait et sélectionne [!UICONTROL Confirm Arrival].</td>
<td>Le client voit le formulaire d’enregistrement de la commande.</td>
</tr>
</tbody>
</table>

## Application Store Assist

Cette section du plan de test couvre les scénarios pour tester les workflows d’ordre, de prélèvement et de remise dans l’application d’assistance au magasin.

**Domaine fonctionnel : application** Store Assist</br>
**Rôle :** Store Associate</br>
**Type de test :** Tous positifs

<table style="table-layout:auto">
<tr>
<th>Fonction</th>
<th>Scénario</th>
<th>Résultats Attendus</th>
</tr>
<tr>
<td>
<strong>Prélèvement d'une seule commande - parcours heureux, ramassage à la porte</strong></td>
<td>Choisissez des articles à quantité unique et multiple. Pas de choix nuls, et ramassage à la rue (avec mise en scène).
</td>
<td>
</td>
</tr>
<tr>
<td><strong>Prélèvement de plusieurs commandes - parcours heureux, prélèvement à la rue</strong></td>
<td>Articles à quantité unique et multiple. Pas de choix nuls, et ramassage en bordure de rue (avec mise en scène)</td>
<td></td>
</tr>
<tr>
<td><strong>Prélèvement d'une seule commande - bon passage en magasin</strong></td>
<td>Articles à quantité unique et multiple. Pas de prélèvements nuls et retrait en magasin (avec staging)</td>
<td>
</td>
</tr>
<tr>
<td><strong>Prélèvement de plusieurs commandes - chemin heureux, prélèvement en magasin</strong></td>
<td>Choisissez des articles à quantité unique et multiple. Pas de choix nuls, et ramassage à la rue (avec mise en scène).</td>
<td></td>
</tr>
<tr>
<td><strong>Prélèvement de commande unique - parcours malheureux, prélèvement en magasin</strong></td>
<td>Prélever des articles à quantité unique ou multiple avec prélèvement partiel ou à prélèvements multiples et prélèvement en magasin (avec prélèvements intermédiaires)</td>
</td>
<td></td>
</tr>
<td><strong>Prélèvement de plusieurs commandes - pas heureux prélèvement en bordure de chemin</strong></td>
<td>Prélever des articles à quantité unique ou multiple avec prélèvement partiel ou à prélèvements multiples et prélèvement en magasin (avec prélèvements intermédiaires)</td>
<td></td>
</tr>
<td><strong>Prélèvement d'une seule commande : pas de chemin heureux, ramassage à la porte</strong></td>
<td>Prélever des articles à quantité unique ou multiple avec prélèvement partiel, prélèvement à prélever et prélèvement à la surface (avec préproduction)</strong></td>
</td>
<td></td>
</tr>
<tr><td><strong>Commande passée - annulée avant le prélèvement</strong></td>
<td></td>
<td></td>
</tr>
<tr>
<td><strong>Commande passée - annulée avant remise</strong></td>
<td></td>
<td></td>
</tr>
<tr>
<td><strong>Commande passée - Recherche dans le module de commande</strong></td>
<td></td>
<td></td>
</tr>
<tr><td><strong>Commande passée : recherche et enregistrement manuel pour la remise</strong></td>
<td></td>
<td></td>
</tr>
<tr><td><strong>Commande passée : tous les articles non sélectionnés ou non disponibles sont marqués par le sélecteur</strong></td>
<td></td>
<td></td></tr>
<tr><td><strong>Commande passée avec des articles groupés - prélèvement et remise</strong></td>
<td></td>
<td></td></tr>
<tr><td><strong>Commande passée - Remise avec rejet</strong></td>
<td></td>
<td></td></tr>
<tr><td><strong>Commande passée - Remise avec rejet de tous les articles</strong></td>
<td></td>
<td></td></tr>
</tbody>
</table>

## Déployer

Après avoir vérifié que la solution a été configurée et testée conformément à vos spécifications, vous êtes prêt à effectuer le déploiement de l’évaluation vers la production.

Le déploiement et les tests varient en fonction de votre infrastructure et de vos fonctionnalités.

>[!TIP]
>
>Pour obtenir des instructions sur le déploiement, des listes de contrôle et des bonnes pratiques pour Adobe Commerce sur les projets d’infrastructure cloud, voir [Déployer votre boutique](https://experienceleague.adobe.com/fr/docs/commerce-cloud-service/user-guide/develop/deploy/staging-production) dans la documentation Adobe Commerce Developer.
