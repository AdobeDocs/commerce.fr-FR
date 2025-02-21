---
title: Configuration de l'utilisateur
description: Configurez des sources Inventory management améliorées comme magasins marchands pour prendre en charge la solution Store Fulfillment pour Adobe Commerce.
role: Admin, Developer
level: Intermediate
feature: Shipping/Delivery, User Account, Tools and External Services
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# Configuration de l&#39;utilisateur

Les utilisateurs de l’application Store Assist sont gérés dans Adobe Commerce. Cependant, ces utilisateurs n’interagissent pas directement avec Adobe Commerce. La gestion des utilisateurs est configurée dans Adobe Commerce pour activer des connexions sécurisées entre Adobe Commerce et l’application.

Le modèle Utilisateur de l&#39;application Store Fulfillment est séparé des autres modèles d&#39;utilisateurs Adobe Commerce. L’application conserve son propre modèle d’autorisation par le biais des rôles utilisateur et des utilisateurs qui peuvent être affectés à l’ensemble des emplacements ou à des emplacements spécifiques. Les autorisations suivantes sont prises en charge : Ordre de prélèvement, Ordre de livraison et Réduction de la quantité d&#39;article (et annulation).

>[!TIP]
>
>Pour de meilleurs résultats, [configurez votre connexion](connect-set-up-service.md) avant d’ajouter des utilisateurs et des autorisations pour les partenaires de la boutique qui utilisent l’application Store Assist.

## Application d’assistance en magasin - Rôles utilisateur

Lors de la configuration initiale de l’utilisateur pour l’application Store Assist, créez des rôles d’utilisateur pour personnaliser les autorisations d’utilisateur pour l’application Store Assist. Par exemple, vous pouvez créer différents rôles pour les responsables de magasin et les associés de magasin et affecter différentes ressources de rôle pour gérer les autorisations pour chaque type d’utilisateur.

Configurez les rôles utilisateur à partir de **[!UICONTROL System > Store Fulfillment App Permissions > All Store Fulfillment App Users]**.

### Infos sur le rôle

| **Champ** | **Description** | **Portée** | **Obligatoire** |
|----------------------------|-------------------------|-----------|--------------|
| **[!UICONTROL Role Name]** | Activer ou désactiver l’utilisateur. | Global | Oui |

### Ressources de rôle

| **Champ** | **Description** | **Portée** | **Obligatoire** |
|----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL Resource Access]** | Répertoriez les groupes d’autorisations disponibles qui peuvent être affectés à un rôle d’utilisateur. Actuellement, la solution Store Fulfillment ne dispose pas de différents niveaux d’autorisation définis pour les rôles de ressource. Tous les rôles utilisateur disposent du même accès aux ressources. | Global | Oui |

## Aide à la boutique - Informations sur l’utilisateur

Gérez les profils utilisateur de l&#39;application Store Assist à partir des paramètres Admin System : **[!UICONTROL System > Store Fulfillment App Permissions > All Store Fulfillment App Users]**.

| **Champ** | **Description** | **Portée** | **Obligatoire** |
|------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL is Active]** | Activer ou désactiver l’utilisateur. | Global | Oui |
| **[!UICONTROL User Name]** | Nom d’utilisateur associé à l’utilisateur | Global | Oui |
| **[!UICONTROL First Name]** | Prénom associé à l’utilisateur | Global | Non |
| **[!UICONTROL Last Name]** | Nom associé à l&#39;utilisateur | Global | Non |
| **[!UICONTROL Role]** | Rôle associé à l’utilisateur | Global | Non |
| **[!UICONTROL Access to all locations]** | Attribuez aux utilisateurs l’accès à tous les magasins ou sélectionnez-les individuellement. | Global | Non |
| **Paramètres régionaux de l’interface** | Si votre magasin comporte plusieurs langues, définissez Paramètres régionaux de l’interface sur la langue à utiliser pour l’interface d’administration. | Global | Non |
| **Actif depuis** | Pour définir une date de début, sélectionnez l’icône de calendrier. | Global | Non |
| **Actif pour** | Définissez la Date d’expiration en sélectionnant l’icône de calendrier. La définition d’une date d’expiration est utile pour configurer des affectations temporaires d’utilisateurs ou de rôles. Après la date d’expiration, le statut du compte d’utilisateur passe à `Inactive`, mais le compte peut toujours être mis à jour si nécessaire. | Global | Non |
