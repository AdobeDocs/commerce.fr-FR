---
title: Modèles d’e-mail de vente
description: Configurez les modèles d’e-mail transactionnel pour communiquer avec les clients et les administrateurs de magasin pendant le processus d’exécution des commandes de retrait de magasin.
role: Admin
level: Intermediate
feature: Shipping/Delivery, Communications, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1233'
ht-degree: 1%

---


# Modèles d’e-mail de vente

Store Fulfillment offre un ensemble étendu de modèles d’e-mails transactionnels pour prendre en charge les workflows de commande et d’exécution. Ils offrent une communication et une messagerie cohérentes et automatisées sur l’ensemble des canaux, informant les clients et les administrateurs de magasin des changements de statut des commandes, des instructions pour les commandes de retrait en magasin, etc.

Les modèles d’e-mail Store Fulfillment sont configurés avec les paramètres et les messages par défaut. Les administrateurs commerçants d’Adobe Commerce peuvent gérer et modifier les configurations, et sélectionner les modèles d’e-mail pour communiquer avec les clients dans différents scénarios. Les administrateurs peuvent également configurer et personnaliser des modèles.

Configurez les modèles d’e-mail de vente à partir de l’administrateur : **[!UICONTROL Stores > Configuration > Sales > Sales Emails]**.

## E-mails - Paramètres généraux

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
<td><strong>Envoi asynchrone</strong></td>
<td>Détermine si les e-mails de vente sont envoyés de manière asynchrone. Options : <br/>**`Désactiver`** - (Par défaut) Les e-mails de ventes sont envoyés lorsqu’ils sont déclenchés par un événement. Utilisez le paramètre par défaut pour accélérer la communication et le temps de réponse lors de la sélection du magasin. <br/>**`Activer`** - L'activation de cette option déplace les processus qui gèrent le passage en caisse et le traitement des notifications électroniques de commande en arrière-plan pour les envoyer à intervalles réguliers prédéterminés.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
</tbody></table>

## Commande prête à être retirée en magasin

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
<td><strong>Activé</strong></td>
<td>Cet e-mail est envoyé au client une fois que l'associé du magasin a terminé le prélèvement de sa commande. Définissez la valeur sur « Non » pour désactiver la notification par e-mail. Si le modèle d’e-mail est désactivé, cela n’empêche pas le vendeur associé de sélectionner une commande.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
<tr>
<td><strong>Commande Prête Pour L'Expéditeur De L'E-Mail De Récupération</strong></td>
<td>Identité de l’expéditeur utilisée lors de l’envoi de la notification par e-mail.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
<tr>
<td><strong>Commande Prête Pour Le Modèle D'E-Mail De Prélèvement</strong></td>
<td>Modèle d’e-mail utilisé pour avertir les clients enregistrés. Un modèle par défaut est fourni avec l’intégration.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
<td><strong>Commande prête pour le modèle d'e-mail de retrait pour invité</strong></td>
<td>Modèle d’e-mail utilisé pour avertir les clients invités. Un modèle par défaut est fourni avec l’intégration.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
<tr>
<td><strong>Commande prête pour le modèle d'e-mail de retrait pour un autre contact de retrait</strong></td>
<td>Modèle d’e-mail utilisé pour informer d’autres contacts nommés dans la commande. Un modèle par défaut est fourni avec l’intégration.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
<tr>
<td><strong>Envoyer La Commande Prête Pour La Copie De L'E-Mail De Prélèvement À</strong></td>
<td>Liste d'adresses e-mail séparées par des virgules permettant d'envoyer une copie de chaque notification.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
<tr>
<td><strong>Méthode De Copie D'E-Mail De Commande D'Envoi Prête Pour Prélèvement</strong></td>
<td>Méthode de copie par e-mail (copie carbone) à utiliser.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
</tbody></table>


## La commande a été retirée de la boutique

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
<td><strong>Activé</strong></td>
<td>Cet e-mail est envoyé au client pour confirmer qu'il a récupéré sa commande dans le magasin. Définissez la valeur sur « Non » pour désactiver la notification par e-mail. Si le modèle d’e-mail est désactivé, cela n’empêche pas le client de sélectionner une commande.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
<tr>
<td><strong>La Commande A Été Récupérée Par L'Expéditeur De L'E-Mail</strong></td>
<td>Identité de l’expéditeur utilisée lors de l’envoi de la notification par e-mail.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
<tr>
<td><strong>La Commande A Été Sélectionnée Comme Modèle D'E-Mail</strong></td>
<td>Modèle d’e-mail utilisé pour avertir les clients enregistrés. Un modèle par défaut est fourni avec l’intégration</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
<td><strong>La commande a été récupérée modèle d'e-mail pour invité</strong></td>
<td>Modèle d’e-mail utilisé pour avertir les clients invités. Un modèle par défaut est fourni avec l’intégration.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
<tr>
<td><strong>L'Envoi A Été Récupéré Une Copie D'E-Mail Vers</strong></td>
<td>Liste d'adresses e-mail séparées par des virgules permettant d'envoyer une copie de chaque notification.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
<tr>
<td><strong>L’Envoi A Été Sélectionné Comme Méthode De Copie D’E-Mail</strong></td>
<td>Méthode de copie par e-mail (copie carbone) à utiliser.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
</tbody></table>

## Commande retardée

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
<td><strong>Activé</strong></td>
<td>Cet e-mail est envoyé au client pour l’informer d’un retard dans le traitement ou le prélèvement de sa commande dans la boutique du vendeur. Définissez la valeur sur « Non » pour désactiver la notification par e-mail. Si le modèle d’e-mail est désactivé, la fonction n’empêche pas le report d’une commande.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
<tr>
<td><strong>Commander l'expéditeur d'e-mail retardé
</strong></td>
<td>Identité de l’expéditeur utilisée lors de l’envoi de la notification par e-mail.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
<tr>
<td><strong>Modèle d’e-mail de commande différée</strong></td>
<td>Modèle d’e-mail utilisé pour avertir les clients enregistrés. Un modèle par défaut est fourni avec l’intégration.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
<td><strong>Modèle d’e-mail de commande différée pour l’invité</strong></td>
<td>Modèle d’e-mail utilisé pour avertir les clients invités. Un modèle par défaut est fourni avec l’intégration.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
<tr>
<td><strong>Envoyer La Copie D'E-Mail De La Commande Différée À</strong></td>
<td>Liste d'adresses e-mail séparées par des virgules permettant d'envoyer une copie de chaque notification.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
<tr>
<td><strong>Méthode de copie différée de la commande d'envoi</strong></td>
<td>Méthode de copie par e-mail (copie carbone) à utiliser.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
</tbody></table>



## Commande annulée

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
<td><strong>Activé</strong></td>
<td>Cet e-mail est envoyé au client pour l'informer que sa commande a été annulée à la boutique. Définissez sur <code>No</code> pour désactiver la notification par e-mail. Si le modèle d’e-mail est désactivé, sa fonction n’empêche pas l’annulation d’une commande.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
<tr>
<td><strong>Commande annulée par l'expéditeur de l'e-mail
</strong></td>
<td>Identité de l’expéditeur utilisée lors de l’envoi de la notification par e-mail.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
<tr>
<td><strong>Modèle d’e-mail de commande annulée</strong></td>
<td>Modèle d’e-mail utilisé pour avertir les clients enregistrés. Un modèle par défaut est fourni avec l’intégration.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
<td><strong>Commande annulée pour l'invité</strong></td>
<td>Modèle d’e-mail utilisé pour avertir les clients invités. Un modèle par défaut est fourni avec l’intégration.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
<tr>
<td><strong>Envoyer La Copie D'E-Mail De Commande Annulée À</strong></td>
<td>Liste d'adresses e-mail séparées par des virgules permettant d'envoyer une copie de chaque notification.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
<tr>
<td><strong>Méthode de copie d'annulation de commande d'envoi</strong></td>
<td>Méthode de copie par e-mail (copie carbone) à utiliser.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
</tbody></table>


## Commande en partie annulée

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
<td><strong>Activé</strong></td>
<td>Cet e-mail est envoyé au client pour l'informer qu'une partie de sa commande a été annulée à la boutique du marchand. Définissez sur <code>No</code> pour désactiver la notification par e-mail. Si le modèle d’e-mail est désactivé, cela n’empêche pas l’annulation partielle d’une commande.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
<tr>
<td><strong>Expéditeur d'e-mail de commande partiellement annulée
</strong></td>
<td>Identité de l’expéditeur utilisée lors de l’envoi de la notification par e-mail.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
<tr>
<td><strong>Modèle d’e-mail de commande partiellement annulée</strong></td>
<td>Modèle d’e-mail utilisé pour avertir les clients enregistrés. Un modèle par défaut est fourni avec l’intégration.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
<td><strong>Modèle d'e-mail de commande partiellement annulée pour un autre contact de retrait</strong></td>
<td>Modèle d’e-mail utilisé pour informer d’autres contacts nommés dans la commande. Un modèle par défaut est fourni avec l’intégration.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
<tr>
<td><strong>Commande partiellement annulée pour l'invité</strong></td>
<td>Modèle d’e-mail utilisé pour avertir les clients invités. Un modèle par défaut est fourni avec l’intégration.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
<tr>
<td><strong>Envoyer La Copie D'E-Mail De Commande Partiellement Annulée À</strong></td>
<td>Liste d'adresses e-mail séparées par des virgules permettant d'envoyer une copie de chaque notification.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
<tr>
<td><strong>Méthode de copie pour l'envoi d'une commande partiellement annulée</strong></td>
<td>Méthode de copie par e-mail (copie carbone) à utiliser.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
</tbody></table>

## Adresse de livraison du magasin

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
<td><strong>La Commande A Expédié À L'Expéditeur De L'E-Mail Des Produits</strong></td>
<td>E-mail envoyé au personnel marchand spécifié sous la forme d'un rapport agrégé de toutes les commandes en cours qui ne peuvent pas être prélevées dans un magasin marchand tant que leur stock n'est pas disponible. </br></br> Les commerçants peuvent utiliser cet état pour lancer et gérer des transferts ou des réapprovisionnements de stock magasin à magasin. </br></br>Cette notification s’applique uniquement lorsque les fonctionnalités [!DNL Ship-to-Store] sont activées.
</br></br>Cette étiquette n'affecte pas le transporteur sélectionné ni ses étiquettes de mode d'expédition disponibles.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
<tr>
<td><strong>Destinataires d'e-mails de magasin d'expédition</strong></td>
<td>Liste d'adresses e-mail séparées par des virgules permettant d'envoyer une copie de chaque notification.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
<tr>
<td><strong>Modèle d’e-mail</strong></td>
<td>Modèle d’e-mail utilisé pour informer les destinataires. Un modèle par défaut est fourni avec l’intégration.</td>
<td>Affichage de la boutique</td>
<td>Non</td>
</tr>
</tbody></table>

>[!NOTE]
>
>Si vous autorisez les commandes en souffrance, vous devez indiquer une adresse e-mail d’administrateur pour recevoir des notifications sur ces commandes. Ajoutez l’adresse aux paramètres de configuration suivants : **[!UICONTROL Send Order Delayed Email Copy To]** dans le modèle [Délai de commande](#order-delayed) et [!UICONTROL Ship To Store Email Recipients] dans le modèle [Livrer au magasin](#ship-to-store).



