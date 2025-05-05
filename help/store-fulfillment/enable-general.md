---
title: Configuration générale
description: Configurez les paramètres généraux à activer  [!DNL Store Fulfillment]  votre magasin. Configurez les paramètres d’extension globaux, les paramètres système pour la journalisation, la synchronisation des données et la sécurité. Fournir des données essentielles pour permettre l'intégration entre Adobe Commerce et les services Store Fulfillment.
role: Admin
level: Intermediate
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '2405'
ht-degree: 0%

---

# Configuration du service de magasin et des ventes

Activez [!DNL Store Fulfillment] extension à partir de l’administrateur [!DNL Commerce] en configurant les paramètres d’extension, les paramètres de sécurité pour les utilisateurs de l’application Store Assist et les options de méthode de diffusion.

>[!IMPORTANT]
>
>La configuration du service Store Fulfillment s’applique uniquement après la connexion de votre instance Adobe Commerce et de l’application [!DNL Store Fulfillment]. Voir [Connexion à la Store Fulfillment](connect-set-up-service.md).

## Gérer les paramètres des services Store Fulfillment

Gérer les paramètres des services Store Fulfillment à partir du menu [!DNL Commerce Admin Store Configuration].

- Activez l’extension, configurez les paramètres globaux et spécifiez les options de sécurité pour les connexions des utilisateurs et comptes de l’application Store Assist en sélectionnant **[!UICONTROL Stores > Configuration > Services > Store Fulfillment by Walmart Commerce Technologies]**.

  ![Configuration des services Admin Store pour la Store Fulfillment](assets/store-services-admin-sf-config.png)

- Configurez les méthodes de diffusion en sélectionnant **[!UICONTROL Store > Configuration > Sales > Delivery Methods > In-Store Pickup]**.

  ![Configuration des ventes de la boutique d’administration pour la Store Fulfillment](assets/store-sales-admin-sf-deliver-config.png)

## Paramètres de base

<table>
<thead>
<tr>
<td><strong>Champ</strong></td>
<td><strong>Description</strong></td>
<td><strong>Champ d’application</strong></td>
<td><strong>Obligatoire</strong></td>
</tr>
</thead>
<tbody>
<tr>
<td><strong>[!UICONTROL Price]</strong></td>
<td>Prix que vous facturez au client pour le retrait en magasin. La valeur par défaut est zéro.</td>
<td>Site internet</td>
<td>Non</td>
</tr>
<tr>
<td><strong>[!UICONTROL Search Radius]</strong></td>
<td>Rayon, en kilomètres, à utiliser lorsqu’un acheteur recherche un emplacement de retrait dans le passage en caisse du magasin. Les résultats de la recherche renvoient uniquement les magasins situés dans le rayon de recherche spécifié.</td>
<td>Site internet</td>
<td>Non</td>
</tr>
<tr>
<td><strong>[!UICONTROL Displayed error message]</strong></td>
<td>Message qui s’affiche lorsqu’un client sélectionne un article qui n’est pas disponible pour le retrait en magasin. Si nécessaire, vous pouvez personnaliser le texte par défaut.
</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
</tbody>
</table>

>[!NOTE]
>
>Le paramètre [!UICONTROL Search Radius] n’est utilisé que si vous avez configuré l’emplacement de magasin [ et la configuration du mappage ](store-location-map-provider-setup.md) pour Adobe Commerce.

## Activer la solution Store Fulfillment

Activez la solution [!DNL Store Fulfillment] pour ajouter les fonctionnalités de cueillette en magasin et en bordure de rue aux expériences d’achat et de passage en caisse dans votre storefront Adobe Commerce.

<table>
<thead>
<tr>
<td><strong>Champ</strong></td>
<td><strong>Description</strong></td>
<td><strong>Champ d’application</strong></td>
<td><strong>Obligatoire</strong></td>
</tr>
 </thead>
 <tbody>
<tr>
<td><strong>[!UICONTROL Enabled]</strong></td>
<td>Activez ou désactivez la solution. Une fois activées, configurez et utilisez les fonctionnalités de Store Fulfillment et établissez la connexion entre votre boutique Adobe Commerce et les services [!DNL Store Fulfillment]. Lorsque cette option est désactivée, toutes les fonctionnalités de Store Fulfillment sont désactivées et il n’y a aucune communication entre Adobe Commerce et les services Store Fulfillment. Les informations de commande ne peuvent pas être traitées ou reçues.</td>
<td>Site internet</td>
<td>Oui</td>
</tr>
</tbody>
</table>

## Ajouter les informations d’identification de compte

<table>
<tr>
<td><strong>Champ</strong></td>
<td><strong>Description</strong></td>
<td><strong>Champ d’application</strong></td>
<td><strong>Obligatoire</strong></td>
</tr>
<tr>
<td><strong>[!UICONTROL Environment]</strong></td>
<td>Sélectionnez <i>[!UICONTROL Sandbox]</i> ou <i>[!UICONTROL Production]</i><br></br>La sélection de [!UICONTROL Sandbox] permet de communiquer avec les services d’exécution dans un environnement de test.<br></br>La sélection de [!UICONTROL Production] permet de communiquer avec les services d’exécution dans un environnement en ligne.<br></br>Vous recevez un ensemble d’informations d’identification pour chaque environnement et pouvez gérer les deux ensembles dans la même installation. <br></br>Enregistrez les informations d’identification avant de valider la connexion.</td>
<td>Global</td>
<td>Oui</td>
</tr>
<tr>
<td><strong>[!UICONTROL API Server URL]</strong></td>
<td>URL du point d’entrée de l’API d’exécution de magasin Wal-Mart. La valeur doit correspondre à l’URL complète fournie lors du processus d’intégration. Les clients Store Fulfillment reçoivent une Sandbox et une URL de production. Lors de l’ajout des valeurs, veillez à copier et coller l’URL complète, y compris la barre oblique « / ».</td>
<td>Global</td>
<td>Oui</td>
</tr>
<tr>
<td><strong>[!UICONTROL Token Auth Server URL]</strong></td>
<td>URL du point d’entrée de l’authentification de l’exécution de la boutique Walmart. La valeur doit correspondre à l’URL complète fournie lors du processus d’intégration. Vous recevez une sandbox et une URL de production. Lors de l’ajout des valeurs, veillez à copier et coller l’URL complète, y compris la barre oblique « / ».</td>
<td>Global</td>
<td>Oui</td>
</tr>
<tr>
<td><strong>[!UICONTROL Merchant Id]</strong></td>
<td>Votre identifiant marchand (client) unique fourni pendant le processus d’intégration. Cet identifiant est utilisé pour acheminer les commandes afin de vous assurer que vos magasins marchands les reçoivent.</td>
<td>Global</td>
<td>Oui</td>
</tr>
<tr>
<td><strong>[!UICONTROL Consumer Id]</strong></td>
<td>Identifiant d’intégration unique fourni lors du processus d’intégration. Cet identifiant est utilisé pour authentifier toutes les communications entre Adobe Commerce et les services de traitement des commandes</td>
<td>Global</td>
<td>Oui</td>
</tr>
<tr>
<td><strong>[!UICONTROL Consumer Secret]</strong></td>
<td>Clé d’intégration unique fournie lors du processus d’intégration. Cette clé est utilisée pour authentifier toutes les communications entre Adobe Commerce et le service de traitement des commandes en magasin.</td>
<td>Global</td>
<td>Oui</td>
</tr>
</table>

Après avoir configuré le [!UICONTROL Account Credentials], sélectionnez <strong>[!UICONTROL Validate Credentials]</strong> pour vérifier et établir une connexion au service d’exécution de magasin pour la première fois.

## Configuration de la journalisation

Les journaux des services d’exécution de magasin sont disponibles dans le fichier journal `var/log/walmart-bopis.log`.

Demandez à l’administrateur système de configurer vos environnements pour autoriser la gestion des exceptions afin que les exceptions liées aux API puissent être capturées par le biais du pare-feu ou du cache.

Étant donné que le fichier journal de l’application peut croître rapidement, activez la journalisation de l’application uniquement pendant une courte durée lorsque cela est nécessaire, par exemple lors de la résolution des problèmes d’exécution du magasin pour une commande [!DNL Commerce]. Cette configuration évite les problèmes de temps de réponse dans les environnements de production causés par des fichiers journaux volumineux.

>[!TIP]
>
>Pour les installations sur site d’Adobe Commerce, demandez à votre administrateur système de configurer la rotation des journaux pour le fichier `var/log/walmart-bopis.log` afin de réduire la taille. Pour les installations sur site d’Adobe Commerce, consultez [Rotation des journaux](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/configuration.html?lang=fr#server-settings) dans le _Guide d’installation d’Adobe Commerce_. Pour les projets d’infrastructure cloud d’Adobe Commerce, voir [Afficher et gérer les journaux](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/test/log-locations.html?lang=fr).

<table>
<thead>
<tr>
<td><strong>Champ</strong></td>
<td><strong>Description</strong></td>
<td><strong>Champ d’application</strong></td>
<td><strong>Obligatoire</strong></td>
</tr>
</thead>
<tbody>
<tr>
<td><strong>[!UICONTROL Debug Mode]</strong></td>
<td>Le mode de débogage est utilisé pour augmenter l’activité consignée dans l’intégration. Lorsqu’elle est désactivée, aucune information de débogage n’est consignée. Lorsqu’elle est activée, toutes les informations de débogage sont consignées <br></br>toutes les données consignées se trouvent dans le fichier : <pre>var/log/walmart-bopis.log</pre>
<td>Global</td>
<td>Non</td>
</tr>
</tbody>
</table>

## Gérer la synchronisation des commandes

Configurez les paramètres permettant de gérer la gestion des erreurs pour la synchronisation des commandes, les attributs de catalogue à utiliser pour l&#39;analyse des codes-barres lors du prélèvement des commandes et configurez les tailles des lots de commandes pour la file d&#39;attente de traitement des commandes du magasin.

Vous pouvez consulter les détails des opérations de synchronisation des commandes depuis le tableau de bord Gestion des files d&#39;attente de traitement des commandes dans Admin (
<strong>[!UICONTROL System > Tools > Store Fulfillment Queue]</strong>).

### Gestion des erreurs de synchronisation

<table>
<tr>
<td><strong>Champ</strong></td>
<td><strong>Description</strong></td>
<td><strong>Champ d’application</strong></td>
<td><strong>Obligatoire</strong></td>
</tr>
<tr>
<td><strong>[!UICONTROL Retry Critical Error]</strong></td>
<td>Indique les tentatives de reprise pour une opération de synchronisation des enregistrements suite à une erreur critique.<br></br>Des erreurs critiques se produisent chaque fois que l’intégration ne parvient pas à obtenir une réponse positive du service d’exécution. Ces problèmes se produisent lorsque le service est en panne ou en cas d’erreur dans les données de commande envoyées.<br></br>Lorsque le seuil de reprise est atteint, l’élément reste dans la file d’attente, mais n’est pas traité à nouveau. Affichez tous les éléments comportant des erreurs de <strong>[!UICONTROL System > Tools > Store Fulfillment Queue]</strong> Management dans l’Administration. Pour résoudre les problèmes liés aux éléments qui échouent régulièrement, contactez votre gestionnaire de compte.</td>
<td>Global</td>
<td>Non</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Error Notification Email]</strong></td>
<td>Activez les notifications d’erreur pour recevoir un e-mail lorsque la [!UICONTROL Retry Critical Error Threshold] est atteinte pour une commande. La notification inclut tous les détails disponibles sur l’erreur.</td>
<td>Global</td>
<td>Non</td>
</tr>
<tr>
<td><strong>[!UICONTROL Send Error Notification Email To]</strong></td>
<td>Liste des adresses e-mail des destinataires délimitées par des virgules pour les notifications d’erreur.</td>
<td>Global</td>
<td>Non</td>
</tr>
<tr>
<td><strong>[!UICONTROL Order Sync Exception Email Template]</strong></td>
<td>Spécifie le modèle d'e-mail utilisé pour avertir les destinataires des erreurs de synchronisation de commande. Un modèle par défaut est fourni. Il ne prend pas en charge la personnalisation.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
</table>

### Synchronisation des commandes

<table>
<thead>
<tr>
<td><strong>Champ</strong></td>
<td><strong>Description</strong></td>
<td><strong>Champ d’application</strong></td>
<td><strong>Obligatoire</strong></td>
</tr>
</thead>
<tbody>
<tr>
<td><strong>[!UICONTROL Barcode Source]</strong></td>
<td>Attribut de catalogue stockant le code analysable pour les articles correspondants dans vos sites de commerçants.<br></br>Si vous n’avez qu’un seul emplacement marchand existant, il est probable que vous utilisiez des codes UPC, tandis que votre canal d’e-commerce identifie les produits par SKU. Dans ce scénario, sélectionnez l’attribut de catalogue contenant le code de l’UPC.<br></br>Ce paramètre garantit que les commandes envoyées à vos magasins listent les articles avec l'identifiant correct afin que les associés de magasin puissent analyser avec précision les articles pendant le processus de prélèvement.<br></br>Si vous n'êtes pas sûr, vérifiez auprès de vos associés d'exécution dans le service Expédition et prélèvement pour déterminer quel attribut doit être envoyé. Si l’attribut n’est actuellement pas inclus dans la base de données, vous pouvez ajouter l’attribut au jeu d’attributs de produit Adobe Commerce.</td>
<td>Site internet</td>
<td>Oui</td>
</tr>
<tr>
<td><strong>[!UICONTROL Barcode Type]</strong></td>
<td>Attribut de catalogue qui stocke la source du code-barres pour les articles correspondants dans vos sites marchands.<br></br>Ce paramètre garantit que les commandes envoyées à vos magasins listent les articles avec un identifiant correct afin que les associés du magasin puissent analyser avec précision les articles pendant le processus de prélèvement. Les options incluent - SKU, UPC, GTIN, UPCA, EAN13, UPCE0, DISA, UAB, CODABAR, Price Embedded UPC.<br></br>En cas de doute, sélectionnez l’option qui ressemble le plus aux valeurs contenues dans votre attribut [!UICONTROL Barcode Source]. Les associés de magasin peuvent toujours faire correspondre manuellement les articles de leur liste de sélection.</td>
<td>Site internet</td>
<td>Oui</td>
</tr>
<tr>
<td><strong>[!UICONTROL Max Number of Items]</strong></td>
<td>Nombre maximal d’éléments à envoyer simultanément depuis la file d’attente de traitement des commandes du magasin.<br></br>Les commandes BOPIS sont envoyées au service d'exécution par lots, à intervalles réguliers. Ce paramètre permet de contrôler la taille du lot.<br></br>La valeur par défaut est de 100 éléments. En fonction du volume et de la capacité de votre commande, vous pouvez augmenter ou diminuer la valeur maximale.</td>
<td>Global</td>
<td>Non</td>
</tr>
</tbody>
</table>

## Activer les options d&#39;expédition Store Fulfillment

Configurez les options d’expédition Store Fulfillment qui déterminent la disponibilité des options de retrait en magasin et de livraison à domicile pour vos magasins Adobe Commerce.

### Magasin de livraison

<table>
<thead>
<tr>
<td><strong>Champ</strong></td>
<td><strong>Description</strong></td>
<td><strong>Champ d’application</strong></td>
<td><strong>Obligatoire</strong></td>
</tr>
</thead>
<tbody>
<tr>
<td><strong>[!UICONTROL Enable Ship To Store]</strong></td>
<td>Le paramètre de livraison à l’entrepôt est basé sur vos fonctionnalités existantes de livraison à l’entrepôt. Si vous utilisez Inventory management ou si vous pouvez accepter et exécuter des commandes dans des magasins sans stock via des transferts de stock magasin à magasin, définissez cette option sur « Oui ».<br></br>Si vous ne pouvez pas prendre en charge l’option de livraison en magasin ou ne souhaitez pas la proposer, définissez sur « Non ». Lorsque cette option est désactivée, les articles de votre catalogue dont le stock est nul pour une boutique marchande ou les articles qui sont inférieurs au [!DNL Out of Stock Threshold] de cet emplacement ne sont pas proposés avec les options de retrait en magasin.<br></br>Vous pouvez ajuster la valeur de ce paramètre par emplacement du marchand.</td>
<td>Global</td>
<td>Non</td>
</tr>
</tbody>
</table>

### Expédier à partir du magasin

<table>
<thead>
<tr>
<td><strong>Champ</strong></td>
<td><strong>Description</strong></td>
<td><strong>Champ d’application</strong></td>
<td><strong>Obligatoire</strong></td>
</tr>
</thead>
<tbody>
<tr>
<td><strong>[!UICONTROL Enable Ship From Store]</strong></td>
<td>Active ou désactive l’option Diffusion à domicile dans vos magasins marchands. Lorsqu’ils sont activés, les emplacements de vos magasins marchands sont pris en compte de manière agrégée avec d’autres sources affectées dans le stock associé à votre site web.<br></br>Dans les services Inventory management standard, l’option [!DNL Ship from Store] est est inhérente et ne peut pas être désactivée. Avec la solution Store Fulfillment, vous pouvez l'activer ou le désactiver.<br></br>Vous pouvez ajuster ce paramètre par emplacement de commerçant et par produit.</td>
<td>Global</td>
<td>Non</td>
</tr>
</tbody>
</table>


## Gérer les comptes utilisateur et les autorisations de l&#39;application Store Fulfillment

Configurez les paramètres de sécurité du compte utilisateur et du mot de passe de l&#39;application Store Fulfillment ainsi que de l&#39;authentification à deux facteurs.

### Sécurité des applications

<table>
<thead>
<tr>
<td><strong>Champ</strong></td>
<td><strong>Description</strong></td>
<td><strong>Champ d’application</strong></td>
<td><strong>Obligatoire</strong></td>
</tr>
 </thead>
 <tbody>
<tr>
<td><strong>[!UICONTROL User Session Lifetime]</strong></td>
<td>Délai, en secondes, pendant lequel une session utilisateur associée au magasin reste active avant la déconnexion automatique. Les valeurs valides sont comprises entre 60 et 31536000.</td>
<td>Global</td>
<td>Non</td>
</tr>
<tr>
<td><strong>[!UICONTROL Maximum Login Failures to Lockout Account]</strong></td>
<td>Indique le nombre de tentatives de connexion ayant échoué autorisées avant qu’un associé de magasin ne soit verrouillé sur son compte.<br></br>Pour désactiver le verrouillage des comptes, définissez la valeur sur 0.</td>
<td>Global</td>
<td>Non</td>
</tr>
<tr>
<td><strong>[!UICONTROL Lockout Time (minutes)]</strong></td>
<td>Nombre de minutes nécessaire pour verrouiller un compte après l’échec de la connexion.</td>
<td>Global</td>
<td>Non</td>
</tr>
<tr>
<td><strong>[!UICONTROL Force Password Change]</strong></td>
<td><em>[!UICONTROL Yes]</em>: obligez l’utilisateur à modifier son mot de passe après la configuration du compte.<br></br><em>[!UICONTROL No]</em> : recommande à l’utilisateur de modifier le mot de passe après la configuration du compte.</td>
<td>Global</td>
<td>Non</td>
</tr>
<tr>
<td><strong>[!UICONTROL Password Lifetime]</strong></td>
<td>Nombre de jours pendant lesquels un mot de passe reste valide avant la modification du mot de passe requis. Laissez ce champ vide pour désactiver cette option.</td>
<td>Global</td>
<td>Non</td>
</tr>
</tbody>
</table>

## Méthodes de diffusion

La Store Fulfillment fonctionne en étendant les fonctionnalités natives d’Adobe Commerce [!DNL In-Store Delivery]. Après avoir installé l’extension, vous pouvez configurer les méthodes de diffusion en magasin à l’aide des paramètres étendus suivants ajoutés à l’administrateur.

- **Récupération en magasin** - Proposez des options de livraison en magasin pendant le processus de passage en caisse.
Ces paramètres configurent les scénarios de livraison les plus courants pour les commandes BOPIS.

- **[!UICONTROL Curbside pick up]**-Offrir des options permettant aux clients de se garer dans un magasin et de se faire livrer leur commande par un employé du magasin.

Configurez ces paramètres à partir de l’Administration en sélectionnant <strong>[!UICONTROL Stores > Configuration > Sales > Delivery Methods > In-Store Pickup]</strong>.

>[!NOTE]
>
>Pour plus d’informations sur la configuration des options de diffusion en magasin, voir [Diffusion en magasin](https://experienceleague.adobe.com/fr/docs/commerce-admin/stores-sales/delivery/basic-methods/shipping-in-store-delivery) dans le _Guide de l’utilisateur d’Adobe Commerce_.


### Configuration des méthodes de diffusion

Grâce à la méthode de livraison en magasin, le client peut sélectionner une source à utiliser comme emplacement de retrait lors du passage en caisse.

<table>
<thead>
<tr>
<td><strong>Champ</strong></td>
<td><strong>Description</strong></td>
<td><strong>Champ d’application</strong></td>
<td><strong>Obligatoire</strong></td>
</tr>
 </thead>
 <tbody>
<tr>
<td><strong>[!UICONTROL Enable In-Store Pickup]</strong></td>
<td>Activez ou désactivez l’option de retrait en magasin disponible lors du passage en caisse pour les clients qui choisissent le retrait en magasin. Lorsque le retrait en magasin est désactivé, l’option ne s’affiche pas.<br></br>Ce paramètre global s’applique à tous les emplacements de magasin de vente au détail. Lorsqu’elle est activée, vous pouvez la désactiver de manière sélective dans le magasin de vente au détail.</td>
<td>Site internet</td>
<td>Non</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Curbside Pickup]</strong></td>
<td>Activez ou désactivez l’option de retrait en bordure de la boutique pendant le processus de passage en caisse pour les clients qui choisissent le retrait en magasin.<br></br>Ce paramètre global s’applique à tous les emplacements de magasin de vente au détail. Lorsqu’elle est activée, vous pouvez la désactiver de manière sélective dans le magasin de vente au détail.</td>
<td>Site internet</td>
<td>Non</td>
</tr>
</tbody>
</table>

### Configuration du titre de la méthode de diffusion

<table>
<thead>
<tr>
<th><strong>Champ</strong></th>
<th><strong>Description</strong></th>
<th><strong>Champ d’application</strong></th>
<th><strong>Obligatoire</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>Titre de la diffusion à domicile</strong></td>
<td>Indique le titre à afficher pour l’option Diffusion à domicile dans les zones de produit, de panier et de passage en caisse. La livraison à domicile fait référence aux fonctionnalités d’expédition standard d’Adobe Commerce, à partir d’un entrepôt, par un transporteur ou directement à l’adresse d’expédition fournie par le client. </br></br>Cette étiquette n'affecte pas les étiquettes de mode d'expédition pour le transporteur sélectionné.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
<tr>
<td><strong>Description de la diffusion à domicile</strong></td>
<td>Description facultative qui s’affiche lorsque le titre de la diffusion à domicile est présenté aux clients. Le plus souvent, la description est un message statique pour communiquer vos promesses de diffusion. Voici quelques exemples :</br><code>Same-day shipping on orders by 4</code></br></br><code>Ships within 2 business days</code></td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
<tr>
<td><strong>Titre de retrait de la boutique</strong></td>
<td>Lorsque des options de livraison sont présentées au client et que le retrait en magasin est disponible, ce libellé s’affiche. </br></br>Vous pouvez personnaliser ce libellé qui s’affiche dans les zones du produit, du panier et du passage en caisse.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
<td><strong>Description du retrait en magasin</strong></td>
<td>Quel que soit l’endroit où apparaît le titre de la cueillette dans la boutique, vous pouvez éventuellement inclure une description. Ce message statique permet d’améliorer les communications client liées à l’expérience de retrait du magasin. Voici quelques exemples :</br></br><code>Get it today for free!</code></br></br><code>Ready for pickup in an hour!</code></td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
<tr>
<td><strong>Titre du retrait en magasin</strong></td>
<td>Lorsque la cueillette en magasin est activée, ce titre s’affiche pour les clients sous la forme de l’option de diffusion cueillette en magasin . Vous pouvez personnaliser son libellé.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
<tr>
<tr>
<td><strong>Titre du ramassage en bordure de trottoir</strong></td>
<td>Lorsque le retrait à domicile est activé, l’option est présentée aux clients sous la forme d’une option de diffusion Transfert en magasin . Vous pouvez personnaliser son libellé ici.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
<tr>
<td><strong>Instructions de retrait en magasin</strong></td>
<td>Lorsqu’une commande est prête à être récupérée dans vos magasins de vente au détail, le client en est informé par e-mail. Si le client a sélectionné [!DNL In-Store Pickup] lors du passage en caisse, vous pouvez personnaliser les instructions de retrait ici. </br></br>Ces instructions sont définies globalement et s’appliquent à tous les magasins de vente au détail. Vous pouvez également personnaliser les instructions au niveau du magasin de vente au détail.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
<tr>
<td><strong>Instructions de ramassage en bordure de trottoir</strong></td>
<td>Spécifie les instructions de ramassage de commande personnalisées à inclure dans les notifications par e-mail des clients pour les commandes de ramassage en bordure de rue. </br></br>Ces instructions sont définies globalement et s’appliquent à tous les magasins de vente au détail. Vous pouvez également personnaliser les instructions au niveau du magasin de vente au détail.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
<tr>
<td><strong>Délai estimé de prélèvement</strong></td>
<td>Nombre de minutes requises avant la réception, l’exécution et le retrait d’une commande. Ces informations s’affichent pour le client lors de la sélection d’un emplacement de magasin de vente au détail pour l’option de livraison en retrait du magasin. Ce paramètre s’applique à tous les magasins de vente au détail. Vous pouvez également personnaliser le délai au niveau de l’emplacement du magasin de vente au détail.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
<tr>
<td><strong>Libellé de la durée estimée de retrait</strong></td>
<td>Affiche le temps estimé jusqu'à ce qu'une commande soit disponible pour le retrait du client. Ces informations s’affichent pour les clients lorsqu’ils sélectionnent un emplacement de magasin de vente au détail pour l’option de diffusion [!DNL In-Store Pickup]. </br></br>Lors de la personnalisation de ce libellé, vous pouvez utiliser le <code>%1</code> de code pour insérer votre <strong>Délai estimé de retrait</strong>. Par exemple :</br></br><code>Ready for Pickup in %1 minutes.</code></br></br>Ce paramètre s’applique à tous les emplacements de magasin de vente au détail. Vous pouvez également personnaliser le délai au niveau de l’emplacement du magasin de vente au détail.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
<tr>
<td><strong>Clause de non-responsabilité relative à la durée de retrait</strong></td>
<td>Contenu affiché sur la page du produit dans l’info-bulle qui répertorie les heures d’ouverture du magasin, les jours fériés, les fermetures inattendues, etc</td>
<td>Affichage de la boutique
</td>
<td>Non
</td>
</tr>
</tbody></table>

### Configuration des titres de disponibilité des stocks

<table>
<thead>
<tr>
<th><strong>Champ</strong></th>
<th><strong>Description</strong></th>
<th><strong>Champ d’application</strong></th>
<th><strong>Obligatoire</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>En stock</strong></td>
<td>Lorsqu’un client utilise l’emplacement de magasin de vente au détail , la disponibilité du stock des articles actuels s’affiche pour chaque emplacement. </br></br>Vous pouvez personnaliser le libellé de statut du <em>[!UICONTROL in-stock]</em> ici.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
<tr>
<td><strong>Rupture de stock</strong></td>
<td>Lorsqu’un client utilise l’emplacement de magasin de vente au détail , la disponibilité du stock des articles actuels s’affiche pour chaque emplacement.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
<tr>
<td><strong>Partiellement en stock</strong></td>
<td>Lorsqu’un client utilise le localisateur de magasin de vente au détail , la disponibilité du stock des articles actuels s’affiche pour chaque emplacement. </br></br>Vous pouvez personnaliser le libellé de statut du <em>[!UICONTROL partially in-stock]</em> ici.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
</tbody></table>

