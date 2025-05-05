---
title: Configuration de plusieurs sites web et d’étendues
description: Configurez les stocks et les méthodes de diffusion pour plusieurs sites web et étendues de magasin.
role: Admin
level: Experienced
feature: Shipping/Delivery, Inventory, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# Configuration de plusieurs sites web et d’étendues

Vous pouvez définir la [Portée](https://experienceleague.adobe.com/fr/docs/commerce-admin/start/setup/websites-stores-views#scope-settings) de quelques éléments pour qu’ils s’adaptent à plusieurs sites web, boutiques et vues de boutique :

- [Gérer les stocks](https://experienceleague.adobe.com/fr/docs/commerce-admin/inventory/stocks/stocks-manage) par étendue

- Gérer les [!DNL Delivery Methods] par étendue

Vous pouvez affecter des stocks à un site web ou à une étendue de magasin. Mettez ensuite à jour les sources du magasin pour définir les méthodes de diffusion disponibles (diffusion à domicile, retrait du magasin).

Une fois la configuration mise à jour, les options de retrait du magasin dans la page des détails du produit (PDP) dans le storefront Adobe Commerce peuvent être sélectionnées uniquement pour les produits disponibles à partir d’une source de stock qui permet le retrait du magasin.

## Gérer les paramètres de prélèvement en magasin

Activez ou désactivez les options de [!UICONTROL In-Store Pickup] pour chaque site web ou étendue de magasin à partir des [ Configurations des méthodes de diffusion ](enable-general.md#delivery-methods) dans l’interface d’administration.

1. Accédez à **[!UICONTROL Stores > Configuration]**.

1. Sélectionnez l’étendue (site web ou magasin) à configurer.

1. Lorsque la portée est sélectionnée, accédez à **[!UICONTROL Sales > Delivery Methods]**.

1. Désactivez ou activez la méthode Diffusion **[!UICONTROL In-Store Pickup]** .

Dans cette section, vous pouvez également indiquer si la collecte en magasin ou en bordure de rue est disponible partout dans le monde.

Gérer les paramètres de [!UICONTROL In-Store Pickup] et de [!UICONTROL Delivery Method] par source de stock. Il existe de nombreuses autres configurations pour une flexibilité totale dans votre implémentation.
