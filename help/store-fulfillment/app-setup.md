---
title: Configuration de l’application
description: Configurez l’application  [!DNL Store Assist]  gérer les workflows et les processus d’exécution de bout en bout des magasins pour les achats en ligne, le retrait dans les commandes en magasin.
level: Intermediate
role: Admin
feature: Shipping/Delivery, Configuration, Tools and External Services
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 0%

---

# Configuration de l’application

Store Assist est une application de plateforme de gestion des commandes en tant que service (FaaS) optimisée par Walmart Commerce Technologies. L’application fournit des fonctionnalités d’exécution en magasin pour traiter les commandes [!DNL buy online, pick up in store] (BOPIS). Grâce à l&#39;assistance magasin, les associés de magasin peuvent voir quels articles ont été commandés par les clients, prélever les bons articles plus rapidement et configurer des commandes exécutées pour une livraison en magasin ou en bordure de rue aux clients.

L’application Store Assist reçoit toutes les informations sur les commandes et les clients, depuis les détails de la commande jusqu’aux heures de retrait, et met les données à la disposition des associés du magasin en ligne, via des appareils mobiles. L’application comprend des modules [!UICONTROL Pick], [!UICONTROL Stage], [!UICONTROL Handoff] et [!UICONTROL Orders] pour aider Store Associates à réaliser des activités telles que :

- Attribuez les dates et heures de livraison des commandes.
- Recevez des notifications des clients lorsqu’ils arrivent pour le retrait de la commande.
- Commandes intermédiaires à transmettre aux clients.
- Suivre le statut des commandes pour toutes les commandes dans les magasins qui leur sont affectés.

>[!NOTE]
>
>Pour en savoir plus sur l’application Store Assist, consultez la rubrique [Workflows d’exécution Store Assist](store-assist-modules.md).

## Configuration de l’application d’assistance de magasin

L’application Store Assist nécessite deux types de configuration :

- Les paramètres système d’administration Adobe Commerce pour [gérer les comptes utilisateur, les rôles utilisateur, les autorisations de ressources](user-setup.md) et [rendre les sélections de modèles et de voitures disponibles pour les clients pendant le processus d’enregistrement](check-in-experience-setup.md).

- Paramètres de configuration front-end pour personnaliser l’interface de l’application d’assistance Store et d’autres paramètres, notamment :

   - **Marque de l’application Store Assist** : personnalisez l’interface utilisateur de l’application avec le logo et les couleurs de votre entreprise.

   - **Mettre à jour les instructions par défaut**—Personnalisez les instructions des modules Sélection, Évaluation, Remise et Commande du programme d&#39;assistance au magasin pour guider Store Associates à chaque étape du processus d&#39;exécution pour votre entreprise.

   - **Localisation** : sélectionnez la langue disponible pour l&#39;application. Choisissez votre format de date et d&#39;heure, puis sélectionnez vos unités de mesure et votre devise par défaut.

   - **Durée d&#39;inactivité** : indiquez la durée pendant laquelle l&#39;application doit être inactive avant de se déconnecter.

   - **Annulation depuis le magasin** : indiquez si les commandes peuvent être annulées depuis le magasin et quels rôles disposent d&#39;autorisations d&#39;annulation

   - **Fenêtre de nettoyage des commandes** : indiquez combien de temps après le [Délai estimé de prélèvement](enable-general.md#delivery-method-title-configuration) une commande prélevée reste en évaluation avant d&#39;être réapprovisionnée (par exemple, trois jours). La valeur par défaut est de sept jours. Si cette configuration est activée, la commande est automatiquement annulée à l&#39;expiration de ce délai. Les articles sont réapprovisionnés et le marchand reçoit un e-mail d&#39;annulation.

   - Personnalisez toutes les instructions de l’application (prélèvement, évaluation, remise).

   - **Notifications de prélèvement** : indiquez si vous souhaitez envoyer une notification push pour lancer le processus de prélèvement une fois qu&#39;un client a passé une commande.

   - **Notifications d&#39;archivage**—Indiquez si vous souhaitez envoyer une notification push pendant le processus d&#39;archivage pour les enlèvements de commande - après l&#39;archivage, lorsque le temps d&#39;attente du client dépasse une période spécifiée. Vous pouvez également désactiver la notification.

   - **Transmettre le processus**—Activez les processus facultatifs lorsque Store Associate livre la commande au client, par exemple si vous avez besoin d&#39;une signature client ou si vous demandez à l&#39;associé de vérifier l&#39;ID client.

   - **Activer le rejet d&#39;article lors du transfert** : permet aux clients de renvoyer ou d&#39;annuler des articles de commande lors du transfert de commande.

  Collaborez avec l’équipe des services clients de Walmart Commerce Technologies pour terminer la configuration frontale de l’application d’assistance au magasin.

## Téléchargement et installation de l’application

Une fois l’application d’assistance en magasin configurée, Store Associates peut la télécharger, l’installer et s’y connecter à partir de ses appareils mobiles.

- Vérifiez que l&#39;appareil mobile répond à la [configuration matérielle et logicielle requise](solution-requirements.md#store-assist-app-requirements) pour la solution Store Fulfillment.

- Téléchargez l’application d’assistance de magasin depuis [Apple App Store](https://apps.apple.com/us/app/store-assist-by-walmart/id1609281539){target="_blank"} ou la [boutique Google Play](https://play.google.com/store/apps/details?id=com.walmart.faas.storeassist){target="_blank"}.

- Store Associates requiert les informations suivantes pour se connecter :

   - **[!UICONTROL Company name]** associé au compte d’assistance de magasin

   - **Informations d’identification du compte Store Assist** : nom d’utilisateur et mot de passe de son compte.

  Un administrateur ou une administratrice d’Adobe Commerce peut créer et gérer des comptes d’utilisateurs et d’utilisatrices [!DNL Store Assist app] pour tous les emplacements de magasin où le [cueillette en magasin](merchant-store-configuration.md#pickup-location-configuration) est activé dans les paramètres des magasins d’administration.
