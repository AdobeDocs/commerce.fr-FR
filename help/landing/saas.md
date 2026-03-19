---
title: Commerce Services Connector
description: Découvrez comment intégrer votre instance Adobe Commerce ou Magento Open Source aux services à l’aide des clés d’API de production et de sandbox.
feature: Services, Saas
role: Admin, User
exl-id: 1aa6ba8b-be39-496e-b83d-a4a7db9f5dd8
badgePaas: label="PaaS uniquement" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."
source-git-commit: 6e107238b8eae31f35f43524aee5690c0fe0e03d
workflow-type: tm+mt
source-wordcount: '1564'
ht-degree: 0%

---

# [!DNL Commerce Services Connector]

Certaines fonctionnalités d’Adobe Commerce et de Magento Open Source sont optimisées par [!DNL Commerce Services] et déployées en tant que SaaS (logiciel en tant que service). Pour utiliser ces services, vous devez connecter votre instance [!DNL Commerce] à l’aide des clés API de production et sandbox, puis spécifier l’espace de données dans la [configuration](#saas-configuration). Il vous suffit de configurer la connexion une seule fois pour chaque instance.

Seul le propriétaire de la licence [!DNL Commerce] peut générer ces clés API. Si vous n’êtes pas le propriétaire de la licence, demandez les clés à la personne ou à l’équipe qui détient la licence Commerce pour votre boutique.

## Services disponibles {#availableservices}

Vous trouverez ci-dessous la liste des fonctionnalités [!DNL Commerce] auxquelles vous pouvez accéder via l’[!DNL Commerce Services Connector] :

| Service | Disponibilité |
| --- | --- |
| [[!DNL Product Recommendations]](/help/product-recommendations/overview.md) optimisé par Adobe AI | Adobe Commerce |
| [[!DNL Live Search]](/help/live-search/overview.md) optimisé par Adobe AI | Adobe Commerce |
| [[!DNL Payment Services]](/help/payment-services/guide-overview.md) | Adobe Commerce et Magento Open Source |
| [[!DNL Catalog Service]](/help/catalog-service/overview.md) | Adobe Commerce |
| [[!DNL Data Connection]](/help/data-connection/overview.md) | Adobe Commerce |

## Architecture

À un niveau élevé, le [!DNL Commerce Services Connector] est constitué des éléments principaux suivants :

![Architecture du connecteur de services Commerce](assets/saas-config-sync-workflow.png)

Les sections suivantes examinent plus en détail chacun de ces éléments.

## Informations d’identification {#apikey}

Les clés API de production et sandbox sont générées à partir du compte [!DNL Commerce] du [propriétaire de la licence](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/start/onboarding). Le compte Commerce est identifié par un ID de [!DNL Commerce] unique (MageID). Le propriétaire de la licence de l’organisation du commerçant peut générer des clés d’API pour des services tels que les recommandations de produits ou la recherche en direct, à condition que le compte soit en règle.

Les clés peuvent être partagées selon le « besoin d’en connaître » avec l’intégrateur de systèmes ou l’équipe de développement qui gère les projets et les environnements au nom du titulaire de la licence. Les développeurs qui ont reçu une [!DNL Shared Access] du propriétaire de la licence ne peuvent pas générer les clés au nom du propriétaire de la licence, même si l’organisation du commerçant figure dans la liste déroulante [!DNL Switch Accounts] de leur compte.

En outre, les intégrateurs de solutions sont autorisés à utiliser [!DNL Commerce Services]. Si vous êtes un intégrateur de solutions, le signataire du contrat du partenaire [!DNL Commerce] doit générer les clés API.

Les identifiants clés *Production* et *Sandbox* se rapportent aux environnements d’espace de données SaaS où [!DNL Commerce Services] stockez des données (et non à vos environnements Adobe Commerce). Vous pouvez utiliser le même jeu de clés API dans vos environnements Adobe Commerce locaux, de développement, d’évaluation et de production. Ce qui importe, c’est que vous colliez la paire de clés appropriée pour l’espace de données que vous configurez.

Le propriétaire de la licence est généralement le contact par Principal sur le compte Adobe Commerce et n’est pas toujours le même que le propriétaire du projet d’infrastructure cloud Adobe Commerce.

### Générer les clés API de production et Sandbox {#genapikey}

1. Connectez-vous à votre compte [!DNL Commerce] sur [https://account.magento.com](https://account.magento.com/customer/account/login){:target="_blank"}.

1. Sous l’onglet **Magento**, sélectionnez **Portail API** dans la barre latérale.

1. Dans le menu _Environnement_, sélectionnez **Production** ou **Sandbox**.

1. Saisissez un nom dans la section _Clés API_, puis cliquez sur **Ajouter** pour ouvrir la boîte de dialogue afin de télécharger la nouvelle clé.

   ![Télécharger la clé privée](assets/download-api-private-key.png)

   >[!WARNING]
   >
   > Vous pouvez copier ou télécharger la clé privée une seule fois. Conservez-le en lieu sûr.

1. Cliquez sur **Télécharger** pour enregistrer la clé privée, puis fermez la boîte de dialogue.

1. Répétez les étapes ci-dessus pour chaque environnement (production et sandbox).

   La section **Clés API** affiche désormais vos clés API (publiques). Vous avez besoin des quatre clés (clé de production et clé sandbox, publique + privée) lorsque vous [sélectionnez ou créez un projet SaaS](#createsaasenv) dans l’un des environnements ou installations associés à la licence.

## Configuration SaaS {#saasenv}

[!DNL Commerce] instances doivent être configurées avec un projet SaaS et un espace de données SaaS afin que [!DNL Commerce Services] puissiez envoyer des données au bon emplacement. Un projet SaaS regroupe tous les espaces de données SaaS. Les espaces de données SaaS sont utilisés pour collecter et stocker des données qui [!DNL Commerce Services] permettent de travailler. Certaines de ces données peuvent être exportées à partir de l’instance [!DNL Commerce] et d’autres peuvent être collectées à partir du comportement de l’acheteur sur le storefront. Ces données sont ensuite conservées dans un espace de stockage cloud sécurisé.

Par [!DNL Product Recommendations] et [!DNL Live Search], l’espace de données SaaS contient des données de catalogue et des données comportementales. Vous pouvez pointer une instance [!DNL Commerce] vers un espace de données SaaS en la [sélectionnant](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas) dans la configuration [!DNL Commerce].

>[!WARNING]
>
> Utilisez votre **espace de données SaaS de production** uniquement avec votre installation de [!DNL Commerce] de production. Son utilisation dans des environnements hors production peut combiner des données de test et des données actives (par exemple, des URL d’évaluation ou des données de catalogue de test). Si cela se produit, [envoyez une demande d’assistance](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/overview) pour demander le nettoyage des données.

Si vous ne trouvez pas les champs de configuration Live Search dans Admin, vérifiez que vous avez saisi la paire de clés API appropriée pour l’espace de données que vous avez sélectionné (les espaces de données de production utilisent des clés de production ; les espaces de données de test utilisent des clés de sandbox). Si vous configurez des clés incorrectes, les services SaaS tels que Live Search ne sont pas disponibles dans cet environnement Adobe Commerce.

### Suppression d’une clé API {#delapikey}

>[!WARNING]
>
>La suppression d’une clé toujours en cours d’utilisation interrompt immédiatement les services connectés.

Avant de supprimer une clé API, générez et stockez en toute sécurité une clé de remplacement. Mettez à jour toutes les intégrations pour utiliser la nouvelle clé et vérifiez que les services dépendants fonctionnent comme prévu.

Si vous ne voyez pas **[!DNL Live Search]** champs de configuration dans le Panneau d’administration, confirmez que vous avez saisi la clé d’API SaaS appropriée pour cet environnement. Utilisez la clé SaaS de production pour l’espace de données de production et la clé d’évaluation pour l’espace de données d’évaluation. Si la mauvaise clé est configurée, les services SaaS (y compris **[!DNL Live Search]**) ne seront pas disponibles dans votre environnement Adobe Commerce.

Sur la clé API à supprimer, cliquez sur **[!UICONTROL Delete]**. Lorsque vous y êtes invité, confirmez l’opération de suppression définitive de la clé.

### Approvisionnement de l’espace de données SaaS

Tous les commerçants Adobe Commerce peuvent accéder à un espace de données de production et à deux espaces de données de test par projet SaaS.

Vous pouvez utiliser les espaces de données de test dans les environnements hors production, mais évitez d’utiliser le même espace de données dans plusieurs environnements en même temps. Si vous souhaitez déplacer un espace de données de test vers un autre environnement, effectuez un nettoyage des données avant de le sélectionner et de le configurer dans le nouvel environnement.

Pour les projets Adobe Commerce Cloud Pro avec plusieurs environnements d’évaluation, vous pouvez demander des espaces de données de test supplémentaires pour chaque environnement d’évaluation en [soumettant une demande d’assistance](https://experienceleague.adobe.com/home?support-tab=home#support). Cependant, si vous ne disposez que d’un environnement d’évaluation et que vous avez besoin d’espaces de données de test supplémentaires, vous disposez des options suivantes :

- Contactez l’équipe du succès client ou votre responsable du succès client désigné pour demander un environnement d’évaluation supplémentaire.

- [Envoyez une demande d’assistance](https://experienceleague.adobe.com/home?support-tab=home#support) pour demander l’espace de données de test supplémentaire et indiquer la justification commerciale de cet espace de données. Cette demande est sujette à approbation.

Les clients Magento Open Source qui utilisent les services de paiement Adobe peuvent également demander un espace de données supplémentaire. Contactez l’équipe des paiements pour obtenir une approbation préalable des espaces de données supplémentaires avant d’envoyer une [demande d’assistance](https://experienceleague.adobe.com/home?support-tab=home#support) pour demander l’espace de données de test.

Les clients qui possèdent plusieurs projets cloud ou installations sur site (en ligne/de production) peuvent également demander des espaces de données de production et de test supplémentaires pour chaque projet ou instance en [soumettant une demande d’assistance](https://experienceleague.adobe.com/home?support-tab=home#support).

### Sélectionner ou créer un projet SaaS {#createsaasenv}

Pour sélectionner ou créer un projet SaaS, demandez les clés d’API [!DNL Commerce] au propriétaire de licence [!DNL Commerce] pour votre boutique :

1. Dans la barre latérale _Admin_, accédez à **Système** > Services > **Commerce Services Connector**.

   Si la section **[!UICONTROL Commerce Services Connector]** ne s’affiche pas, installez les modules [!DNL Commerce] pour le [[!DNL Commerce] service](#availableservices) souhaité et assurez-vous que le package `magento/module-services-id` est installé.

1. Dans les sections _[!UICONTROL Sandbox API Keys]_&#x200B;et&#x200B;_[!UICONTROL Production API Keys]_, collez vos valeurs clés.

   - Les clés privées doivent inclure des `-----BEGIN PRIVATE KEY-----` au début de la clé et des `-----END PRIVATE KEY-----` à la fin de la clé.
   - Si vous ne disposez pas d’une copie des clés réelles, demandez-les au propriétaire de la licence, puis connectez les valeurs à la configuration.

   Ne collez pas les valeurs de clé copiées à partir d’une sauvegarde ou d’un instantané de base de données. Lorsque la configuration est enregistrée, une couche de chiffrement supplémentaire est appliquée et les clés ne fonctionnent pas.

1. Cliquez sur **Enregistrer**.

   Tous les projets SaaS associés à vos clés apparaissent dans le champ **Projet** de la section **Identifiant SaaS**.

1. S&#39;il n&#39;existe aucun projet SaaS, cliquez sur **Créer un projet**. Ensuite, dans le champ **Projet**, entrez un nom pour votre projet SaaS.

   Pour éviter toute confusion, n’utilisez pas un service Commerce spécifique comme nom de projet (par exemple, *Live Search*, *Product Recommendations* ou *Data Connection*). À moins que votre licence n’ait été configurée pour plusieurs projets SaaS, vous pouvez utiliser le même projet SaaS pour plusieurs services.

1. Sélectionnez l’**Espace de données** à utiliser pour la configuration actuelle de votre magasin de [!DNL Commerce].

   Si vous disposez d’instances distinctes à intégrer aux services Commerce, [envoyez un ticket d’assistance](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) pour demander un nouveau projet SaaS pour chaque instance supplémentaire. Une fois que l’assistance a créé le projet SaaS, configurez le connecteur de services Commerce pour l’instance **à l’aide des mêmes clés API** et sélectionnez le nouveau projet SaaS et le nouvel espace de données.

>[!WARNING]
>
> Si vous générez de nouvelles clés sur le portail API, mettez immédiatement à jour les clés API dans la configuration Admin. Si l’administrateur utilise toujours d’anciennes clés, vos extensions SaaS ne fonctionnent plus et la collecte de données est interrompue.

Pour modifier les noms de votre projet SaaS ou de votre espace de données, cliquez sur **Renommer** en regard de l’un des deux. La modification du nom n’affecte pas votre service, car le nom n’est qu’un libellé pour vous aider à identifier et à différencier les projets des espaces de données.

## Organisation IMS (facultatif) {#organizationid}

Pour connecter votre instance Adobe Commerce au Adobe Experience Platform, connectez-vous à votre compte Adobe à l’aide de votre Adobe ID. Une fois que vous êtes connecté, l’organisation IMS associée à votre compte Adobe s’affiche dans cette section.

## Export de données SaaS

Lorsque votre instance [!DNL Commerce] se connecte à [!DNL Commerce Services], le processus d’exportation de données SaaS exporte les données Commerce de votre serveur [!DNL Commerce] vers [!DNL Commerce SaaS Services] afin qu’elles puissent être synchronisées avec les services Commerce connectés. Dans Admin, vous pouvez vérifier l’état de synchronisation à l’aide du tableau de bord [Data Management](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard). Pour plus d&#39;informations, consultez le [Guide d&#39;exportation de données SaaS](../data-export/overview.md).
