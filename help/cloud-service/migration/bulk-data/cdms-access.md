---
title: Vérifier l’accès au service de migration
description: Découvrez comment vérifier l’accès de bout en bout à l’API du service de migration des données de Commerce, en confirmant l’accessibilité du réseau, l’authentification IMS et l’autorisation du client.
feature: Cloud
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
role: Developer
level: Intermediate
autotag-review: '2026-07-22T19:18:53.554Z'
TQID: 'https://experienceleague.adobe.com/csDq2Bbha2IieqxsDDG0iS1IHhAJ02fD-cwd8KFIsSk'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
subfeature_v2:
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 670b6214b28be93a16130552a226a8cadb487324
workflow-type: tm+mt
source-wordcount: 452
ht-degree: 1%

---

# Vérifier l’accès au service de migration

{{bulk-data-early-access}}

Utilisez ce guide pour vérifier l’accès de bout en bout à l’API Commerce Data Migration Service (CDMS) à partir de votre environnement. Un appel réussi valide simultanément l’accessibilité du réseau à partir de vos adresses IP de sortie (liste autorisée IP), l’authentification IMS et l’autorisation du client.

Remplissez ce guide après avoir terminé tous les éléments de la [liste de contrôle de préparation du client](readiness-checklist.md) et avant d’exécuter la migration décrite dans le [guide de migration](migration-guide.md).

## Conditions préalables

- Informations d’identification de serveur à serveur OAuth 2.0 (identifiant client et secret client) créées dans [&#128279;](https://developer.adobe.com/console/).
- Votre identifiant de l’organisation IMS, au format `<org>@AdobeOrg`. L’organisation doit être propriétaire du client cible.
- Le `tenantId` cible, un identifiant client IMS alphanumérique de 22 caractères.
- Adresses IP sortantes envoyées à et traitées par Adobe pour la passerelle CDMS. Contactez l’équipe d’Adobe si vous avez des doutes sur les adresses IP ou leur statut.
- L’hôte de service spécifique à la région du tableau [Hôtes de service par environnement et par région](#service-hosts-by-environment-and-region).

## Générer un jeton d’accès IMS

Générez un jeton d’accès à l’aide de vos informations d’identification de serveur à serveur OAuth 2.0 avec l’octroi `client_credentials`. L’hôte IMS de cette étape est le même pour toutes les régions de données. Seul l’hôte CDMS change par région.

```bash
curl -X POST "https://ims-na1.adobelogin.com/ims/token/v3" \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -H "x-org-id:<your-org-id>@AdobeOrg" \
  -d "grant_type=client_credentials" \
  -d "client_id=<your-ims-client-id>" \
  -d "client_secret=<your-ims-client-secret>" \
  -d "scope=AdobeID,openid,read_organizations,additional_info.projectedProductContext,additional_info.roles,adobeio_api,read_client_secret,manage_client_secrets"
```

## Appel de l’API List Migrations

La requête suivante récupère la liste des migrations pour le client et nécessite le jeton d’accès de l’étape précédente. Sélectionnez l’hôte correspondant à votre région dans le tableau [Hôtes de service par environnement et par région](#service-hosts-by-environment-and-region). L’indicateur `-i` imprime la ligne d’état HTTP et les en-têtes de réponse afin que vous puissiez confirmer le résultat.

```bash
curl -i "https://<host>/<tenantId>/v1/migrations" \
  -H "Authorization: Bearer <your IMS access token>"
```

## Interprétation de la réponse

| Code HTTP | Signification | Exemple de corps de réponse |
| --- | --- | --- |
| 200 | Opération réussie. La connectivité, l’authentification et l’autorisation du client ont été transmises. Le corps de la réponse contient la liste des migrations pour le client. | `{"migrations":[...]}` |
| 401 | Jeton porteur manquant ou non valide, rejeté avant d’atteindre le service. [Régénérer le jeton](#generate-an-ims-access-token). | Variable (générée par la passerelle) |
| 403 | L’utilisateur authentifié ne dispose pas des autorisations de migration pour ce client. | `{"error":"access_denied","message":"You do not have permission to access this tenant"}` |
| 500 | Erreur interne du serveur. | `{"error":{"message":"Internal Server Error","status":500}}` |

>[!NOTE]
>
>Si la requête expire ou si la connexion est refusée et qu’aucun statut HTTP n’est renvoyé, votre adresse IP de sortie n’est probablement pas limitée, ou vous utilisez un hôte incorrect. Confirmez l’hôte de région dans le tableau suivant et vos adresses IP définies.

## Hôtes de service par environnement et par région

| Région ou environnement | Etablissement d&#39;accueil |
| --- | --- |
| Sandbox ou pré-production | `https://na1-sandbox.api.commerce.adobe.com` |
| Amérique du Nord | `https://na1.api.commerce.adobe.com` |
| Europe | `https://eu1.api.commerce.adobe.com` |
| Inde | `https://in1.api.commerce.adobe.com` |
| UK | `https://uk1.api.commerce.adobe.com` |
| Australie et Nouvelle-Zélande | `https://au1.api.commerce.adobe.com` |

## Étapes suivantes

Une fois l’accès confirmé, passez au [&#x200B; guide de migration &#x200B;](migration-guide.md) pour commencer la configuration de l’environnement et l’exécution de la migration.
