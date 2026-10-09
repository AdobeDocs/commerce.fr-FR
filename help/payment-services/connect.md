---
title: Connexion De Votre Instance
description: Connectez votre instance Commerce à l’aide d’une clé API et d’une clé privée, puis spécifiez l’espace de données dans la configuration.
exl-id: 5038fd31-bac5-419e-a172-66919a9b5272
feature: Payments, Checkout, Configuration, Paas
badgePaas: label="PaaS uniquement" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: 00451af3-7b97-5414-9992-3a6c269e413f
    internal-label: Paas
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 76e77db86adecdbd3be76040970c0d0899c34cdc
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 0%
---

# Connexion De Votre Instance

Connectez votre instance Commerce à l’aide d’une clé API et d’une clé privée, puis spécifiez l’espace de données dans la configuration à l’aide du [connecteur de services Commerce](../landing/saas.md). **Vous ne configurez cette connexion qu’une seule fois.**

>[!VIDEO](https://video.tv.adobe.com/v/3447835)

>[!INFO]
>
> Consultez notre vidéo [[!DNL Adobe Commerce]  Connecteur de services &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-commerce-services-connector) pour plus d’informations.

* Si vous avez *déjà connecté votre instance*, en obtenant et en utilisant vos informations d’identification d’API et en configurant les services Commerce, vous pouvez passer à [configuration de votre sandbox de test](sandbox.md).
* Si vous *devez toujours connecter votre instance*, consultez les informations de cette rubrique sur [l’obtention des informations d’identification d’API](#obtain-api-credentials) et [la configuration des services Commerce](#configure-commerce-services).
* Si vous *ne savez pas si votre instance est connectée*, accédez à **Système** > Services > **Connecteur de services Commerce** et affichez les valeurs des clés API publiques et privées dans les sections [!UICONTROL Sandbox Keys] et [!UICONTROL Production Keys], ainsi que les champs *Projet* et *Espace de données* dans la section [!UICONTROL SaaS Identifier]. Si ces valeurs sont présentes, votre instance est connectée.

>[!NOTE]
>
>Tous les commerçants autorisés à utiliser les Services de paiement peuvent utiliser un espace de données de production et deux espaces de données de test.

## Obtention des informations d’identification API

Pour utiliser un service SaaS Commerce, vous devez utiliser les clés API de votre instance (clé API publique Commerce et clé privée) pour le sandbox et la production, qui sont créées et gérées dans votre [tableau de bord de mon compte](https://account.magento.com/customer/account/login). [La paire de clés](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas) peut être créée pour un compte Commerce (un pour le sandbox et un pour la production), bien qu’une seule paire puisse être utilisée activement à la fois.

>[!NOTE]
>
>Vous avez besoin d’aide pour accéder à votre tableau de bord [!UICONTROL My Account] ? Voir [Création d’un compte Commerce](https://experienceleague.adobe.com/en/docs/commerce-admin/start/commerce-account/commerce-account-create).

Une fois créée, une clé API publique est toujours disponible dans le tableau de bord de Mon compte. Il peut être copié ou supprimé selon les besoins. La clé API privée devient visible lorsque vous créez une clé API publique pour le sandbox ou l’environnement de production ; elle n’est disponible que pour copie ou enregistrement dans la boîte de dialogue qui s’ensuit et n’est pas accessible plus tard.

Une paire de clés API donnée est valide pour tous les services Commerce d’un environnement. Par conséquent, si les services Commerce sont déjà configurés pour votre instance, votre paire de clés API est déjà présente dans le connecteur de services Commerce.

En cas de perte de votre clé API, une nouvelle paire de clés API doit être [générée](../landing/saas.md#genapikey) et [appliquée](../landing/saas.md#createsaasenv) à la configuration du connecteur de services Commerce dans l’administration. Si les clés incorrectes sont configurées ou qu’aucune clé n’existe dans la configuration, une boîte de dialogue d’erreur de vérification du compte s’affiche dans Payment Services pour vous informer que le compte n’a pas été vérifié.

Consultez la [liste des services Commerce disponibles qui utilisent l’API](../landing/saas.md#availableservices).

Pour savoir comment générer une clé API pour un sandbox ou des environnements de production, voir [&#x200B; Informations d’identification &#x200B;](../landing/saas.md#apikey).

>[!IMPORTANT]
>
>Il est recommandé de ne pas régénérer une paire de clés API *et* de modifier l’identifiant SaaS et/ou l’espace de données sur une instance de production active. Les données de votre instance seront perdues si elles sont modifiées.

## Configuration des services Commerce

La même clé API peut être utilisée entre les instances, mais chaque instance doit avoir son propre [espace de données SaaS](../landing/saas.md#saasenv).

>[!NOTE]
>
>Les commerçants doivent utiliser les mêmes clés générées pour le MageID pour leurs droits de paiement.

Maintenant que vous avez obtenu vos informations d’identification, vous pouvez configurer votre projet SaaS et l’espace de données Saas.

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]**.
1. Cliquez sur **[!UICONTROL Configure Commerce Services]**.

   Cette option est visible si vous n’avez pas encore configuré les services Commerce pour votre compte.

   Vous accédez à la zone de configuration dans Admin, **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**>**[!UICONTROL Commerce Services Connector]**, pour configurer votre connecteur de services Commerce.

1. Pour configurer vos services Commerce, suivez les étapes décrites dans [Configuration SaaS](../landing/saas.md#saasenv).

   >[!INFO]
   >
   > Consultez notre vidéo [[!DNL Adobe Commerce]  Connecteur de services &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-commerce-services-connector#configuration-faqs) pour plus d’informations.

## Point d’entrée

[!DNL Payment Services] utilise le [connecteur de services Commerce](../landing/saas.md) pour se connecter aux services Commerce et effectuer le déploiement en tant que SaaS. Ce [!DNL Commerce Services Connector] communique via le point d’entrée à l’adresse :

* `commerce-beta.adobe.io` pour les environnements sandbox.
* `commerce.adobe.io for` pour les environnements en ligne.
