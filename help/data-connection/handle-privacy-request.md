---
title: Gestion  [!DNL Commerce]  demandes d’accès à des informations personnelles par les services
description: Découvrez comment les services  [!DNL Commerce]  gèrent les demandes d’accès et de suppression de données.
role: Admin, Leader
feature: Security, Compliance
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# Demandes d’accès à des informations personnelles

Adobe Experience Platform Privacy Service fournit une API RESTful et une interface utilisateur pour vous aider à gérer les demandes de données des clients. Avec Privacy Service, vous pouvez envoyer des demandes d’accès et de suppression de données clients personnelles des applications Adobe Experience Cloud, ce qui facilite l’automatisation de la conformité aux réglementations de confidentialité légales et au sein de l’organisation.

Pour plus d’informations sur Privacy Service et sur la création et la gestion des demandes d’accès à des informations personnelles, consultez la documentation de Adobe Experience Platform :

* Présentation de [Privacy Service](https://experienceleague.adobe.com/fr/docs/experience-platform/privacy/home)
* [Gestion des tâches de confidentialité dans l’interface utilisateur de Privacy Service](https://experienceleague.adobe.com/fr/docs/experience-platform/privacy/ui/user-guide)

## Gestion des demandes individuelles de confidentialité des données

Vous pouvez soumettre des requêtes individuelles pour accéder aux données des clients et les supprimer de [!DNL Commerce] de deux manières :

* Via l’interface utilisateur de **Privacy Service**. Voir la documentation [ici](https://experienceleague.adobe.com/fr/docs/experience-platform/privacy/ui/user-guide#_blank).
* Via l’API **Privacy Service**. Consultez la documentation [ici](https://developer.adobe.com/experience-platform-apis/references/privacy-service/#_blank) et les informations d’API [ici](https://developer.adobe.com/experience-platform-apis/#_blank).

Privacy Service prend en charge deux types de demandes : **accès aux données** et **suppression des données**.

>[!NOTE]
>
>Cet article se concentre sur les demandes d’accès à des informations personnelles pour [!DNL Commerce]. Si vous prévoyez d’effectuer des demandes d’accès à des informations personnelles pour [lac de données Platform](https://experienceleague.adobe.com/fr/docs/experience-platform/catalog/privacy), [profil client en temps réel](https://experienceleague.adobe.com/fr/docs/experience-platform/profile/privacy) ou [service d’identités](https://experienceleague.adobe.com/fr/docs/experience-platform/identity/privacy), reportez-vous à leurs guides d’utilisation respectifs. Notez que les demandes de suppression et d’accès doivent être envoyées individuellement à chaque système, car une demande d’accès à des informations personnelles envoyée à Commerce ne supprime pas les données de tous ces systèmes.

## Accès aux données

Pour les **demandes d’accès**, spécifiez « Commerce (Personalization) » à partir de l’interface utilisateur (ou `commerceMarketingData` comme code de produit dans l’API).

## Suppression de données

Pour les demandes de suppression, Privacy Service supprime [!DNL Commerce] données stockées dans les services SaaS Commerce à des fins marketing, ce qui signifie que les profils et les commandes des titulaires de données ne sont plus envoyés aux applications marketing Adobe pour être utilisés dans les campagnes et les parcours clients. Cependant, Privacy Service ne supprime pas les données de l’application [!DNL Commerce], car elles peuvent être nécessaires pour les besoins transactionnels des commerçants. Les commerçants sont responsables de toutes les demandes de suppression/d’accès aux données dans l’application [!DNL Commerce]. Voir [Sécurité de la responsabilité partagée et modèle opérationnel](https://experienceleague.adobe.com/fr/docs/commerce-operations/security-and-compliance/shared-responsibility) pour en savoir plus.

[!DNL Commerce] informera les commerçants des demandes de suppression en leur envoyant des informations pour les titulaires de données qui demandent la suppression de certaines données.

## Création de demandes d’accès et de suppression

### Conditions préalables

Pour envoyer des demandes d’accès et de suppression de données pour Adobe [!DNL Commerce], vous devez disposer des éléments suivants :

* un identifiant de l’organisation IMS ;
* un identifiant d’identité de la personne sur laquelle vous souhaitez agir et le ou les espaces de noms correspondants. Pour plus d’informations sur les espaces de noms d’identité dans Adobe [!DNL Commerce] et Experience Platform, consultez la [ présentation des espaces de noms d’identité](https://experienceleague.adobe.com/fr/docs/experience-platform/identity/features/namespaces).

### Exemple de demande/suppression d’accès RGPD :

Pour les **demandes d’accès**, spécifiez « Commerce (Personalization) » à partir de l’interface utilisateur (ou « commerceMarketingData » en tant que code de produit dans l’API).

Pour les **requêtes de suppression**, assurez-vous que la case à cocher « Commerce (Personalization) » est activée. En outre, si les données de profil client et de commande ont déjà été envoyées de [!DNL Commerce] à Adobe Experience Platform, vous devez envoyer des requêtes de suppression aux services en aval suivants.

* Profil (code de produit : « profileService »)
* Lac de données AEP (code de produit : « AdobeCloudPlatform »)
* Identité (code produit : « identité »)

Pour envoyer des demandes d’accès et de suppression via l’API Privacy, vous devez vous authentifier et gérer les autorisations pour Privacy Service :

* [Authentification et accès à l’API Privacy Service](https://experienceleague.adobe.com/fr/docs/experience-platform/privacy/api/getting-started)
* [Gestion des autorisations pour Privacy Service](https://experienceleague.adobe.com/fr/docs/experience-platform/privacy/permissions)

**En-têtes obligatoires**

```bash
curl --location --request POST 'https://platform.adobe.io/data/core/privacy/jobs' \
--header 'Content-Type: application/json' \
--header 'x-api-key: {{CLIENT_ID}}' \
--header 'x-gw-ims-org-id: {{IMS_ORGID}}' \
--header 'Authorization: Bearer {{ACCESS_TOKEN}}' \
```

**Requête**

```json
{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{{IMS_ORGID}}"
      }
    ],
    "users": [
      {
        "key": "sampleUserKey1",
        "action": ["access"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "dsmith@sample.com",
            "type": "standard"
          }
        ]
      },
      {
        "key": "sampleUserKey2",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "ajones@sample.com",
            "type": "standard"
          }
        ]
      }
    ],
    "include": ["commerceMarketingData"],
    "expandIds": false,
    "priority": "normal",
    "regulation": "gdpr"
}
```

**Réponse**

```json
{
    "requestId": "17284033173196154RX-223",
    "totalRecords": 3,
    "jobs": [
        {
            "jobId": "a52ca032-858e-11ef-bbb4-27391388a0a6",
            "customer": {
                "user": {
                    "key": "sampleUserKey1",
                    "action": [
                        "access"
                    ],
                    "userIDs": [
                        {
                            "namespace": "email",
                            "value": "dsmith@sample.com",
                            "type": "standard",
                            "namespaceId": 6,
                            "isDeletedClientSide": false
                        }
                    ]
                }
            }
        },
        {
            "jobId": "a52ca034-858e-11ef-bbb4-d5d952d69769",
            "customer": {
                "user": {
                    "key": "sampleUserKey2",
                    "action": [
                        "delete"
                    ],
                    "userIDs": [
                        {
                            "namespace": "email",
                            "value": "ajones@sample.com",
                            "type": "standard",
                            "namespaceId": 6,
                            "isDeletedClientSide": false
                        }
                    ]
                }
            }
        },
        {
            "jobId": "a52ca033-858e-11ef-bbb4-8361a5022341",
            "customer": {
                "user": {
                    "key": "sampleUserKey2",
                    "action": [
                        "access"
                    ],
                    "userIDs": [
                        {
                            "namespace": "email",
                            "value": "ajones@sample.com",
                            "type": "standard",
                            "namespaceId": 6,
                            "isDeletedClientSide": false
                        }
                    ]
                }
            }
        }
    ]
}
```
