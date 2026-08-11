---
title: Clés d’accès restreintes
description: Découvrez comment créer, affecter et faire pivoter des clés d’accès restreintes pour protéger les vues de catalogue dans  [!DNL Adobe Commerce Optimizer]  avec l’authentification par jeton signé.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et  [!DNL Adobe Commerce Optimizer]  (infrastructure SaaS gérée par Adobe)."
TQID: https://experienceleague.adobe.com/Jmze0Pq3kSNMIXqkkML-hmmlZnv-XKgeEgRB8Q8NZ6s
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
nudge: true
source-git-commit: 688bc6e28a4c5a94b1fe55c84f7c05401dd651bc
workflow-type: tm+mt
source-wordcount: 791
ht-degree: 0%

---

# Clés d’accès restreintes

Les clés d’accès restreint permettent aux applications clientes autorisées d’accéder à une [vue de catalogue privée](catalog-view.md) ; seules les requêtes portant un jeton signé valide à partir d’une clé attribuée peuvent récupérer les données du catalogue. Toutes les autres requêtes sont refusées, y compris celles des acheteurs anonymes, des acheteurs qui n’ont pas explicitement eu accès à cette vue de catalogue et des scripts qui analysent l’API.

## Cas d’utilisation de clés d’accès limité

En [!DNL Adobe Commerce Optimizer], **[!UICONTROL Price Book ID]** détermine les prix affichés par une requête ; il détermine la tarification et non qui peut effectuer la requête. Tout client qui connaît l’ID et l’ID de catalogue d’une vue peut récupérer ces données via l’API de marchandisage. Les clés d’accès restreint ajoutent un contrôle distinct et complémentaire : elles définissent la portée des personnes pouvant accéder à une vue de catalogue, indépendamment du catalogue des prix en vigueur.

Les clés d’accès restreint sont généralement utilisées pour :

- **Tarification B2B basée sur un contrat** : limitez une vue de catalogue liée à un catalogue de prix négocié afin que seul l&#39;acheteur auquel il s&#39;applique puisse l&#39;interroger. Les autres organisations d&#39;achat et le public ne peuvent pas le faire.
- **Portail des partenaires et revendeurs** : limitez un sous-ensemble du catalogue aux partenaires approuvés qui s’intègrent directement à l’API de marchandisage.
- **Prévisualisations de version préliminaire** : laissez un système interne ou partenaire de confiance prévisualiser les produits à venir avant qu’ils ne soient visibles publiquement.

>[!IMPORTANT]
>
>La génération de clés, la signature de jeton et la rotation sont actuellement gérées entièrement par l’application cliente principale qui authentifie les acheteurs. [!DNL Adobe Commerce Optimizer] ne génère ni ne fait pivoter ces clés en votre nom.

## Fonctionnement des clés d’accès restreintes

Une clé d’accès restreint est le composant public d’une paire de clés RSA. Votre application cliente génère et utilise cette clé pour prouver qu’elle est autorisée à lire une vue de catalogue privée. Dans ce contexte, « application cliente » désigne le système principal qui authentifie les acheteurs, par exemple la logique personnalisée sur [!DNL Adobe Commerce] ou un serveur principal tiers, et jamais le storefront lui-même.

Les étapes suivantes décrivent comment une paire de clés et un jeton signé passent de la création à la validation :

1. Votre application cliente génère une paire de clés RSA et conserve la clé privée.
1. Vous enregistrez la clé **publique** dans [!DNL Commerce Optimizer] en tant que clé d’accès restreint.
1. Votre application cliente signe un jeton Web JSON (JWT) avec la clé privée et l’inclut à chaque demande vers une vue de catalogue privée.
1. [!DNL Commerce Optimizer] valide la signature du jeton par rapport à la clé publique enregistrée et, si elle est valide, renvoie les données de catalogue demandées.

## Créer une clé d’accès restreinte

Pour les tests initiaux des vues de catalogue privé, générez une paire de clés à l’aide d’un outil tel que [!DNL OpenSSL]. Gardez la clé privée secrète : seule la clé publique est téléchargée sur [!DNL Commerce Optimizer].

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

   ![Ajoutez le formulaire de clé d’accès restreint, avec les champs Titre, Date d’expiration et Clé publique &#x200B;](../assets/restricted-access-keys-add.png){width="70%" zoomable="yes"}

   - **[!UICONTROL Title]** : libellé permettant d&#39;identifier la clé, affiché dans la liste des clés et dans le sélecteur de clé de la vue du catalogue, par exemple `ACME Corp wholesale portal — Tier 1 pricing`.
   - **[!UICONTROL Expiration date]** : date et heure (UTC) au-delà desquelles la clé cesse d’être honorée, même pour un jeton qui n’a pas encore expiré.
   - **[!UICONTROL Public key]** : clé publique RSA codée en PEM au format SPKI (Subject Public Key Info), y compris les marqueurs `-----BEGIN PUBLIC KEY-----` et `-----END PUBLIC KEY-----`. Doit être unique dans l’environnement.

1. Cliquez sur **[!UICONTROL Save]**.

Les clés sont immuables après leur création. Pour modifier n’importe quelle valeur, supprimez la clé et créez-en une. Voir [&#x200B; Rotation d’une clé &#x200B;](#rotate-a-key) pour ce faire sans interruption de l’accès.

## Attribution d’une clé à une vue de catalogue

Une clé d’accès restreint ne restreint l’accès qu’après son affectation à une vue de catalogue avec **[!UICONTROL Catalog Protection]** activé. Voir [Protection d’une vue de catalogue](private-catalog-view.md#protect-a-catalog-view) pour connaître les étapes de configuration.

## Supprimer une clé

1. Sur la page **[!UICONTROL Restricted access keys]**, recherchez la clé à supprimer, puis cliquez sur **[!UICONTROL Delete]**.

   Si la clé est affectée à une ou plusieurs vues de catalogue, un avertissement explique que les applications clientes qui reposent sur cette clé perdent l’accès. Les vues de catalogue elles-mêmes restent protégées et ne deviennent pas accessibles au public.

1. Confirmez la suppression.

## Rotation d’une touche

Pour faire pivoter une clé sans interruption d’accès, notez qu’une vue de catalogue peut être associée à trois clés à la fois :

1. Générez une nouvelle paire de clés et ajoutez la nouvelle clé publique en tant que nouvelle clé d’accès restreint.
1. Attribuez la nouvelle clé à la vue catalogue avec la clé existante.
1. Commencez à signer de nouveaux jetons avec la nouvelle clé privée pour terminer la substitution de clé.
1. Une fois que toutes les applications clientes sont confirmées sur la nouvelle clé, supprimez l’ancienne clé.

## Limites

Voir [Vues du catalogue et limites des politiques](../boundaries-limits.md#catalog-views-and-policies).

## Plus comme ceci

- [Vues de catalogue privé](private-catalog-view.md) : découvrez comment protéger une vue de catalogue avec des clés d’accès restreintes.

