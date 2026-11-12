---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 0%
---
Par défaut, une [vue de catalogue](catalog-view.md) est publique. Limitez l’accès à une vue de catalogue afin que seules les requêtes disposant d’un jeton signé valide puissent récupérer ses données.

Une vue de catalogue devient privée de deux manières :

- **Automatiquement, pour les catalogues partagés B2B** : pour les déploiements B2B d’Adobe Commerce qui utilisent les services de marchandisage avec le modèle de données de catalogue composable (CCDM), les vues de catalogue privé sont automatiquement créées et configurées pour vous, en fonction de la configuration du catalogue partagé dans [!DNL Adobe Commerce]. Voir [Vues de catalogue privé automatique pour les catalogues partagés B2B](#automatic-private-catalog-views-for-b2b-shared-catalogs).

- **Manuellement, pour toute vue de catalogue** : pour restreindre l’accès à une vue de catalogue B2C qui serait autrement publique, suivez les étapes de la section [Protection d’une vue de catalogue](#protect-a-catalog-view). Consultez [Cas d’utilisation de clés d’accès restreint](restricted-access-keys.md#restricted-access-key-use-cases) pour obtenir des exemples, tels que les portails partenaires et les aperçus de version préliminaire.

La protection du catalogue s’applique uniquement à la vue de catalogue sélectionnée. Cela ne modifie pas les politiques ou les calques de la vue. Elle limite l&#39;affichage à un seul catalogue des prix. Voir [Restriction du catalogue des prix sur les affichages de catalogue privé](#price-book-restriction-on-private-catalog-views).

## Comprendre le périmètre de protection

La protection du catalogue s’applique uniquement à la vue du catalogue dans laquelle elle est activée. Il protège les demandes de catalogue et de recherche, mais ne modifie pas les politiques ou les calques de la vue, protège d’autres vues de catalogue ou sécurise les opérations de panier, de passage en caisse ou de commande.

Le serveur principal de commerce connecté doit appliquer indépendamment l’éligibilité d’achat.

## Restriction du catalogue des prix pour les vues de catalogue privé

Une vue de catalogue privée ne peut référencer qu’un seul catalogue des prix. Cela diffère d’une vue de catalogue public, qui peut utiliser plusieurs tarifs.

Lorsque [!UICONTROL Catalog Protection] est activé, le sélecteur de catalogue des prix sur le formulaire d’affichage du catalogue passe d’une commande à sélection multiple à une commande à sélection unique (bouton radio).

![Restriction du catalogue privé pour la consultation du catalogue des prix](/help/assets/ccdm-shared/setup/catalog-view-private-pricebook-restrictions.png)

- Si vous activez [!UICONTROL Catalog Protection] sur une vue de catalogue à laquelle plusieurs tarifs sont affectés, vous ne pouvez pas enregistrer la vue tant que vous n&#39;avez pas supprimé tous les tarifs, sauf un.
- Si vous avez précédemment enregistré une vue de catalogue privée avec plusieurs affectations de catalogue de prix avant l&#39;existence de cette restriction, la configuration de la vue de catalogue n&#39;est pas automatiquement modifiée. Cependant, la prochaine fois que vous modifierez la vue, vous devrez supprimer tous les tarifs sauf un avant de pouvoir enregistrer les mises à jour.

Dans chaque cas, le système affiche le message de validation suivant : `A protected catalog view can use only one price book. Select 'Single price book only' to continue.`

Les vues de catalogue public ne sont pas affectées par cette restriction et peuvent continuer à faire référence à plusieurs catalogues de prix.

## Vues de catalogue privé automatiques pour les catalogues partagés B2B

[!BADGE Private beta]{type=Caution tooltip="Nécessite l’extension B2B du connecteur Adobe Commerce Optimizer, qui est actuellement en version bêta privée."}

Pour les déploiements B2B d’Adobe Commerce qui utilisent les services de marchandisage avec le CCDM, le système crée et configure automatiquement les vues de catalogue privé, en fonction de la configuration de catalogue partagé dans [!DNL Adobe Commerce]. Cette configuration inclut la vue de catalogue, la politique, une clé d’accès restreint initiale et une référence au catalogue. Avec cette configuration, vous gérez les clés d’accès restreint à partir de la page **Clés d’accès restreint** de l’administrateur Commerce (**Système** > **Transfert de données**).

Si vous n’utilisez pas de catalogues partagés B2B, par exemple pour protéger une vue de catalogue pour un portail partenaire ou un aperçu de version préliminaire, suivez les instructions de la section [Protection d’une vue de catalogue](#protect-a-catalog-view) pour en configurer une manuellement.

## Protection d’une vue de catalogue

>[!NOTE]
>
>Ignorez cette procédure pour les vues de catalogue associées aux catalogues partagés B2B gérés par [!DNL Adobe Commerce Optimizer Connector for B2B]. Voir [Vues de catalogue privé automatique pour les catalogues partagés B2B](#automatic-private-catalog-views-for-b2b-shared-catalogs).

Avant de commencer, [créez une clé d’accès restreint](restricted-access-keys.md) à partir de la clé publique générée par votre application cliente.

1. Dans la vue catalogue, créez ou modifiez le formulaire, basculez **[!UICONTROL Catalog Protection]** sur **[!UICONTROL Enabled]**.

1. Sous **[!UICONTROL Restricted Access Keys]**, sélectionnez jusqu’à trois [clés d’accès restreint](restricted-access-keys.md) à affecter à cette vue de catalogue.

   ![Protection du catalogue activée sur le formulaire de modification de la vue du catalogue, avec une clé d&#39;accès restreinte attribuée](/help/assets/ccdm-shared/setup/catalog-view-protected.png){width="70%" zoomable="yes"}

1. Cliquez sur **[!UICONTROL Save catalog view]**.

   La vue Catalogue est maintenant protégée. Seules les requêtes portant un jeton signé valide d’une clé attribuée peuvent récupérer ses données.

   >[!NOTE]
   >
   >Patientez jusqu’à cinq minutes pour que les modifications apportées à la configuration de la protection du catalogue prennent effet.

## Vérifier que l’accès est appliqué

Pour confirmer qu’une vue de catalogue privé rejette les requêtes non autorisées, appelez son point d’entrée GraphQL avec et sans jeton signé, à l’aide des en-têtes suivants :

| En-tête | Objectif |
| --- | --- |
| `AC-View-ID` | Vue du catalogue à interroger. |
| `AC-Price-Book-ID` | Le catalogue des prix à appliquer. |
| `AC-Catalog-View-Access-Token` | JWT signé prouvant l’autorisation pour la vue de catalogue. |

Une requête sans jeton valide renvoie une erreur GraphQL au lieu des données de catalogue, par exemple :

```json
{
  "errors": [
    {
      "message": "Access key validation failed: Missing token",
      "extensions": { "x-commerce-exception": "access-key-invalid" }
    }
  ]
}
```

Une requête portant un jeton signé par une clé attribuée non expirée renvoie les données du catalogue comme prévu. Pour plus d’informations sur la signature d’un jeton JWT et l’appel de l’API de marchandisage, consultez la [documentation destinée aux développeurs](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api#authentication).

## Gestion des clés d’accès restreintes

Si [!UICONTROL Catalog Protection] est activé et que toutes les clés affectées expirent, la vue de catalogue devient inaccessible. Les vitrines qui reposent sur cette vue de catalogue ne peuvent pas servir de données à partir de celle-ci. Attribuez une nouvelle clé non expirée pour restaurer l’accès. Pour obtenir des instructions, voir [Faire pivoter une clé](restricted-access-keys.md#rotate-a-key).

>[!NOTE]
>
>Pour les déploiements B2B d’Adobe Commerce à l’aide des services de marchandisage avec CCDM, vous gérez les clés d’accès à partir de la page **Clés d’accès restreint** de l’administrateur Commerce (**Système** > **Transfert de données**). Pour plus d&#39;informations, consultez la section [Gestion des clés d&#39;accès restreint](https://experienceleague.adobe.com/fr/docs/commerce-admin/systems/data-transfer/data-sync/catalog-view-sync/restricted-access-keys) du Guide d&#39;intégration *[!DNL Adobe Commerce Optimizer Connector]*.

## Plus comme ceci

- [Vues catalogue](catalog-view.md) : découvrez comment les vues catalogue organisent votre catalogue de produits par structure d’entreprise, politiques et prix.
- [Clés d’accès restreint](restricted-access-keys.md) : créez, attribuez et faites pivoter les clés utilisées pour signer les jetons pour la protection du catalogue.
