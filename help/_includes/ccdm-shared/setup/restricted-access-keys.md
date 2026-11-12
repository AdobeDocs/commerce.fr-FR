---
source-git-commit: b6b737220a6dadf55b03da54e8d74226ed578cd0
workflow-type: tm+mt
source-wordcount: '1639'
ht-degree: 0%
---
# Clés d’accès restreintes

Les clés d’accès restreint permettent aux applications clientes autorisées d’accéder à une [vue de catalogue privée](private-catalog-view.md). Seules les requêtes portant un jeton signé valide à partir d’une clé attribuée peuvent récupérer les données du catalogue. Toutes les autres requêtes sont refusées, y compris celles des acheteurs qui n’ont pas d’accès explicite à cette vue de catalogue et aux scripts qui analysent l’API des services de marchandisage Adobe Commerce.

Les clés d’accès restreint sont configurées de l’une des deux façons suivantes :

- **Automatiquement, pour les catalogues partagés B2B** : le système met en service et affecte la clé initiale pour les vues de catalogue associées à un catalogue partagé B2B. Ensuite, vous gérez les clés et l’affectation des clés à partir de l’administrateur Commerce. Voir [Authentification des vues de catalogue](https://experienceleague.adobe.com/fr/docs/commerce-admin/b2b/shared-catalogs/catalog-views-manage) dans le *Guide d’administration de Commerce*. L’approvisionnement automatique est disponible dans les déploiements suivants :

  - **Adobe Commerce as a Cloud Service avec CCDM** pour Adobe Commerce B2B.
  - **Adobe Commerce sur le cloud ou sur site** intégré à Adobe Commerce Optimizer via [!DNL Adobe Commerce Optimizer Connector for B2B]. L’extension B2B du connecteur est requise.

- **Manuellement, pour toute vue de catalogue**—Pour protéger vous-même une vue de catalogue, par exemple pour un portail partenaire ou un aperçu de version préliminaire, suivez les étapes de cette rubrique en commençant par [Créer une clé d&#39;accès restreinte](#create-a-restricted-access-key).

## Cas d’utilisation de clés d’accès limité

**[!UICONTROL Price Book ID]** détermine les prix affichés par une demande ; il détermine la tarification, et non qui peut effectuer la demande. Tout client qui connaît l’ID et l’ID de catalogue d’une vue peut récupérer ces données via l’API des services de marchandisage. Les clés d’accès restreint ajoutent un contrôle distinct et complémentaire : elles définissent la portée des personnes pouvant accéder à une vue de catalogue, indépendamment du catalogue des prix en vigueur.

Les clés d’accès restreint sont généralement utilisées pour :

- **Tarification B2B basée sur un contrat** : restreignez une vue de catalogue liée à un catalogue de prix négocié afin que seul l&#39;acheteur auquel il s&#39;applique puisse l&#39;interroger. Les autres organisations d&#39;achat et le public ne peuvent pas le faire. Pour les catalogues partagés B2B, cette configuration est automatique. Voir [Gestion des clés et rotation](#key-management-and-rotation).
- **Portail des partenaires et revendeurs** : limitez un sous-ensemble du catalogue aux partenaires approuvés qui s’intègrent directement à l’API des services de marchandisage.
- **Prévisualisations de version préliminaire** : laissez un système interne ou partenaire de confiance prévisualiser les produits à venir avant qu’ils ne soient visibles publiquement.

## Fonctionnement des clés d’accès restreintes

Une clé d’accès restreint est le composant public d’une paire de clés RSA. Votre application cliente génère et utilise cette clé pour prouver qu’elle est autorisée à lire une vue de catalogue privée. Dans ce contexte, l’_application cliente_ fait référence au système principal qui authentifie les acheteurs, par exemple la logique personnalisée sur [!DNL Adobe Commerce] ou un serveur principal tiers, et jamais le storefront lui-même.

Les étapes suivantes décrivent comment une paire de clés et un jeton signé passent de la création à la validation pour les vues de catalogue qui ne font pas partie d’un catalogue partagé B2B.

1. Votre application cliente génère une paire de clés RSA et conserve la clé privée.
1. Vous enregistrez la clé **publique** dans le système en tant que clé d&#39;accès restreint.
1. Votre application cliente signe un jeton Web JSON (JWT) avec la clé privée et l’inclut à chaque demande vers une vue de catalogue privée.

   Le système valide la signature du jeton par rapport à la clé publique enregistrée et, si elle est valide, renvoie les données de catalogue demandées.

## Accéder à l’espace de travail de clé d’accès restreint

La façon dont vous ouvrez l’espace de travail des clés d’accès restreint dépend du produit que vous utilisez :

- **Administrateur Adobe Commerce** (Adobe Commerce as a Cloud Service) : Sélectionnez *Système* > *Transfert De Données* > **Clés D’Accès Restreint**.
- **Adobe Commerce Optimizer Studio** : sélectionnez *Configuration du magasin* > **Clés d’accès restreintes**.

## Créer une clé d’accès restreinte

>[!NOTE]
>
>Cette section et les deux qui suivent décrivent le processus manuel de gestion des clés d’accès restreint. Pour les catalogues partagés B2B avec approvisionnement automatique des clés, gérez les clés à partir de l’administrateur Commerce. Voir [Clés D&#39;Accès Restreint](https://experienceleague.adobe.com/fr/docs/commerce-admin/systems/data-transfer/data-sync/catalog-view-sync/restricted-access-keys).

### Ajout d’une clé d’accès restreint

Sélectionnez l’onglet correspondant à l’outil que vous utilisez pour gérer les clés : Commerce Admin ou Adobe Commerce Optimizer Studio.

>[!BEGINTABS]

>[!TAB Administrateur Adobe Commerce]

Les clients qui utilisent Adobe Commerce as a Cloud Service avec CCDM, ou Adobe Commerce Optimizer connecté à Adobe Commerce par le biais du connecteur, peuvent générer des paires de clés RSA à partir de l’administrateur Commerce. Voir [Gérer les clés d&#39;accès restreint](https://experienceleague.adobe.com/fr/docs/commerce-admin/systems/data-transfer/data-sync/catalog-view-sync/restricted-access-keys).

>[!TAB Adobe Commerce Optimizer Studio - gestion manuelle des clés]

Les clients qui utilisent Adobe Commerce Optimizer Studio doivent générer et gérer leurs propres paires de clés RSA, puis ajouter la clé publique au système. Il s’agit du workflow requis pour Adobe Commerce Optimizer avec un serveur principal tiers. Les clients qui utilisent le connecteur peuvent également utiliser ce workflow à la place de l’administrateur Commerce.

**Générer une paire de clés RSA**

Pour les tests initiaux des vues de catalogue privé, générez une paire de clés à l’aide d’un outil tel que [!DNL OpenSSL]. Gardez la clé privée secrète. Seule la clé publique est téléchargée sur le système en tant que clé d’accès restreint.

```bash
openssl genrsa -out private-key.pem 2048
openssl rsa -in private-key.pem -pubout -out public-key.pem
```

La taille de la clé doit être comprise entre 2 048 et 8 192 bits. `public-key.pem` contient la valeur que vous collez dans le champ **[!UICONTROL Public key]** ci-dessous.

**Ajouter la clé publique au système**

1. Dans l&#39;espace de travail Clé d&#39;accès restreint, cliquez sur **[!UICONTROL Add Restricted Access Key]**.

   ![Liste Clés d&#39;accès restreint, avec le bouton Ajouter une clé d&#39;accès restreint](/help/assets/ccdm-shared/setup/restricted-access-keys.png){width="70%" zoomable="yes"}

1. Saisissez les détails clés :

   ![Ajoutez le formulaire de clé d&#39;accès restreint, avec le titre, la date d&#39;expiration et les champs de clé publique](/help/assets/ccdm-shared/setup/restricted-access-keys-add.png){width="70%" zoomable="yes"}

   - **[!UICONTROL Title]** : libellé permettant d’identifier la clé, affiché dans la liste des clés et dans le sélecteur de clé de la vue de catalogue, par exemple `ACME Corp wholesale portal — Tier 1 pricing`.
   - **[!UICONTROL Expiration date]** - Date et heure (UTC) au-delà desquelles la clé cesse d’être honorée, même pour un jeton qui n’a pas encore expiré.
   - **[!UICONTROL Public key]** : clé publique RSA codée en PEM au format SPKI (Subject Public Key Info), y compris les marqueurs `-----BEGIN PUBLIC KEY-----` et `-----END PUBLIC KEY-----`. Doit être unique dans l’environnement.

1. Cliquez sur **[!UICONTROL Save]**.

>[!ENDTABS]

Les clés sont immuables après leur création. Pour modifier n’importe quelle valeur, supprimez la clé et créez-en une. Voir [Rotation d&#39;une clé](#rotate-a-key) pour ce faire sans interruption d&#39;accès.

## Attribution d’une clé à une vue de catalogue

Une clé d’accès restreint authentifie l’accès uniquement après son affectation à une vue de catalogue avec **[!UICONTROL Catalog Protection]** activé. Voir [Protéger une vue de catalogue](private-catalog-view.md#protect-a-catalog-view) pour les étapes de configuration.

## Supprimer une clé

1. Dans l’espace de travail **[!UICONTROL Restricted access keys]**, recherchez la clé que vous souhaitez supprimer et supprimez-la.

   Si la clé est affectée à une ou plusieurs vues de catalogue, un avertissement explique que les applications clientes qui reposent sur cette clé perdent l’accès. Les vues de catalogue elles-mêmes restent protégées et ne deviennent pas accessibles au public.

1. Confirmez la suppression.

## Gestion des clés et rotation

Les clés d’accès restreint sont gérées de l’une des deux façons suivantes, selon la manière dont vous utilisez la protection du catalogue :

- **Automatiquement, pour les catalogues partagés B2B** : pour les déploiements B2B d’Adobe Commerce utilisant les services de marchandisage avec CCDM, et pour les déploiements de Adobe Commerce Optimizer intégrés via [!DNL Adobe Commerce Optimizer Connector for B2B] (qui nécessite l’extension B2B), le service génère et attribue automatiquement la première clé d’accès restreint lors de la création d’une vue de catalogue. Chaque vue de catalogue obtient sa propre clé. Ensuite, vous pouvez gérer chaque clé à partir des pages Catalogue partagé ou Compte d’entreprise . Vous pouvez également afficher et gérer les clés de la page **Clés d’accès restreint** de l’administrateur Commerce (**Système** > **Transfert de données**). Voir [Gérer la configuration de la vue du catalogue](https://experienceleague.adobe.com/fr/docs/commerce-admin/b2b/shared-catalogs/catalog-views-manage).

  Chaque combinaison d’un catalogue partagé et d’une vue de magasin est projetée en tant que vue de catalogue distincte. Une projection correspond à la vue de catalogue, à la politique, à la référence du catalogue et aux données de configuration des clés d’accès restreint qui sont exportées vers la couche de données des services de marchandisage pour cette combinaison. Ainsi, un catalogue partagé affecté à plusieurs vues de magasin produit plusieurs vues de catalogue, chacune avec sa propre clé. Modifier ou faire pivoter une clé pour une vue de catalogue sans affecter les autres.

  Les clés ont par défaut une longue période d’expiration. Si vous devez faire pivoter une clé, ajoutez le remplacement dans le fichier Admin et conservez les deux actifs jusqu’à ce que vous supprimiez l’ancienne.

- **Manuellement, pour toute vue de catalogue** : la manière dont vous générez et gérez les clés dépend de votre contexte de produit. Dans les deux cas, le client principal qui authentifie les acheteurs signe les jetons.

  - **Administrateur Commerce (Adobe Commerce as a Cloud Service avec CCDM ou Adobe Commerce Optimizer avec le connecteur)**—Générez des paires de clés RSA dans l&#39;administrateur Commerce, puis créez, attribuez et supprimez des clés sur la page **Clés d&#39;accès restreint**. Adobe Commerce ne fait pas pivoter les clés automatiquement. Pour faire pivoter une clé, voir [Faire pivoter une clé](#rotate-a-key).
  - **Adobe Commerce Optimizer Studio**—Studio ne génère pas de clés. Il s’agit du workflow obligatoire pour Adobe Commerce Optimizer avec un serveur principal tiers, que les clients du connecteur peuvent également utiliser. Utilisez votre application cliente pour générer la paire de clés RSA, conserver la clé privée et ajouter la clé publique en tant que clé d’accès restreint. Suivez les étapes décrites plus haut dans cette rubrique pour créer, ajouter et supprimer des clés. Pour faire pivoter une clé, voir [Faire pivoter une clé](#rotate-a-key).

### Rotation d’une touche

Pour faire pivoter une clé sans interruption d’accès, notez qu’une vue de catalogue peut être associée à trois clés à la fois :

Sélectionnez l’onglet correspondant à l’outil que vous utilisez pour gérer les clés : Commerce Admin ou Adobe Commerce Optimizer Studio.

>[!BEGINTABS]

>[!TAB Administrateur Adobe Commerce]

Voir [Sélection et rotation des clés](https://experienceleague.adobe.com/fr/docs/commerce-admin/systems/data-transfer/data-sync/catalog-view-sync/restricted-access-keys#key-selection-and-rotation). Cela s’applique à Adobe Commerce as a Cloud Service avec CCDM et aux projets Adobe Commerce intégrés à Adobe Commerce Optimizer par le biais du connecteur Adobe Commerce Optimizer.

>[!TAB Adobe Commerce Optimizer Studio (gestion manuelle des clés)]

Cette procédure est requise pour Adobe Commerce Optimizer avec un serveur principal tiers. Les clients qui utilisent le connecteur peuvent également l’utiliser à la place de l’administrateur Commerce.

1. Générez une nouvelle paire de clés et ajoutez la nouvelle clé publique en tant que nouvelle clé d’accès restreint.
1. Attribuez la nouvelle clé à la vue catalogue avec la clé existante.
1. Commencez à signer de nouveaux jetons avec la nouvelle clé privée pour terminer la substitution de clé.
1. Une fois que toutes les applications clientes sont confirmées sur la nouvelle clé, supprimez l’ancienne clé.

>[!ENDTABS]

## Limites

Voir [Vues de catalogue et limites de politique](https://experienceleague.adobe.com/fr/docs/commerce/optimizer/boundaries-limits).

## Plus comme ceci

- [Vues de catalogue privé](private-catalog-view.md) : découvrez comment protéger une vue de catalogue avec des clés d’accès restreintes.
