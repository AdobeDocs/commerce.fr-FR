---
title: Connexion en tant que client avec des codes uniques
description: Découvrez comment utiliser la fonction Connexion en tant que client OTC pour générer des codes à usage unique pour l’authentification du client dans  [!DNL Adobe Commerce as a Cloud Service].
role: Admin
level: Intermediate
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
source-git-commit: 2de1006ad3cee936d114bcf1b9a98b43a54d8c76
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 0%

---

# Connexion en tant que client

{{accs-sandbox-experimental}}

La fonctionnalité Connexion en tant que client en vente libre (Code à usage unique) permet aux utilisateurs administrateurs de générer un code de courte durée à usage unique pour un client. Ce code peut être échangé contre un jeton d’accès client via GraphQL, ce qui permet d’activer les workflows sans mot de passe **Connexion en tant que client** pour les scénarios d’achat assistés par le vendeur.

La connexion en tant que client comprend les composants suivants :

* **Interface utilisateur d’administration** - Sur la page de modification du client, les administrateurs peuvent demander un code à usage unique (OTC) au lieu de se connecter directement en tant que client.
* **API REST** - Point d’entrée programmatique pour la génération OTC, utile pour les scripts d’administration et les intégrations tierces.
* **API GraphQL** - Mutations qui échangent un OTC contre un jeton d’accès client pour les flux commerciaux storefront ou headless.

## Générer un code unique à partir de l’administrateur

Le bouton Se connecter en tant que client OTC remplace le bouton standard se connecter en tant que client de la page de modification du client par un bouton [!UICONTROL **Obtenir la connexion du client OTC**]. Le code à usage unique généré peut ensuite être utilisé avec le storefront ou GraphQL pour les achats assistés par le vendeur.

>[!NOTE]
>
>Le bouton **Se connecter en tant que client** n’est pas disponible sur les pages Commande, Facture, Expédition et Avoir.

### Conditions préalables

Vous devez répondre aux exigences suivantes avant d’utiliser la fonction de connexion en tant que client :

* **Autorisation d’administrateur** - L’utilisateur administrateur doit disposer de l’autorisation Liste de contrôle d’accès (ACL) `Magento_LoginAsCustomer::login` activée dans son rôle d’administrateur pour se connecter en tant que client.

* **Consentement du client** - L’attribut d’extension `login_as_customer_assistance_allowed` doit être défini sur **2**. Elle peut être configurée sur la page **Modifier le client** dans l’administration ou via GraphQL lors de la création ou de la modification d’un client.

  ![Configuration de l’attribut de l’extension de consentement du client sur la page Modifier le client](./assets/customer-consent-attribute.png){width="600" zoomable="yes"}

* **Connexion en tant qu’extension client activée** - La fonctionnalité Connexion en tant que client n’est pas disponible lorsque l’extension Connexion en tant que client est désactivée. Pour vérifier que l’extension est activée, accédez à [!UICONTROL **Magasins**] > [!UICONTROL **Configuration**] > [!UICONTROL **Clients**] > [!UICONTROL **Se connecter en tant que client**] > [!UICONTROL **Activer l’extension**].

### Demander un code à usage unique (OTC)

1. Accédez à [!UICONTROL **Clients**] et sélectionnez un client pour ouvrir la page de modification.

1. Sur la page Modifier le client, cliquez sur [!UICONTROL **Obtenir la connexion du client OTC**].

   ![Bouton Obtenir la connexion du client OTC sur la page Modifier le client](./assets/get-customer-login-otc-button.png){width="600" zoomable="yes"}

1. Saisissez un [!UICONTROL **Motif**] (obligatoire) et cliquez sur [!UICONTROL **Demander**].

   ![Boîte de dialogue modale de demande OTC avec le champ Motif](./assets/otc-reason-modal.png){width="600" zoomable="yes"}

   >[!NOTE]
   >
   >Le champ **Motif** est obligatoire. Il est transmis au flux de génération OTP et est réservé à une utilisation dans les fonctionnalités d’audit et de journalisation des événements à venir.

1. Le document OTC généré s’affiche dans la boîte de dialogue modale. Utilisez ce code avec la mutation `generateCustomerToken` ou `exchangeOtpForCustomerToken` GraphQL pour l’autorisation du client.

   ![OTC généré affiché dans la fenêtre modale](./assets/otc-generated-code.png){width="300" zoomable="yes"}

>[!IMPORTANT]
>
>Le code à usage unique généré en vente libre est valide pendant 30 secondes par défaut et est invalidé après une seule utilisation. La TTL peut être configurée en envoyant un ticket d’assistance [support](https://experienceleague.adobe.com/home?lang=fr&support-tab=home#support).

Une fois le code unique généré, vous pouvez l’utiliser en accédant à votre storefront et en vous connectant à l’aide des informations d’identification suivantes :

* **E-mail** : adresse e-mail du client
* **Mot de passe** : code à usage unique (OTC) généré

## Génération d’un code unique à l’aide de l’API REST

Le point d’entrée de `V1/customer/:customerId/otp` POST fournit un moyen par programmation de générer un OTC pour un client. Cela s’avère utile pour les interfaces utilisateur d’administration, les scripts ou les intégrations tierces qui doivent déclencher l’émission OTC de manière cohérente.

### contrat REST

| Poste | Valeur |
|---|---|
| **Méthode** | POSTER |
| **URL** | `/rest/V1/customer/:customerId/otp` |
| **Authentification** | Jeton d’administration (porteur). ACL requise : `Magento_LoginAsCustomer::login`. |
| **Corps de la requête** | JSON avec un champ de `reason` facultatif. Utilisé pour les audits et la journalisation. |
| **Réponse de succès** | HTTP 200, JSON avec `otp` (chaîne hexadécimale de 32 caractères). |
| **Réponses d’erreur** | Erreurs d’API web standard (par exemple, 401, 403). Si l’option Connexion en tant qu’assistance clientèle est désactivée pour le client, peut apparaître sous la forme d’une exception 500 ou mappée. |

### Exemple de requête

```text
POST /rest/V1/customer/:customerId/otp
Content-Type: application/json
```

```json
{"reason": "Support session"}
```

### Exemple de réponse

```json
{"otp": "a1b2c3d4e5f6789012345678abcdef01"}
```

## Échanger un code unique contre un jeton client à l’aide de GraphQL

Après avoir généré un OTC (à partir de l’interface utilisateur d’administration ou de l’API REST), utilisez l’une des mutations GraphQL suivantes pour l’échanger contre un jeton d’accès client.

### mutation `generateCustomerToken`

La mutation `generateCustomerToken(email, password)` renvoie un jeton client. L’argument `password` est évalué dans l’ordre suivant :

1. **Mot de passe du client (par défaut)** - Mot de passe du compte du client.
1. **Jeton de réinitialisation du mot de passe du client (utilisation unique)** - Jeton valide provenant de l’**Mot de passe oublié** (par exemple, la mutation `requestPasswordResetEmail`). Consommé lors de la première utilisation.
1. **OTC généré par l’administrateur (code unique)** - Code généré par un administrateur pour le client via l’API REST ou l’interface utilisateur d’administration. Utilisation unique, de courte durée (30 secondes par défaut).

**Schéma:**

```graphql
type Mutation {
  generateCustomerToken(email: String!, password: String!): CustomerToken
}

type CustomerToken {
  token: String!
}
```

**Exemple : connexion avec l’administrateur OTC**

```graphql
mutation GenerateCustomerToken($email: String!, $password: String!) {
  generateCustomerToken(email: $email, password: $password) {
    token
  }
}
```

Variables (utilisez OTC comme `password`) :

```json
{
  "email": "customer@example.com",
  "password": "<admin-generated-OTC>"
}
```

**Exemple : connexion avec mot de passe**

```graphql
mutation GenerateCustomerToken($email: String!, $password: String!) {
  generateCustomerToken(email: $email, password: $password) {
    token
  }
}
```

Variables :

```json
{
  "email": "customer@example.com",
  "password": "CustomerPassword123"
}
```

**Exemple : connexion avec jeton de réinitialisation du mot de passe**

Une fois que le client a demandé une réinitialisation de mot de passe (par exemple, `requestPasswordResetEmail`), le jeton de réinitialisation reçu via le lien d’e-mail peut être utilisé comme `password` dans `generateCustomerToken` (utilisation unique).

```graphql
mutation GenerateCustomerToken($email: String!, $password: String!) {
  generateCustomerToken(email: $email, password: $password) {
    token
  }
}
```

Variables (utilisez le jeton de réinitialisation comme `password`) :

```json
{
  "email": "customer@example.com",
  "password": "<reset-password-token-from-email-link>"
}
```

**Exemple de réponse :**

```json
{
  "data": {
    "generateCustomerToken": {
      "token": "<customer-access-token>"
    }
  }
}
```

### mutation `exchangeOtpForCustomerToken`

La mutation `exchangeOtpForCustomerToken` échange un jeton de réinitialisation de mot de passe ou OTP généré par un administrateur contre un jeton d’accès client. Le mot de passe à usage unique est invalidé après un échange réussi. Ce point d’entrée respecte la configuration reCAPTCHA.

**Schéma:**

```graphql
type Mutation {
  exchangeOtpForCustomerToken(
    email: String!
    otp: String!
  ): CustomerToken
}

type CustomerToken {
  token: String!
}
```

**Exemple de requête :**

```graphql
mutation ExchangeOtpForCustomerToken($email: String!, $otp: String!) {
  exchangeOtpForCustomerToken(email: $email, otp: $otp) {
    token
  }
}
```

Variables :

```json
{
  "email": "customer@example.com",
  "otp": "<one-time-password>"
}
```

**Exemple de réponse :**

```json
{
  "data": {
    "exchangeOtpForCustomerToken": {
      "token": "<customer-access-token>"
    }
  }
}
```

### Résumé des mutations

| Mutation | Cas d’utilisation |
|---|---|
| `generateCustomerToken(email, password)` | Point d’entrée unique : mot de passe du client, jeton de réinitialisation du mot de passe, OTC de l’administrateur ou OTP (essayé après la réinitialisation du mot de passe). |
| `exchangeOtpForCustomerToken(email, otp)` | Échange de jetons OTP ou Réinitialiser le mot de passe. OTP (ou jeton de réinitialisation de mot de passe) est utilisé après utilisation. |

Le jeton de réinitialisation de mot de passe et Admin OTC sont tous deux transmis en tant qu’argument `password` à `generateCustomerToken`. Le programme de résolution détecte le type de jeton et le valide en conséquence.
