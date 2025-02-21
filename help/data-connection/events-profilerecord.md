---
title: Enregistrements de profil
description: Découvrez les données capturées par un enregistrement de profil.
role: Admin, Developer
feature: Personalization, Integration, Eventing
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# [!DNL Data Connection] des enregistrements de profil

La section suivante décrit les données d’enregistrement de profil Commerce disponibles lorsque vous installez l’extension [!DNL Data Connection]. Les données des enregistrements de profil sont envoyées au Adobe Experience Platform.

## Enregistrement de profil

Les mises à jour des enregistrements de profil sont disponibles dans Experience Platform lorsqu’un nouveau profil est créé, mis à jour ou supprimé.

### Données collectées à partir de l’enregistrement de profil

La section suivante décrit les données capturées pour un enregistrement de profil.

| Champ | Description |
|---|---|
| `channel` | Contient des informations sur la source des données. `_id` et `_type` contiennent tous deux des [valeurs d’espace de noms](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/namespaces). |
| `channel._id` | Identifiant unique du canal, tel que `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifie la source des données du canal, telles que les `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `person` | Contient des informations sur le client. |
| `person.name` | Contient des informations sur le nom du client. |
| `person.name.firstName` | Contient le prénom du client. |
| `person.name.lastName` | Contient le nom du client. |
| `person.birthDate` | Date de naissance de l’acheteur. |
| `personalEmail` | Adresse e-mail personnelle. |
| `personalEmail.address` | L’adresse technique, par exemple, `name@domain.com` telle qu’elle est généralement définie dans les normes RFC2822 et suivantes. |
| `billingAddress` | Adresse postale de facturation. |
| `billingAddress.street1` | Informations au niveau de la rue du Principal, numéro de l’appartement, numéro de la rue et nom de la rue. |
| `billingAddress.street2` | Deuxième ligne facultative d&#39;informations concernant la rue. |
| `billingAddress.city` | Nom de la ville. |
| `billingAddress.state` | Nom de l’état. Il s’agit d’un champ à structure libre. |
| `billingAddress.country` | Nom du territoire administré par le gouvernement. À l’exception de `xdm:countryCode`, il s’agit d’un champ à structure libre pouvant contenir le nom du pays dans n’importe quelle langue. |
| `billingAddress.primary` | Indique s’il s’agit de l’adresse de facturation principale. Valeur toujours `False`. |
| `billingAddressPhone` | Numéro de téléphone associé à l’adresse de facturation. |
| `billingAddressPhone.number` | Numéro de téléphone. Notez que le numéro de téléphone est une chaîne et peut inclure des caractères significatifs tels que des crochets `()`, des tirets `-` ou des caractères pour indiquer des identifiants de sous-numérotation tels que des extensions `x` par exemple `1-353(0)18391111` ou `+613 9403600x1234`. |
| `billingAddressPhone.primary` | Indique s’il s’agit du numéro de téléphone principal de l’adresse de facturation. Valeur toujours `False`. |
| `shippingAddress` | Adresse postale d’expédition. |
| `shippingAddress.street1` | Informations au niveau de la rue du Principal, numéro de l’appartement, numéro de la rue et nom de la rue. |
| `shippingAddress.street2` | Deuxième ligne facultative d&#39;informations concernant la rue. |
| `shippingAddress.city` | Nom de la ville. |
| `shippingAddress.state` | Nom de l’état. Il s’agit d’un champ à structure libre. |
| `shippingAddress.country` | Nom du territoire administré par le gouvernement. À l’exception de `xdm:countryCode`, il s’agit d’un champ à structure libre pouvant contenir le nom du pays dans n’importe quelle langue. |
| `shippingAddress.primary` | Indique s&#39;il s&#39;agit de l&#39;adresse d&#39;expédition principale. Valeur toujours `False`. |
| `shippingAddressPhone` | Numéro de téléphone associé à l’adresse de livraison. |
| `shippingAddressPhone.number` | Numéro de téléphone. Notez que le numéro de téléphone est une chaîne et peut inclure des caractères significatifs tels que des crochets `()`, des tirets `-` ou des caractères pour indiquer des identifiants de sous-numérotation tels que des extensions `x` par exemple `1-353(0)18391111` ou `+613 9403600x1234`. |
| `shippingAddressPhone.primary` | Indique s’il s’agit du numéro de téléphone principal de l’adresse de livraison. Valeur toujours `False`. |
| `userAccount` | Indique les détails de fidélité, les préférences, les processus de connexion et d’autres préférences du compte. |
| `userAccount.startDate` | Date de création du profil. |

>[!NOTE]
>
>Chaque enregistrement de profil inclut également le champ [`identityMap`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/field-groups/profile/identitymap) , qui inclut l’ID de client Commerce généré par le système comme identifiant principal du profil et un ID d’e-mail utilisé comme identifiant secondaire.

Découvrez comment [créer un schéma spécifique aux enregistrements de profil](profile-data.md) qui peut ingérer les données de vos enregistrements de profil.
