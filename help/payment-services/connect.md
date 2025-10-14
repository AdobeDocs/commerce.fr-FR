---
title: Connexion De Votre Instance
description: Connectez votre instance Commerce à l’aide d’une clé API et d’une clé privée, puis spécifiez l’espace de données dans la configuration.
exl-id: 5038fd31-bac5-419e-a172-66919a9b5272
feature: Payments, Checkout, Configuration, Paas
badgePaas: label="PaaS uniquement" type="Informative" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."
source-git-commit: 0f2e9c3a7d990a46bafc5f3b8a083436d42643b5
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---


# Connexion De Votre Instance

Connectez votre instance Commerce à l’aide d’une clé API et d’une clé privée, puis spécifiez l’espace de données dans la configuration à l’aide du [connecteur de services Commerce](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/saas.html?lang=fr). **Vous ne configurez cette connexion qu’une seule fois.**

>[!VIDEO](https://video.tv.adobe.com/v/3448019?captions=fre_fr)

>[!INFO]
>
> Consultez notre vidéo [[!DNL Adobe Commerce]  Connecteur de services &#x200B;](https://experienceleague.adobe.com/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-commerce-services-connector.html?lang=fr) pour plus d’informations.

* Si vous avez *déjà connecté votre instance*, en obtenant et en utilisant vos informations d’identification d’API et en configurant les services Commerce, vous pouvez passer à [configuration de votre sandbox de test](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/sandbox.html?lang=fr).
* Si vous *devez toujours connecter votre instance*, consultez les informations de cette rubrique sur [l’obtention des informations d’identification d’API](#obtain-api-credentials) et [la configuration des services Commerce](#configure-commerce-services).
* Si vous *ne savez pas si votre instance est connectée*, accédez à **Système** > Services > **Connecteur de services Commerce** et affichez les valeurs des clés API publiques et privées dans les sections [!UICONTROL Sandbox Keys] et [!UICONTROL Production Keys], ainsi que les champs *Projet* et *Espace de données* dans la section [!UICONTROL SaaS Identifier]. Si ces valeurs sont présentes, votre instance est connectée.

>[!NOTE]
>
>Tous les commerçants autorisés à utiliser les Services de paiement peuvent utiliser un espace de données de production et deux espaces de données de test.

## Obtention des informations d’identification API

Pour utiliser un service SaaS Commerce, vous devez utiliser les clés API de votre instance (clé API publique Commerce et clé privée) pour le sandbox et la production, qui sont créées et gérées dans votre [tableau de bord de mon compte](https://account.magento.com/customer/account/login). [La paire de clés](https://experienceleague.adobe.com/fr/docs/commerce-admin/config/services/saas) peut être créée pour un compte Commerce (un pour le sandbox et un pour la production), bien qu’une seule paire puisse être utilisée activement à la fois.

>[!NOTE]
>
>Vous avez besoin d’aide pour accéder à votre tableau de bord [!UICONTROL My Account] ? Voir [Création d’un compte Commerce](https://experienceleague.adobe.com/fr/docs/commerce-admin/start/commerce-account/commerce-account-create).

Une fois créée, une clé API publique est toujours disponible dans le tableau de bord de Mon compte. Il peut être copié ou supprimé selon les besoins. La clé API privée devient visible lorsque vous créez une clé API publique pour le sandbox ou l’environnement de production ; elle n’est disponible que pour copie ou enregistrement dans la boîte de dialogue qui s’ensuit et n’est pas accessible plus tard.

Une paire de clés API donnée est valide pour tous les services Commerce d’un environnement. Par conséquent, si les services Commerce sont déjà configurés pour votre instance, votre paire de clés API est déjà présente dans le connecteur de services Commerce.

En cas de perte de votre clé API, une nouvelle paire de clés API doit être [générée](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/connect.html?lang=fr#generate-an-api-key-and-private-key) et [appliquée](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/connect.html?lang=fr#configure-saas-project) à la configuration du connecteur de services Commerce dans l’administration. Si les clés incorrectes sont configurées ou qu’aucune clé n’existe dans la configuration, une boîte de dialogue d’erreur de vérification du compte s’affiche dans Payment Services pour vous informer que le compte n’a pas été vérifié.

Consultez la [liste des services Commerce disponibles qui utilisent l’API](https://experienceleague.adobe.com/fr/docs/commerce-merchant-services/user-guides/integration-services/saas#availableservices).

Pour savoir comment générer une clé API pour un sandbox ou des environnements de production, voir [&#x200B; Informations d’identification &#x200B;](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/saas.html?lang=fr#apikey).

>[!IMPORTANT]
>
>Il est recommandé de ne pas régénérer une paire de clés API *et* de modifier l’identifiant SaaS et/ou l’espace de données sur une instance de production active. Les données de votre instance seront perdues si elles sont modifiées.

## Configuration des services Commerce

La même clé API peut être utilisée entre les instances, mais chaque instance doit avoir son propre [espace de données SaaS](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/saas.html?lang=fr#saasenv).

>[!NOTE]
>
>Les commerçants doivent utiliser les mêmes clés générées pour le MageID pour leurs droits de paiement.

Maintenant que vous avez obtenu vos informations d’identification, vous pouvez configurer votre projet SaaS et l’espace de données Saas.

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]**.
1. Cliquez sur **[!UICONTROL Configure Commerce Services]**.

   Cette option est visible si vous n’avez pas encore configuré les services Commerce pour votre compte.

   Vous accédez à la zone de configuration dans Admin, **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**>**[!UICONTROL Commerce Services Connector]**, pour configurer votre connecteur de services Commerce.

1. Pour configurer vos services Commerce, suivez les étapes décrites dans [Configuration SaaS](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/integration-services/saas.html?lang=fr#saasenv).

   >[!INFO]
   >
   > Consultez notre vidéo [[!DNL Adobe Commerce]  Connecteur de services &#x200B;](https://experienceleague.adobe.com/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-commerce-services-connector.html?lang=fr#configuration-faqs) pour plus d’informations.

## Point d’entrée

[!DNL Payment Services] utilise le [connecteur de services Commerce](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/saas.html?lang=fr) pour se connecter aux services Commerce et effectuer le déploiement en tant que SaaS. Ce [!DNL Commerce Services Connector] communique via le point d’entrée à l’adresse :

* `commerce-beta.adobe.io` pour les environnements sandbox.
* `commerce.adobe.io for` pour les environnements en ligne.
