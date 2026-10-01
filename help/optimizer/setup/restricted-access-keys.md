---
title: Clés d’accès restreintes
description: Découvrez comment les clés d’accès restreint protègent les vues de catalogue dans [!DNL Adobe Commerce Optimizer], qu’elles soient créées automatiquement pour les catalogues partagés B2B ou gérées manuellement.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et [!DNL Adobe Commerce Optimizer] (infrastructure SaaS gérée par Adobe)."
TQID: https://experienceleague.adobe.com/Jmze0Pq3kSNMIXqkkML-hmmlZnv-XKgeEgRB8Q8NZ6s
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
    internal-label: Optimization
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
nudge: true
source-git-commit: f93bd673624c58050696da772ce733874ce594e5
workflow-type: tm+mt
source-wordcount: '1251'
ht-degree: 0%
---
# Clés d’accès restreintes

Les clés d’accès restreint permettent aux applications clientes autorisées d’accéder à une [vue de catalogue privée](catalog-view.md) ; seules les requêtes portant un jeton signé valide à partir d’une clé attribuée peuvent récupérer les données du catalogue. Toutes les autres requêtes sont refusées, y compris celles des acheteurs qui n’ont pas reçu explicitement l’accès à cette vue de catalogue et les scripts qui analysent l’API.

Les clés d’accès restreint sont configurées de l’une des deux façons suivantes :

- [!BADGE ]{type=Caution tooltip="Nécessite l’extension B2B du connecteur Adobe Commerce Optimizer, qui est actuellement en version bêta privée."} **Automatiquement, pour les catalogues partagés B2B**—Pour les déploiements intégrés avec le [!DNL Adobe Commerce Optimizer Connector for B2B], le connecteur met en place et attribue la clé initiale. Ensuite, vous gérez les clés et l’affectation des clés à partir de l’administrateur Commerce. Voir [Authentification des vues de catalogue](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/shared-catalogs/catalog-views-manage) dans le *Guide d’administration de Commerce**.

- **Manuellement, pour toute vue de catalogue**—Pour protéger vous-même une vue de catalogue, par exemple pour un portail partenaire ou un aperçu de version préliminaire—suivez les étapes de cette rubrique en commençant par [Créer une clé d’accès restreinte](#create-a-restricted-access-key).

## Cas d’utilisation de clés d’accès limité

En [!DNL Adobe Commerce Optimizer], **[!UICONTROL Price Book ID]** détermine les prix affichés par une requête ; il détermine la tarification et non qui peut effectuer la requête. Tout client qui connaît l’ID et l’ID de catalogue d’une vue peut récupérer ces données via l’API de marchandisage. Les clés d’accès restreint ajoutent un contrôle distinct et complémentaire : elles définissent la portée des personnes pouvant accéder à une vue de catalogue, indépendamment du catalogue des prix en vigueur.

Les clés d’accès restreint sont généralement utilisées pour :

- **Tarification B2B basée sur un contrat** : limitez une vue de catalogue liée à un catalogue de prix négocié afin que seul l&#39;acheteur auquel il s&#39;applique puisse l&#39;interroger. Les autres organisations d&#39;achat et le public ne peuvent pas le faire. Pour les catalogues partagés B2B, cette configuration est automatique. Voir [ Gestion des clés et rotation ](#key-management-and-rotation).
- **Portail des partenaires et revendeurs** : limitez un sous-ensemble du catalogue aux partenaires approuvés qui s’intègrent directement à l’API de marchandisage.
- **Prévisualisations de version préliminaire** : laissez un système interne ou partenaire de confiance prévisualiser les produits à venir avant qu’ils ne soient visibles publiquement.

## Fonctionnement des clés d’accès restreintes

Une clé d’accès restreint est le composant public d’une paire de clés RSA. Votre application cliente génère et utilise cette clé pour prouver qu’elle est autorisée à lire une vue de catalogue privée. Dans ce contexte, _application cliente_ fait référence au système principal qui authentifie les acheteurs, par exemple la logique personnalisée sur [!DNL Adobe Commerce] ou un serveur principal tiers, et jamais le serveur frontal storefront lui-même.

Les étapes suivantes décrivent comment une paire de clés et un jeton signé passent de la création à la validation pour les vues de catalogue qui ne font pas partie d’un catalogue partagé B2B.

1. Votre application cliente génère une paire de clés RSA et conserve la clé privée.
1. Vous enregistrez la clé **publique** dans [!DNL Commerce Optimizer] en tant que clé d’accès restreint.
1. Votre application cliente signe un jeton Web JSON (JWT) avec la clé privée et l’inclut à chaque demande vers une vue de catalogue privée.
1. [!DNL Commerce Optimizer] valide la signature du jeton par rapport à la clé publique enregistrée et, si elle est valide, renvoie les données de catalogue demandées.

## Créer une clé d’accès restreinte

>[!NOTE]
>
>Cette section et les trois qui suivent décrivent le flux manuel [!DNL Adobe Commerce Optimizer] Studio. Si vous utilisez des catalogues partagés B2B avec le [!DNL Adobe Commerce Optimizer Connector B2B extension], gérez les clés à partir de l’administrateur Commerce. Voir [Clés d’accès restreintes](../../aco-connector/restricted-access-keys.md) dans la documentation du _connecteur Adobe Commerce Optimizer_.

Pour les tests initiaux des vues de catalogue privé, générez une paire de clés à l’aide d’un outil tel que [!DNL OpenSSL]. Gardez la clé privée secrète. Seule la clé publique est chargée dans [!DNL Commerce Optimizer].

```bash
openssl genrsa -out private-key.pem 2048
openssl rsa -in private-key.pem -pubout -out public-key.pem
```

La taille de la clé doit être comprise entre 2 048 et 8 192 bits. `public-key.pem` contient la valeur que vous collez dans le champ **[!UICONTROL Public key]** ci-dessous.

## Ajouter une clé d’accès restreint à [!DNL Commerce Optimizer]

1. Dans le menu de gauche de [!DNL Adobe Commerce Optimizer Studio], accédez à **[!UICONTROL Store setup]**, puis cliquez sur **[!UICONTROL Restricted access keys]**.

   ![Liste Clés d&#39;accès limité, avec le bouton Ajouter une clé d&#39;accès limité](../assets/restricted-access-keys.png){width="70%" zoomable="yes"}

1. Cliquez sur **[!UICONTROL Add Restricted Access Key]**.

1. Saisissez les détails clés :

   ![Ajoutez le formulaire de clé d’accès restreint, avec les champs Titre, Date d’expiration et Clé publique ](../assets/restricted-access-keys-add.png){width="70%" zoomable="yes"}

   - **[!UICONTROL Title]** : libellé permettant d&#39;identifier la clé, affiché dans la liste des clés et dans le sélecteur de clé de la vue du catalogue, par exemple `ACME Corp wholesale portal — Tier 1 pricing`.
   - **[!UICONTROL Expiration date]** : date et heure (UTC) au-delà desquelles la clé cesse d’être honorée, même pour un jeton qui n’a pas encore expiré.
   - **[!UICONTROL Public key]** : clé publique RSA codée en PEM au format SPKI (Subject Public Key Info), y compris les marqueurs `-----BEGIN PUBLIC KEY-----` et `-----END PUBLIC KEY-----`. Doit être unique dans l’environnement.

1. Cliquez sur **[!UICONTROL Save]**.

Les clés sont immuables après leur création. Pour modifier n’importe quelle valeur, supprimez la clé et créez-en une. Voir [ Rotation d’une clé ](#rotate-a-key) pour ce faire sans interruption de l’accès.

## Attribution d’une clé à une vue de catalogue

Une clé d’accès restreint n’authentifie l’accès qu’après son affectation à une vue de catalogue avec **[!UICONTROL Catalog Protection]** activé. Voir [Protection d’une vue de catalogue](private-catalog-view.md#protect-a-catalog-view) pour connaître les étapes de configuration.

## Supprimer une clé

1. Sur la page **[!UICONTROL Restricted access keys]**, recherchez la clé à supprimer, puis cliquez sur **[!UICONTROL Delete]**.

   Si la clé est affectée à une ou plusieurs vues de catalogue, un avertissement explique que les applications clientes qui reposent sur cette clé perdent l’accès. Les vues de catalogue elles-mêmes restent protégées et ne deviennent pas accessibles au public.

1. Confirmez la suppression.

## Gestion des clés et rotation

Les clés d’accès restreint sont gérées de l’une des deux façons suivantes, selon la manière dont vous utilisez la protection du catalogue :

- **Automatiquement, pour les catalogues partagés B2B**—[!BADGE Private Beta]{type=Caution tooltip="Nécessite l’extension B2B du connecteur Adobe Commerce Optimizer, qui est actuellement en version bêta privée."} Pour les déploiements intégrés avec le [!DNL Adobe Commerce Optimizer Connector for B2B], le service génère et attribue automatiquement la première clé d’accès restreint lors de la création d’une vue de catalogue. Chaque vue de catalogue obtient sa propre clé. Ensuite, vous pouvez gérer chaque clé à partir des pages Catalogue partagé ou Compte d’entreprise . Vous pouvez également afficher et gérer les clés à partir de la page Commerce Admin **Clés d’accès restreint** (**Système** > **Transfert de données**). Voir [Gérer la configuration de la vue du catalogue](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/shared-catalogs/catalog-views-manage).

  Chaque combinaison d’un catalogue partagé et d’une vue de magasin à laquelle elle est affectée est projetée en tant que vue de catalogue distincte. Une projection correspond à la vue de catalogue, à la politique, à la référence du catalogue et aux données de configuration de clé d’accès restreint que le connecteur exporte vers [!DNL Adobe Commerce Optimizer] pour cette combinaison. Ainsi, un catalogue partagé affecté à plusieurs vues de magasin produit plusieurs vues de catalogue, chacune avec sa propre clé. Modifier ou faire pivoter une clé pour une vue de catalogue sans affecter les autres.

  Les clés ont par défaut une longue période d’expiration. Si vous devez faire pivoter une clé, ajoutez le remplacement dans le fichier Admin et conservez les deux actifs jusqu’à ce que vous supprimiez l’ancienne. Voir [Modifications du catalogue partagé B2B](/help/aco-connector/get-started.md#monitor-b2b-shared-catalog-changes).

- **Manuellement, pour toute vue de catalogue** : pour les vues de catalogue qui ne sont pas associées à un catalogue partagé B2B dans le serveur principal Adobe Commerce, la génération de clés, la signature de jeton et la rotation sont entièrement gérées par l’application cliente du serveur principal qui authentifie les acheteurs. [!DNL Adobe Commerce Optimizer] ne génère ni ne fait pivoter ces clés en votre nom. Suivez les étapes décrites plus haut dans cette rubrique pour créer, ajouter et supprimer des clés. Pour faire pivoter une touche, voir [Faire pivoter une touche](#rotate-a-key).

### Rotation d’une touche

Pour faire pivoter une clé sans interruption d’accès, notez qu’une vue de catalogue peut être associée à trois clés à la fois :

1. Générez une nouvelle paire de clés et ajoutez la nouvelle clé publique en tant que nouvelle clé d’accès restreint.
1. Attribuez la nouvelle clé à la vue catalogue avec la clé existante.
1. Commencez à signer de nouveaux jetons avec la nouvelle clé privée pour terminer la substitution de clé.
1. Une fois que toutes les applications clientes sont confirmées sur la nouvelle clé, supprimez l’ancienne clé.

## Limites

Voir [Vues du catalogue et limites des politiques](../boundaries-limits.md#catalog-views-and-policies).

## Plus comme ceci

- [Vues de catalogue privé](private-catalog-view.md) : découvrez comment protéger une vue de catalogue avec des clés d’accès restreintes.
- [Modifications du catalogue partagé B2B ](/help/aco-connector/get-started.md#monitor-b2b-shared-catalog-changes)—Découvrez comment le [!DNL Adobe Commerce Optimizer Connector] automatise la gestion des clés pour les catalogues partagés B2B.

