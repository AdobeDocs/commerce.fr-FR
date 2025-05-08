---
title: Commerce Services Connector
description: Découvrez comment intégrer votre instance Adobe Commerce ou Magento Open Source aux services à l’aide des clés d’API de production et de sandbox.
feature: Services, Saas
role: Admin, User
exl-id: 1aa6ba8b-be39-496e-b83d-a4a7db9f5dd8
badgePaas: label="PaaS uniquement" type="Informative" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."
source-git-commit: 55b342895be0fc81511644a95c52a79bdd34fc98
workflow-type: tm+mt
source-wordcount: '1420'
ht-degree: 0%

---

# [!DNL Commerce Services Connector]

Certaines fonctionnalités d’Adobe Commerce et de Magento Open Source sont optimisées par [!DNL Commerce Services] et déployées en tant que SaaS (logiciel en tant que service). Pour utiliser ces services, vous devez connecter votre instance [!DNL Commerce] à l’aide des clés API de production et sandbox, puis spécifier l’espace de données dans la [configuration](#saas-configuration). Il vous suffit de configurer la connexion une seule fois pour chaque instance.

## Services disponibles {#availableservices}

Vous trouverez ci-dessous la liste des fonctionnalités [!DNL Commerce] auxquelles vous pouvez accéder via l’[!DNL Commerce Services Connector] :

| Service | Disponibilité |
| ---|--- |
| [[!DNL Product Recommendations]](/help/product-recommendations/overview.md) optimisé par Adobe Sensei | Adobe Commerce |
| [[!DNL Live Search]](/help/live-search/overview.md) optimisé par Adobe Sensei | Adobe Commerce |
| [[!DNL Payment Services]](/help/payment-services/guide-overview.md) | Adobe Commerce et Magento Open Source |
| [[!DNL Site-Wide Analysis Tool]](https://experienceleague.adobe.com/fr/docs/commerce-operations/tools/site-wide-analysis-tool/intro) | Adobe Commerce |
| [[!DNL Catalog Service]](/help/catalog-service/overview.md) | Adobe Commerce |
| [[!DNL Data Connection]](/help/data-connection/overview.md) | Adobe Commerce |

## Architecture

À un niveau élevé, le [!DNL Commerce Services Connector] est constitué des éléments principaux suivants :

![Architecture du connecteur de services Commerce](assets/saas-config-sync-workflow.png)

Les sections suivantes examinent plus en détail chacun de ces éléments.

## Informations d’identification {#apikey}

Les clés API de production et sandbox sont générées à partir du compte [!DNL Commerce] du [propriétaire de la licence](https://experienceleague.adobe.com/fr/docs/commerce-cloud-service/start/onboarding). Le compte Commerce est identifié par un ID de [!DNL Commerce] unique (MageID). Le propriétaire de la licence de l’organisation du commerçant peut générer des clés d’API pour des services tels que les recommandations de produits ou la recherche en direct, à condition que le compte soit en règle.

Les clés peuvent être partagées selon le « besoin d’en connaître » avec l’intégrateur de systèmes ou l’équipe de développement qui gère les projets et les environnements au nom du titulaire de la licence. Les développeurs qui ont reçu une [!DNL Shared Access] du propriétaire de la licence ne peuvent pas générer les clés en leur nom, même si l’organisation du commerçant figure dans la liste déroulante [!DNL Switch Accounts] de leur compte .

En outre, les intégrateurs de solutions sont également autorisés à utiliser [!DNL Commerce Services]. Si vous êtes un intégrateur de solutions, le signataire du contrat du partenaire [!DNL Commerce] doit générer les clés API.

>[!NOTE]
>Les identifiants clés *Production* et *Sandbox* ne font pas référence à votre environnement. Vous utilisez le même ensemble de clés API pour chacun de vos environnements, par exemple les environnements locaux, de développement, d’évaluation ou de production.
>
>Le propriétaire de la licence est généralement le contact par Principal sur le compte Adobe Commerce et n’est pas toujours le même que le propriétaire du projet d’infrastructure cloud Adobe Commerce.

### Générer les clés API de production et Sandbox {#genapikey}

1. Connectez-vous à votre compte [!DNL Commerce] sur [https://account.magento.com](https://account.magento.com/customer/account/login){:target="_blank"}.

1. Sous l’onglet **Magento**, sélectionnez **Portail API** dans la barre latérale.

1. Dans le menu _Environnement_, sélectionnez **Production** ou **Sandbox**.

   >[!NOTE]
   >
   >Les *Production* et *Sandbox* se rapportent aux environnements d’espace de données où les données sont stockées dans les systèmes principaux SaaS d’Adobe. Il ne fait pas référence aux environnements de commerce dans lesquels vous utiliserez les clés.

1. Saisissez un nom dans la section _Clés API_, puis cliquez sur **Ajouter** pour ouvrir la boîte de dialogue afin de télécharger la nouvelle clé.

   ![Télécharger la clé privée](assets/download-api-private-key.png)

   >[!WARNING]
   >
   > Cette boîte de dialogue vous offre la seule possibilité de copier ou de télécharger vos clés.

1. Cliquez sur **Télécharger** puis sur **Annuler**.

1. Répétez les étapes ci-dessus pour chaque environnement (production et sandbox).

   La section **Clés API** affiche désormais vos clés API (publiques). Vous avez besoin des quatre clés (clé de production et clé sandbox, publique + privée) lorsque vous [sélectionnez ou créez un projet SaaS](#createsaasenv) dans l’un des environnements ou installations associés à la licence.

## Configuration SaaS {#saasenv}

[!DNL Commerce] instances doivent être configurées avec un projet SaaS et un espace de données SaaS afin que [!DNL Commerce Services] puissiez envoyer des données au bon emplacement. Un projet SaaS regroupe tous les espaces de données SaaS. Les espaces de données SaaS sont utilisés pour collecter et stocker des données qui [!DNL Commerce Services] permettent de travailler. Certaines de ces données peuvent être exportées à partir de l’instance [!DNL Commerce] et d’autres peuvent être collectées à partir du comportement de l’acheteur sur le storefront. Ces données sont ensuite conservées dans un espace de stockage cloud sécurisé.

Par [!DNL Product Recommendations], l’espace de données SaaS contient des données de catalogue et des données comportementales. Vous pouvez pointer une instance [!DNL Commerce] vers un espace de données SaaS en la [sélectionnant](https://experienceleague.adobe.com/fr/docs/commerce-admin/config/services/saas) dans la configuration [!DNL Commerce].

>[!WARNING]
>
> Utilisez votre **espace de données SaaS de production** uniquement sur votre installation de [!DNL Commerce] de production pour éviter les collisions de données. Dans le cas contraire, vous risquez de polluer les données de votre site de production avec des données de test, ce qui entraîne des retards de déploiement. Par exemple, vos données de produit de production peuvent être écrasées par erreur à partir de données d’évaluation, telles que les URL d’évaluation.
> Si cela se produit, [envoyez une demande d’assistance](https://experienceleague.adobe.com/fr/docs/commerce-knowledge-base/kb/overview) pour demander le nettoyage des données.

### Approvisionnement de l’espace de données SaaS

Tous les commerçants Adobe Commerce peuvent accéder à un espace de données de production et à deux espaces de données de test par projet SaaS.

Vous pouvez utiliser les espaces de données de test dans n’importe quel environnement hors production tant que vous n’utilisez pas le même espace de données dans plusieurs environnements en même temps. Pour utiliser l’espace de données de test dans un autre environnement, effectuez un nettoyage des données avant de sélectionner et de configurer l’espace de données dans cet environnement.

Pour les projets Adobe Commerce Cloud Pro avec plusieurs environnements d’évaluation, vous pouvez demander des espaces de données de test supplémentaires pour chaque environnement d’évaluation en [soumettant une demande d’assistance](https://experienceleague.adobe.com/home?lang=fr&support-tab=home#support). Cependant, si vous ne disposez que d’un environnement d’évaluation et que vous avez besoin d’espaces de données de test supplémentaires, vous disposez des options suivantes :

- Contactez l’équipe du succès client ou votre responsable du succès client désigné pour demander un environnement d’évaluation supplémentaire.

- [Envoyez une demande d’assistance](https://experienceleague.adobe.com/home?lang=fr&support-tab=home#support) pour demander l’espace de données de test supplémentaire et indiquer la justification commerciale de l’espace de données supplémentaire. Cette demande est sujette à approbation.

Les clients Magento Open Source qui utilisent les services de paiement Adobe peuvent également demander un espace de données supplémentaire. Contactez l’équipe des paiements pour obtenir une approbation préalable des espaces de données supplémentaires avant d’envoyer une [demande d’assistance](https://experienceleague.adobe.com/home?lang=fr&support-tab=home#support) pour demander l’espace de données de test.

Les clients qui possèdent plusieurs projets cloud ou installations sur site (en ligne/de production) peuvent également demander des espaces de données de production et de test supplémentaires pour chaque projet ou instance en [soumettant une demande d’assistance](https://experienceleague.adobe.com/home?lang=fr&support-tab=home#support).

### Sélectionner ou créer un projet SaaS {#createsaasenv}

Pour sélectionner ou créer un projet SaaS, demandez la clé API [!DNL Commerce] au propriétaire de la licence [!DNL Commerce] de votre boutique :

>[!NOTE]
>
> Si vous ne voyez pas la section **[!UICONTROL Commerce Services Connector]** dans la configuration [!DNL Commerce], vous devez installer les modules [!DNL Commerce] pour le [[!DNL Commerce] service](#availableservices) souhaité.

1. Dans la barre latérale _Admin_, accédez à **Système** > Services > **Commerce Services Connector**.

   Si la section **[!UICONTROL Commerce Services Connector]** n’apparaît pas dans la configuration [!DNL Commerce], installez les modules [!DNL Commerce] correspondant au [[!DNL Commerce] service](#availableservices) souhaité. Assurez-vous également que le package `magento/module-services-id` est installé.

1. Dans les sections _[!UICONTROL Sandbox API Keys]_&#x200B;et&#x200B;_[!UICONTROL Production API Keys]_, collez vos valeurs clés.

   - Les clés privées doivent inclure des `----BEGIN PRIVATE KEY---` au début de la clé et des `----END PRIVATE KEY----` à la fin de la clé.
   - Si vous ne disposez pas d’une copie des clés réelles, demandez-les au propriétaire du compte, puis connectez les valeurs à la configuration.

   >[!WARNING]
   >
   > Si vous ajoutez des valeurs de clé en interrogeant une sauvegarde ou un instantané de base de données et en collant les valeurs dans la configuration, une couche de chiffrement supplémentaire est appliquée et les clés ne fonctionnent pas.

1. Cliquez sur **Enregistrer**.

Tous les projets SaaS associés à vos clés apparaissent dans le champ **Projet** de la section **Identifiant SaaS**.

1. S&#39;il n&#39;existe aucun projet SaaS, cliquez sur **Créer un projet**. Ensuite, dans le champ **Projet**, entrez un nom pour votre projet SaaS.

>[!NOTE]
>
>Pour éviter toute confusion, n’utilisez pas un service Commerce spécifique comme nom de projet, par exemple *Recherche en direct*, *Recommandations de produits* ou *Connexion de données*.  À moins que votre licence n’ait été configurée pour plusieurs projets SaaS, vous pouvez utiliser le même projet SaaS pour plusieurs services.

1. Sélectionnez l’**Espace de données** à utiliser pour la configuration actuelle de votre magasin de [!DNL Commerce].

>[!NOTE]
>
>Si vous disposez d’instances distinctes à intégrer aux services Commerce, [envoyez un ticket d’assistance](https://experienceleague.adobe.com/fr/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) pour demander un nouveau projet SaaS pour chaque instance supplémentaire. Une fois que la prise en charge a créé le projet SaaS, configurez l’intégration des services Commerce pour l’instance à l’aide de la même clé API et sélectionnez le nouveau projet SaaS pour l’espace de données.

>[!WARNING]
>
> Si vous générez de nouvelles clés dans la section Portail API de Mon compte, mettez immédiatement à jour les clés API dans la configuration Admin. Si vous générez de nouvelles clés et ne les mettez pas à jour dans Admin, vos extensions SaaS ne fonctionnent plus et vous perdez des données importantes.

Pour modifier les noms de votre projet SaaS ou de votre espace de données, cliquez sur **Renommer** en regard de l’un des deux. La modification du nom n’affecte pas votre service, car le nom n’est qu’un libellé pour vous aider à identifier et à différencier les projets des espaces de données.

## Organisation IMS (facultatif) {#organizationid}

Pour connecter votre instance Adobe Commerce au Adobe Experience Platform, connectez-vous à votre compte Adobe à l’aide de votre Adobe ID. Une fois que vous êtes connecté, l’organisation IMS associée à votre compte Adobe s’affiche dans cette section.

## Export de données SaaS

Lorsque votre instance [!DNL Commerce] se connecte à [!DNL Commerce Services], le processus d’exportation de données SaaS exporte les données Commerce de votre serveur [!DNL Commerce] vers [!DNL Commerce SaaS Services] afin qu’elles puissent être synchronisées avec les services Commerce connectés. Dans Admin, vous pouvez vérifier l’état de synchronisation à l’aide du tableau de bord [Data Management](https://experienceleague.adobe.com/fr/docs/commerce-admin/systems/data-transfer/data-dashboard). Pour plus d&#39;informations, consultez le [Guide d&#39;exportation de données SaaS](../data-export/overview.md).
