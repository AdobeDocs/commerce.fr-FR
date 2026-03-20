---
title: Points d’entrée REST du compte de carte cadeau
description: Découvrez comment utiliser les API REST de compte de carte cadeau pour créer, mettre à jour, supprimer et interroger des comptes de carte cadeau par programmation dans [!DNL Adobe Commerce as a Cloud Service].
role: Admin, Developer
level: Experienced
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
source-git-commit: 160180d9d779514f6faee3c7de46531ebf191c7d
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 0%

---

# API du compte de carte cadeau

{{accs-sandbox-experimental}}

Les points d’entrée REST de compte de carte cadeau offrent une gestion programmée des comptes de carte cadeau au niveau du compte, et non au niveau du panier ou du devis. Utilisez cette API pour créer, récupérer, mettre à jour et supprimer des comptes de carte cadeau ou pour configurer des comptes de carte cadeau en bloc via le point d’entrée d’importation JSON.

Ces points d’entrée sont conçus pour :

* Administrateurs gérant les programmes de cartes-cadeaux
* Intégrations tierces fournissant des cartes-cadeaux à partir de systèmes externes, tels que ERP, CRM et plateformes marketing
* Workflows automatisés pour la création de cartes-cadeaux en bloc

## Authentification

Tous les points d’entrée nécessitent un jeton de support d’intégration ou d’administration. Le jeton doit être associé à un rôle qui inclut la ressource Liste de contrôle d’accès (ACL) `Magento_GiftCardAccount::giftcardaccount`.

Pour les opérations d’importation en bloc, le rôle doit également inclure la ressource ACL `Magento_ImportExport::import_api`.

## Site Web et contexte de magasin

Les valeurs d’affichage du site web et du magasin sont résolues à partir des en-têtes de requête HTTP, et non du corps de la requête. Transmettez l’un des en-têtes suivants à chaque requête :

* `Store: <store_view_code>`
* `Magento-Website-Code: <website_code>`

L’API résout automatiquement le site web à partir de ces en-têtes. N’incluez pas `website_id` dans la payload de requête REST.

>[!NOTE]
>
>Le point d’entrée d’importation en bloc est une exception. Comme l’importation fonctionne en bloc et peut cibler des sites web spécifiques, chaque ligne du payload d’importation nécessite une valeur de `website_id` explicite.

## Référence de l’API REST

L’API expose les opérations suivantes sous `/V1/giftcardaccounts`, toutes sécurisées par la ressource ACL `Magento_GiftCardAccount::giftcardaccount` :

| Méthode | URL | Description |
|--------|-----|-------------|
| POSTER | `/rest/V1/giftcardaccounts` | Créer un compte de carte cadeau |
| GET | `/rest/V1/giftcardaccounts` | Liste des comptes (prend en charge searchCriteria) |
| GET | `/rest/V1/giftcardaccounts/:id` | Obtenir le compte par ID |
| GET | `/rest/V1/giftcardaccounts/code/:code` | Obtenir le compte par code |
| PUT | `/rest/V1/giftcardaccounts/:id` | Mettre à jour le compte (sémantique de fusion) |
| DELETE | `/rest/V1/giftcardaccounts/:id` | Supprimer le compte |

### Référence du champ

| Champ | Type | Valeurs valides | Création REST | Importer |
|---|---|---|---|---|
| `code` | chaîne | 255 caractères maximum | Obligatoire | Obligatoire |
| `balance` | flotteur | >= 0 | Obligatoire | Obligatoire |
| `status` | int | `0` (désactivé), `1` (activé) | Facultatif, la valeur par défaut est `1` | Facultatif, la valeur par défaut est `1` |
| `state` | int | `0` (disponible), `1` (utilisé), `2` (utilisé), `3` (expiré) | Facultatif, la valeur par défaut est `0` | Facultatif, la valeur par défaut est `0` |
| `is_redeemable` | int | `0` ou `1` | Facultatif, la valeur par défaut est `1` | Facultatif, la valeur par défaut est `1` |
| `date_expires` | chaîne | `YYYY-MM-DD` ou nul | Facultatif | Facultatif |
| `date_created` | chaîne | `YYYY-MM-DD` | Auto-set | Facultatif, définition automatique si omis |
| `website_id` | int | Identifiant de site web valide | Non accepté (résolution automatique à partir des en-têtes) | Obligatoire |

### Créer un compte de carte cadeau

Crée un compte de carte cadeau avec détection de code dupliqué.

| Poste | Valeur |
|---|---|
| **Méthode** | `POST` |
| **URL** | `/V1/giftcardaccounts` |

**Corps de la requête :**

```json
{
  "giftcardAccount": {
    "code": "GIFT-1234-ABCD",
    "balance": 100.00,
    "status": 1,
    "state": 0,
    "is_redeemable": 1,
    "date_expires": "2027-12-31"
  }
}
```

**Réponse (200) :**

```json
{
  "account_id": 42,
  "code": "GIFT-1234-ABCD",
  "balance": 100,
  "status": 1,
  "state": 0,
  "is_redeemable": 1,
  "date_expires": "2027-12-31",
  "date_created": "2026-03-12"
}
```

### Récupérer un compte de carte cadeau par ID

| Poste | Valeur |
|---|---|
| **Méthode** | `GET` |
| **URL** | `/V1/giftcardaccounts/:id` |

**Réponse (200) :**

Renvoie un seul objet de compte de carte cadeau.

### Récupérer un compte de carte cadeau par code

| Poste | Valeur |
|---|---|
| **Méthode** | `GET` |
| **URL** | `/V1/giftcardaccounts/code/:code` |

>[!IMPORTANT]
>
>Si un code de carte cadeau est purement numérique (par exemple, `12345`), une demande de `/V1/giftcardaccounts/12345` correspond à l’itinéraire de l’ID, et non à l’itinéraire du code. Utilisez toujours `/V1/giftcardaccounts/code/12345` pour les recherches basées sur du code lorsque le code peut être numérique.

**Réponse (200) :**

Renvoie un seul objet de compte de carte cadeau.

### Liste des comptes de carte cadeau avec critères de recherche

| Poste | Valeur |
|---|---|
| **Méthode** | `GET` |
| **URL** | `/V1/giftcardaccounts` |

Transmettez des critères de recherche en tant que paramètres de requête. L’exemple suivant renvoie les comptes de carte cadeau où `status` est égal à `1` (activé) :

```text
GET /V1/giftcardaccounts?searchCriteria[filterGroups][0][filters][0][field]=status&searchCriteria[filterGroups][0][filters][0][value]=1&searchCriteria[pageSize]=10&searchCriteria[currentPage]=1
```

**Réponse (200) :**

```json
{
  "items": [
    {
      "account_id": 42,
      "code": "GIFT-1234-ABCD",
      "balance": 100,
      "status": 1,
      "state": 0,
      "is_redeemable": 1,
      "date_expires": "2027-12-31",
      "date_created": "2026-03-12"
    }
  ],
  "search_criteria": { ... },
  "total_count": 1
}
```

### Mettre à jour un compte de carte cadeau

Met à jour un compte de carte cadeau existant à l’aide de la sémantique de fusion. Seuls les champs non nuls de la requête sont appliqués. Le champ `code` est immuable. La transmission d’un autre code renvoie une erreur de validation.

| Poste | Valeur |
|---|---|
| **Méthode** | `PUT` |
| **URL** | `/V1/giftcardaccounts/:id` |

**Corps de la requête :**

```json
{
  "giftcardAccount": {
    "balance": 75.00,
    "status": 1
  }
}
```

**Réponse (200) :**

Renvoie l’objet de compte de carte cadeau mis à jour.

### Supprimer un compte de carte cadeau

| Poste | Valeur |
|---|---|
| **Méthode** | `DELETE` |
| **URL** | `/V1/giftcardaccounts/:id` |

**Réponse (200) :**

```json
true
```

## Importation en bloc via JSON

Les comptes de carte cadeau peuvent être approvisionnés en bloc à l’aide de `POST /V1/import/json` avec le type d’entité `giftcardaccount`. Ce point d’entrée nécessite la ressource de liste de contrôle d’accès (ACL) `Magento_ImportJsonApi::import_api` en plus de la liste de contrôle d’accès du compte de carte cadeau.

### Comportements pris en charge

| Comportement | Description |
|---|---|
| `append` | Crée de nouveaux comptes de carte cadeau. Si un code existe déjà, cette ligne échoue et l’importation se poursuit avec les lignes restantes. |
| `replace` | Met à jour et insère les comptes de carte cadeau par code. Crée le compte si le code n’existe pas et le remplace s’il existe. |
| `delete` | Supprime les comptes de carte cadeau par code. |

### Exemple de requête

```json
{
  "source": {
    "entity": "giftcardaccount",
    "behavior": "append",
    "validation_strategy": "validation-stop-on-errors",
    "allowed_error_count": "10",
    "items": [
      {
        "code": "BULK-001",
        "balance": 50.00,
        "website_id": 1,
        "status": 1,
        "state": 0,
        "is_redeemable": 1,
        "date_expires": "2027-06-30"
      },
      {
        "code": "BULK-002",
        "balance": 25.00,
        "website_id": 1
      }
    ]
  }
}
```

### Importer les détails du comportement

* Chaque ligne du payload d’importation nécessite une `website_id` explicite, contrairement aux points d’entrée REST qui déduisent le site web à partir des en-têtes de requête.
* Chaque ligne est validée indépendamment. Les lignes non valides génèrent des erreurs par ligne sans affecter les lignes valides du même lot.
* Les codes en double dans le même lot sont détectés et signalés comme des erreurs par ligne plutôt que de provoquer une restauration de transaction.
* L’importation écrit directement dans la base de données pour des raisons de performances et contourne le cycle de vie d’enregistrement du modèle fournisseur. Les entrées de l&#39;historique des modifications de solde ne sont pas créées pendant l&#39;importation.
* Les opérations de création REST rejettent les anciennes dates d’expiration. L’importation accepte les dates d’expiration antérieures par défaut, afin de prendre en charge la migration des données historiques.

## Gestion des erreurs

L’API renvoie des codes d’état HTTP standard :

| Code de statut | Condition |
|---|---|
| `400` | Erreur de validation. Champs obligatoires manquants, valeurs non valides ou date d’expiration passée lors de la création REST. |
| `401` | Jeton du porteur manquant ou non valide. |
| `403` | Le jeton ne dispose pas de la ressource ACL requise. |
| `404` | Compte de carte cadeau introuvable. |
| `409` | Code de carte cadeau en double. |

La validation d’entrée couvre les champs obligatoires, les plages de valeurs (l’état doit être `0` ou `1`, l’état doit être `0`-`3`, le solde doit être non négatif), le format de date et la sécurité de type. Les valeurs non numériques des champs numériques sont rejetées.
